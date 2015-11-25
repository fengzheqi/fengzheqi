title: HTML5中canvas标签小谈
date: 2015-11-25
tags: HTML
---

### HTML5中canvas标签小谈
#### 一、 canvas（画布）
&emsp;&emsp;在HTML5出现之前，网页中只能用`img`标签来显示静态图片，为看增强图形实时绘制和渲染的效果，后来引入了一些第三方解决方案，如Flash Play等。
&emsp;&emsp;在HTML5发布之后，引入了`canvas`标签，允许JavaScript动态的绘制图形。

#### 二、canvas中运用WebGL

##### 1. WebGL简介
&emsp;&emsp;HTML5作为最新的HTML标准，扩展了传统HTML的特性，并致力于使浏览器从简单的展示工具发展为复杂的应用平台，人们希望网页不仅仅是由二维图形组成。WebGL被设计出来的目的，就是在网页上创建三维的应用和用户体验。
&emsp;&emsp;WebGL起源于openGL ES 2.0，而openGL ES 2.0常用于嵌入式计算机、智能手机、家用游戏机等设备。WebGL的只要优点有：
- 开发环境简单。只需要一个编辑器和浏览器级可以编写代码
- 跨平台。因为WebGL是内嵌在浏览器中，所以适合多种设备运行