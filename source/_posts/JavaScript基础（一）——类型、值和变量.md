title: JavaScript基础（一）——类型、值和变量
date: 2015-11-14
tags: JavaScript
---

### JavaScript基础（一）——类型、值和变量

#### 1. JavaScript类型
JavaScript的数据类型分为原始类型（primitive type）和对象类型（object type）。原始类型值也称为原始值，是不可变的；而对象也称为引用类型（reference type），对象值都是应用（reference）。
ps.其中`Null`和`Undefined`作为特殊数据类型纳入原始类型，symbol类型为ES6新加入的数据类型，目的是起唯一标识作用。
![JavaScript类型图](http://img1.ph.126.net/oPvQlzGFa4ximJvx9AdVhQ==/6631366832863549264.png)
*注：图中英文单词首字母大写是指代数据类型，而在利用`typeof`运算符判断操作符类型时，返回的是小写的字符串（例如`number`）。Null作为特例，`typeof`判断时返回`object`。*

#### 2. 数字（Number）
- JavaScript不区分整数值和浮点数值，JavaScript中的所有的数组均用浮点数值表示
- JavaScript中的算术运算在溢出（overflow）、下溢（underflow）和被零整除时不会报错。溢出：超过上限返回`Infinity`，超过下限返回`-Infinity`；下溢（无限接近0）：正数下溢返回0，负数下溢返回-0，-0和0可认为相等；被零整除：返回`Infinity`或者`-Infinity`（特例0除以0时返回`NaN`）。
- JavaScript采用了IEEE-754浮点数表示法（几乎所有现代编程语言所采用），存在着精度的问题，比如对于0.1，只能无限近似0.1。

#### 3. 文本（String）
- 字符串（`string`）是一组由16位值组成的**不可变**的有序序列
- 在字符串中，若遇到类似单引号`'`特殊符号，必须使用反斜线`\`转义
- 字符串提供了`length`属性和众多可调用的方法，详见[MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)

#### 4. 布尔值（Boolean）
- 布尔值只有两个值，保留字`true`和`false`
- 下列六个值在JavaScript类型转换中会转换为`false`：`undefined`、`null`、`0`、`-0`、`NaN`、`""`

#### 5. null和undefined
- `null`是JavaScript语言中的关键字，表示空值。在对`null`执行`typeof`时，返回`object`，可以将`null`认为是一个特殊的对象值，含义是“非对象”
- `undefined`可以理解为未定义的值，表示变量没有初始化。在ES5中`undefined`是只读的，不可修改
- `null`和`undefined`都不包含任何属性和方法。使用“.”和“[ ]”来存取这两个值的成员或方法都会产生一个类型错误

#### 6. 全局对象和包装对象
- 全局对象（global object）在JavaScript中有着重要的用途：全局对象的属性是全局定义的符号，JavaScript程序可以直接使用
- 全局对象的初始属性包括：**全局属性**、**全局函数**、**构造函数**、**全局对象**等，详见[MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference)
- 在代码的最顶级——不在任何函数内的JavaScript代码——可以使用JavaScript关键字this来引用全局对象
- 包装对象：已下面代码为例
	代码中s为字符串，不是对象，怎么可以调用属性呢？这是因为有包装对象，JavaScript在执行到s.length时，会首先使用new String（s）生成一个`String`对象，然后调用属性，一旦属性引用结束，包装对象随即销毁。
	
	```javascript
	var s = "hello";
	console.log(s.length);
	```

- `null`和`undefined`没有对象，也不能调用任何属性和方法

#### 7. 作用域和声明
- 在函数体内，局部变量优先级高于全局变量
- 在JavaScript中没有像C语言块级作用域的概念，JavaScript中使用的是函数作用域（function scope）：变量在声明他们的函数体以及这个函数体嵌套的任意函数体内都是有定义的。
- 在JavaScript中具有“声明提前”的机制，什么是声明提前呢？就是只要你在作用域下声明了变量，不管这个声明在哪，都会提前至作用域的顶部。不过只有程序执行到var语句时，才会真正的赋值。
- “声明提前”也适合函数的声明，而且函数的“声明提前”也会把函数的`statement`也提前

	```javascript
	/*
	*函数声明
	*/
	function add(num1, num2) {
	return num1 + num2;
	}
	```

#### 8. 类型转换
由于JavaScript类型转换太过于复杂，以后抽个时间再写一篇博客，不过可以推荐大家这篇：[JavaScript的类型转换(字符转数字，数字转字符)](http://blog.csdn.net/yangqicong/article/details/6865513)

#### 参考文献
- JavaScript权威指南.第六版.David Flanagan著.淘宝前端团队译
	