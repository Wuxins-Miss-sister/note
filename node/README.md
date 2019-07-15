

# Node.js 第1天

## 上午总结

- Node.js 是什么
  
  -  Node.js 不是一门语言
  
  - Node.js不是库，不是框架
  
  - Node.js是一个js运行时环境
  
  - 简单来讲就是Node.js可以解析和执行js代码
  
  - 以前只有浏览器可以解析执行js代码
  
  - 也就是说现在的js可以完全脱离浏览器来运行 一切都归功于node.js
  
- + JavaScript 运行时
  + 既不是语言，也不是框架，它是一个平台
  
- Node.js 中的 JavaScript
  + 没有 BOM、DOM
  + EcmaScript 基本的 JavaScript 语言部分
  + 在 Node 中为 JavaScript 提供了一些服务器级别的 API
    * 文件操作的能力
    * http 服务的能力

## 总结

- Node 中的 JavaScript
  + EcmaScript
    * 变量
    * 方法
    * 数据类型
    * 内置对象
    * Array
    * Object
    * Date
    * Math
  + 模块系统
    * 在 Node 中没有全局作用域的概念
    * 在 Node 中，只能通过 require 方法来加载执行多个 JavaScript 脚本文件
    * require 加载只能是执行其中的代码，文件与文件之间由于是模块作用域，所以不会有污染的问题
      - 模块完全是封闭的
      - 外部无法访问内部
      - 内部也无法访问外部
    * 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突污染的问题
    * 但是某些情况下，模块与模块是需要进行通信的
    * 在每个模块中，都提供了一个对象：`exports`
    * 该对象默认是一个空对象
    * 你要做的就是把需要被外部访问使用的成员手动的挂载到 `exports` 接口对象中
    * 然后谁来 `require` 这个模块，谁就可以得到模块内部的 `exports` 接口对象
    * 还有其它的一些规则，具体后面讲，以及如何在项目中去使用这种编程方式，会通过后面的案例来处理
  + 核心模块
    * 核心模块是由 Node 提供的一个个的具名的模块，它们都有自己特殊的名称标识，例如
      - fs 文件操作模块
      - http 网络服务构建模块
      - os 操作系统信息模块
      - path 路径处理模块
      - 。。。。
    * 所有核心模块在使用的时候都必须手动的先使用 `require` 方法来加载，然后才可以使用，例如：
      - `var fs = require('fs')`
- http
  + require
  + 端口号
    * ip 地址定位计算机
    * 端口号定位具体的应用程序
  + Content-Type
    * 服务器最好把每次响应的数据是什么内容类型都告诉客户端，而且要正确的告诉
    * 不同的资源对应的 Content-Type 是不一样，具体参照：http://tool.oschina.net/commons
    * 对于文本类型的数据，最好都加上编码，目的是为了防止中文解析乱码问题
  + 通过网络发送文件
    * 发送的并不是文件，本质上来讲发送是文件的内容
    * 当浏览器收到服务器响应内容之后，就会根据你的 Content-Type 进行对应的解析处理

- 模块系统
- Node 中的其它的核心模块
- 做一个小管理系统：
  
  + CRUD
- Express Web 开发框架
  
  + `npm install express`
  
- ##### 服务端渲染和客户端渲染的区别

\+ 客户端渲染不利于 SEO 搜索引擎优化

\+ 服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的

\+ 所以你会发现真正的网站既不是纯异步也不是纯服务端渲染出来的

\+ 而是两者结合来做的

\+ 例如京东的商品列表就采用的是服务端渲染，目的了为了 SEO 搜索引擎优化

\+ 而它的商品评论列表为了用户体验，而且也不需要 SEO 优化，所以采用是客户端渲染
    
    
## 自己的笔记

## ![node起步](nodeimg/node起步.png)

    Node.js uses an event-driven,non-blocking I/O model that makes it lightweight and efficien
      
    ​    event-driven 事件驱动
      
    ​    non-blocking I/O model非阻塞IO模型（异步）
      
    ​    lightweight and efficien 轻量和高效


​     

    Node.js package ecosystem,npm is the largest ecosystem of open source libraries 
      
    in the world
      
      npm 是世界上最大的开源库生态系统 
      
    绝大多数js 相关的包都存放在npm上 这样做的目的是为了让开发人员更方便的去下载


