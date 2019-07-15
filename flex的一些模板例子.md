## 使用Flex实现5种常用布局

本文分享使用Flex实现5种常用布局，包括Sticky Footer、Fixed-Width Sidebar、Sidebar、Sticky Header和Sticky Sidebar。

- 作者：meikidd来源：[segmentfault](https://segmentfault.com/a/1190000012275086)|*2017-12-07 14:40*

  [ 收藏](javascript:favorBox('open');)[  分享](javascript:;)

**Sticky Footer**

经典的上-中-下布局。

当页面内容高度小于可视区域高度时，footer 吸附在底部；当页面内容高度大于可视区域高度时，footer 被撑开排在 content 下方

[demo link](http://meikidd.github.io/flex-layout/demos/1.html)

[![img](https://s2.51cto.com/oss/201712/07/80d6ad06d2c564da2442423057647d40.png-wh_651x-s_4239649419.png)](https://s2.51cto.com/oss/201712/07/80d6ad06d2c564da2442423057647d40.png-wh_651x-s_4239649419.png)

```
<body>      <header>HEADER</header>      <article>CONTENT</article>      <footer>FOOTER</footer>    </body> 
body {    min-height: 100vh;    display: flex;    flex-direction: column;  }  article {    flex: auto;  } 
```

**Fixed-Width Sidebar**

在上-中-下布局的基础上，加了左侧定宽 sidebar。

[demo link](http://meikidd.github.io/flex-layout/demos/2.html)

[![img](https://s1.51cto.com/oss/201712/07/a12f5b0a5e3e842d4c16874c3bafc9aa.png)](https://s1.51cto.com/oss/201712/07/a12f5b0a5e3e842d4c16874c3bafc9aa.png)

```
<body>    <header>HEADER</header>   
<div class="content">    
<aside>ASIDE</aside>    
<article>CONTENT</article>  
</div>   
<footer>FOOTER</footer> 
</body> 
body
{    min-height: 100vh;    display: flex;    flex-direction: column;  } 
.content {    flex: auto;    display: flex;  } 
.content article {    flex: auto;  } 
```

**Sidebar**

左边是定宽 sidebar，右边是上-中-下布局。

[demo link](http://meikidd.github.io/flex-layout/demos/3.html)

[![img](https://s2.51cto.com/oss/201712/07/48efb5ce281a596e16ac4f497f67544b.png)](https://s2.51cto.com/oss/201712/07/48efb5ce281a596e16ac4f497f67544b.png)

```
<body>    <aside>ASIDE</aside>    <div class="content">      <header>HEADER</header>      <article>CONTENT</article>      <footer>FOOTER</footer>    </div>  </body> 
body {    min-height: 100vh;    display: flex;  }  aside {    flex: none;  }  .content {    flex: auto;    display: flex;    flex-direction: column;  }  .content article {    flex: auto;  } 
```

**Sticky Header**

还是上-中-下布局，区别是 header 固定在顶部，不会随着页面滚动。

[demo link](http://meikidd.github.io/flex-layout/demos/4.html)

[![img](https://s3.51cto.com/oss/201712/07/01333ceedf479c0eb2d911001aebe81e.png)](https://s3.51cto.com/oss/201712/07/01333ceedf479c0eb2d911001aebe81e.png)

```
<body>    <header>HEADER</header>    <article>CONTENT</article>    <footer>FOOTER</footer>  </body>
body {    min-height: 100vh;    display: flex;    flex-direction: column;    padding-top: 60px;  }  header {    height: 60px;    position: fixed;    top: 0;    left: 0;    right: 0;    padding: 0;  }  article {    flex: auto;    height: 1000px;  } 
```

**Sticky Sidebar**

左侧 sidebar 固定在左侧且与视窗同高，当内容超出视窗高度时，在 sidebar 内部出现滚动条。左右两侧滚动条互相独立。

[demo link](http://meikidd.github.io/flex-layout/demos/5.html)

[![img](https://s1.51cto.com/oss/201712/07/01131af80fce386cbff6e54cc1d21745.png)](https://s1.51cto.com/oss/201712/07/01131af80fce386cbff6e54cc1d21745.png)

```
<body>    <aside>      ASIDE      <p>item</p>      <p>item</p>      <!-- many items -->      <p>item</p>    </aside>    <div class="content">      <header>HEADER</header>      <article>CONTENT</article>      <footer>FOOTER</footer>    </div>  </body> 
body {    height: 100vh;    display: flex;  }  aside {    flex: none;    width: 200px;    overflow-y: auto;    display: block;  }  .content {    flex: auto;    display: flex;    flex-direction: column;    overflow-y: auto;  }  .content article {    flex: auto;  }  
```