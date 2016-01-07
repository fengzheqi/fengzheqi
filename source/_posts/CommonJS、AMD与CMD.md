title: CommonJS、AMD与CMD
date: 2015-12-8
tags: MongoDB
---

# CommonJS Modules 小译

CommonJS中定义了很多规范，这篇文章只是简述一下CommonJS中有关Module部分的规范。

## 目的
为了能够使系统中的各个模块协同合作，也为了现在和未来在客户端、服务端约定统一的模块语法规范。

## 特性
这些模块具有以下特性：保证私有的作用域、保证从其他模块引用单个对象的灵活性、暴露本身的API。为了实现模块间的协同合作，规范定义了以下最基础的特性。

## 内容

### 模块上下文

- 在模块中，定义一个自由变量`require`函数
  - `require`函数接受一个模块标识符。
  - `require`函数中返回暴露给其他模块调用的API。
  - 如果有依赖循环，可能存在引入的依赖模块还没加载完就被调用的情况。为了避免这种情况发生，`require`函数必须在依赖模块被调用前就准备好相关暴露接口。
  - 如果被调用的模块没有被返回，`require`函数返回一个错误信息。

- 在模块中定义一个自由变量`exports`，即一个对象，该模块可以添加其API来在执行

### 模块标识符
- 模块名是由一个或多个单词以正斜杠为分隔符拼接成的字符串
- 单词须为驼峰形式，或者"."，".."
- 模块名不允许文件扩展名的形式，如".js"
- 模块名可以为 "相对的" 或 "顶级的"。如果首字符为"."或".."则为"相对的"模块名
- 顶级的模块名从根命名空间的概念模块解析
- 相对的模块名从 "require" 书写和调用的模块解析

### 未说明部分
在规范中并没有将以下两个部分解释清楚：
- 模块是否存储在数据库中、文件系统、工厂函数、或者可变的外部library
- 模块加载器是否支持对模块标识符路径的解析

## 单元测试
- [Unit Tests at Google Code](http://code.google.com/p/interoperablejs/) by Kris Kowal
- [Unit Tests Git Mirror](http://github.com/ashb/interoperablejs/tree/master) by Ash Berlin

## 示例代码
meth.js

```javascript
exports.add = function() {
	var sum = 0, 
		i = 0, 
		args = arguments, 
		l = args.length;
	while (i < l) {
		sum += args[i++];
	}
		return sum;
};
```

increment.js

```javascript
var add = require('math').add;
exports.increment = function(val) {
	return add(val, 1);
};
```

program.js

```javascript
var inc = require('increment').increment;
var a = 1;
inc(a); // 2
```

### 原文地址
- http://www.commonjs.org/specs/modules/1.0/


