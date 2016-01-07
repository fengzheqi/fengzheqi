title: 前端面试总结（JavaScript篇）
date: 2015-12-24
tags: JavaScript
---

## JavaScript语言基础
1. **JavaScript数据类型**
	javaScript的数据类型分为两大类：简单数据类型和复杂数据类型。
	简单数据类型：Undefined、Null、Boolean、Number、String；
	复杂数据类型：Object
	其中，简单数据类型的值也称为原始值（Primitive Value）；复杂数据类型的值称为引用类型的值。
	
2. **JavaScript字符串转化**
	参考博客[JavaScript字符串的操作](http://www.cnblogs.com/fengzheqi/p/5087240.html)
3. **this问题**
	参考博客
4. **模块化原理（作用域）**
	参考博客：[JavaScript基础–作用域](http://www.cnblogs.com/fengzheqi/p/5105517.html)
5. **JavaScript原型链**
	参考博客
6. **闭包及闭包的用处**
	参考博客
7. **常用数组方法**
	参考博客
8. **js数组去重复项**
	参考博客
9. **常见算法的JS实现（例如：实现将两个不同长度的数组组合，顺序越乱越好，以及其的复杂度）**
10. **call与apply的作用及不同，以及bind的用法**
	call方法: [见MDN中call()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)；
	apply方法：[见MDN中apply()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)；
	bind方法：[见MDN中bind()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)；
	`call()`与`apply()`的作用类似，作用同于理解是这样：比如一个对象想调用另外一个对象的方法，但又希望方法的作用域是自己的作用域，这个时候就可以利用`call()`或者`apply()`来解决这个问题。
	`call()`与`apply()`的不同点在于它们的第二个参数，`call()`方法接受的是一个参数列表，而`apply()`的第二参数是一个包含多个参数的数组。	
	`bind()`是在ES5.1中新加的一个方法，作用与`call()`、`apply()`类似，不过`bind()`返回是函数，而`call()`和`apply()`是直接执行调用了的函数。
	所以三者只是用法差不多，作用是类似的。可参考[javascript中apply、call和bind的区别](http://www.cnblogs.com/cosiray/p/4512969.html)

11. **变量名提升**
	参考博客：[JavsScript基础–声明提升](http://www.cnblogs.com/fengzheqi/p/5106783.html)

12. **== 与 ===**
"=="与"==="都属于关系表达式的范畴，用来比较两个值是否相等，`==`可以理解为`相等`，而`===`则理解为`严格相等`，如何理解？在关系表达式中，利用`==`进行两个值的比较时，通常会进行类型转换，比如`null`、`undefined`在`==`的表达式中都会转换为`false`，所以它们`相等`。而利用`===`比较时，比较的两个值是不做类型转换的，
所以`null === undefined`返回false。一般来说，在代码中推荐使用`===`。

	扩展：`==`与`===`的运算规则
	1. `===`
	-  如果两个值类型不同，则它们不相等；
		-  如果两个值一个是null，一个是undefined，则它们不相等；
	- 如果两个值都是`true`或都是`false`，则它们相等；
	- 如果其中一个是`NaN`，或者两个都是`NaN`，则它们不相等（`NaN`和任何值都不相等，包括本身）；
	- 如果两个值都是数字且数值相等，则它们相等（`0`与`-0`相等）；
	- 如果两个值都是字符串，且编码和数值相同，则它们相同（连个字符串含义相同但编码不同，则不相等）；
	- 如果两个引用值都指向同一个对象、数组或函数，则它们是相等的。
	2. `==`
	- 如果两个值的类型相同，则按照`===`的运算规则；
	- 如果两个值的类型不同，`==`认为它们可能相等。检测相等时会遵守以下规则和类型转换；
			- 如果一个值是null，另一个是undefined，则它们相等；
			- 如果一个值是数字，另一个是字符串，先将字符串转换为数字，然后利用转换后的值进行比较；
			- 如果其中一个是true，则将其转换为1再进行比较。如果其中一个是false，则将其转换为0再进行比较；
			- 如果其中一个值是对象，另一个值为数字或字符串，则对象先通过`valueOf()`或者`toString()`方法转换为原始值，再进行比较；
			- 其他不同类型的值进行比较，均不相等。

13. **"use strict"作用**
	"use strict"是ES5推出来的一个严格模式，是为了JavaScript在更格言的条件下运行。主要目的如下：
	- 消除JavaScript语法的一些不合理、不严谨之处和不安全的因素，减少一个怪异行为；
	- 提高编译器效率，增加运行速度；
	- 为未来的JavaScript做好铺垫。

	添加"use strict"通常有两种用法，第一种是在脚本文件的第一行添加，但这种方式在多个脚本合并的时候回失效，不推荐使用；第二种是添加在函数中第一行，整个函数以"严格模式"运行。如果希望在整个脚本中运行"严格模式"，在可以将脚本写成一个立即执行的匿名函数里，比如`(function(){"use strict";})();`
	具体的"严格模式"下还有其他什么限制，可以参考阮一峰的博客：[JavaScript严格模式详解](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html)

14. **函数柯里化（Currying）**
	函数的柯里化：柯里化（Currying），又称部分求值（Partial Evaluation），是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。
	柯里化有三个作用：1.参数复用；2.提前返回；3.延迟计算/运行。细节可参考张鑫旭的博客：[JS中的柯里化(currying)](http://www.zhangxinxu.com/wordpress/2013/02/js-currying/)

14. **JS中random的概率问题**
	参考博客：[Math.random()随机数的二三事](http://www.soulteary.com/2014/07/05/js-math-random-trick.html)
15. **JS中的垃圾回收机制**
	在JS中进行垃圾回收，是为了避免无用的实体消耗系统的内存。JS不像C/C++，他有自己的一套垃圾回收机制（Garbage Collection）。主要有两种方法：**标记清除**、**引用计数**。
	**标记清除**：垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了，因为环境中的变量已经无法访问到这些变量了，然后垃圾回收器相会这些带有标记的变量机器所占空间。
	**引用计数**：引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。
	参考博客：[JavaScript垃圾回收机制](http://www.cnblogs.com/hustskyking/archive/2013/04/27/garbage-collection.html)
16. **常见的JS设计模式**

## 客户端JavaScript

1. **同源策略及跨域请求的方法和原理（比较JSONP和document.domain的不同及优劣，以及HTML5的跨域方案）**

	同源策略限制了一个源（origin）从其它源（origin）中加载文本或脚本资源。
	同源定义：如果两个页面拥有相同的协议（protocol）、主机名和端口（如果指定），那么这两个页面就属于同一个源（origin）。

	跨域请求目前方法有：JSONP、document.domain和HTML5的跨域方案（CORS特性）。
	
	
	**JSONP**：JSON with padding，填充式JSON。JSONP是由两部分组成：回调函数（callback）和数据（json）。回调函数是当响应到来时应该在页面中调用的函数，一般在请求中指定。同时，JSONP是通过动态`<script>`元素来使用的，使用时可以为src属性指定一个跨域的URL。
	**原理**：是首先在客户端注册一个callback, 然后把callback的名字传给服务器；此时，服务端生成json数据，然后以JavaScript的语法组装一个function，function的名称就是传过来的callback参数名；最后json数据以参数的形式插入到function(..)的“..”中，这样就生成了一段js语法的代码，返回给客户端。客户端浏览器解析`script`标签，并执行返回的JavaScript文档（代码），此时客户端直接调用callback函数执行代码，其中参数数据就是之前在服务端生成的json数据。

	**document.domain**：Document内置的属性。用来获取/设置当前网页的原始域部分，用于同源策略。获取原始域：例如`var badDomain = "www.baidu.com/map";`，那么在document.domain`www.baidu.com`。设置原始域：例如`document.domain = string`，注意一点就是设置原始域只能设置为它的上一级域。例如`www.baidu.com`，只能把document.domain设置为`baidu.com`。
	**原理**：document.domain实现跨域的前提条件是这两个域名必须属于同一个基础域名!而且所用的协议，端口都要一致，否则无法利用document.domain进行跨域。所以`wwww.example.com`与`blog.example.com`是没法实现跨域的，但是这个两个基础域名的上级域名，也就是`example.com`是相同的，所以将这两个页面的document.domain都设置为`example.com`就可以实现跨域了。

	**HTML5跨域方案**：利用CORS（Cross-Origin Resource Sharing）新特性。
	**原理**：CORS通过服务器增加一个特殊的Header[Access-Control-Allow-Origin]来告知客户端跨域的限制，如果浏览器支持CORS的话，如果判断Origin通过的话，就会允许XHR进行请求。使用这个Header返回被允许请求跨域请求的来源域，例如网站`a.com`设置了下面的`Header Access-Control-Allow-Origin: http://b.com`。这样设置之后，通过`http://b.com`下的页面对于`a.com`进行ajax请求就会被允许，而其他网站对`a.com`依旧会被阻拦，通过这种方式网站拥有者可以自己对此进行限制。当然，如果不想限制来源，可以通过`Access-Control-Allow-Origin: *`来允许任何站点对该资源进行跨域请求

	参考资料：
	- [MDN-JavaScript 的同源策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)
	- [AJAX跨域请求-JSONP获取JSON数据](http://justcoding.iteye.com/blog/1366102/)

2. **JSONP原理及优缺点**
	原理参考第1个问题。
	**优点**：借用了json的优势，比如可读性好，轻量等；其次简单易用，实现了跨域请求。
	**缺点**：1.JSONP是从其他域加载代码执行，必须保证被请求的域是安全可靠的，如果被请求的域不被信任， Web 应用程序更容易受到攻击；2.JSONP发生请求错误时，并不容易确定，如果动态脚本插入有效，就执行调用；如果无效，就静默失败。失败是没有任何提示的。
 
3. **XMLHttpRequest**
	博客
	
4. **事件委托**
	博客
5. **session与Cookie**
	博客
6. **JavaScript动画算法**
7. **拖拽的实现**
8. **事件冒泡和事件捕获**
9. **浏览器检测（能力检测、怪癖检测等）**
10. **AJAX请求的细节**
	AJAX请求的细节：
	- 从Web表单中获取需要的数据；
	- 建立要连接的URL；
	- 打开到服务器的连接；
	- 设置服务器在完成后要运行的函数；
	- 发送请求。
	
	推荐阅读：[掌握Ajax](http://www.ibm.com/developerworks/cn/views/xml/libraryview.jsp?sort_by=&show_abstract=true&show_all=&search_flag=&contentarea_by=XML&search_by=%E6%8E%8C%E6%8F%A1+Ajax&topic_by=-1&type_by=%E6%89%80%E6%9C%89%E7%B1%BB%E5%88%AB&ibm-search=%E6%90%9C%E7%B4%A2)
	
11. **客户端存储及他们的异同（例如：cookie, sessionStorage和localStorage等）**

## 安全与测试
1. **你如何测试你的JS代码**
2. **DOM1\DOM2\DOM3都有什么不同**
3. **XSS**
4. **JavaScript代码测试**

## JQuery
1. **jQuery链式调用的原理**

## NodeJS
1. **NodeJS健壮性方面的实践（子进程等）**
2. **NodeJS能否用利用多核实现在计算性能上的劣势等**
3. **NodeJS的优缺点及使用场景**

## AngularJS
1. **AngularJS的文件管理及打包（包括模板打包及请求、JS的打包和请求等）**
2. **AngularJS的JS模块管理及实践**
3. **在你的Angular App页面里随意加一个JS文件，会有什么影响**
4. **AngularJS directive及自己如何定义directive**
5. **AngularJS双向绑定的原理及实现**

## ES6
1. **ES6及jQuery新引进的Promise有什么用处**

## 前端工程化
1. **前端模块化（AMD和CommonJS的原理及异同，requirejs的用法）**
	博客
2. **seaJS的用法及原理，依赖加载的原理、初始化、实现等**
3. **webpack的使用**