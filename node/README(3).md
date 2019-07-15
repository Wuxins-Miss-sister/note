# Node.js 第4天课堂笔记

## 知识点

- Express
- 基于文件做一套 CRUD

## 复习

- jQuery 的 each 和 原生的 JavaScript 方法 forEach

  - EcmaScript 5 提供的

    不兼容ie8

    JQuery2以下的版本是兼容ie8的

  - 它的each方法主要用来遍历JQuery实例对象（伪数组）

    ```javascript
     Array.prototype.mySlice = function(){
        var start = 0
        var end = this.length
        if(arguments.length === 1){
           start = arguments[0]
           }else if(arguments.length === 2){
               start = arguments[0]
               end = arguments[1]
           }
        var tmp = []
        for(var i = start; i < end; i++){
        tmp.push(this[i])
    	}
    	return tmp
    }    
    var fakeArr = {
        0:'abc',
        1:'efg',
        2:'haha',
        length:3
    }
    console.log([].mySlice.call(fakeArr))
    ```

    

  - 同时他也可以作为低版本浏览器中forEach替代品

  - jQuery的实例对象不能使用forEach方法，如果想要使用必须转为数组才可以使用

  - `[].slice.call(jQuery实例对象)`

  - 模块中导出对个成员和导出单个成员

- 301 和 302 的区别

  - 301永久重定向，浏览器会记住
  - 302临时重定向

- 模块中导出单个成员和导出多个成员的方式

  - module.exports = xxx`
  - 通过多次：`exports.xxx = xxx`
  - 导出多个也可以：`moudle.exports = {多个成员}`

- module.exports 和 exports 的区别
  + exports 只是 module.exports 的一个引用而已，目的只是为了简化写法
  + 每个模块最终 return 的是 module.exports
  + 每个模块中都有一个module对象
  + module对象中有一个exports对象
  + 我们可以把需要导出的成员都挂载到module.exports接口对象中 
  + 也就是：`module.exports.xxx = xxx`的方式
  + 但是每次都`module.exports.xxx = xxx`很麻烦，点的太多
  + 所以Node为了你方便，同时在每一个模块中都提供了一个成员叫：`exports`
  + `exports === module.exports`结果为 `true`
  + 所以对于`moudle.exports.xxx = xxx`的方式 完全可以`exports.xxx = xxx`
  + 当一个模块需要导出单个成员的时候，这个时候必须使用`module.exports = xxx`的方式
  + 不要使用 `exports.xxx = xxx`不管用
  + 因为每个模块最终向外`return`的是`module.exports`
  + 而`exports`只是`module.exports`的一个引用
  + 所以即便你为`exports = xx`重新赋值，也不会影响`module.exports`
  + 但是有一种赋值方式比较特殊：`exports = module.exports`这个用来重新建立引用关系的

- require 方法加载规则

  - 深入浅出Node.js(三)：深入Node.js的模块机制
  - 优先从缓存加载
  - 核心模块
  - 路径形式的模块
    * `./xxx`
    * `../xxxx`
    * `/xxxx` / 在这里表示的是磁盘根路径
    * `c:/xxx`
  - 第三方模块
    * 第三方模块的标识就是第三方模块的名称（不可能有第三方模块和核心模块的名字一致）
    * npm
      - 开发人员可以把写好的框架、库发布到 npm 上
      - 使用者在使用的时候就可以很方便的通过 npm 来下载
    * 使用方式：`var 名字 = require('npm install 的那个包名')`
    * node_modules
    * node_modules/express
    * node_modules/express/package.json
    * node_modules/express/package.json main
    * 如果 package.json 或者 package.json main 不成立，则查找备选项：index.js
    * 如果以上条件都不成立，则继续进入上一级目录中的 node_modules 按照上面的规则继续查找
    * 如果直到当前文件模块所属磁盘根目录都找不到，最后报错：`can not find module xxx`

- package.json 包描述文件
  + 就是产品的说明书

    

    ```cmd
    C:\Users\Lenovo\Desktop\npm-demo>npm init
    This utility will walk you through creating a package.json file.
    It only covers the most common items, and tries to guess sensible defaults.
    
    See `npm help json` for definitive documentation on these fields
    and exactly what they do.
    
    Use `npm install <pkg>` afterwards to install a package and
    save it as a dependency in the package.json file.
    
    Press ^C at any time to quit.
    package name: (npm-demo)
    version: (1.0.0)
    description: test
    entry point: (index.js) main.js
    test command:
    git repository:
    keywords:
    author: Yao
    license: (ISC)
    About to write to C:\Users\Lenovo\Desktop\npm-demo\package.json:
    
    {
      "name": "npm-demo",
      "version": "1.0.0",
      "description": "test",
      "main": "main.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "author": "Yao",
      "license": "ISC"
    }
    
    
    Is this OK? (yes) yes
    
    ```

  + `dependencies` 属性，用来保存项目的第三方包依赖项信息

  + 如果你的`node_modules`删除了也不用担心，我们只需要：`npm install` 就会自动把`package.json`中的`dependencies`中所有的依赖项都下载回来

  + 所以建议每个项目都要有且只有一个 package.json (存放在项目的根目录)

  + 我们可以通过 `npm init [--yes]` 来生成 package.json 文件

  + 同样的，为了保存依赖项信息，我们每次安装第三方包的时候都要加上：`--save` 选项。

- npm 常用命令

- node package manager

- npm网站

  - http:npmjs.com

  #### npm命令行工具

  npm init  使用时先初始化

  npm install art-template jquery bootstrap  一下安装三个

  然后好像包后面@是版本

  -- save  安装时在package.json 中存储依赖

  install

  uninstall

  ```
  npm --version
  ```

  查看版本 

  ```
  npm install --global npm
  ```

  升级npm（自己升级自己）

  #### 常用命令

  - npm init 
    - npm init -y 可以跳过向导，快速生成
  - npm install 
  - npm install
    - 只下载
  - npm install -save包名
    - 下载并且保存依赖项（package.json文件中的dependencies选项）
    - npm i -S包名  缩写
  - npm uninstall包名 
    - 只删除，如果有依赖项会依然保存 
    - npm un 包名
  - npm  uninstall --save 包名
    - 删除的同时也会把依赖信息也去除
    - npm un-S包名
  - npm help
    - 查看使用帮助 
  - npm 命令 --help
    - 查看指定命令的使用帮助 
    - 例如我忘记了uninstall命令的简写了，这个时候，可以输入`npm uninstall --help`来查看使用帮助 

## 解决npm被墙问题

npm存储包文件的服务器在国外，有时候会被墙，速度很慢，所以我们需要解决这个问题 

http://npm.taobao.org 淘宝的开发团队吧npm在国内做了一个备份

安装淘宝的cnpm：

```sh
#在任意目录执行都可以
#--global 表示安装到全局，而非当前目录
#--global 不能省略，否则不管用
npm install --global cnpm
```

接下来你安装包的时候把之前的``npm``替换成`cnpm`.

举个例子：

```shell
#这里还是走国外的npm服务器，速度比较慢
npm install jquery

