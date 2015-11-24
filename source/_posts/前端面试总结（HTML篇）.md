title: 前端面试总结（HTML篇）
date: 2015-11-22
tags: HTML
---

### 前端面试总结（HTML篇）

#### 1. ie的某些兼容性问题
我的博客：[IE的兼容性问题](http://fengzheqi.com/2015/10/18/%E6%B5%8F%E8%A7%88%E5%99%A8%E5%85%BC%E5%AE%B9/)

#### 2. HTML5的新特性
推荐博客：
1. [28 HTML5 Features, Tips, and Techniques you Must Know](http://code.tutsplus.com/tutorials/25-html5-features-tips-and-techniques-you-must-know--net-13520)
2. [翻译-你必须知道的28个HTML5特征、窍门和技术](http://www.zhangxinxu.com/wordpress/2010/08/%E7%BF%BB%E8%AF%91-%E4%BD%A0%E5%BF%85%E9%A1%BB%E7%9F%A5%E9%81%93%E7%9A%8428%E4%B8%AAhtml5%E7%89%B9%E5%BE%81%E3%80%81%E7%AA%8D%E9%97%A8%E5%92%8C%E6%8A%80%E6%9C%AF/)

#### 3. canvas画图

#### 4. doctype的作用
doctype告诉浏览器它使用了什么文档类型。它指出阅读程序应该用什么规则集来解释文档中的标记。XHTML中有三种，包括过度型、严格型、框架型。HTML4严格。随着XML的流行，HTML推出了XHTML标准，其中严格模式严格遵守了XML的规范，例如属性必须有值、标签必须闭合等，同时也抛弃了一些不推荐的标签。而XHTML过度版本，则稍微比严格模式松散些，一些不推荐的标签依然可用外。当页面有框架时，则应该使用框架型。再就是HTML5的版本。使用HTML5的Doctype会默认触发标准模式。

#### 5. HTML5中引进`data-`有什么作用
在HTML5中我们可以使用data-前缀设置我们需要的自定义属性，来进行一些数据的存放。

在JS中取得`data-`中数据有两种方法，一种是利用dataset属性集来获取（推荐），另外一种是利用getAttribute()方法。虽然dataset的执行速度比getAttribute慢一点，但是更加方便，而且这种速度上的差异可以忽略。

推荐博客：[HTML5自定义属性对象Dataset简介](http://www.zhangxinxu.com/wordpress/2011/06/html5%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B1%9E%E6%80%A7%E5%AF%B9%E8%B1%A1dataset%E7%AE%80%E4%BB%8B/)

#### 6. HTML中标准模式和怪异模式有什么不同
由于历史的原因，各个浏览器在对页面的渲染上存在差异，甚至同一浏览器在不同版本中，对页面的渲染也不同。在W3C标准出台以前，浏览器在对页面的渲染上没有统一规范，产生了差异(Quirks mode或者称为Compatibility Mode)；由于W3C标准的推出，浏览器渲染页面有了统一的标准(CSScompat或称为Strict mode也有叫做Standars mode)，这就是二者最简单的区别。

W3C标准推出以后，浏览器都开始采纳新标准，但存在一个问题就是如何保证旧的网页还能继续浏览，在标准出来以前，很多页面都是根据旧的渲染方法编写的，如果用的标准来渲染，将导致页面显示异常。为保持浏览器渲染的兼容性，使以前的页面能够正常浏览，浏览器都保留了旧的渲染方法（如：微软的IE）。这样浏览器渲染上就产生了Quircks mode和Standars mode，两种渲染方法共存在一个浏览器上。 

那么浏览器究竟该采用哪种模式渲染呢？这就引出的DTD，既是网页的头部声明，浏览器会通过识别DTD而采用相对应的渲染模式：

1. 浏览器要使老旧的网页正常工作，但这部分网页是没有doctype声明的，所以浏览器对没有doctype声明的网页采用quirks mode解析；
2. 对于拥有doctype声明的网页，什么浏览器采用何种模式解析，这里有一张详细列表可参考：http://hsivonen.iki.fi/doctype/ ；
3. 对于拥有doctype声明的网页，这里有几条简单的规则可用于判断：对于那些浏览器不能识别的doctype声明，浏览器采用strict mode解析；
4. 在doctype声明中，没有使用DTD声明或者使用HTML4以下（不包括HTML4）的DTD声明时，基本所有的浏览器都是使用quirks mode呈现，其他的则使用strict mode解析； 
5. 可以这么说，在现有有doctype声明的网页，绝大多数是采用strict mode进行解析的；
6. 在ie6中，如果在doctype声明前有一个xml声明(比如:<?xml version="1.0" encoding="iso-8859-1"?>)，则采用quirks mode解析。这条规则在ie7中已经移除了。 

#### 7. 写出你常用的HTML标签
- `<!-- -->`：注释
- `<!DOCTYPE>`：定义文档类型，通常是HTML5
- `<html>`：定义 HTML 文档
- `<head>`：定义关于文档的信息
- `<base>`：定义页面中所有链接的默认地址或默认目标，常用属性href
- `<meta>`：定义关于 HTML 文档的元信息
- `<title>`：定义文档的标题
- `<style>`：定义文档的样式信息

- `<body>`：定义文档的主体
- `<br>`：定义简单的折行
- `<hr>`：定义水平线
- `<h1> to <h6>`：定义 HTML 标题
- `<p>`：定义段落
- `<span>`：定义文档中的节
- `<div>`：定义文档中的节
- `<img>`：定义图像
- `<form>`：定义供用户输入的 HTML 表单
- `<a>`：定义锚，常用属性id、class、href、name
- `<label>`：定义 input 元素的标注
- `<input>`：定义输入控件
- `<select>`：定义选择列表（下拉列表）
- `<option>`：定义选择列表中的选项
- `<ol>`：定义有序列表
- `<ul>`：定义无序列表
- `<li>`：定义列表的项目
- `<table>`：定义表格
- `<thead>`：定义表格中的表头内容
- `<th>`：定义表格中的表头单元格
- `<tbody>`：定义表格中的主体内容
- `<tr>`：定义表格中的行
- `<td>`：定义表格中的单元
- `<tfoot>`：定义表格中的表注内容（脚注）
- `<textarea>`：定义多行的文本输入控件
- `<button>`：定义按钮 (push button)

- `<script>`：定义客户端脚本