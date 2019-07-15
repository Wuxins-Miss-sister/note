# Node.js 第7天课堂笔记

## 知识点

- 上午
  + 多人社区案例
  + Express 中间件
- 下午
  + Vue

---

## 反馈

```javascript
funtion extend (source, target) {
  for (var key in source) {
    target[key] = source[key]
  }
}

var obj1 = {
  foo: 'bar'
}

var obj2 = {
  name: 'Jack'
}

// obj2 就拥有了 obj1 的所有成员了
extend(obj1, obj2)
```

-  唉............
- 老师我想问下 那个操作文件路径不受打开命令执行node命令所属路径影响什么意思，是可以在任意窗口打开都可以访问到吗。。。。。
- 慢点 心急吃不了热豆腐
-  老师讲的很好 很清晰 希望老师下午第一节上课时间短点 第一节很困 上课时间太长听课效率有点低
-  老师 写案例的时候 一个文件的代码量多了 可不可以把字体稍微调小点便于看全局结构 有时候感觉自己连不上
- extend还不是很理解
  + 模板继承
  + extend 把复制过来
  + layout
  + index （extend layout）
  + index 就具有了 layout 的内容
  + index 还可以有自己的自定义内容
- 能不能把命令系统地罗列一下,@ 0 @
-  听得时候都差不多听懂了，可是自己做的时候发现不知道从何入手，即使是看着老师的需求与代码，也根本不懂怎么写了，感觉自己听完了就全都忘光了，很郁闷！
- 我现在学习的感觉就像 你是个俄国人，教我了一句外语，你已经重复 了很多遍，我也努力再听，但是当你说完的那一刻，我就完全不知道你说了什么。就是仅仅过了一耳朵，再加上内容太多，我已经感觉完全跟不上了，怎么办，我有点崩溃。怎么破
  + 上帝撒了一把智慧，可惜我打了一把伞
  + 多花时间、废寝忘食
- 老师你是不是喜欢Anglebaby?我同桌问的，她是个女的
  + Angelababy
- 如何在浏览器中模拟所谓的art-template高级技术？关于浏览器操作cookie的插件如何使用，需要注意些什么？还可以安装一些什么谷歌浏览器插件，有助于提高开发效率或模拟项目、测试的实用插件！
  + 只是一个工具
  + https://github.com/js-cookie/js-cookie
  + EditThisCookie Chrome 浏览器插件
-  文件引入有规则吗，像router.js中，需要重新引入第三方模块express，但是body-parser在routre页面也使用了呀，但是怎么不用引入
  +  这主要是中间件的原因
- req.session对象不清楚 希望老师再讲讲
  + req.session.xxx = xxx
  + req.session.xxx
  + Session 是基于 Cookie 实现的
- session 那块还是不怎么明白
-  课间下课尽量要准时，特别是上午第一节课比较困，听课效率低，反正下课次数固定，也不会让上课时间减少。 下午5点半增加上课时间多多益善
-  思路有点乱，有些小地方不明确，总的来说练得太少
- mongoose中的Schema用的不熟练
  + 多写写
-  如果先启动node服务，再开启数据库，数据库服务开启了，但是数据库并没有连接，这样会出现所有的操作都会失效的情况，必须打开新的命令行使用mongo命令手动连接数据库 反过来，如果先开启数据库，再开启node服务，就不会出现这样的问题，因为user.js代码中mongoose.connect('mongodb://localhost/test', { useMongoClient: true })自动连接了数据库，刚开始以为数据库竟然和node产生了依赖，原来并不是！ 希望老师控制每节课的上课时间，一节课集中精力的时间最多20分钟，接下来的20分钟基本只有一半的效率，后面的时间效率只会指数减小，所以希望老师能在45分钟左右就休息一次，也能提高效率； 老师讲的很细，很认真，也很负责，希望能在最后一个月的时间学好最重要的内容，就像你说的，因为刚好遇见你！
  +  你说的对，加油。
- 一到数据库就蒙。数据库始终连接不上去。我觉得不知道我数据库都学了什么?_?
- nice！

---

## 复习

- path 模块
- __dirname 和 __filename
  + **动态的** 获取当前文件或者文件所处目录的绝对路径
  + 用来解决文件操作路劲的相对路径问题
  + 因为在文件操作中，相对路径相对于执行 `node` 命令所处的目录
  + 所以为了尽量避免这个问题，都建议文件操作的相对路劲都转为：**动态的绝对路径**
  + 方式：`path.join(__dirname, '文件名')`
- art-template 模板引擎(include、block、extend)
  + include
  + extend
  + block
  + 动手写一写
- 表单同步提交和异步提交区别
  + 字符串交互
  + 请求（报文、具有一定格式的字符串）
  + HTTP 就是 Web 中的沟通语言
  + 服务器响应（字符串）
  + 01
  + 服务器端重定向针对异步请求无效
- Express 中配置使用 express-session 插件
  + 插件也是工具
  + 你只需要明确你的目标就可以了
  + 我们最终的目标就是使用 Session 来帮我们管理一些敏感信息数据状态，例如保存登陆状态
  + 写 Session
    * req.session.xxx = xx
  + 读 Session
    * req.session.xxx
  + 删除 Session
    * req.session.xxx = null
    * 更严谨的做法是 `delete` 语法
    * delete req.session.xxx
- 概述案例中注册-登陆-退出的前后端交互实现流程

---

### 中间件

http://expressjs.com/en/guide/using-middleware.html         科学上网

中间件的本质就是一个处理方法，我们把用户从请求到响应的整个过程分发到多个中间件中去处理，这样做的目的是提高代码的灵活性，动态可扩展的

## 应用程序级别中间件

万能匹配（不关系任何请求路径和请求方法）

