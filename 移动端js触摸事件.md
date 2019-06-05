# [移动端 js touch事件](https://www.cnblogs.com/fengfan/p/4506555.html)

随着智能手机和平板电脑的普及, 越来越多的人用移动设备浏览网页，我们平时在pc浏览器上用的鼠标事件，比如：click, mouseover等， 已经无法满足移动设备触摸屏的特点，触摸时代的到来，离不开那些触摸事件。

### 触摸事件包含4个接口。

**TouchEvent**

代表当触摸行为在平面上变化的时候发生的事件.

**Touch**

代表用户手指与触摸平面间的一个接触点.

**TouchList**

代表一系列的Touch; 一般在用户多个手指同时接触触控平面时使用这个接口.

**DocumentTouch**

包含了一些创建 Touch对象与TouchList对象的便捷方法.

（参考于 https://developer.mozilla.org/zh-CN/docs/Web/API/Touch_events ）

TouchEvent接口可以响应基本触摸事件（如单个手指点击），它包含了一些具体的事件， 

**事件类型**：

touchstart : 触摸开始（手指放在触摸屏上）

touchmove : 拖动（手指在触摸屏上移动）

touchend : 触摸结束（手指从触摸屏上移开）

touchenter ：移动的手指进入一个dom元素。

touchleave ：移动的手指离开一个dom元素。

还有一个touchcancel，是在拖动中断时候触发。

**事件属性**：

altKey : 该属性返回一个布尔值，表示在指定的事件发生时，Alt 键是否处于按下状态， event.altKey=true|false|1|0

type : 触摸时触发的事件类型，比如touchstart

每个触摸事件都包括了三个触摸属性列表：

\1. touches：当前位于屏幕上的所有手指触摸点的一个列表。

\2. targetTouches：当前元素对象上所有触摸点的列表。

\3. changedTouches：涉及当前事件的触摸点的列表。

它们都是一个数组，每个元素代表一个触摸点。

每个触摸点对应的Touch都有三对重要的属性，clientX/clientY、pageX/pageY、screenX/screenY。

其中screenX/screenY代表事件发生的位置对于屏幕的偏移量，clientX/clienYt和pageX/pageY都代表事件发生位置对应对象的偏移量，不过区别是clientX/clientY不包括对象滚动而隐藏的偏移量，而pageX/pageY包括对象滚动而隐藏的偏移量。移开屏幕的那个触摸点，只会包含在changedTouches列表中，而不会包含在touches 和targetTouches 列表中， 所以changedTouches在项目当中会比较常用。

 示例：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body onload="start();">
<style type="text/css">
#dom {
  width:500px;
  height:500px;
  background:black;
}
</style>
<div id="dom"></div>
<script type="text/javascript">
function onTouchStart(e){
    console.log(e);
}
function start(){
    var dom = document.getElementById('dom');
    dom.addEventListener('touchstart', onTouchStart, false);
}
</script>
</body>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

控制台输出如下：