​     

    Node.js能做什么
      
    Web 服务器后台
      
    命令行工具
      
    ​      npm（node）
      
    ​      Git（c 语言）
      
    ​      hexo（node）


​     

    游戏服务器  …
      
    对于前端开发来讲接触最多的是他的命令行工具
      
    自己写的很少 主要是使用别人第三方的
      
    Webpack
      
    Gulp
      
    Npm


​     

    预备知识
      
    Html
      
    Css
      
    Js
      
    简单的明亮行操作
      
    学习资源
      
    学习是一个过程
      
    深入浅出node.Js
      
    朴灵   偏理论 几乎没有任何实战
      
    Node.js权威指南
      
    阮一峰 那找


​      
​    

   ![node书籍](nodeimg/node书籍.png)


​     

    这门课你能学到啥 
      
    B/S编程模型
      
     Browser-Server
      
     back-end
      
     任何服务器技术这种BS编程模型都是一样 和语言无关 
      
     Node 只是作为我们学习BS编程模型的一个工具而已
      
    模块化编程
      
    ​    以前认知的js只能通过script标签来加载 
      
    ​    在Node中可以象@import（） 一样来引用 加载 js脚本文件
      
    Node常用Api
      
    异步编程
      
    ​     回调函数
      
      promise
      
     async
      
     generator
      
    Express开发框架
      
    Es6
      
       只是新语法而已


​     

    2起步


​     

    傻瓜的next
      
    已经安装过重新安装就升级
      
    node --version
      
    环境变量
      
    3 . 
      
    Shift + 右键能进去
      
    \# Node.js 第2天课堂笔记


​     

    创建编写js脚本文件
      
    打开终端 ，定位到脚本文件所属目录
      
    输入node 文件名执行对应的文件


​     

    注意文件名不要用node.js来执行
      
    最好不用中文
      
    没有 bom 和 dom
      
      读文件写文件


​     

    //浏览器中的js是没有操作文档的能力的
      
    //但是Node中的js具有文件操作能力


​     

   //fs** **是** **file-system** **的简写 ，就是文件系统的意思**
      
    //fs 是 file-system 的简写 ，就是文件系统的意思
    //在Node中如果进行文件操作,就必须引入fs核心模块
    //在fs这个核心模块中,就提供了所有的文件操作相关的API
    //例如 fs.readFile 就是用来读取文件的
    // 1 使用require 方法加载 fs核心模块 
    var fs = require('fs')
    //2 读取文件
    //第一个参数就是要读取的文件路径
    //第二个参数就是一个回调函数
    //成功
    //如果读取成功 error就是错误对象 data 数据
    //如果读取成功 error就是 null error null
    //失败 
    //如果读取成功 data就是读取的数据  data null  undefined 没有数据
    //如果读取失败error就是书错误对象  error  错误对象
     fs.readFile('aaa.txt',function(error,data){
     	//1版本 
    // 	console.log(data.toString())
     	
     	//2版本  通过判断error是否为 null 来判断你是否有错误发生
     	if(error){
     		console.log('读取文件失败')
     	}else{
     		console.log(data.toString())
     	}
     	
    // 	<Buffer 61 61 61 61 61>
    //  文件中存储的其实都是16进制 人类都不认识 
    //  但是无论是二进制还是16进制 人类都不认识 
    //   所以我们通过toString 方法把其转为我们能认识的字符
        
     })
    //第一个参数：文件路径     文件路径和文件名不允许有特殊字符
    //第二个参数 文件内容   
    //第三个参数 回调函数 
    // error 形参 随便写     
    //  成功
    //  文件写入成功
    //  error是null
    //  失败 
    //  文件写入失败
    //  error就是错误对象
    //第一版 
    //fs.writeFile('aaa.txt','node 牛逼11',function(error){
    //	console.log('文件写入成功')
    //	})
    //第二版 
    fs.writeFile('aaa.txt','node 牛逼22',function(error){
    	if(error){
    		console.log('写入失败')
    	}else{
    		console.log('文件写入成功')
    	}
    })



​     


    javascript代码风格
      
    var foo = 'bar'
      
    var foo ='bar'
      
    var foo= 'bar'
      
    var foo = "bar"


