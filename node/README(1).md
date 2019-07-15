# Node.js 第2天课堂笔记

## 知识点

### 代码风格

```javascript
var foo = 'bar'
var foo ='bar'
var foo= 'bar'
var foo = "bar"

if (true) {
  console.log('hello') 
}

if (true) {
    console.log('hello') 
}

if (true ){
      console.log('hello') 
}
```

为了约定大家的代码风格，所以在社区中诞生了一些比较规范的代码风格规范：dnsajkndkjsabnjkdnjksandjknsajkdnjkasnjkdnjksandjknsajkdnjksajkdnas

- [JavaScript Standard Style](https://standardjs.com/)
- Airbnb JavaScript Style

## 复习

## 上午总结

- 代码风格
- 无分号
  + `(`
  + `[`
  + `
  + 最好前面补分号，避免一些问题
  + 《编写可维护的 JavaScript》
  + 不仅是功能，还要写的漂亮
- 服务端渲染
  + 说白了就是在服务端使用模板引擎
  + 模板引擎最早诞生于服务端，后来才发展到了前端

- 服务端渲染和客户端渲染的区别
  + 客户端渲染不利于 SEO 搜索引擎优化
  + 服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的
  + 所以你会发现真正的网站既不是纯异步也不是纯服务端渲染出来的
  + 而是两者结合来做的
  + 例如京东的商品列表就采用的是服务端渲染，目的了为了 SEO 搜索引擎优化
  + 而它的商品评论列表为了用户体验，而且也不需要 SEO 优化，所以采用是客户端渲染

## 自己的笔记

代码风格问题  <https://standardjs.com/> 阅读一下

 

下面的更细

<https://github.com/airbnb/javascript>

 

//当你采用了无分号代码风格的时候，只需要注意一下情况就不会有上面的问题了

//  当一行代码是以:

//         (

//         [

//         `

//开头的时候，则在前面补上一个分号用以避免一些语法解析错误，

//所以你会发现在一些第三方的代码中能看到一上来就以一个；开头

//无论你的代码是否有分号，都建议你加上

//有些人也会用花里胡哨的！  ~

## Node中的重定向

resp.statusCode = 302

resp.setHeader('Location','/')

resp.end()

##  node里的 console

任意目录终端中输入node命令直接敲回车 

就可以使用一些测试 而且核心模块都不用引入 

 

象浏览器中的命令行

学名是 

REPL

 

read 读取输入

 

eval 执行代码

 

print 输出

 

loop 循环

 ## 在Node中使用模板引擎

![服务端渲染](nodeimg/服务端渲染.png)

![客户端渲染](nodeimg/客户端渲染.png)

服务端渲染出来的页面网页源代码可以看到全部模板

客户端渲染出来的页面看不到

 

   服务端渲染和客户端渲染的区别

​         客户端渲染不利于SEO搜索引擎优化

服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的

所以你会发现真正的网站既不是纯异步也不是纯服务器渲染出来的

而是两者结合来做的

例如京东的商品列表就采用的是服务端渲染，目的为了SEO搜索引擎优化

而他的商品评论列表为了用户体验，而且也不需要SEO优化所以采用是客户端渲染

## 模板引擎的使用

//art-template

//art-template 不仅可以在浏览器使用，也可以在node中使用

//安装 ：

// npm install art-template

// 该命令在哪执行就会把包下载到哪里。默认会下载到node——modules目录中

//node_modules不要改，也不支持改

//在node中使用模板引擎

//在Node中使用art-template模块引擎

//模块引起最早就是诞生于服务器领域，后来才发展到了前端

//1.安装 npm install art-template

//2.在需要的文件模块中加载 art-template

//只需要使用require方法加载就可以了：require('art-template')

//参数中的art-template 就是你下载的包的名字

//也就是说你install的名字是什么，则你require中的就是什么

//3.查文档，使用模块引擎的API

let template = require('art-template')

let fs = require('fs')

fs.readFile('./template3.html',(err,data)=>{

if(err){

return console.log('读取文件失败了')

}

//默认读取到的data是二进制数据

//而模板引擎的render方法需要接收的是字符串

//所以我们在这里需要把data二进制数据转为字符串才可以给模板引擎使用

let ret = template.render(data.toString(),{

name: 'Wuxin',

age:22,

province:'北京市',

hobbies:[

'写代码',

'唱歌',

'玩游戏'

]

})

console.log(ret)

})

 

 

// D:\Web\Node\第二天>node text-template.js

// <!DOCTYPE html>

// <html lang="en">

// <head>

// <meta charset="UTF-8">

// <meta name="viewport" content="width=device-width, initial-scale=1.0">

// <meta http-equiv="X-UA-Compatible" content="ie=edge">

// <title>在浏览器中使用</title>

// </head>

// <body>

// <p>大家好，我叫 Wuxin</p>

// <p> 我今年22</p>

// <h1>我来自北京市</h1>

// <p>我喜欢 写代码 唱歌 玩游戏 </p>

// </body>

// </html>

 

 

<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,
initial-scale=1.0">

<meta http-equiv="X-UA-Compatible" content="ie=edge">

<title>在浏览器中使用</title>

</head>

<body>

<p>大家好，我叫 {{name}}</p> 

<p> 我今年{{age}}</p> 

<h1>我来自{{province}}</h1> 

<p>我喜欢{{each hobbies}} {{$value}} {{/each}}</p>

</body>

</html>

 

 

 

浏览器中使用

<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,
initial-scale=1.0">

<meta http-equiv="X-UA-Compatible" content="ie=edge">

<title>在浏览器中使用</title>

</head>

<body>

<!-- 注意：在浏览器中需要引用lib/template-web.js文件 

强调：模板引擎不关心你的字符串内容，只关心自己能认识的模板标记语法，例如{{}}

这个语法被称为mustache语法，八字胡

-->

<script src="./node_modules/art-template/lib/template-web.js"></script>

<script type="text/template" id='tpl'>

大家好，我叫 {{name}}

我今年{{age}}

我来自{{province}} 

我喜欢{{each hobbies}} {{$value}} {{/each}}

</script>

<script>

// 里面放《html》《/html》会被识别为字符串

var ret = template('tpl',{

name:'Jack',

age:22,

province:'北京市',

hobbies:[

'写代码',

'唱歌',

'玩游戏'

]

})

console.log(ret)

</script>

</body>

</html>

##  处理网站中的url

let url = require('url')

let obj = url.parse('http://127.0.0.1:3000/pinglun?name=%E5%A7%9A%E7%BA%AF%E5%87%AF&message=8454515',true)

console.log(obj)

console.log(obj.query)

 

// D:\Web\Node\第二天>node url模块.js

// Url {

// protocol: 'http:',

// slashes: true,

// auth: null,

// host: '127.0.0.1:3000',

// port: '3000',

// hostname: '127.0.0.1',

// hash: null,

// search: '?name=%E5%A7%9A%E7%BA%AF%E5%87%AF&message=8454515',

// query: [Object: null prototype] { name: '姚纯凯', message: '8454515' },

// pathname: '/pinglun',

// path: '/pinglun?name=%E5%A7%9A%E7%BA%AF%E5%87%AF&message=8454515',

// href: '[http://127.0.0.1:3000/pinglun?name=%E5%A7%9A%E7%BA%AF%E5%87%AF&message=8454515](http://127.0.0.1:3000/pinglun?name=姚纯凯&message=8454515)'

// }

 ## 在node中使用时间插件

let sd = require('silly-datetime')

 

comment.dateTime = sd.format(new Date(),'YYYY-MM-DD HH:mm').toString()

## 留言本

/ / 晚 上 写 案 例 照 着 下 面 的 步 骤 写 ： 
/ index.html 
1 · 
2 · 开 放 public 目 录 中 的 静 态 资 源 
当 请 求 /public/xxx 的 时 候 ， 读 取 响 应 public 
/post post.html 
3 · 
/pinglun 
4 · 
4 · 1 接 收 表 单 提 交 数 据 
4 ． 2 存 储 表 单 提 交 的 数 据 
4 ． 3 让 表 单 重 定 向 到 / 
statusCode 
setHeader 


 

 

 