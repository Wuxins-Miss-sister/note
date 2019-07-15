# Node.js 第6天课堂笔记

## 知识点

- 多人社区案例

## 反馈

## 复习

- MongoDB 数据库
  + 灵活
  + 不用设计数据表
  + 业务的改动不需要关心数据表结构
  + DBA 架构师 级别的工程师都需要掌握这项技能
    * 设计
    * 维护
    * 分布式计算
- mongoose
  + mongodb 官方包也可以操作 MongoDB 数据库
  + 第三方包：WordPress 项目开发团队
  + 设计 Schema
  + 发布 Model（得到模型构造函数）
    * 查询
    * 增加
    * 修改
    * 删除
- Promise
  + http://es6.ruanyifeng.com/#docs/promise
  + callback hell 回调地狱
  + 回调函数中套了回调函数
  + Promise(EcmaScript 6 中新增了一个语法 API)
  + 容器
    * 异步任务（pending）
    * resolve
    * reject
  + then 方法获取容器的结果（成功的，失败的）
  + then 方法支持链式调用
  + 可以在 then 方法中返回一个 promise 对象，然后在后面的 then 方法中获取上一个 then 返回的 promise 对象的状态结果



## 总结

- path 模块

- `__dirname` 和` __filename`
  
  + **动态的** 获取当前文件或者文件所处目录的绝对路径
  + 用来解决文件操作路劲的相对路径问题
  + 因为在文件操作中，相对路径相对于执行 `node` 命令所处的目录
  + 所以为了尽量避免这个问题，都建议文件操作的相对路径都转为：**动态的绝对路径**
  + 方式：`path.join(__dirname, '文件名')`

  
  
- 表单同步提交和异步提交区别
  
  + 以前没有 ajax 都是这么干的，甚至有些直接就是渲染了提示信息出来了
  + 异步提交页面不会刷新，交互方式更灵活
  
- Express 中配置使用 express-session 插件

- 概述案例中注册-登陆-退出的前后端交互实现流程

## Node综合Web案例

###### 1.目录结构

```js
|---app.js		项目的入口文件
|---controllers
|---models         存储使用mongoose设计的数据模型
|---node_modules   第三方包
|---package.json   包描述文件
|---package-lock.json   第三方包版本锁定文件（npm 5以后才有）
|---public    公共的静态资源
|---README.md    项目说明文档
|---routes		如果业务比较多，代码量大，最好把路由按照业务的分类存储到routes目录中
|---views        存储视图目录
|---router.js    简单一点把所有的路由都放到这个文件
```

###### 2.模板页

art-template 模板引擎(include、block、extend)

- include      用于重复组件  比如标题 和 下面的结尾
- extend       模板继承和子模版 
- block

  ```html
  layout.html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <link rel="stylesheet" href="/node_modules/bootstrap/dist/css/bootstrap.css">
      {{ block 'head' }} {{ /block }}
  </head>
  <body>
      {{ include './header.html'}}
      <!--留一个坑-->
      {{ block 'content'}}
          <h1>默认内容</h1>
      {{ /block }}
      {{ include './footer.html'}}
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script src="/node_modules/bootstrap/dist/js/bootstrap.js"></script>
      {{ block 'script' }} {{ /block }}
  </body>
  </html>
  ```

  ```html
  index.html
  {{ extend './layout.html' }}
  
  {{ block 'head'}}
  <style>
      body{
          background: skyblue
      }
  </style>
  {{ /block }}
  {{ block 'content'}}
  <div>
      <h1>index 页面填坑内容</h1>
  </div>
  {{ /block }}
  
  {{ block 'script'}}
  <script>
      alert('index 页面自己的js')
  </script>
  {{ /block }}
  ```

  ```html
  list.html
  {{extend './layout.html'}}
  
  {{ block 'content'}}
      <div>
          <h1>列表页自己的内容</h1>
      </div>
  {{ /block }}
  ```

  ```
  header.html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>header</title>
  </head>
  <body>
      <div>
          <h1>公共的头部</h1>
      </div>
  </body>
  </html>
  ```
###### 3.路由设计

| 路径      | 方法 | get参数 | post参数                | 是否需要登录 | 备注         |
| --------- | ---- | ------- | ----------------------- | ------------ | ------------ |
| /         | GET  |         |                         |              | 渲染首页     |
| /register | GET  |         |                         |              | 渲染注册页面 |
| /register | POST |         | email,nickname,password |              | 处理注册请求 |
| /login    | GET  |         |                         |              | 渲染登录页面 |
| /login    | POST |         | email,password          |              | 处理登录请求 |
| /logout   | GET  |         |                         |              | 处理退出请求 |

