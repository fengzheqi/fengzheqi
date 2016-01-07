title: JavaScript字符串的操作
date: 2015-12-28
tags: JavaScript
---

# JavaScript字符串的操作

平常我们在写JS代码时，遇到最频繁的操作之一也许是字符相关的操作了，同时在面试中也常常会设计字符串的转化的问题，今天刚好将看到资料和前人的经验总结一下，整理如下，希望大家补充和纠正。

## 1. 非字符串转化为字符串

### 1.1 原始值转字符串
|		值		|		转换为字符串	|	值			|	转换为字符串	|
|:-------------:|:-----------------:|:-------------:|:-------------:|
|	undefined	|	"undefined"		|	0			|	"0"			|
|	null		|	"null"			|	NaN			|	"NaN"		|
|	true		|	"true"			|	Infinity	|	"Infinity"	|
|	false		|	"false"			|	-Infinity	|	"-Infinity"	|

### 1.2 对象转字符串
如果是`{}`、`[]`和`function{}`等对象 转字符串情况又如何呢？

对象转换为字符串，有两个调用的方法：`toString()`和`valueOf()`。调用规则是这样的：
1. 如果对象具有`toString()`方法，则调用这个方法。如果它返回一个原始值（undefined、null、number、boolean、string），JavaScript将这个值转化为字符串，并返回这个字符串结果。
2. 如果对象没有`toString()`方法，或者这个方法并不返回一个原始值，那么JavaScript会调用`valueOf()`方法。如果存在这个方法，则JavaScript调用它。如果返回值是原始值，JavaScript将这个值转换为字符串，并返回这个字符串结果。
3. 否则，JavaScript无法从`toString()`或`valueOf()`获得一个原始值，抛出异常。

事实上大部分情况对象都会调用`toString()`方法，我们来研究一下。
- 默认的`toString()`方法，即`Object.prototype.toString()`，并不会返回一个有效的值，例子如下：
		
	```
	({x:1, y:2}).toString() // => "[object Object]"
	```
	
- 数组（Array）对象在原型里自定义了`toString()`，即`Array.prototype.toString()`，所以数组在调用`toString()`时，有一些不同。
	数据在调用`toString()`时，覆盖了Object的`toString()`方法。	`toString()` 方法返回一个字符串，该字符串由数组中的每个元素的 `toString()` 返回值经调用 `join()` 方法连接（由逗号隔开）组成。

	```
	var a = [];
	var b = [1, 2, 3];
	a.toString();// => ""
	b.toString();// => "1,2,3"
	```
	
	

- 函数（Function）对象在原型里自定义了`toString()`，即`Function.prototype.toString()`。
	Function 对象覆盖了从 Object 继承来的 `Object.prototype.toString()` 方法。函数的 `toString()` 方法会返回一个表示函数源代码的字符串。具体来说，包括 function关键字，形参列表，大括号，以及函数体中的内容。

	```
	(function(x) {f(x);}).toString(); // => "function(x) {\n f(x); \n}"
	```
	
	

- 日期（Date）对象在原型里自定义了`toString()`，即`Date.prototype.toString()`。
	Date 对象覆盖了从 Object 继承来的 `Object.prototype.toString()` 方法。Date的 `toString()` 方法总是返回一个美式英语日期格式的字符串。当一个日期对象被用来作为文本值或用来进行字符串连接时，`toString()` 方法会被自动调用。

	```
	var date = new Date();
	date.toString(); // => "Mon Dec 28 2015 21:58:10 GMT+0800 (中国标准时间)"
	```

	

- 正则（RegExp）对象在原型里自定义了`toString()`，即`RegExp.prototype.toString()`。
	RegExp 对象覆盖了 Object 继承来的 `Object.prototype.toString()` 方法。对于 RegExp 对象，toString 方法返回一个该正则表达式的字符串形式。

	```
	var reg = new RegExp("a+b+c");
	console.log(reg.toString()); // => "/a+b+c/"
	```
	
	