#使用cnmp就会通过淘宝的服务器来下载jquery
cnpm install jquery
```

如果不想安装`cnpm`又想使用淘宝的服务器来下载

```shell
npm install jquery --registry=https://registry.npm.taobao.org
```

但是每一次手动这样加参数很麻烦，所以我们可以把这个选项加入配置文件中；

```shell
npm config set registry https://registry.npm.taobao.org

#查看npm配置信息
npm config list
```

只要经过上面命令的配置，则你以后所有的`npm install`都会默认通过淘宝的服务器来下载

## 修改完代码自动重启

我们这里可以使用一个第三方命名工具：`nodemon`来帮我们解决频繁修改代码服务器重启问题。`nodemon`是一个基于	Node.js开发的一个第三方命令行工具，我们使用的

时候需要独立安装 

```shell
#在任意目录执行该目录都可以
#也就是说，所有需要 --global 来安装的包都可以在任意目录执行
npm install --global nodemon
```

安装完毕之后，使用

```shell
之前node app.js

#使用nodemon
nodemon app.js
```

只要是通过`nodemon app.js`启动的服务，则它会监视你的文件变化，当文件发生变化的时候，自动帮你重启服务器。

测试安装没安装上可以用   --version

### package.json和package-lock.json

npm 5 以前是不会有`package-lock.json`这个文件的

npm5以后才加入了这个文件的

当你安装包的时候，npm都会生成或者更新`package-lock.json`这个文件

- npm5以后的版本安装包不需要加`--save`参数，它会自动保存依赖信息
- 当你安装包的时候，会自动创建或者是更新`package-lock.json`这个文件
- `package-lock.json`这个文件会保存`node_modules`中所有包的信息（版本，下载地址）
  - 这样的话重新`npm install`的速度就可以提升 
- 从文件来看有一个`lock`称之为锁
  - 这个lock是用来锁定版本的
  - 如果项目依赖了1.1.1版本
  - 如果你重新install其实会下载最新版本，而不是1.1.1
  - 我们的目的就是希望可以锁住1.1.1这个版本
  - 所以这个package-lock.json这个文件的另一个作用就是锁定版本号，防止自动升级新版

## Node中的其他成员

在每个模块中除了`require`,`exports`等模块相关API之外，还有两个特殊的成员

- `__dirname`  **动态获取**   可以用来获取当前文件模块所属目录的绝对路径   
- `__filename`  **动态获取** 可以用来获取当前文件的绝对路径
- `__dirname`和`__filename`是不受执行node命令所属路径影响的

在文件操作中，使用相对路径是不可靠的，因为在Node中文件操作的路径被设计为相对于node命令所处的路径（不是bug，人家这样设计是有使用场景）

所以为了解决这个问题，很简单，只需要把相对路径变为绝对路径就可以了

那这里我们就可以使用`__dirname`或者`__filename`来帮我们解决这个问题了

在拼接路径的过程中，为了避免手动拼接带来的一些低级错误，所以推荐多使用：`path.join()`来辅助拼接

所以为了尽量避免刚才所描述这个问题，大家以后在文件操作中使用的相对路径都统一转换为 `动态的绝对路径`。

> 补充:模块中的路径标识跟这里的路径没关系，不受影响（相对于文件模块）

## Path核心模块

> 参考文档：https://nodejs.org/dist/latest-v10.x/docs/api/path.html

- path.basename
  - 获取一个路径的文件名（默认包含扩展名）
- path.dirname
  - 获取一个路径中的目录部分
- path.extname
  - 获取一个路径中的扩展名部分
- path.parse
  - 把一个路径转为对象
    - root根路径
    - dir目录
    - base包含后缀名的文件名
    - ext后缀名
    - name不包含后缀名的文件名
- path.join
  - 当你需要进行路径拼接的时候，推荐使用这个方法
- path.isAbsolute判断一个路径是否是绝对路径

```js
例子
> path.basename('c:/asdad/sd/ds/index.js')
'index.js'
> path.basename('c:/asdad/sd/ds/index.js','.js')
'index'
> path.dirname('c:/asdad/sd/ds/index.js','.js')
'c:/asdad/sd/ds'
> path.extname('c:/asdad/sd/ds/index.js')
'.js'
> path.isAbsolute('c:/asdad/sd/ds/index.js')
true
> path.isAbsolute('/asdad/sd/ds/index.js')
true
> path.isAbsolute('./asdad/sd/ds/index.js')
false
> path.parse('./asdad/sd/ds/index.js')
{ root: '',
  dir: './asdad/sd/ds',
  base: 'index.js',
  ext: '.js',
  name: 'index' }
