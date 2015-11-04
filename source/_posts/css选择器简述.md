title: css选择器简述
date: 2015-11-04
tags: CSS
---

### CSS选择器简述
&emsp;&emsp;在css中，选择器的重要性不言而喻，平常用的时候总是会忘记，刚好抽个时间整理一下，如有遗漏和不对的地方，希望大家多提意见:)

#### 一、分类

##### 1.基本选择器分类
- 元素选择器
- 类选择器
- id选择器
- 属性选择器

##### 2.文档结构分类
- 后代选择器（子代选择器）
- 相邻选择器

##### 3.伪类与伪元素
- 伪类选择器
- 伪元素选择器 

#### 二、选择器举例
##### 1.元素选择器
根据`html`元素来选择，例如：
``` css
 p {marigin:20px;}
```
##### 2.类选择器
根据元素中`class`属性来选择，例如：
``` css
.nav {color:#fff;}
```
##### 3.id选择器
根据元素中`id`属性来选择，例如：
``` css
#header {font-size: 14px;}
```
##### 4.属性选择器
根据元素定义的属性来选择，例如：
``` css
input[type=text] {padding: 10px;}
```
##### 5.后代选择器
在dom结构中，当我们需要对文档结构进行选择时，则可以利用后代选择器，例如：
``` css
/*对div内的全部p元素应用margin、padding规则*/
 div p {margin:20px; padding:10px;}
```
**子代选择器**：如果只是对子代进行选择，则可利用如下规则
``` css 
/*对tr下第一个td应用color:#ccc样式*/
tr > td {color: #ccc;}
```
##### 6.相邻选择器
对于选择同一级的节点，可以使用相邻选择器，如下：
``` css
/*p和div属于同一级相邻元素*/
 p + div {margin: 20px}
```
##### 7.伪类选择器
在元素`a`中，常常需要对hover，visited等伪类做样式控制，在css中可以这样写：
``` css
/*在定义a元素的伪类时，顺序很重要，link-visited-focus-hover-active*/
a:link {color: navy;}
a:visited {color: gray;}
a:focus {color: green;}
a:hover {color: red;}
a:active {color: yellow;}
```
##### 8.伪元素选择器
伪元素目前在css2.1中定义了4个：设置首字母样式、设置第一行样式、设置之前和之后元素的样式。例如：
``` css
p:first-letter {color: red;}
p:first-line {color: purple;}
h2:before {content: "**"; color: silver;}
h2:after {content: "the end";}
```

#### 三、常见选择器例子
``` css
/*css中分组,对h2、p都应用样式*/
h2, p {color: gray;}

/*选择器混用，如下例，查找的是元素p中class="warning"的元素*/
p.warning {font-weight: bold;}

/*多类选择器，对于一个元素中同时包含多个类的元素。ps. 注意匹配的是同时包含这些类的元素*/
.warning.urgent {background: silver;}
```