## 2.字符串的常用操作

定义在String原型对象中的方法，大概有二三十个，完全记得这么多方法对于普通人来说太难了，不过常用的七八个方法是应该记住的，其他的只需要有印象，用的时候在[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)查就可以了。

### 2.1 字符串属性
字符串默认只定义了两个属性：`length`和`prototype`。`length`表示字符串长度；`prototype`表示原型。

	```
	var myStr = "this is a string";
	console.log(myStr.length); // => 16
	```

### 2.2 字符串查找
字符串查找对应两个方法：`indexOf()`、`lastIndexOf()`。
- `indexOf()`
	>  **str.indexOf(searchValue[, fromIndex])**
	
	 searchValue：表示被查找的值； fromIndex：表示调用该方法的字符串中开始查找的位置，可以是任意整数，默认值为 0。`indexOf()` 方法返回指定值在字符串对象中首次出现的位置。如果不存在，则返回 -1。
	
	```
	var myStr = "this is a string";
	console.log(myStr.indexOf("a"));// => 8
	```

- `lastIndexOf()`
 >  **str.lastIndexOf(searchValue[, fromIndex])**	

 searchValue：表示被查找的值； fromIndex：表示调用该方法的字符串中开始查找的位置，往前查找，可以是任意整数，默认值为 0。`lastIndexOf()` 方法返回指定值在调用该方法的字符串中最后出现的位置，如果没找到则返回 -1。从该字符串的后面向前查找，从 fromIndex 处开始。

- **小结**：`index()`是从前向后查找，`lastIndexOf()`是从后向前查找，两个方法只是查找方式不一样，但是两个方法中被查找的index值一直是不变。

### 2.3 字符串的截取与分割
这里涉及到四个方法：`slice()`、`split()`、`substring()`、`substr()`。之所以把这四个方法一起讲，是因为平常我们有时候将它们混淆，先看看它们各自用法。

- `slice()`：`slice()`方法提取字符串中的一部分，并返回这个新的字符串。
 >  **str.slice(beginSlice[, endSlice])**	

 beginSlice：从该索引（以 0 为基数）处开始提取原字符串中的字符，如果该参数为负数，则它表示从原字符串中的倒数第几个字符开始抽取。endSlice：在该索引（以 0 为基数）处结束提取字符串；如果省略该参数，slice会一直提取到字符串末尾；如果该参数为负数，则它表示在原字符串中的倒数第几个字符结束抽取.。

	```
	var myStr = "this is a string";
	console.log(myStr.slice(5)); //=> "is a string" 
	console.log(myStr.slice(5, 7)); //=> "is"
	```

- `split()`：`split()` 方法通过把字符串分割成子字符串来把一个 String 对象分割成一个字符串数组。
 >  **str.split([separator][, limit])**	

	separator：指定用来分割字符串的字符（串）。limit：一个整数，限定返回的分割片段数量。

	```
	var myStr = "this is a string";
	console.log(myStr.split(" ")); //=> ["this", "is", "a", "string"]
	console.log(myStr.split(" ", 3)); //=> ["this", "is", "a"]
	```

- `substring()`：`substring()` 返回字符串两个索引之间（或到字符串末尾）的子串。
 >  **str.substring(indexA[, indexB])**	

	indexA：一个 0 到字符串长度之间的整数。indexB：(optional) 一个 0 到字符串长度之间的整数。

	```
	var myStr = "this is a string";
	console.log(myStr.substring(2)); //=> "is is a string"
	console.log(myStr.substring(2, 3)); //=>  "i"
	```


- `substr()`：`substr()` 方法返回字符串中从指定位置开始的指定数量的字符。
 >  **str.substr(start[, length])**	

	start：开始提取字符的位置。length：提取的字符数。

	```
	var myStr = "this is a string";
	console.log(myStr.substr(2)); //=> "is is a string"
	console.log(myStr.substr(2, 2)); //=>  "is"
	```