> path.jion('c:/a','b')
TypeError: path.jion is not a function
> path.join('c:/a','b')
'c:\\a\\b'
> path.join('c:/a','b','jjj')
'c:\\a\\b\\jjj'
>
```

## Express

原生的http在某些方面表现不足以应对我们开发需求，所以我们就需要使用框架来加快我们的开发效率，框架的目的就是提高效率，让我们的代码更高度统一

在Node中，又很多Web开发框架，我们这里以学习`express`为主

- http://expressjs.com/

- TJ    koa  express  创建者。。。好狠 

  ![1557042356862](nodeimg/1557042356862.png)

- Express 基本使用

- 起步

  #### 安装：

  ``````shell
  npm install --save express
  ``````

  npm install -g express-generator  

  express项目生成器  

  直接 >express server -e

  ```js
  1) 全局安装 express-generator (安装它的目的 是为了 运行 express命令 )     
  cnpm i express-generator -g    
  备注: 可以运行命令 express --version 检测一下 是否能使用   
  2) 可以使用 express 命令 来快速从创建一个项目目录        express 项目文件夹的名字 -e      
  示例: express demo -e 
  备注:            项目文件夹的名字:  会自动生成一个项目文件夹            -e:  使用 ejs 模板   
  3) 进入项目目录, 运行 cnpm i, 一次性安装所有的依赖模块        cd demo        cnpm i bin: 启动目录 里面包含了一个启动文件  www 默认监听端口是 3000 (不用)    node_modules:   所有安装的依赖模块 都在这个文件夹里面    public:  所有的前端静态资源  html css image  js    routes:  放的是 路由 文件 (默认有两个)             路由主要定义 url 和 资源 的映射关系 ( 一一对应关系 )             主要用来接收前端发送的请求 响应数据给前端    views: 主要放置 ejs 后端模板文件    app.js:  入口文件(主文件) 总路由 (其他的路由 要由它来分配)    package.json:  包描述文件  最重要的是 依赖的模板列表 dependencies                   依赖列表里面的所有模板 可以通过 cnpm i  一次性全部安装
  
  
  D:\Web\Vue>cd vuex
  
  D:\Web\Vue\vuex>express server -e
  
    warning: option `--ejs' has been renamed to `--view=ejs'
  
  
     create : server\
     create : server\public\
     create : server\public\javascripts\
     create : server\public\images\
     create : server\public\stylesheets\
     create : server\public\stylesheets\style.css
     create : server\routes\
     create : server\routes\index.js
     create : server\routes\users.js
     create : server\views\
     create : server\views\error.ejs
     create : server\views\index.ejs
     create : server\app.js
     create : server\package.json
     create : server\bin\
     create : server\bin\www
  
     change directory:
       > cd server
  
     install dependencies:
       > npm install
  
     run the app:
       > SET DEBUG=server:* & npm start
  
  
  D:\Web\Vue\vuex>cd server
  
  D:\Web\Vue\vuex\server>npm i
  npm notice created a lockfile as package-lock.json. You should commit this file.
  added 53 packages from 38 contributors and audited 141 packages in 4.161s
  found 0 vulnerabilities
  
  ```

  

  

  #### hello world

  ```javascript
  let express = require('express')
  
  //创建 app
  let app = express()
  
  app.get('/',(req,res)=>{
      res.send('hello world')
  })
  app.listen(3000,()=>{
      console.log('express app is running')
  })
  ```

  ##### 基本路由：

  路由器

  请求方法

  请求路径

  请求处理函数

  get：

  ```javascript
  //当你以GET方法请求/的时候，执行对应的处理函数
  app.get('/',(req,res)=>{
      res.send('hello world')
  })
  ```

  post:

  ```javascript
  //当你以POST方法请求/的时候，指定对应的处理函数
  app.post('/',(req,res)=>{
      res.send('hello world')
  })
  ```

  静态服务：

  ```	javascript
  //  /static/xxx
  app.use('/public',express.static('public'))
  
  //  /static/xxx
  app.use('/static',express.static('.public'))
  
  //  /public资源
  app.use(express.static('public'))
  
  //  /files资源
  app.use(express.static('files'))
  
  //
  app.use('/static',express.static(path.join(_dirname,'public')))
  ```

  使用 Express 把之前的留言本案例自己动手改造一下

- npm install --save express-art-template

## 模块标识中的 `/` 和文件操作路径中的 `/`

文件操作路径

```javascript
//在文件操作的相对路径中
//     ./data/a.txt 相对于当前目录
//      data/a.txt  相对于当前目录
//      /data/a.txt 绝对路径，当前文件模块所处于磁盘根目录
//      c:/xx/xx。。。绝对路径