###### 4.模型设计

###### 5.功能实现

## 表单同步提交和异步提交

​      表单具有默认的提交行为，默认是同步的，同步表单提交，浏览器会锁死（转圈儿）等待服务端的响应结果。

​      表单的同步提交之后，无论服务端响应的是什么，都会直接把响应的结果覆盖掉当前页面。

​      后来有人想到了一种办法，来解决这个问题。

这个项目属于前后端混合开发方式

之后的开发属于前后端分离开发方式

##   服务端重定向针对异步请求无效

只有同步才能重定项

服务端重定向只针对同步请求才有效，异步请求无效

res.redirect('/')

客户端自己跳 

if (err_code === 0) {

​            // window.alert('注册成功！')

​            // 服务端重定向针对异步请求无效

​            window.location.href = '/'

## 通过Session保存登录状态

  领过苹果的不能再领了

  老师发苹果

  HTTP 是无状态的

  你自己记住你自己

  Cookie 小纸条

  Cookie 可以用来保存一些不太敏感的数据。

  但是不能用来保存用户登陆状态。

  isVIP: true

  记住用户名、购物车

  Session

  超市 -》 电子柜（）服务端

  你（客户端）（二维码小票（开箱凭证）Cookie）（凭证是唯一的，不可能重复）

  一旦丢失，不可找回，如果小票丢失，你的状态也就丢失了。

  钥匙是服务器给你的，所以这就很安全了，不太容易伪造出来。

  这个时候我们就可以包一些敏感的数据保存到服务端。

  客户端只需要拿着这把钥匙就可以了。

##  在Express配置使用`express-session`插件

https://www.npmjs.com/package/express-session

//在Express这个框架中，默认不支持Session和Cookie

//但是我们可以使用第三方中间件：express-session来解决

//1.npm install express-session 

//2.配置

//3.使用

//当把这个插件配置好之后，我们就可以通过req.session来发访问和设置Session成员

//添加  Session 数据：req.session.foo = 'bar'

//访问  Session 数据：req.session.foo

```js
const session = require('express-session')

app.use(session({
    //配置加密字符串，它会在原有加密基础之上和这个字符串拼起来去加密
    //目的是为了增加安全性，防止客户端恶意伪造
    secret: 'keyboard cat', 
    resave: false,
    saveUninitialized: true // 无论你是否使用Session，我都默认直接给你分配一把钥匙
  }))


 //注册成功，使用Session记录用户的登录状态
        req.session.user = user 

//渲染模板把session传出去
router.get('/',(req,res) => {
    console.log(req.session.user)
    res.render('index.html',{
        user: req.session.user
    })
})

利用session判断是否登录来利用模板引擎渲染页面
 <ul class="nav navbar-nav navbar-right">
          {{if user }}
          <a class="btn btn-default navbar-btn" href="/topics/new">发起</a>
          <li class="dropdown">
            <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false"><img width="20" height="20" src="../public/img/avatar-max-img.png" alt=""> <span class="caret"></span></a>
            <ul class="dropdown-menu">
              <li class="dropdown-current-user">
               
              </li>
              <li role="separator" class="divider">当前登录用户 {{ user.nickname }}</li>
              <li><a href="#">个人主页</a></li>
              <li><a href="/settings/profile">设置</a></li>
              <li><a href="/logout">退出</a></li>
            </ul>
          </li>

          {{ else }}
          <a class="btn btn-primary navbar-btn" href="/login">登录</a>
          <a class="btn btn-success navbar-btn" href="/register">注册</a>
          {{ /if}}
    
           使用
           //添加Session数据
           req.session.foo = 'bar'
           //获取Session数据
           req.session.foo
            
            提示：默认Session数据是内存存储的，服务器一旦重启就会丢失，真正的生产环境会把Session进行持久化存储
```



模板引擎默认值

## 书写步骤

- 创建目录结构
- 整合静态页-模板页
  - include
  - block
  - extend
- 设计用户登录，退出，注册的路由
- 用户注册
  - 先处理好客户端页面的内容（表单控件的name，收集表单数据，发起请求）
  - 服务端
    - 获取客户端表单请求数据
    - 操作数据库
    - 如果有错，发送500告诉客户端服务器错了
    - 其他的根据你的业务发送不同的响应数据
  - 用户登录
  - 用户退出