- **小结**：四个方法各自用法如上，有一两个注意地方：`split()`返回的是数组，可以这样记忆，split后面有t，可以看着`[`，即数组；涉及到index的截取的方法，都是取头不取尾。

### 2.4 字符串索引
字符串的索引涉及两个方法：`indexOf()`、`charOf()`。

- `indexOf()`：返回指定值在字符串对象中首次出现的位置。从 fromIndex 位置开始查找，如果不存在，则返回 -1。
 
 >  **str.indexOf(searchValue[, fromIndex])**	

	searchValue：一个字符串表示被查找的值。fromIndex ：表示调用该方法的字符串中开始查找的位置。可以是任意整数。默认值为 0。如果 fromIndex < 0 则查找整个字符串（如同传进了 0）。

	```
	var myStr = "this is a string";
	console.log(myStr.indexOf("a")); // => 8
	```

- `charOf()`：返回字符串中指定位置的字符。

 > **str.charAt(index)**
	
	index：0 到 字符串长度-1 的一个整数。

	```
	var myStr = "this is a string";
	console.log(myStr.charAt(8)); // => "a"
	```

### 2.5 字符串合并
涉及到一个方法：`concat()`.
- `concat()`：将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回。
	
 > **string.concat(string2, string3[, ..., stringN])**
	
	string2...stringN：原字符串连接的多个字符串

	```
	var myStr1 = "this is ";
	var myStr2 = "a string";
	console.log(myStr1.concat(myStr2)); // => "this is a string"
	```

### 2.6 字符串匹配
涉及到两个方法：`match()`、`search()`
- `match()`：当字符串匹配到正则表达式（regular expression）时，`match()` 方法会提取匹配项，返回一个数组。如果正则表达式没有 g 标志，返回和 RegExp.exec(str) 相同的结果。而且返回的数组拥有一个额外的 input 属性，该属性包含原始字符串。另外，还拥有一个 index 属性，该属性表示匹配结果在原字符串中的索引（以0开始）。如果正则表达式包含 g 标志，则该方法返回一个包含所有匹配结果的数组。如果没有匹配到，则返回 null。

 > **str.match(regexp);**
	
	regexp：一个正则表达式对象。如果传入一个非正则表达式对象，则会隐式地使用 new RegExp(obj) 将其转换为正则表达式对象。

	```
	var myStr = "this is a string";
	var pattern1 = /i[a-z]/;
	var pattern2 = /i[a-z]/g;
	console.log(myStr.match(pattern1));// =>["is", index: 2, input: "this is a string"]
	console.log(myStr.match(pattern2));// =>["is", "is", "in"]
	```

- `search()`：执行一个查找，看该字符串对象与一个正则表达式是否匹配。如果匹配成功，则 search() 返回正则表达式在字符串中首次匹配项的索引。否则，返回 -1。

	> **str.search(regexp)**

	regexp：一个正则表达式对象。如果传入一个非正则表达式对象，则会隐式地使用 new RegExp(obj) 将其转换为正则表达式对象。

	```
	var myStr = "this is a string";
	var pattern = /i[a-z]/;
	console.log(myStr.search(pattern));// => 2
	console.log(myStr.search("z"));// => -1
	```

### 2.7 字符串大小写转换
涉及的两个方法：`toLowerCase()`、`toUpperCase()`。
- `toLowerCase()`：将调用该方法的字符串值转为小写形式，并返回。

	```
	var myStr = "This is a String";
	console.log(myStr.toLowerCase()); // => "this is a string"
	```

- `toUpperCase()`： 将调用该方法的字符串值转换为大写形式，并返回。

	```
	var myStr = "This is a String";
	console.log(myStr.toUpperCase()); // => "THIS IS A STRING"
	```



## 3 总结
以上就是我关于字符串操作的大概总结，可能有需要完善和纠正的地方，希望有想法和建议，希望大家多多留言。