// / 代表的磁盘根目录
// fs.readFile('/data/a.txt',(err,data)=>{
//     if(err){
//         return console.log('读取失败')
//     }
//     console.log(data.toString())
// })
```

模块操作路径

````
//这里如果忽略了。则也是磁盘根目录
require('/data/foo.js')

//相对路径
require('./data/foo.js')

//模块加载的路径中的相对路径不能省略
````

## Express 中配置使用 art-template 模板引擎

安装

```shell
npm install --save art-template
npm install --save express-art-template
```

配置：

```javascript
app.engine('art',require('express-art-template'))
app.engine('html',require('express-art-template'))
```

使用：

```javascript
//express默认先去views目录里找index.html 
app.get('/',function (req,res) {
    res.render('index.html',{
        title:"管理系统"
    })
  })
```

如果希望修改默认的`views`视图渲染存储目录，可以

`````javascript
//注意：第一个参数views千万不要写错
app.set('views',目录路径)
`````

## 在Express获取表单GET请求参数

Express内置了一个API，可以直接通过`req.query`来获取

```
req.query
```

## 在Express获取表单POST请求体数据 

在Express中没有内置获取表单POST请求体的API，这里我们需要使用一个第三方包：body-parser

安装

```shell
npm install --save body-parser
```

配置

````js
var express = require('express')
//引包
var bodyParser = require('body-parser')

var app = express()
//配置 body-parser
//只要加入这个配置，则在req请求对象上会多出来一个属性：body
//也就是说你可以直接通过req.body来获取表单POST请求体数据了
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))

// parse application/json
app.use(bodyParser.json())

app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
````

使用：

`````js
app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
`````

## crud

###### 起步

- 初始化

- 安装依赖

- 模板处理

###### 路由设计

| 请求方法 | 请求路径         | get参数 | post参数                    | 备注             |
| :------- | ---------------- | ------- | --------------------------- | ---------------- |
| GET      | /students        |         |                             | 渲染首页         |
| GET      | /students/new    |         |                             | 渲染添加学生页面 |
| POST     | /students/new    |         | name,age,gender,hobbies     | 处理添加学生请求 |
| GET      | /students/edit   | id      |                             | 渲染编辑页面     |
| POST     | /students/edit   |         | id，name,age,gender,hobbies | 处理编辑请求     |
| GET      | /students/delete | id      |                             | 处理删除请求     |

###### 提取路由模块

```js
// router.js路由模块
// 职责
//     处理路由
//     根据不同的请求方法+请求路径设置具体的请求处理函数
//     模块职责要单一，不要乱写
//     我们划分模块的目的就是为了增强项目代码的课维护性
//     提升开发效率
//Express提供了一种更好的方式
//专门用来包装路由的
const express = require('express')