![img](https://images0.cnblogs.com/blog2015/134316/201505/151753211425883.png)

 

------

 **触摸事件跟鼠标事件的触发先后顺序：**

Touchstart > toucheend > mousemove > mousedown > mouseup > click

很多情况下触摸事件跟鼠标事件会同时触发（目的是为了让没有对触摸设备优化的代码仍然可以在触摸设备上正常工作），如果使用了触摸事件，可以调用event.preventDefault()来阻止鼠标事件被触发。而手指在屏幕上移动touchmove则不会触发鼠标事件和单击事件,在touchmove事件中加入preventDefault, 可以禁止浏览器滚动屏幕，也不会影响单击事件的触发。

以上事件，都系统内置的，可以直接使用，通过这些内置事件，可以组合成很多非原生的多点触摸手势touch手势。

![img](https://images0.cnblogs.com/blog2015/134316/201505/161512284701099.png)

 

Hammer.js是一个轻量级的JavaScript库， 能让你的网站轻松实现触控事件, 它依赖于jQuery，用来控制触摸设备上的多点触控特性。

官网： http://hammerjs.github.io/

多点触摸的实现，想了解更多可以参考： http://www.cnblogs.com/iamlilinfeng/p/4239957.htm 

 

------

 

**zepto**是轻量级兼容juqery的库，适用于移动端开发, 具体使用方法，可参看官网, http://zeptojs.com/

**zepto touch** 是用于单点手势触发的一个touch事件模块。

Touch.js 下载地址： https://github.com/madrobby/zepto/blob/master/src/touch.js

**先看zepto的touch模块实现：**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 $(document)
     .on('touchstart ...',function(e){
              ...
             ...
              now = Date.now()
             delta = now - (touch.last || now)
              if (delta > 0 && delta <= 250) touch.isDoubleTap = true
              touch.last = now
     })
     .on('touchmove ...', function(e){
     })
     .on('touchend ...', function(e){
            ...
            if (deltaX < 30 && deltaY < 30) {
                   var event = $.Event('tap')
                 
                   touch.el.trigger(event)
            }
     })      
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

touch 模块绑定事件 touchstart, touchmove, touchend 到 document上，然后通过计算事件触发的时间差，位置差来实现自定义的tap，swipe事件。

------

 手机上也有click事件，从触摸到响应click事件，有会300的毫秒的延迟，原因在于:

**"**Apple 准备发布iphone的时候，为了解决手机上web页面太小的问题，增加了双击屏幕放大的功能，(double tap to zoom )，当用户触摸屏幕的时候，浏览器不知道用户是要double tap还是要click，所以浏览器在第一次tap事件后会等300ms来判断到底是double tap还是click ，如果在300ms以内点击的话，会以为是double tap，反之是click。**"**

去掉click事件 300ms 的方法：

(1)  在meta里，加 user-scalable=no 可以阻止双击放大，（缺点： 部分浏览器支持）

(2)  使用fastclick.js  它利用多touchstart touchmove 等原生事件的封装，来实现手机上的各种手势，比如tap， swipe 等, 

下载地址 https://github.com/ftlabs/fastclick  

调用很简单：

```
$(function() {
    FastClick.attach(document.body);
});
```

缺点： 文件量有点大，为了解决一小延迟的问题，有点得不偿失。

 

------

 

 **自定义事件**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 // 创建事件对象

  var obj = new Event('sina');
  var elem = document.getElementById('dom');
  //监听sina事件
  elem.addEventListener('sina', function(e){
    console.log(e);
  },false);

  //分发sina事件
  elem.dispatchEvent(obj);
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

另外一个创建事件对象的方法是通过CustomEvent，相比于Event的好处是，它可以给处理事件的函数，自定义detail值，这在实际开发中，可能会经常用到。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
  // 创建事件对象
  var obj = new window.CustomEvent('sina', {
      detail: {'name': 'lily'}
  });
  var elem = document.getElementById('dom');
  //监听sina事件
  elem.addEventListener('sina', function(e){
    // 可以接收到创建事件时，传入的detail值。
    console.log(e. detail);  // {'name': 'lily'}
  },false);
  //分发sina事件
  elem.dispatchEvent(obj);
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

创建自定义事件，一个兼容性较好的函数：

![img](https://images0.cnblogs.com/blog2015/134316/201505/161515186736896.png)

 

------

 

**zepto tap “点透”问题**

Zepto 的tap事件是通过document绑定了touchstart和touchend事件实现，如果绑定tap方法的dom元素在tap方法触发后会隐藏、而“隐藏后，它底下同一位置正好有一个dom元素绑定了click的事件, 而clic事件有300ms延迟，触发click事件。则会出现“点透”现象。 

解决方案：

1 fastclick.js

它的实际原理是在目标元素上绑定touchstart ,touchend事件，然后在touchend这个库直接在touchend的时候就触发了dom上的click事件而替换了本来的触发时间，touch事件是绑定到了具体dom而不是document上,所以e.preventDefault是有效的，可以阻止冒泡，也可以阻止浏览器默认事件。

http://www.cnblogs.com/yexiaochai/p/3442220.html

2、利用fastclick的事件原理， 直接写一段， 采用 e.preventDefault();  阻止“默认行为”，将事件绑定到dom元素上，缺点在于不能使用事件代理。

```
elem.addEventListener(touchend, function(e){
　　e.preventDefault()
},false);
```

\3.  在事件捕获阶段，如果时间差，位置差，均小于指定的值，就阻止冒泡和默认click事件的触发。

![img](https://images0.cnblogs.com/blog2015/134316/201505/161507357675209.png)

4． 用户点击的时候“弹出”一个顶层DIV，屏蔽掉所有事件传递，然后定时自动隐藏, 这个方法比较巧妙。

 

------

 

参考：

tap 模块

https://github.com/alexgibson/tap.js

ghost click

http://ariatemplates.com/blog/2014/05/ghost-clicks-in-mobile-browsers/

JavaScript和事件

http://f2e.im/t/850

 