```js
app.use(function(req,res,next){
    console.log('Time',Date.now())
    next()
})
```

只要以'/xxx/'开头的：

```json
app.use('/a',function(req,res,next){
	console.log('Time',Date.now())
	next()
})
```

---

## 路由级别中间件

get:

```js
app.get('/',function(req,res){
    res.send('Hello World')
})
```

post:

```js
app.post('/',function(req,res){
    res.send('Got a POST request')
})
```

put:

```js
app.put('/user',function(req,res){
    res.send('Got a PUT request at /user')
})
```

delete:

```js
app.delete('/user',function(req,res){
    res.send('Got a delect request at /user')
})
```



---

## 错误中间件

```js
app.use(function(err,req,res,next){
    console.error(err.stack)
    res.status(500).send('Something broke!')
})
```



## 内置中间件

- [express.static](http://expressjs.com/en/4x/api.html#express.static) serves static assets such as HTML files, images, and so on.
- [express.json](http://expressjs.com/en/4x/api.html#express.json) parses incoming requests with JSON payloads. **NOTE: Available with Express 4.16.0+**
- [express.urlencoded](http://expressjs.com/en/4x/api.html#express.urlencoded) parses incoming requests with URL-encoded payloads. **NOTE: Available with Express 4.16.0+**

## 第三方中间件

http://expressjs.com/en/resources/middleware.html

## Express middleware

The Express middleware modules listed here are maintained by the [Expressjs team](https://github.com/orgs/expressjs/people).

| Middleware module                                            | Description                                                  | Replaces built-in function (Express 3) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------------- |
| [body-parser](http://expressjs.com/en/resources/middleware/body-parser.html) | Parse HTTP request body. See also: [body](https://github.com/raynos/body), [co-body](https://github.com/visionmedia/co-body), and [raw-body](https://github.com/stream-utils/raw-body). | express.bodyParser                     |
| [compression](http://expressjs.com/en/resources/middleware/compression.html) | Compress HTTP responses.                                     | express.compress                       |
| [connect-rid](http://expressjs.com/en/resources/middleware/connect-rid.html) | Generate unique request ID.                                  | NA                                     |
| [cookie-parser](http://expressjs.com/en/resources/middleware/cookie-parser.html) | Parse cookie header and populate `req.cookies`. See also [cookies](https://github.com/jed/cookies) and [keygrip](https://github.com/jed/keygrip). | express.cookieParser                   |
| [cookie-session](http://expressjs.com/en/resources/middleware/cookie-session.html) | Establish cookie-based sessions.                             | express.cookieSession                  |
| [cors](http://expressjs.com/en/resources/middleware/cors.html) | Enable cross-origin resource sharing (CORS) with various options. | NA                                     |
| [csurf](http://expressjs.com/en/resources/middleware/csurf.html) | Protect from CSRF exploits.                                  | express.csrf                           |
| [errorhandler](http://expressjs.com/en/resources/middleware/errorhandler.html) | Development error-handling/debugging.                        | express.errorHandler                   |
| [method-override](http://expressjs.com/en/resources/middleware/method-override.html) | Override HTTP methods using header.                          | express.methodOverride                 |
| [morgan](http://expressjs.com/en/resources/middleware/morgan.html) | HTTP request logger.                                         | express.logger                         |
| [multer](http://expressjs.com/en/resources/middleware/multer.html) | Handle multi-part form data.                                 | express.bodyParser                     |
| [response-time](http://expressjs.com/en/resources/middleware/response-time.html) | Record HTTP response time.                                   | express.responseTime                   |
| [serve-favicon](http://expressjs.com/en/resources/middleware/serve-favicon.html) | Serve a favicon.                                             | express.favicon                        |
| [serve-index](http://expressjs.com/en/resources/middleware/serve-index.html) | Serve directory listing for a given path.                    | express.directory                      |
| [serve-static](http://expressjs.com/en/resources/middleware/serve-static.html) | Serve static files.                                          | express.static                         |
| [session](http://expressjs.com/en/resources/middleware/session.html) | Establish server-based sessions (development only).          | express.session                        |
| [timeout](http://expressjs.com/en/resources/middleware/timeout.html) | Set a timeout period for HTTP request processing.            | express.timeout                        |
| [vhost](http://expressjs.com/en/resources/middleware/vhost.html) | Create virtual domains.                                      | express.vhost                          |

### 全局处理错误

```js
var express = require('express')
var fs = require('fs')

var app = express()

// app.get('/abc', function (req, res, next) {
//   console.log('abc')
//   // req.foo = 'bar'
//   req.body = {}
//   next()
// })

// app.get('/abc', function (req, res, next) {
//   console.log(req.body)
//   console.log('abc 2')
// })

app.get('/', function (req, res, next) {
  fs.readFile('.d/sa./d.sa/.dsa', function (err, data) {
    if (err) {
      // return res.status(500).send('Server Error')
      // 当调用 next 的时候，如果传递了参数，则直接往后找到带有 四个参数的应用程序级别中间件
      // 当发生错误的时候，我们可以调用 next 传递错误对象
      // 然后就会被全局错误处理中间件匹配到并处理之
      next(err)
    }
  })
})

app.get('/', function (req, res, next) {
  console.log('/ 2')
})



app.get('/a', function (req, res, next) {
  fs.readFile('./abc', function (err, data) {
    if (err) {
      // return res.status(500).send('Server Error') 
      next(err)
    }
  })
})

app.use(function (req, res, next) {
  res.send('404')
})

// 配置错误处理中间件
app.use(function (err, req, res, next) {
  res.status(500).send(err.message)
})

app.listen(3000, function () {
  console.log('app is running at port 3000.')
})


```