//1.创建一个路由容器
const router = express.Router()

//2.把路由都挂载到router路由容器中
router.get('/students',(req,res)=>{
    
})
router.get('/students/new',(req,res)=>{
   
})
router.post('/students/new',(req,res)=>{
    
})
router.get('/students/edit',(req,res)=>{
    
})
router.post('/students/edit',(req,res)=>{
    
})
router.get('/students/delect',(req,res)=>{
    
})
//3.将router模块导出
module.exports = router
```

```js
const router = require（'./router'）

//把路由容器挂载到app服务中 
app.use(router)

```

###### 设计操作数据的API文件模块

```
// student.js
// 数据操作文件模块
// 职责：操作文件中的数据，只处理数据，不关心业务

//获取所有学生列表
exports.find = ()=>{

}

//添加保存学生
exports.save = ()=>{
    
}


//更新学生
exports.update = ()=>{
    
}


//删除学生
exports.delete = ()=>{
    
}
```



```js
function fn(callback) {
    //var callback = function(data){console.log(data)}
    setTimeout(()=>{
        var data = 'hello'
        callback(data)
    },1000)
  }
  //调用 fn，得到内部的data

//如果需要获取一个函数中异步操作的结果，则必须通过回调函数来获取

fn(function(data){
    console.log(data)
})

回调函数：获取异步操作的结果
```

##### 	自己编写的步骤

- 处理模板

- 配置发放静态资源

- 配置模板引擎

- 简单路由：/students渲染静态页面出来

- 路由设计

- 提取路由模块

- 由于接下来的一系列的业务操作都需要处理文件数据，所以我们需要封装student.js

- 先写好student.js文件结构

  - 查询所有的学生列表的API find
  - findByid
  - save
  - updateById
  - deleteById

- 实现具体功能

  - 通过路由收到请求
- 接受请求中的数据（get，post）
  
  - req.query
    - req.body
  - 接受请求中的数据（get，post）
- 根据操作结果给客户端发送响应
- 业务功能顺序
  - 列表
  - 添加
  - 编辑
  - 删除
## 模块化思想

模块如何划分：

- 模块职责要单一

- Vue

- angular

- React

  

## 上午总结

### 演讲	

> 说服
> PPT
> 脑图
> markdown
> 结构思维

- 找痛点 why 为什么
- 解决方案 what 是什么
- 怎么去使用 how 怎么用
- where 在哪儿用
- when  什么时候用
- 结构思维
- 文件路径中的 `/` 和模块标识中的 `/`
- nodemon
- Express
  + art-template 模板引擎的配置
  + body-parser 解析表单 POST 请求体
- 技术只是一种解决问题的手段、工具而已
  + 第三方的东西，不要纠结
  + 先以解决问题为主
- 详解了 express 静态服务 API
  
  + app.use('/public/', express.static('./public'))
  
## 下午总结

## 目标

- 文件路径中的 `/` 和模块标识中的 `/`
- Express 中配置使用 art-template 模板引擎
- Express 中配置使用 body-parser
- Express 中配置处理静态资源
- CRUD 案例中单独提取路由模块

