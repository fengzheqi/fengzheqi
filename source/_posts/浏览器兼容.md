title: IE的兼容性问题
date: 2015-10-18
tags: HTML
---

## 前言
前端开发人员经常要碰到浏览器的兼容问题，大部分情况下，chrome、Firefox对web标准支持度较好，兼容性问题相对较少。但目前在国内，ie6的份额还是比较大，设计传统系统时不时需要考虑兼容。平时抽个时间在网上收集了一下，整理了部分，希望大家指正、补充。

## 基础

### HTML兼容
HTML的兼容比较容易处理，主要是高版本浏览器用了低版本浏览器无法识别的元素，导致其不能解析，所以平时需要注意一点；其次，在一些css库（比如bootstrap）里会简单的设置一些新标签的样式，以便向后兼容，大家也可以关注一下这些的库的源码。

### CSS兼容
CSS的兼容，一方面是了解并熟悉CSS的通用的方法，其次也可以掌握一些Hack，虽然Hack并不推荐，但学习学习还是可以解决燃眉之急的。
  ```css
/* CSS属性级Hack */
color:red; /* 所有浏览器可识别*/
_color:red; /* 仅IE6 识别 */
*color:red; /* IE6、IE7 识别 */
+color:red; /* IE6、IE7 识别 */
*+color:red; /* IE6、IE7 识别 */
color:red; /* IE6、IE7 识别 */
color:red\9; /* IE6、IE7、IE8、IE9 识别 */
color:red\0; /* IE8、IE9 识别*/
color:red \0; /* 仅IE9识别 */
color:red!important; /* IE6 不识别!important 有危险*/

/* CSS选择符级Hack */
*html #demo { color:red;} /* 仅IE6 识别 */
*+html #demo { color:red;} /* 仅IE7 识别 */
body:nth-of-type(1) #demo { color:red;} /* IE9+、FF3.5+、Chrome、Safari、Opera 可以识别 */
head:first-child+body #demo { color:red; } /* IE7+、FF、Chrome、Safari、Opera 可以识别 */
:root #demo { color:red\9; } : /* 仅IE9识别 */

/* IE条件注释Hack */
<!--[if IE 6]>此处内容只有IE6.0可见<![endif]-->
<!--[if IE 7]>此处内容只有IE7.0可见<![endif]-->
```

下面也大概介绍一些常见的BUG：
> 1. css盒模型在IE6下解析有问题，我们知道就width来说，一个块级元素的magin、padding、border和width的7个属性的宽度之和，应该小于或等于其父级元素的内容区域（width），而我们一般设置宽度若是未达到其长度，浏览器就会重置margin-right的值，将之它们的和等于其值，当然若是我们为margin设置负值，那么元素的width可能超出其父元素。在标准下，width为元素内容区所占区域，也就是不包括margin、border和padding；在ie6中，width为元素内容区+padding+border，这种情况可以采用CSShack技术处理。

> 2. IE6的双倍边距BUG，在块级元素浮动后本来外边距10px,但IE解释为20px,解决办法是加上display: inline。  
**问题**：在IE6下如果某个标签使用了float属性，同时设置了其外边距“margin:10px 0 0 10px”可以看出，上边距和左边距同样为10px，但第一个对象距左边有20px。  
**解决办法**：当将其display属性设置为inline时问题就都解决了。  
**说明**：这是因为块级对象默认的display属性值是block，当设置了浮动的同时，还设置了它的外边距 就会出现这种情况。
也许你会问：“为什么第二个对象和第一个对象之间就不存在双倍边距的BUG”？
因为浮动都有其相对应的对象，只有相对于其父对象的浮动 对象才会出现这样的问题。
第一个对象是相对父对象的，而第二个对象是相对第一个对象的，所以第二个对象在设置后不会出现问题。
另外在一些特殊布局中，可能需要组合使用display:block;和display:inline;才能达到预期效果。
当然最坏的情况下，我们就可以使用"margin:10px 0 0 10px;*margin:10px 0 0 10px;_margin:10px 0 0 5px"，
这种“标准属性;*IE7识别属性;_IE6识别属性”HACK方式解决。  
**总结**：这个现象仅当块级对象设置了浮动属性后才会出现，内联对象（行级对象）不会出现此问题。并且只有设置左边距和右边距的值才会出问题，上下边距不会出现问题。
margin双布局可以说是IE6下经典的bug之一。产生的条件是：block元素+浮动+margin。
而为什么display:inline可以解决这个双边距bug，首先是inline元素或inline-block元素是不存在双边距问题的。
然后，float:left等浮动属性可以让inline元素haslayout，会让inline元素表现得跟inline-block元素的特性一样， 支持高宽，垂直margin和padding等，
所以div class的所有样式可以用在这个display inline的元素上。

