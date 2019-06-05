# [better-scroll的参数和方法](https://www.cnblogs.com/cangqinglang/p/8553746.html)



## 格式：let obj = new BScroll(object,{[option1,],.,.});

 

注意，如果在某一个组件内创建了一个BScroll的实例，在组件生命周期结束前要注意调用destroy方法，否则在滑动过程中切换页面会导致一直触发scroll事件，导致一些意想不到的问题，切记！！！

##  

Options 参数

 

> - startX: `0` 开始的X轴位置
> - startY: `0` 开始的Y轴位置
> - scrollY: `true` 滚动方向为 Y 轴
> - scrollX: true 滚动方向为 X 轴
> - click: `true` 是否派发click事件，通常判断浏览器派发的click还是betterscroll派发的click，可以用_constructed，若是bs派发的则为true
> - directionLockThreshold: `5`
> - momentum: `true` 当快速滑动时是否开启滑动惯性
> - bounce: `true` 是否启用回弹动画效果
> - selectedIndex: `0` wheel 为 true 时有效，表示被选中的 wheel 索引
> - rotate: `25` wheel 为 true 时有效，表示被选中的 wheel 每一层的旋转角度
> - wheel: `false` 该属性是给 picker 组件使用的，普通的列表滚动不需要配置
> - snap: `false` 该属性是给 slider 组件使用的，普通的列表滚动不需要配置
> - snapLoop: `false` 是否可以无缝循环轮播
> - snapThreshold: `0.1` 用手指滑动时页面可切换的阈值，大于这个阈值可以滑动的下一页
> - snapSpeed: `400`, 轮播图切换的动画时间
> - swipeTime: `2500` swipe 持续时间
> - bounceTime: `700` 弹力动画持续的毫秒数
> - adjustTime: `400` wheel 为 true 有用，调整停留位置的时间
> - swipeBounceTime: `1200` swipe 回弹 时间
> - deceleration: `0.001` 滚动动量减速越大越快，建议不大于0.01
> - momentumLimitTime: `300` 符合惯性拖动的最大时间
> - momentumLimitDistance: `15` 符合惯性拖动的最小拖动距离
> - resizePolling: `60` 重新调整窗口大小时，重新计算better-scroll的时间间隔
> - preventDefault: `true` 是否阻止默认事件
> - preventDefaultException: `{ tagName: /^(INPUT|TEXTAREA|BUTTON|SELECT)$/ }` 阻止默认事件
> - HWCompositing: `true` 是否启用硬件加速
> - useTransition: `true` 是否使用CSS3的Transition属性
> - useTransform: `true` 是否使用CSS3的Transform属性
> - probeType: `1` 滚动的时候会派发scroll事件，会截流。`2`滚动的时候实时派发scroll事件，不会截流。 `3`除了实时派发scroll事件，在swipe的情况下仍然能实时派发scroll事件

 

 Events 事件

> - beforeScrollStart - 滚动开始之前触发
> - scrollStart - 滚动开始时触发
> - scroll - 滚动时触发
> - scrollCancel - 取消滚动时触发
> - scrollEnd - 滚动结束时触发
> - touchend - 手指移开屏幕时触发
> - flick - 触发了 fastclick 时的回调函数
> - refresh - 当 better-scroll 刷新时触发
> - destroy - 销毁 better-scroll 实例时触发
>
> Example:
>
> let scroll = new BScroll(document.getElementById('wrapper'),{
>
>    probeType: 3
>
> })
>
>  
>
> scroll.on('scroll', (pos) => {
>
>   console.log(pos.x + '~' + pos.y)
>
> })

 

## 函数列表

> - scrollTo(x, y, time, easing)
>
> 滚动到某个位置，x,y 代表坐标，time 表示动画时间，easing 表示缓动函数
> scroll.scrollTo(0, 500)
>
>  
>
> - scrollToElement(el, time, offsetX, offsetY, easing)
>
> 滚动到某个元素，el（必填）表示 dom 元素，time 表示动画时间，offsetX 和 offsetY 表示坐标偏移量，easing 表示缓动函数
>
>  
>
> - refresh()
>
> 强制 scroll 重新计算，当 better-scroll 中的元素发生变化的时候调用此方法
>
>  
>
> - getCurrentPage()
>
> snap 为 true 时，获取滚动的当前页，返回的对象结构为 {x, y, pageX, pageY}，其中 x,y 代表滚动横向和纵向的位置；pageX，pageY 表示横向和纵向的页面索引。用法如：getCurrentPage().pageX
>
>  
>
> - goToPage(x, y, time, easing)
>
> snap 为 true，滚动到对应的页面，x 表示横向页面索引，y 表示纵向页面索引， time 表示动画，easing 表示缓动函数（可省略不写）
>
>  
>
> - enable()启用 better-scroll，默认开启
>
>  
>
> - disable()  禁用 better-scroll
>
>  
>
> - destroy() 销毁 better-scroll，解绑事件