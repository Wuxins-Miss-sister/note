# [Flex 弹性布局(****************************************************)](https://www.cnblogs.com/libin-1/p/6024980.html)



多行自适应，多列自适应，间隔也能自适应，任意对齐

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102145155143-782417636.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102145154361-1757353953.png)

 

 

**创建弹性容器  flex container**

display: block | inline  | inline-block  | none | flex

 

 

**弹性元素  flex item**

是不是flex container 弹性容器中所有的子元素都是  弹性元素呢？

不是的，只有弹性容器，在文档流中的直接子元素(不包含孙子元素 )才是弹性元素。

 

 

**flex 布局特性**

排列和方向

| flex排列和方向的属性 | 描述       |
| -------------------- | ---------- |
| flex-direction       | 弹性的方向 |
| flex-wrap            | 弹性的换行 |
| flex-flow            | 弹性的流   |
| order                | 弹性的顺序 |

 

 

flex-direction

| flex-direction取值 | 描述     |
| ------------------ | -------- |
| row                | 行       |
| row-reverse        | 从右向左 |
| column             | 从上到下 |
| column-reverse     | 从下到上 |

 

row (flex-direction默认值)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102145156330-484205738.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102145155924-123759659.png)

 

 

row-reverse

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102145157174-956818276.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102145156768-1865504942.png)

 

column

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102145157877-31994888.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102145157455-2111504589.png)

 

column-reverse

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102145158768-1367105097.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102145158408-697622862.png)

 

举个栗子：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>flex direction</title>
    <style type="text/css">
    .container{margin: 20px;line-height: 40px;font-size: 20px;color: #fff;background-color: #963297;}
    .item{margin: 10px;line-height: 40px;text-align: center;background-color: #c99702;}
    .container0 .item, .container1 .item{padding: 0 12px;}


    .container{display:flex;}
    .container1{flex-direction: row-reverse;}
    .container2{flex-direction: column;}
    .container3{flex-direction: column-reverse;}
    </style>
</head>
<body>
<div class="container container0">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
</div>
<div class="container container1">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
</div>
<div class="container container2">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
</div>
<div class="container container3">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
</div>
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102150754143-1944261621.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102150753580-1599563659.png)

 

 

flex-wrap

| flex-wrap取值 | 描述             |
| ------------- | ---------------- |
| nowrap        | 不换行（默认值） |
| wrap          | 换行             |
| wrap-reverse  |                  |

 

wrap

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154950111-1290705342.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102154949486-1250854368.png)

 

举个栗子：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>flex-direction</title>
    <style type="text/css">
    .container{width: 400px;margin: 20px;line-height: 40px;font-size: 20px;color: #fff;background-color: #963297;}
    .item{margin: 10px;width: 100px;line-height: 40px;text-align: center;background-color: #c99702;}

    .container{display: flex;}
    .container1{flex-wrap: wrap;}
    .container2{flex-wrap: wrap-reverse;}
    </style>
</head>
<body>

<div class="container container0">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
</div>

<div class="container container1">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
</div>

<div class="container container2">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
</div>

</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154951955-1931728523.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102154951018-468118532.png)

 

[flex-flow(推荐使用)](http://www.css88.com/book/css/properties/flex/flex-flow.htm)

**语法:**

**flex-flow**：<' [flex-direction](http://www.css88.com/book/css/properties/flex/flex-direction.htm) '> || <' [flex-wrap](http://www.css88.com/book/css/properties/flex/flex-wrap.htm) '>

默认值：看各分拆属性
适用于：flex容器
继承性：无
动画性：否
计算值：指定值

 

**取值：**

<' flex-direction '>：定义弹性盒子元素的排列方向。
<' flex-wrap '>：控制flex容器是单行或者多行。

 

**说明:**

复合属性。设置或检索弹性盒模型对象的子元素排列方式。

 

推荐使用 flex-flow ,而不是单独用flex-direction  或 flew-wrap

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154953143-1678064290.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102154952611-1602221486.png)初始值   row   nowrap

 

 

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154954549-26411838.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102154954127-852955257.png)[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154955893-1995109308.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102154954924-836357268.png)

 

 

