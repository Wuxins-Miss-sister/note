# px、em、rem、%、vw、wh、vm等单位有什么区别？

2019年05月20日 10:49:29

 

jnshu_it

 

阅读数 4685

更多

所属专栏： [修真院前端小课堂](https://blog.csdn.net/column/details/29472.html)



 版权声明：本文为知乎机构号【技能树IT修真院】原创文章，未经允许不得转载。 https://blog.csdn.net/jnshu_it/article/details/77161717

这里是修真院前端小课堂，本篇分析的主题是

【px、em、rem、%、vw、wh、vm等单位有什么区别？】![img](https://img-blog.csdnimg.cn/2019042618352625.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2puc2h1X2l0,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/2019052010492190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9qbnNodS5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

这里是修真院前端小课堂，每篇分享文从

【背景介绍】【知识剖析】【常见问题】【解决方案】【编码实战】【扩展思考】【更多讨论】【参考文献】

八个方面深度解析前端知识/技能，本篇分享的是：

【px、em、rem、%、vw、wh、vm等单位有什么区别？】

### 1.背景介绍

传统的项目开发中，我们只会用到px、%、em这几个单位，它可以适用于大部分的项目开发，并且拥有比较良好的兼容性。但是你知道吗？从css3开始，浏览器对逻辑单位的支持又提升到了另外一个境界，增加了rem、vh、vw、vm等一些新的长度单位，我们可以利用这些新的单位开发出比较良好的响应式页面，随之覆盖多种不同分辨率的终端，包括移动设备等。现在让我们来看下这些长度单位有什么区别。

### 2.知识剖析

1、px

px就是pixel的缩写，意为像素。px就是一张图片最小的一个点，一张位图就是千千万万的这样的点构成的，比如常常听到的电脑像素是1024x768的，表示的是水平方向是1024个像素点，垂直方向是768个像素点。

兼容性：

2、em

参考物是父元素的font-size，具有继承的特点。如果自身定义了font-size按自身来计算（浏览器默认字体是16px），整个页面内1em不是一个固定的值。

兼容性：

 

3、rem

css3新单位，相对于根元素html（网页）的font-size，不会像em那样，依赖于父元素的字体大小，而造成混乱。

兼容性：

 

4、%

一般宽泛的讲是相对于父元素，但是并不是十分准确。

1、对于普通定位元素就是我们理解的父元素

2、对于position: absolute;的元素是相对于已定位的父元素

3、对于position: fixed;的元素是相对于ViewPort（可视窗口）

兼容性：

 

3、vw

css3新单位，viewpoint width的缩写，视窗宽度，1vw等于视窗宽度的1%。

举个例子：浏览器宽度1200px, 1 vw = 1200px/100 = 12 px。

兼容性：

 

4、vh

css3新单位，viewpoint height的缩写，视窗高度，1vh等于视窗高度的1%。

举个例子：浏览器高度900px, 1 vh = 900px/100 = 9 px。

兼容性：

 

4、vm

css3新单位，相对于视口的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vm

举个例子：浏览器高度900px，宽度1200px，取最小的浏览器高度，1 vm = 900px/100 = 9 px。

由于现在vm的兼容性较差，这里就不做展示了。

你随便转，比例变了算我输

### 3.常见问题

vh vw vm实际应用场景？

### 4.解决方案

vh vw是不包含页面滚动条的视窗宽度(innerwidth)，%包含了滚动条的宽度在里面了(outerwidth)。

一般的情况下%就可以满足大部分自适应设计的需求，可以用height：100vh做一个高度占满屏幕的自适应，没有滚动条。

用vw，vh设定的大小只和视窗大小有关，所以用来开发多种屏幕设备的应用用这个单位还是挺合适的。

### 5.编码实战

[点击这里](http://www.jnshu.com/login/1/81391788)

### 6.扩展思考

css还有哪些长度单位？

in:寸

cm:厘米

mm:毫米

t:point，大约1/72寸

pc:pica，大约6pt，1/6寸

1in = 2.54cm = 25.4 mm = 72pt = 6pc = 96px