​     

    if (true) {
      
      console.log('hello') 
      
    }


​     

    if (true) {
      
    ​    console.log('hello') 
      
    }


​     

    if (true ){
      
    ​      console.log('hello') 
      
    }
      
    \``` 
      
    为了约定大家的代码风格，所以在社区中诞生了一些比较规范的代码风格规范：dnsajkndkjsabnjkdnjksandjknsajkdnjkasnjkdnjksandjknsajkdnjksajkdnas


​     

    \- [JavaScript Standard Style](https://standardjs.com/)
      
    \- Airbnb JavaScript Style


## ip地址和端口号的概念

所有联网的程序都需要进行网络通信

计算机中只有一个物理网卡，而且同一个局域网中，网卡的地址必须是惟一的

网卡是通过唯一的ip地址来进行定位的

​             ip地址用来定位计算机 

​     端口号用来定位具体的应用程序

​              所有需要联网通信的应用程序都会占用一个端口号

​    （所有需要联网通信的软件都必须具有端口号）

![网络通信](nodeimg/网络通信.png)

可以同时开启多个服务，但一定要不同服务占用的端口号不一致才可以![IP地址和端口号](nodeimg/IP地址和端口号.png)

## 读写文件

//浏览器中的js是没有文件操作的能力的

// 但是Node中的js具有文件操作的能力

//fs 是 file-system的简写，就是文件系统的意思

//在Node中如果想要进行文件操作，就必须要引入fs这个核心模块

//在fs这个核心模块中，就提供了所有的文件操作相关的API

//例如：fs.readFile就是用来读取文件的

//1.使用require方法加载fs核心模块 

let fs = require('fs');

//2.读取文件 

//第一个参数就是要读取的文件路径 

//第二个参数就是一个回调函数 

// error 

// 如果读取失败，error就是错误对象

// 如果读取成功，error就是null

// data

// 如果读取成功，data就是读取到的数据

// 如果读取失败，error就是错误对象

// 成功 

// data数据

// error null

// 失败 

// data undefined 没有数据

// error 错误对象

// console.log(data)//二进制数据 

//文件中存储的其实都是二进制数据 0 1

//这里为什么看到的不是0和1呢？原因是二进制转为16进制了

//但是无论是二进制还是16进制，人类都不认识

//所以我们可以通过toString方法把其转为我们能认识的字符

//})

// 二进制数据{<Buffer 2f 2f e6 b5 8f e8 a7 88 e5 99 a8 e4 b8 ad e7 9a 84 6a 73 e6 98 af e6 b2 a1 e6 9c 89 e6 96 87 e4 bb b6 e6 93 8d e4 bd 9c e7 9a 84 e8 83 bd e5 8a 9b e7 ... 945 more bytes>}

fs.readFile('./hello.txt',(error,data)=>{

// console.log(data.toString());

//在这里就可以通过判断error来确认是否有错误发生

if(error){

console.log('读取文件失败')

}else{

console.log(data.toString());

}

})

// error 是个对象

// D:\Web\Node\第一天>node ioread.js

// [Error: ENOENT: no such file or directory, open 'D:\Web\Node\第一天\ahello.txt'] {

// errno: -4058,

// code: 'ENOENT',

// syscall: 'open',

// path: 'D:\\Web\\Node\\第一天\\ahello.txt'

// }

 

 

 

 

 

 

 

 

 

let fs = require('fs');

//第一个的参数：文件路径

//第二个参数：文件内容

//第三个参数：回调函数 

//error

// 成功：

// 文件写入成功 

// error 是null

// 失败：

// 文件写入失败 

// error就是错误对象

fs.writeFile('./hello.txt','百词斩挺棒的',(error)=>{

// console.log(error);

if(error){

console.log('写入失败')

}else{

console.log('写入成功了')

}

})

//window 文件里面不能有一些特殊字符

// D:\Web\Node\第一天>node iowrite.js

// [Error: ENOENT: no such file or directory, open 'D:\Web\Node\第一天\hello>.txt'] {

// errno: -4058,

// code: 'ENOENT',

// syscall: 'open',

// path: 'D:\\Web\\Node\\第一天\\hello>.txt'

// }

 