order

order 是一个『相对值』 ，是排在主轴上的顺序

order 值越大，排名越靠后。

| order取值 | 描述      |
| --------- | --------- |
| order     | 整数      |
| initial   | 初始值  0 |

![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154957315-658073128.png)

 

举个栗子:

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>order</title>
    <style type="text/css">
    .container{
        display: flex;
        background-color: #963297;
        width: 300px;
        padding:3px;
    }

    .item{
        color: #fff;
        width: 50px;
        line-height: 30px;
        background-color: #d29201;
        margin: 4px;
        text-align: center;
    }
    .item1{order: 10;}
    .item2{order: 2;}
    .item3{order: 3;}

    </style>
</head>
<body>
<div class="container">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102154958299-406777820.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102154958002-2048009504.png)

 

 

**弹性**

**flex弹性相关的属性**

- flex-grow
- flex-shrink
- flex-basis

 

[flex-basis](http://www.css88.com/book/css/properties/flex/flex-basis.htm)

设置『flex item』的 『初始宽度、 高度』

横向排列时，设置的是宽

纵向排列时，设置的是高

 

#### 语法：

> **flex-basis**：[](http://www.css88.com/book/css/values/length/index.htm) | [](http://www.css88.com/book/css/values/numeric/percentage.htm) | auto | content
>
> **默认值**：auto
>
> **适用于**：flex子项
>
> **继承性**：无
>
> **动画性**：是，当值为非关键字时
>
> **计算值**：指定值
>
>  

#### 取值：

>  
>
> <length>
>
> ： 用长度值来定义宽度。不允许负值
>
> <percentage>
>
> ：用百分比来定义宽度。不允许负值auto： 无特定宽度值，取决于其它属性值content： 基于内容自动计算宽度

#### 说明：

> **设置或检索弹性盒伸缩基准值。**

- 如果所有子元素的基准值之和大于剩余空间，则会根据每项设置的基准值，按比率伸缩剩余空间
- 对应的脚本特性为**flexBasis**。

 

[flex-grow](http://www.css88.com/book/css/properties/flex/flex-grow.htm)

设置元素所能分配到的空余空间的比例。

**语法:**

> **flex-grow**：[](http://www.css88.com/book/css/values/numeric/number.htm)
>
> **默认值**：0
>
> **适用于**：flex子项
>
> **继承性**：无
>
> **动画性**：是
>
> **计算值**：指定值
>
>  

取值：

 

- [](http://www.css88.com/book/css/values/numeric/number.htm)：用数值来定义扩展比率。不允许负值

 

#### 说明：

- 根据弹性盒子元素所设置的扩展因子作为比率来分配剩余空间。

flex-basis + flow-grow / sum(flow-grow) * remain

 

[flex-shrink](http://www.css88.com/book/css/properties/flex/flex-shrink.htm)

把负的剩余空间平摊

**语法:**

> flex-shrink：<number>
> 默认值：1
> 适用于：flex子项
> 继承性：无
> 动画性：是
> 计算值：指定值

 

取值:

> <number>：用数值来定义收缩比率。不允许负值

 

说明:

> 设置或检索弹性盒的收缩比率。
> 根据弹性盒子元素所设置的收缩因子作为比率来收缩空间。

flex-basis + flow-shrink / sum(flow-shrink) * remain

 

[flex(推荐使用)](http://www.css88.com/book/css/properties/flex/flex.htm)

语法

> flex：none | <' flex-grow '> <' flex-shrink >'? || <' flex-basis '>
> 默认值：看各分拆属性
> 适用于：flex子项
> 继承性：无
> 动画性：否
> 计算值：看各分拆属性

 

取值

> none：none关键字的计算值为: 0 0 auto
> <' flex-grow '>：用来指定扩展比率，即剩余空间是正值时此「flex子项」相对于「flex容器」里其他「flex子项」能分配到空间比例。
> 在「flex」属性中该值如果被省略则默认为「1」
> <' flex-shrink '>：用来指定收缩比率，即剩余空间是负值时此「flex子项」相对于「flex容器」里其他「flex子项」能收缩的空间比例。
> 在收缩的时候收缩比率会以伸缩基准值加权
> 在「flex」属性中该值如果被省略则默认为「1」
> <' flex-basis '>：用来指定伸缩基准值，即在根据伸缩比率计算出剩余空间的分布之前，「flex子项」长度的起始数值。
> 在「flex」属性中该值如果被省略则默认为「0%」
> 在「flex」属性中该值如果被指定为「auto」，则伸缩基准值的计算值是自身的 <' width '> 设置，如果自身的宽度没有定义，则长度取决于内容。

说明

> 复合属性。设置或检索弹性盒模型对象的子元素如何分配空间。
> 如果缩写「flex: 1」, 则其计算值为「1 1 0%」
> 如果缩写「flex: auto」, 则其计算值为「1 1 auto」
> 如果「flex: none」, 则其计算值为「0 0 auto」
> 如果「flex: 0 auto」或者「flex: initial」, 则其计算值为「0 1 auto」，即「flex」初始值

举个栗子:

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>flex</title>
    <style type="text/css">
    .container{
        background-color: #963297;
    }

    .item{margin: 10px;line-height: 40px;text-align: center;color: #fff;font-size: 20px;background-color: #c99702;font-size: 50px;}
    .container{display: flex;flex-flow: column;}/* 弹性布局，且纵向排列 */
    html,body,.container{height: 100%;}
    .item{flex: 1 1 0;}/* flex-grow:1;  flex-shrink:1; flex-basis:0; */
    .item3{flex: 2;}/* flex-grow:2; */
    </style>
</head>
<body>
<div class="container">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102165537752-954693882.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102165537205-1188851756.png)

 

 

**对齐**

和『对齐』相关的属性有:

- justify-content
- align-items
- align-self
- align-content

 

 

justify-content

justify-content: flex-start | flex-end | center | space-between | space-around

默认值：flex-start

设置 main-axis 方向上对齐方式

justify-content 和 text-align是类似的，比text-align 更丰富一些。

 

举个栗子:

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>justify-content</title>
    <style type="text/css">
    .container{margin: 20px;line-height: 40px;font-size: 20px;color: #fff;background-color: #963297;}

    .item{margin: 10px;width: 100px;line-height: 40px;text-align: center;background-color: #c99702;}

    .container{display: flex; }
    .fs{justify-content: flex-start;}
    .fe{justify-content: flex-end;}
    .c{justify-content: center;}
    .sb{justify-content: space-between;}
    .sa{justify-content: space-around;}


    /*.container{flex-flow: column; width: 120px;height: 300px;}*/
    </style>
</head>
<body>

<div class="container fs">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>

<div class="container fe">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>

<div class="container c">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>

<div class="container sb">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>

<div class="container sa">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>

<div class="container fs">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
</div>

</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102172447502-2045103719.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102172446830-1420957680.png)

 

 

 

 

[align-items](http://www.css88.com/book/css/properties/flex/align-items.htm)

设置『辅轴方向上』的对齐方式

语法:

> align-items：flex-start | flex-end | center | baseline | stretch
> 默认值：stretch
> 适用于：flex容器
> 继承性：无
> 动画性：是
> 计算值：指定值

 

取值:

> flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
> flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
> center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
> baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
> stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。

 

说明:

> 定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式。
> 对应的脚本特性为alignItems。

 

 

举个栗子：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>align-items</title>
    <style type="text/css">
    .container{margin: 20px;line-height: 40px;font-size: 20px;color: #fff;background-color: #963297;}
    .item{margin: 10px;width: 100px;line-height: 40px;text-align: center;background-color: #c99702;}


    .container{display: flex;}
    .item1{line-height: 100px;}
    .item2{line-height: 70px;}
    .fs{align-items: flex-start;}
    .fe{align-items: flex-end;}
    .c{align-items: center;}
    .s{align-items: stretch;}
    .b{align-items: baseline;}

    </style>
</head>
<body>
    <div class="container fs">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
    </div>
    <div class="container fe">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
    </div>
    <div class="container c">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
    </div>
    <div class="container s">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
    </div>
    <div class="container b">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
    </div>
    
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102173855158-1588478072.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102173854721-747640691.png)

 

我看不懂，最后的 baseline。 觉得应该和 flex-start相同。而实际和center相同。 求解释

 

 

 

align-self

**align-self**：auto | flex-start | flex-end | center | baseline | stretch

设置『单个 flex item 』在cross-axis 方向上的对齐方式

 

举个栗子：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>align-self</title>
    <style type="text/css">
    .container{margin: 20px;line-height: 40px;font-size: 20px;color: #fff;background-color: #963297;}
    .item{margin: 10px;width: 100px;line-height: 40px;text-align: center;background-color: #c99702;}
    

    .container{display: flex;align-items: flex-start;}
    .item1{line-height: 100px;}
    /*.item2{align-self: flex-end;}*/
    /*.item2{align-self: center;}*/
    /*.item2{align-self: baseline;}*/
    /*.item2{align-self: stretch;}*/
    </style>
</head>
<body>
        <div class="container">
            <div class="item item1">1</div>
            <div class="item item2">2</div>
            <div class="item item3">3</div>
        </div>
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102175233846-1847288339.png)

 

 

 

flex-start

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102175235158-1005503269.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102175234658-463133521.png)flex-end

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102175235924-739668447.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102175235596-125656173.png)center

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102175237127-377445208.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102175236440-1998923323.png)baseline

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102175237971-462420883.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102175237580-2116099939.png)stretch

 

 

 

align-content

**align-content**：flex-start | flex-end | center | space-between | space-around | stretch

设置 cross-axis 辅轴方向上行对齐方式

flex换行了，多行之间的对齐方式

默认值： stretch 拉伸

 

举个栗子：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>align-content</title>
    <style type="text/css">
    .container{margin: 20px;width: 800px;line-height: 40px;font-size: 20px;color: #fff;background-color: #963297;}
    .item{margin: 10px;width: 200px;line-height: 40px;text-align: center;background-color: #c99702;}

    .container{display: flex;}
    .container{height: 800px;flex-flow: row wrap; align-items: flex-start;}

    /*.container{align-content: flex-start;}*/
    /*.container{align-content: flex-end;}*/
    /*.container{align-content: center;}*/
    /*.container{align-content: space-between;}*/
    /*.container{align-content: stretch;}*/

    </style>
</head>
<body>
<div class="container">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
        <div class="item item4">4</div>
        <div class="item item5">5</div>
        <div class="item item6">6</div>
        <div class="item item7">7</div>
        <div class="item item8">8</div>
        <div class="item item9">9</div>
        <div class="item item10">10</div>
</div>
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102181613424-15113042.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102181613002-1340837775.png)

 

 

 

布局--三行两列自适应布局

核心代码

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<div class="head">head</div>
<div class="body">
        <div class="side">side</div>
        <div class="main">main</div>
</div>
<div class="foot">foot</div>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

```
body{display: flex;flex-flow: column;}
.head,.foot{height: 100px;}
.body{flex-flow: 1; display: flex;}
.side{width: 200px;}
.main{flex: 1;}
```

 

举个栗子：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>三行两列自适应布局</title>
    <style type="text/css">
    html,body{margin: 0;text-align: center;}
    .head, .foot{line-height: 100px;background-color: #000;color: #fff;}
    .side{background-color: yellow;}
    .main{background-color: pink;}


    html,body{height: 100%;}
    body{display: flex;flex-flow: column;}
    .head,.foot{height: 100px;}
    .body{flex: 1;display: flex;}
    .side{width: 200px;}
    .main{flex: 1;}

    .main{margin-left: 10px;}
    /*.body{width: 960px;align-self: center;}*/
    </style>
</head>
<body>
<div class="head">head</div>
<div class="body">    
        <div class="side">side</div>
        <div class="main">main</div>
</div>
<div class="foot">foot</div>
</body>
</html>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

[![image](https://images2015.cnblogs.com/blog/601779/201611/601779-20161102202407627-1494007430.png)](http://images2015.cnblogs.com/blog/601779/201611/601779-20161102202407158-714048026.png)

 