> 3. IE6下图片下方有空隙产生；解决这个BUG的方法也有很多,可以是改变html的排版,或者设置img 为display:block，
或者设置vertical-align 属性为vertical-align:top bottom middle text-bottom都可以解决.

> 4. IE6 3px bug 两个浮动层中间有间隙，这个IE的3PX BUG也是经常出现的,
解决的办法是给右边元素也同样浮动 float:left 或者相对IE6定义.left margin-right:-3px;
经典两列布局，float: left;width:200px; 第二个，margin-left,200px; 他们之间会产生3px的间距。

> 5. 在IE6中没有min-width的概念，其默认width就是min-width，所以有时字体过多它会选择撑开容器。

> 6.  IE6无法定义1px左右高度的容器，是因为默认的行高造成的,解决的方法也有很多,
例如: overflow:hidden zoom:0.08 line-height:1px ⑦ 使用margin ： 0 auto；方法使容器居中依然在IE6中行不通，我们要对其父容器使用text-align:center;

> 7. 被点击访问过的超链接样式不在具有hover和active了,很多人应该都遇到过这个问题,
解决方法是改变CSS属性的排列顺序: L-V-H-A 。
a:link {}  a:visited {}  a:hover {}  a:active {}

> 8. 在使用绝对定位/相对定位时，设置z-index在ie中可能会失效，是因为其元素依赖于其父元素的z-index，而父元素默认为0 ？
所以子元素z-index高，而父元素底，依然不会改变其显示顺序；

> 9. 外边距叠加问题：
box{ margin:10px; background-color:Red; }
box p { margin:20px; background:gray; }
&lt;div id="box"&gt;&lt;p&gt;dd&lt;/p&gt;&lt;/div&gt;
该代码会导致外边距叠加，并且外边距跑到div包裹外去，bug是由于块级子元素高度计算方式造成的。
若是元素没有垂直边框或者padding，那么它的高度就是包含的子元素的顶部和底部边框的的距离。

### JavaScript兼容
在javascript中，各个浏览器基本语法差距不大，其兼容问题主要出现在各个浏览器的实现上，尤其对事件的支持有很大问题，在此我就说说我知道的几个问题。

1. 在标准的事件绑定中绑定事件的方法函数为 addEventListener，而IE使用的是attachEvent。

2. 标准浏览器采用事件捕获的方式，IE采用的是事件冒泡机制，即标准由最外元素至最内元素或者IE由最内元素到最外元素；最后标准方亦觉得IE这方面的比较合理，所以便将事件冒泡纳入了标准，这也是addEventListener第三个参数的由来，而且事件冒泡作为了默认值。

3. 事件处理中非常有用的event属性获得亦不相同，标准浏览器是作为参数带入，而ie是window.event方式获得，获得目标元素标准浏览器为e.target，ie为e.srcElement。

4. 然后在ie中是不能操作tr的innerHtml的。

5. 然后ie日期函数处理与其它浏览器不大一致，比如： var year= new Date().getYear(); 在IE中会获得当前年，但是在firefox中则会获得当前年与1900的差值。通常使用getFullYear()。

6. 关于AJAX的实现上亦有所不同；如果要支持ie6，需要判断MSXML2.XMLHTTP的版本，如果是ie7+或者其他浏览器，可以直接调用原生的XHR来实现。  

就javascript来说，各大浏览器之间的差异还是不少的，但是具体我变得这里都不大关注了，因为我们开发过程中一般都会使用类库，若是不使用，都会自己积累形成一个类库，所以就js而言，兼容性问题基本解决了。
