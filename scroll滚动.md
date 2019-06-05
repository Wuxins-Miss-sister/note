# [深入理解滚动scroll](https://www.cnblogs.com/xiaohuochai/p/5831640.html)![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAoklEQVQ4T+2T4Q2CMBCFv27CBjgCG+gIjAAbOAIjOIJs4Ai6gRvIBpjXXCOp19T/8pJLoTneXcj3Ah91wAV4bu68xwXoAZ2EzEAmE9AWTB6AelRDyaAx9zgh0wE4ATczcTdIE7wl0oe7wX/8RMHigfQTB3fDdM1IEvYyONdIVEOSqDwCY2Z2NaS/UNbqMSQmvauUPlfbNKpBSdTUVyXSs/XyBlRCNBG20I28AAAAAElFTkSuQmCC)



## 前面的话

　　前面两篇博文分别介绍过[偏移大小](http://www.cnblogs.com/xiaohuochai/p/5828369.html)、[客户区大小](http://www.cnblogs.com/xiaohuochai/p/5830053.html)。本文介绍元素尺寸中内容最多的一部分——滚动scroll

 

### 滚动宽高

**scrollHeight**

　　scrollHeight表示元素的总高度，包括由于溢出而无法展示在网页的不可见部分

**scrollWidth**

　　scrollWidth表示元素的总宽度，包括由于溢出而无法展示在网页的不可见部分

　　[注意]IE7-浏览器返回值是不准确的

　　【1】没有滚动条时，scrollHeight与clientHeight属性结果相等，scrollWidth与clientWidth属性结果相等

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>
<script>
//120 120
console.log(test.scrollHeight,test.scrollWidth);
//120 120
console.log(test.clientHeight,test.clientWidth);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【2】存在滚动条时，但元素设置宽高大于等于元素内容宽高时，scroll和client属性的结果相等

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:1;">
    内容<br>内容<br>
</div>
<script>
//103(120-17) 103(120-17)
console.log(test.scrollHeight,test.scrollWidth);
//103(120-17) 103(120-17)
console.log(test.clientHeight,test.clientWidth);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【3】存在滚动条，但元素设置宽高小于元素内容宽高，即存在内容溢出的情况时，scroll属性大于client属性

　　[注意]scrollHeight属性存在兼容性问题，chrome和safari浏览器中，scrollHeight包含padding-bottom；而IE和firefox不包含padding-bottom

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:200px;">
    内容</div>
<script>
//chrome/safari:220(200+10+10)
//firefox/IE:210(200+10)
console.log(test.scrollHeight);
//103(120-17)
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

### 页面尺寸

　　document.documentElement.clientHeight表示页面的可视区域的尺寸，而document.documentElement.scrollHeight表示html元素内容的实际尺寸。但是由于各个浏览器表现不一样，分为以下几种情况

　　【1】html元素没有滚动条时，IE和firefox的client和scroll属性始终相同，且返回可视区的尺寸大小；而safari和chrome表现正常，clientHeight返回可视区域大小，而scrollHeight返回元素内容大小

```
//firefox:  755 755
//chrome:   947 8(body元素的margin)
//safari:   744 8(body元素的margin)
//IE:       768 768
console.log(document.documentElement.clientHeight,document.documentElement.scrollHeight)
```

　　【2】html元素存在滚动条时，各个浏览器都表现正常。clientHeight返回可视区域大小，而scrollHeight返回元素内容大小

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<script>
//firefox:  755 1016(1000+8*2)
//chrome:   947 1016(1000+8*2)
//safari:   744 1016(1000+8*2)
//IE:       768 1016(1000+8*2)
console.log(document.documentElement.clientHeight,document.documentElement.scrollHeight)
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**兼容**

　　因此要取得文档实际高度时，要取得<html>元素的scrollHeight和clientHeight的最大值

```
var docHeight = Math.max(document.documentElement.scrollHeight,document.documentElement.clientHeight);
var docWidth  = Math.max(document.documentElement.scrollWidth,document.documentElement.clientWidth);
```

 

### 滚动长度

**scrollTop**

　　scrollTop属性表示被隐藏在内容区域上方的像素数。元素未滚动时，scrollTop的值为0，如果元素被垂直滚动了，scrollTop的值大于0，且表示元素上方不可见内容的像素宽度

**scrollLeft**

　　scrollLeft属性表示被隐藏在内容区域左侧的像素数。元素未滚动时，scrollLeft的值为0，如果元素被水平滚动了，scrollLeft的值大于0，且表示元素左侧不可见内容的像素宽度

　　当滚动条滚动到内容底部时，符合以下等式

```
scrollHeight == scrollTop  + clientHeight
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:200px;">
    内容</div>
<button id='btn1'>点击</button>
<div id="result"></div>
<script>
btn1.onclick = function(){
    result.innerHTML = 'scrollTop:' + test.scrollTop+';clientHeight:' + test.clientHeight + ';scrollHeight:' + test.scrollHeight
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



　　与scrollHeight和scrollWidth属性不同的是，scrollLeft和scrollTop是可写的

　　[注意]为scrollLeft和scrollTop赋值为负值时，并不会报错，而是静默失败

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:200px;">
    内容</div>
<button id='btn1'>向下滚动</button>
<button id='btn2'>向上滚动</button>
<script>
btn1.onclick = function(){test.scrollTop += 10;}
btn2.onclick = function(){test.scrollTop -= 10;}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



 

### 页面滚动

　　理论上，通过document.documentElement.scrollTop和scrollLeft可以反映和控制页面的滚动；但是chrome和safari浏览器是通过document.body.scrollTop和scrollLeft来控制的

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<button id='btn1' style="position:fixed;top:0;">点击</button>
<div id="result" style="position:fixed;top:30px;"></div>
<script>
btn1.onclick = function(){
    result.innerHTML = 'html的scrollTop:' + document.documentElement.scrollTop +';body的scrollTop:' + document.body.scrollTop;
}
</script>    
</body>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



　　所以，页面的滚动高度兼容写法是

```
var docScrollTop = document.documentElement.scrollTop || document.body.scrollTop
```

**回到顶部**

　　可以利用scrollTop来实现回到顶部的功能

```
function scrollTop(){
    if((document.body.scrollTop || document.documentElement.scrollTop) != 0){
        document.body.scrollTop = document.documentElement.scrollTop = 0;
    }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<button id='btn' style="position:fixed">回到顶部</button>
<script>
function scrollTop(){
    if((document.body.scrollTop || document.documentElement.scrollTop) != 0){
        document.body.scrollTop = document.documentElement.scrollTop = 0;
    }
}
btn.onclick = scrollTop;
</script>
</body>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



　　还有两个window的只读属性可以获取整个页面滚动的像素值，它们是pageXOffset和pageYOffset

**pageXOffset**

　　pageXOffset表示水平方向上页面滚动的像素值

**pageYOffset**

　　pageYOffset表示垂直方向上页面滚动的像素值

　　[注意]IE8-浏览器不支持

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<button id='btn1' style="position:fixed;top:0;">点击</button>
<div id="result" style="position:fixed;top:30px;"></div>
<script>
btn1.onclick = function(){
    result.innerHTML = 'pageYOffset:' + window.pageYOffset;
}
</script>    
</body>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



 

### 滚动方法

**scrollTo(x,y)**

　　scrollTo(x,y)方法滚动当前window中显示的文档，让文档中由坐标x和y指定的点位于显示区域的左上角

```
<body style="height:1000px">
<button id='btn' style="position:fixed">滚动</button>
<script>
btn.onclick = function(){scrollTo(0,0);}
</script>
```

**scrollBy(x,y)**

　　scrollBy(x,y)方法滚动当前window中显示的文档，x和y指定滚动的相对量

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<button id='btn1' style="position:fixed">向下滚动</button>
<button id='btn2' style="position:fixed;top:40px">向上滚动</button>
<script>
btn1.onclick = function(){scrollBy(0,100);}
btn2.onclick = function(){scrollBy(0,-100);}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



【小应用】

　　利用scrollBy()加setInterval[计时器](http://www.cnblogs.com/xiaohuochai/p/5773183.html)实现简单的快速滚动功能

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<button id='btn1' style="position:fixed">开始滚动</button>
<button id='btn2' style="position:fixed;top:40px">停止滚动</button>
<script>
var timer = 0;
btn1.onclick = function(){
    timer = setInterval(function(){
        scrollBy(0,10);
    },100)}
btn2.onclick = function(){
    clearInterval(timer);
    timer = 0;
}
</script>    
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



**scrollIntoView()**

　　Element.scrollIntoView方法滚动当前元素，进入浏览器的可见区域

　　该方法可以接受一个布尔值作为参数。如果为true，表示元素的顶部与当前区域的可见部分的顶部对齐（前提是当前区域可滚动）；如果为false，表示元素的底部与当前区域的可见部分的尾部对齐（前提是当前区域可滚动）。如果没有提供该参数，默认为true

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<div id="test" style="height:100px;width:100px;position:absolute;left:0;top:500px;background-color:green"></div>
<button id='btn1' style="position:fixed">滚动到页面开头</button>
<button id='btn2' style="position:fixed;top:40px">滚动到页面结尾</button>
<script>
btn1.onclick = function(){
    test.scrollIntoView();
};
btn2.onclick = function(){
    test.scrollIntoView(false);
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



**scrollIntoViewIfNeeded()**

　　scrollIntoViewIfNeeded(true)方法只在当前元素在视口中不可见的情况下，才滚动浏览器窗口或容器元素，最终让它可见。如果当前元素在视口中可见，这个方法什么也不做 

　　如果将可选的alignCenter参数设置为true，则表示尽量将元素显示在视口中部(垂直方向)

　　[注意]该方法只有chrome和safari支持

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<div id="test" style="height:100px;width:100px;position:absolute;left:0;top:500px;background-color:green"></div>
<button id='btn' style="position:fixed">滚动到页面中间</button>
<script>
btn.onclick = function(){
    test.scrollIntoViewIfNeeded(true)
};
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



**scrollByLines(lineCount)**

　　scrollByLines(lineCount)方法将元素的内容滚动指定的行髙，lineCount值可以是正值， 也可以是负值

　　[注意]该方法只有safari支持

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:200px;">
    内容</div>
<button id='btn1'>向下滚动</button>
<button id='btn2'>向上滚动</button>
<script>
btn1.onclick = function(){test.scrollByLines(1);}
btn2.onclick = function(){test.scrollByLines(-1);}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**scrollByPages(pageCount)**

　　scrollByPages(pageCount)方法将元素的内容滚动指定的页面高度，具体高度由元素的高度决定

　　[注意]该方法只有safari支持

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:200px;">
    内容</div>
<button id='btn1'>向下滚动</button>
<button id='btn2'>向上滚动</button>
<script>
btn1.onclick = function(){test.scrollByPages(1);}
btn2.onclick = function(){test.scrollByPages(-1);}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

### 滚动事件

　　scroll事件是在window对象上发生的，它表示的是页面中相应元素的变化。当然，scroll事件也可以用在有滚动条的元素上

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="height:1000px">
<div id="result" style="position:fixed;top:10px;"></div>
<script>
window.onscroll = function(){
    result.innerHTML = '页面的scrollTop:' + (document.documentElement.scrollTop||document.body.scrollTop);
}
</script>    
</body>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)



 

## 最后

　　本文详细介绍了滚动scroll的知识，基本上囊括了关于滚动现有的所有属性和方法。本文中并未详细介绍滚动条，详细内容[移步至此](http://www.cnblogs.com/xiaohuochai/p/5294409.html)

　　下文将以实例的形式，对滚动的属性和方法进行应用，总结回到顶部的多种写法，并尝试优化

　　欢迎交流



# 偏移量

# [深入理解定位父级offsetParent及偏移大小](https://www.cnblogs.com/xiaohuochai/p/5828369.html)![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAoklEQVQ4T+2T4Q2CMBCFv27CBjgCG+gIjAAbOAIjOIJs4Ai6gRvIBpjXXCOp19T/8pJLoTneXcj3Ah91wAV4bu68xwXoAZ2EzEAmE9AWTB6AelRDyaAx9zgh0wE4ATczcTdIE7wl0oe7wX/8RMHigfQTB3fDdM1IEvYyONdIVEOSqDwCY2Z2NaS/UNbqMSQmvauUPlfbNKpBSdTUVyXSs/XyBlRCNBG20I28AAAAAElFTkSuQmCC)



## 前面的话

　　偏移量(offset dimension)是javascript中的一个重要的概念。涉及到偏移量的主要是offsetLeft、offsetTop、offsetHeight、offsetWidth这四个属性。当然，还有一个偏移参照——定位父级offsetParent。本文将详细介绍该部分内容

![img](https://images2015.cnblogs.com/blog/740839/201609/740839-20160901091826449-1099471755.jpg)

 

### 定位父级

　　在理解偏移大小之前，首先要理解offsetParent。人们并没有把offsetParent翻译为偏移父级，而是翻译成定位父级，很大原因是offsetParent与定位有关

　　定位父级offsetParent的定义是：与当前元素最近的经过定位(position不等于static)的父级元素，主要分为下列几种情况 

　　【1】元素自身有fixed定位，offsetParent的结果为null

　　当元素自身有[fixed固定定位](http://www.cnblogs.com/xiaohuochai/p/5321487.html#anchor2)时，我们知道固定定位的元素相对于视口进行定位，此时没有定位父级，offsetParent的结果为[null](http://www.cnblogs.com/xiaohuochai/p/5665637.html#anchor3)

　　[注意]firefox浏览器有兼容性问题

```
<div id="test" style="position:fixed"></div>    
<script>
//firefox并没有考虑固定定位的问题，返回<body>，其他浏览器都返回null
console.log(test.offsetParent);
</script>
```

　　【2】元素自身无fixed定位，且父级元素都未经过定位，offsetParent的结果为<body>

```
<div id="test"></div>    
<script>
console.log(test.offsetParent);//<body>
</script>
```

　　【3】元素自身无fixed定位，且父级元素存在经过定位的元素，offsetParent的结果为离自身元素最近的经过定位的父级元素

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="div0" style="position:absolute;">
    <div id="div1" style="position:absolute;">
        <div id='test'></div>    
    </div>    
</div>
<script>
console.log(test.offsetParent);    //<div id="div1">
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【4】<body>元素的parentNode是null

```
console.log(document.body.offsetParent);//null
```

**IE7-浏览器Bug**

　　对于定位父级offsetParent来说，IE7-浏览器存在以下bug

　　【bug1】当元素本身经过[绝对定位](http://www.cnblogs.com/xiaohuochai/p/5312917.html)或[相对定位](http://www.cnblogs.com/xiaohuochai/p/5321487.html#anchor1)，且父级元素无经过定位的元素时，IE7-浏览器下，offsetParent是<html>

```
<div id="test" style="position:absolute;"></div>    
<script>
//IE7-浏览器返回<html>，其他浏览器返回<body>
console.log(test.offsetParent);
</script>
<div id="test" style="position:relative;"></div>    
<script>
//IE7-浏览器返回<html>，其他浏览器返回<body>
console.log(test.offsetParent);
</script>
<div id="test" style="position:fixed;"></div>    
<script>
//firefox并没有考虑固定定位的问题，返回<body>，其他浏览器都返回null
console.log(test.offsetParent);
</script>
```

　　【bug2】如果父级元素存在触发haslayout的元素或经过定位的元素，且offsetParent的结果为离自身元素最近的经过定位或触发haslayout的父级元素

　　[注意]关于haslayout的详细信息[移步至此](http://www.cnblogs.com/xiaohuochai/p/4845314.html)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="div0" style="display:inline-block;">
    <div id='test'></div>    
</div>
<script>
//IE7-浏览器返回<div id="div0">，其他浏览器返回<body>
console.log(test.offsetParent);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="div0" style="position:absolute;">
    <div id="div1" style="display:inline-block;">
        <div id='test'></div>    
    </div>    
</div>
<script>
//IE7-浏览器返回<div id="div1">，其他浏览器返回<div id="div0">
console.log(test.offsetParent);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="div0" style="display:inline-block;">
    <div id="div1" style="position:absolute;">
        <div id='test'></div>    
    </div>    
</div>
<script>
//所有浏览器都返回<div id="div1">
console.log(test.offsetParent);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

### 偏移量

　　偏移量共包括offsetHeight、offsetWidth、offsetLeft、offsetTop这四个属性

**offsetWidth**

　　offsetWidth表示元素在水平方向上占用的空间大小，无单位(以像素px计)

```
offsetWidth =  border-left-width + padding-left + width + padding-right + border-right-width; 
```

**offsetHeight**

　　offsetHeight表示元素在垂直方向上占用的空间大小，无单位(以像素px计)

```
offsetHeight =  border-top-width + padding-top + height + padding-bottom + border-bottom-width
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width:100px; height:100px; padding:10px; margin:10px; border:1px solid black;"></div>    
<script>
//122=1+10+100+10+1
console.log(test.offsetWidth);
console.log(test.offsetHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　[注意]如果存在垂直[滚动条](http://www.cnblogs.com/xiaohuochai/p/5294409.html)，offsetWidth也包括垂直滚动条的宽度；如果存在水平滚动条，offsetHeight也包括水平滚动条的高度

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width:100px; height:100px; padding:10px; margin:10px; border:1px solid black; overflow: scroll;"></div>    
<script>
//IE8-浏览器将垂直滚动条的宽度计算在width宽度和height高度中，width和height的值仍然是100px；
//而其他浏览器则把垂直滚动条的宽度从width宽度中移出，把水平滚动条的高度从height高度中移出，则滚动条宽度为17px，width宽度和height高度为剩下的83px

if(window.getComputedStyle){
    console.log(getComputedStyle(test).width,getComputedStyle(test).height)//83px
}else{
    console.log(test.currentStyle.width,test.currentStyle.height);//100px
}
//122=1+10+100+10+1
console.log(test.offsetWidth,test.offsetHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**offsetTop**

　　offsetTop表示元素的上外边框至offsetParent元素的上内边框之间的像素距离

**offsetLeft**

　　offsetLeft表示元素的左外边框至offsetParent元素的左内边框之间的像素距离

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="out" style="padding: 5px;position: relative;background-color: pink;margin: 6px;border:1px solid black">
    <div id="test" style="width:100px; height:100px; margin:10px;background-color:green;"></div>        
</div>
<script>
//15=test.marginTop(10) + out.paddingTop(5)
alert(test.offsetTop);
//15=test.marginLeft(10) + out.paddingLeft(5)
alert(test.offsetLeft);
</script>    
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**IE7-Bug**

　　IE7-浏览器在offsetTop属性的处理上存在bug

　　【1】若父级设置position: relative，则在IE7-浏览器下，offsetTop值为offsetParent元素的paddingBottom值

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="out" style="padding: 5px;position: relative;">
    <div id="test" style="width:100px; height:100px; margin:10px;"></div>        
</div>
<script>
//其他浏览器返回15(5+10)，而IE7-浏览器返回5
console.log(test.offsetTop);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【2】若父级设置position: aboslute(或其他触发haslayout的条件)，offsetTop值为offsetParent元素的paddingBottom值和当前元素的marginTop值的较大值

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="out" style="padding: 5px;position:absolute;">
    <div id="test" style="width:100px; height:100px; margin:10px;"></div>        
</div>
<script>
//其他浏览器返回15(5+10)，而IE7-浏览器返回10(10和5的较大值)
console.log(test.offsetTop);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

### 页面偏移

　　要知道某个元素在页面上的偏移量，将这个元素的offsetLeft和offsetTop与其offsetParent的相同属性相加，并加上offsetParent的相应方向的边框，如此循环直到根元素，就可以得到元素到页面的偏移量

　　[注意]在默认情况下，IE8-浏览器下如果使用currentStyle()方法获取<html>和<body>(甚至普通div元素)的边框宽度都是medium，而如果使用[clientLeft](http://www.cnblogs.com/xiaohuochai/p/5830053.html#anchor1)(或clientTop)获取边框宽度，则是实际的数值

```
html,body{border: 0;}
body{margin:0;}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
function getElementLeft(element){
    var actualLeft = element.offsetLeft;
    var current = element.offsetParent;
    while(current != null){
        actualLeft += current.offsetLeft + current.clientLeft;
        current = current.offsetParent;
    }
    return actualLeft + 'px';
}
function getElementTop(element){
    var actualTop = element.offsetTop;
    var current = element.offsetParent;
    while(current != null){
        actualTop += current.offsetTop + current.clientTop;
        current = current.offsetParent;
    }
    return actualTop + 'px';
} 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div style="padding: 20px;border:1px solid black;position:absolute;">
    <div id="test" style="width:100px; height:100px; margin:10px;"></div>        
</div>        
<script>
//其他浏览器返回31(10+20+1)，而IE7-浏览器返回21((20和10的较大值)+1)
console.log(getElementTop(test));
//所有浏览器返回31(10+20+1)
console.log(getElementLeft(test));
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

### 注意事项

　　【1】所有偏移量属性都是只读的

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width:100px; height:100px; margin:10px;"></div>        
<script>
console.log(test.offsetWidth);//100
//IE8-浏览器会报错，其他浏览器则静默失败
test.offsetWidth = 10;
console.log(test.offsetWidth);//100
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【2】如果给元素设置了display:none，则它的偏移量属性都为0

```
<div id="test" style="width:100px; height:100px; margin:10px;display:none"></div>
<script>
console.log(test.offsetWidth);//0
console.log(test.offsetTop);//0
</script>
```

　　【3】每次访问偏移量属性都需要重新计算

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width:100px; height:100px; margin:10px;"></div>        
<script>
console.time("time");
for(var i = 0; i < 100000; i++){
    var a = test.offsetWidth;
}
console.timeEnd('time');//65.129ms
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width:100px; height:100px; margin:10px;"></div>        
<script>
console.time("time");
var a = test.offsetWidth;
for(var i = 0; i < 100000; i++){
    var b = a;
}
console.timeEnd('time');//1.428ms
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　由上面代码对比可知，重复访问偏移量属性需要耗费大量的性能，所以要尽量避免重复访问这些属性。如果需要重复访问，则把它们的值保存在变量中，以提高性能



# [深入理解客户区尺寸client](https://www.cnblogs.com/xiaohuochai/p/5830053.html)![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAoklEQVQ4T+2T4Q2CMBCFv27CBjgCG+gIjAAbOAIjOIJs4Ai6gRvIBpjXXCOp19T/8pJLoTneXcj3Ah91wAV4bu68xwXoAZ2EzEAmE9AWTB6AelRDyaAx9zgh0wE4ATczcTdIE7wl0oe7wX/8RMHigfQTB3fDdM1IEvYyONdIVEOSqDwCY2Z2NaS/UNbqMSQmvauUPlfbNKpBSdTUVyXSs/XyBlRCNBG20I28AAAAAElFTkSuQmCC)



## 前面的话

　　关于元素尺寸，一般地，有偏移大小offset、客户区大小client和滚动大小scroll。前文已经介绍过[偏移属性](http://www.cnblogs.com/xiaohuochai/p/5828369.html)，后文将介绍[scroll滚动大小](http://www.cnblogs.com/xiaohuochai/p/5831640.html)，本文主要介绍客户区大小client

![img](https://images2015.cnblogs.com/blog/740839/201609/740839-20160901152045574-1466453.jpg)

 

### 客户区大小

　　客户区大小client指的是元素内容及其内边距所占据的空间大小

**clientHeight**

　　clientHeight属性返回元素节点的客户区高度

```
clientHeight = padding-top + height + padding-bottom
```

**clientWidth**

　　clientWidth属性返回元素节点的客户区宽度

```
clientWidth = padding-left + width + padding-right
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>
<script>
//120(10+100+10)
console.log(test.clientHeight);
console.log(test.clientWidth);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　[注意]滚动条宽度不计算在内

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll"></div>
<script>
//103(120-17)，滚动条宽度为17px
console.log(test.clientHeight);
console.log(test.clientWidth);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width:100px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:1;height:100px">
    内容<br>内容<br>内容<br>内容<br>内容<br>内容<br>
</div>
<script>
//83(100-17)
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　当height和纵向padding的和为0(以及小于17px的情况)时，如果仍然存在滚动条，各浏览器表现不一样

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height:0;margin: 10px;border: 1px solid black;overflow:scroll"></div>
<script>
//chrome/safari:-17(0-17)
//firefox/IE:0
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height:10px;margin: 10px;border: 1px solid black;overflow:scroll"></div>
<script>
//chrome/safari:-7(10-17)
//firefox/IE:0
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**bug**

　　如果设置overflow:scroll，使得滚动条始终存在，当不设置高度height值时，各个浏览器表现不一样。firefox存在一个最小高度为34px的垂直滚动条，IE7-浏览器存在一个最小高度为19px的垂直滚动条，而其他浏览器的垂直滚动条无最小高度　

　　所以，当clientHeight的值小于34px时，firefox会返回34；当clientHeight的值小于19px时，IE7-会返回19

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;margin: 10px;border: 1px solid black;overflow:scroll"></div>
<script>
//chrome/IE8+/safari:0(因为height和padding都是0)
//firefox:34(设置overflow:scroll之后，默认存在一个高34px的垂直滚动条)
//IE7-:19(默认存在一个高19px的垂直滚动条)
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;margin: 10px;border: 1px solid black;font-size:20px;line-height:1;overflow:scroll">内容</div>
<script>
//chrome/IE8+/safari:20(20*1)
//firefox:34(20<34)
//IE7-:20(20>19)
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;padding-top:20px;margin: 10px;border: 1px solid black;font-size:20px;line-height:1;overflow:scroll">内容</div>
<script>
//chrome/IE8+/safari:40(20*1+20)
//firefox:40(40>34)
//IE7-:40(40>19)
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**clientLeft**

　　clientLeft属性返回左边框的宽度

**clientTop**

　　clientTop属性返回上边框的宽度

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>
<script>
//1 1
console.log(test.clientLeft);
console.log(test.clientTop);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　[注意]如果display为inline时，clientLeft属性和clientTop属性都返回0

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="display:inline;width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>
<script>
//0 0
console.log(test.clientLeft);
console.log(test.clientTop);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

### 页面大小

　　常用document.documentElement的client属性来表示页面大小(不包含滚动条宽度)

　　[注意]在IE7-浏览器中，<html>元素默认存在垂直滚动条

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="overflow:scroll">
<script>
//1903(1920-17)
console.log(document.documentElement.clientWidth);
//930(947-17)
console.log(document.documentElement.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　另一对常用的表示页面大小的属性是window.innerHeight和innerWidth属性(包含滚动条宽度)

　　innerHeight和innerWidth表示的是浏览器窗口大小减去菜单栏、地址栏等剩余的页面尺寸，由于滚动条是属于页面的，所以包含滚动条

　　[注意]IE8-浏览器不支持innerHeight和innerWidth属性

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<body style="overflow:scroll">
<script>
//1920
console.log(window.innerWidth);
//947
console.log(window.innerHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　如果没有滚动条，这两类属性在电脑端表示同样的值，但是却表示不同的含义。在移动端，innerWidth和innerHeight表示的是视觉视口，即用户正在看到的网站的区域；而document.documentElement.clientWidth和clientHeight表示的是布局视口，指CSS布局的尺寸。详细情况[移步至此](http://www.cnblogs.com/xiaohuochai/p/5496995.html)

　　[注意]页面的客户区大小和页面的实际大小是不同的，页面的实际大小将由后文的[scroll滚动大小](http://www.cnblogs.com/xiaohuochai/p/5831640.html)来表示

 

### 注意事项

　　【1】所有客户区client属性都是只读的

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>
<script>
console.log(test.clientHeight);
//IE8-浏览器会报错，其他浏览器则静默失败
test.clientHeight = 10;
console.log(test.clientHeight);
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【2】如果给元素设置了display:none，则客户区client属性都为0

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;display:none;"></div>
<script>
console.log(test.clientHeight);//0
console.log(test.clientTop);//0
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　【3】每次访问客户区client属性都需要重新计算，重复访问需要耗费大量的性能，所以要尽量避免重复访问这些属性。如果需要重复访问，则把它们的值保存在变量中，以提高性能

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>      
<script>
console.time("time");
for(var i = 0; i < 100000; i++){
    var a = test.clientHeight;
}
console.timeEnd('time');//66.798ms
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>         
<script>
console.time("time");
var a = test.clientHeight;
for(var i = 0; i < 100000; i++){
    var b = a;
}
console.timeEnd('time');//1.705ms
</script>
```

