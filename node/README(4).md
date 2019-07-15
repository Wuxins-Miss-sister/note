# Node.js 第5天课堂笔记

## 知识点

- Express
- MongoDB
- 项目
  + 一天半的时间

## 反馈

-  新版sublime 怎么格式化 怎么一起选中长度不等的内容 怎么改颜色 有的写对了也没颜色 仍然是白色
  +  HTML-CSS-JS Prettify
-  代码量好多
  +  真正的开发是咱们这个小案例的无数倍
-  callback是不是相当于函数自调用?
  +  很简单，函数也是一种数据类型，既可以当作参数进行传递，也可以当作方法的返回值
- 我们现在用的模块化是CMD吧 老师能不能给我们扩展一下AMD
  + PHP 中为什么就可以直接 `require`、`include` 因为 PHP 当初在设计的时候就加入了这个功能
  + PHP 这门语言天生就支持
  + 模块作用域
  + 可以使用 API 来进行文件与文件之间的依赖加载
  + 在 Node 这个环境中对 JavaScript 进行了特殊的模块化支持 CommonJS
  + JavaScript 天生不支持模块化
    * require
    * exports
    * Node.js 才有的
  + 在浏览器中也可以像在 Node 中的模块一样来进行编程
    * `<script>` 标签来引用加载，而且你还必须考虑加载的顺序问题
    * require.js 第三方库 AMD
    * sea.js     第三方库 CMD
  + 无论是 CommonJS、AMD、CMD、UMD、EcmaScript 6 Modules 官方规范
    * 都是为了解决 JavaScript 的模块化问题
    * CommonJS、AMD、CMD 都是民间搞出来的
    * EcmaScript 是官方规范定义
    * 官方看民间都在乱搞，开发人员为了在不同的环境使用不同的 JavaScript 模块化解决方案
    * 所以 EcmaScript 在 2015 年发布了 EcmaScript 2016 官方标准
    * 其中就包含了官方对 JavaScript 模块化的支持
    * 也就是说语言天生就支持了
    * 但是虽然标准已经发布了，但是很多 JavaScript 运行换将还不支持
    * Node 也是只在 8.5 版本之后才对 EcmaScript 6 module 进行了支持
    * 后面学 Vue 的时候会去学习
    * less 编译器 > css
    * EcmaScript 6 -> 编译器 -> EcmaScript 5
    * 目前的前端情况都是使用很多新技术，然后利用编译器工具打包可以在低版本浏览器运行。
    * 使用新技术的目的就是为了提高效率，增加可维护性
-  内心极度脆弱。。。有心杀敌 无力回天，总感觉时间不够用。
  +  不要猥琐发育，就得浪
- 虽然比较多 但是因为老师讲的很清晰 还是愿意去写的 对于 node.js 的奥义 封装异步的API 就是需要多练
- 老师讲的很清晰 讲课也很洒脱 老师是不是被夸的已经习惯了 后面讲的回掉函数有点懵了
- 老师讲的很好，思路清晰，项目跟着老师的笔记一步一步敲，so easy
-  觉得老师讲课真的超级棒啊 传智的实力担当 双击没毛病 老铁666
- 都坐下 基本操作 哇,老师,一般敢说这句话的都是大神,我还是个菜鸟,学的那是一脸懵逼
-  有点懵，看着老师的思路做，可是还是不知道从何入手，唉。。。
  +  本着达芬奇画鸡蛋的精神
  +  《使徒行者》三哥
  +  《反黑》陈小春
    *  卧底 8年卧底
    *  文职工作
    *  报了电脑版
    *  吃饭都在看书
    *  学习 -》吃饭也是看书
    *  边角余料
- var router = require('./router') 这一步不是加载router.js并执行该文件吗 为什么还要执行app.use(router) app.use 不是开放静态资源吗 app.use(router)在这里是什么意思，挂载到 app 服务中的意思是？ module.exports = app 也不懂
  + 这里涉及到一个中间件的概念
  + app.use 不仅仅是用来处理静态资源的
  + 还可以做很多工作
  + 配置 body-parse 也是通过 app.use 来配置的
  + 这叫中间件，其中有一套规则
- npm init --yes 生成一个package.json 文件 npm --save 文件名 又生成一个package-lock.json文件,又生成的文件和初始化生成的文件有区别吗?
  + 当你安装包的时候，新版的 npm 还会自动生成一个文件：package-lock.json
-  早上听的还可以，下午感觉一头蒙，还好老师讲了晚上自己做案例的具体步骤，不然感觉无从下手，还是反馈多一点好，还可以回顾回顾，不然感觉老师一天讲的知识太多了，消化不了，嘤嘤嘤~~~
- 其实拖堂的效率也不高啊。。可能是我天资愚笨
  + 对自己有信息
  + 撸起袖子加油干、一张蓝图绘到底
-  老师你好，每节课的事件有点长，上课时间长注意力就容易模糊。听课效率确实有问题，有时候同桌都快憋不住了，为了不丢下知识点，依旧在憋着，好担心...
- 为什么模板引擎在app.js中引入之后在router.js中不引入可以直接使用，而express还需要在router.js中再引入一次 app.js中路由器挂载不是很懂 router.js中为什么要创建一个路由器容器，不知道作用是干什么的 es6中的find方法不是很懂
  + 中间件
  + EcmaScript 6 的 find 方法
- 老师，你后来讲的回调函数那里，关于增删改查案例一个已经够呛了，你竟然在最后都讲完了； 虽然增删改查文件的操作在php之前讲过，但是真的忘了，而且php学的也不好； 还有：对于php是世界上最好的语言，我持怀疑态度，觉得它是世界上最难理解的语言； 诶！苦恼！又来了一个node，知道后边的boss都很难应付，比如什么angular、react和vue，现在其实也做好了心理准备！ 来者不拒吧！看来这一个月注定是一个煎熬的日子！
  + PHP 是世界上最好的语言（贬义）
  + 一切我抗
- 在express框架中怎么判断访问页面不存在的情况？

## 复习

- 文件路径中的 `/` 和模块标识中的 `/`
- Express 中配置使用 art-template 模板引擎
- Express 中配置使用 body-parser
- Express 中配置处理静态资源
- CRUD 案例中单独提取路由模块



## 回调函数

异步编程

不成立的情况 

```js
function add(x,y) {
    console.log(1)
    setTimeout(()=>{
        console.log(2)
        let ret = x + y
        return ret
    },1000)
    console.log(3)
    //到这里执行就结束了，不会等到前面的定时器，所以直接就返回了默认值 undefined
  }
  console.log(add(10,20))
1 3 undefined 2
```

```js
function add(x,y) {
      let ret
    console.log(1)
    setTimeout(()=>{
        console.log(2)
        ret = x + y
    },1000)
    console.log(3)
    return ret
    //到这里执行就结束了，不会等到前面的定时器，所以直接就返回了默认值 undefined
  }
  console.log(add(10,20))
```

```js
回调函数 
let add = (x,y,callback) => {  // 实现这个目的
    console.log(1)
    setTimeout(()=>{
        let ret = x + y
        callback(ret)
    },1000)
}

add(10,20,callback = ret =>   // 获取后进行的操作 
    console.log(ret)
    )
```

+ 如果需要得到一个函数内部异步操作的结果，这是时候必须通过回调函数来获取

+ ```
  setTimeout readFile writeFile ajax
  ```

+ 在调用的位置传递一个函数进来

+ 在封装的函数内部调用传递进来的函数

+ 基于原生XMLHTTPRequest封装方法 

  ```js
   function get(url,callback) {  
     let xhr = new XMLHttpRequest()
    
      //当请求加载成功之后要调用指定的函数 
      xhr.onload = function(){
          //我现在需要得到这里的xhr.responseText
          callback(xhr.responseText)
      }
      xhr.open("get",url,true)
      xhr.setRequestHeader('Content-type','application/json')
     
      xhr.send()
  }
      get('./data.json',function(data){
          console.log(data)
      })
  ```

+ ```js
  自己es6更改版本 
  let get = (url,callback) => {
      let xhr = new XMLHttpRequest()
      xhr.onload = () => {
          callback(xhr.responseText)
      }
      xhr.open('get',url,true)
      xhr.setRequestHeader('Content-type','application/json')
      xhr.send()
  }
      get('./data.json',(data)=>console.log(data))
  ```

+ 

- find、findIndex、forEach
  + 数组的遍历方法，都是对函数作为参数一种运用
    
    + every
    
  + some 
  
  + includes
  
  + map
  
  + reduce
  
    ```js
    //es6 对数组新增了很多方法
    //  find
    //  findIndex
    
    //find接受一个方法作为参数，方法内部返回一个条件
    //find会遍历所有的元素，执行你给定的带有条件返回值得函数
    //符合该条件的元素会作为find方法的返回值
    //如果遍历结束还没有符合该条件的元素，则返回 undefined
    
    let users = [
        {id : 1,name:'张三'},
        {id : 2,name:'张三'},
        {id : 3,name:'张三'},
        {id : 4,name:'张三'},
    ]
    
    Array.prototype.myFind = function (conditionFunc) {
    //let conditionFunc = function (item,index){return item.id === 4}
        for(var i = 0;i < this.length;i++){
            if(conditionFunc(this[i],i)){
              // return item.id === 4  某个元素符合要求就会返回true
                return this[i]
               // return i  这个就是返回下标  findindex
                
            }
        }
      }
    
    let ret = users.myFind(function (item,index) {
        return item.id === 4
      })
      
    console.log(ret)
    ```
  
- package-lock.json 文件的作用
  + 下载速度快了
  + 锁定版本
  
- JavaScript 模块化
  
  - 模块具有模块作用域 
  
  - 可以使用API来进行文件与文件之间的依赖加载
  
  - 在Node这个环境中对JavaScript进行了特殊的模块化支持CommonJS
  
  - JavaScript天生不支持模块化 
  
  - require
  
  - exports
  
  - Node.js才有的
  
  - Node 中的 CommonJS
  
  - 在浏览器中也可以象在Node中的模块一样来进行编程
  
    - `<script>`标签来引用加载，而且你还必须考虑加载的顺序问题
  
    * AMD require.js  第三方
    * CMD sea.js   第三方 
  
  - EcmaScript 官方在 EcmaScript 6 中增加了官方支持
  
  - EcmaScript 6
  
  - 后面我们会学，编译工具
  
  - 目前的前端情况都是使用很多新技术，然后利用编译工具打包可以在低版本浏览器运行
  
  - 使用新技术的目的就是为了提高效率，增加可维护性 
  
## MongoDB 数据库
+ 关系型数据库和非关系型数据库
  
    表就是关系
    
    或者说表与表之间存在关系
    
    - 所有的关系型数据库都需要通过`sql`语句来操作
    - 所有的关系型数据库在操作之间都需要设计表结构
    - 而且数据表还支持约束
      - 唯一的
      - 主键
      - 默认值
      - 非空
    
    - 非关系型数据库非常的灵活
    - 有的非关系型数据库就是key-value
    - 但是MongoDB是长的最像辊系型数据库的费辊系型数据库
      - 数据库-》数据库
      - 数据表-》集合（数组）
      - 表记录-》（文档对象）
    - MongoDB不需要设计表结构
    - 也就是说你可以随意的往里面存数据，没有结构性这一说
    - 下载
    - 安装
    - 配置环境变量
    - 最后输入`mongod --version`测试是否安装成功
    - 去官网下载然后解压本地存在c盘里 添加path环境变量
    - C:\Program Files\MongoDB\bin 安装目录 配置成功
    - 控制台里面 mongod --version
    
    ```shell
    C:\Users\Lenovo>mongod --version
    db version v4.0.9
    git version: fc525e2d9b0e4bceff5c2201457e564362909765
    allocator: tcmalloc
    modules: none
    build environment:
        distmod: 2008plus-ssl
        distarch: x86_64
        target_arch: x86_64
    
    ```
    
+ MongoDB 的数据存储结构
  
    * 数据库
    * 集合（表）
    * 文档（表记录）

- MongoDB 官方有一个 mongodb 的包可以用来操作 MongoDB 数据库
  
  + 这个确实和强大，但是比较原始，麻烦，所以咱们不使用它

## 启动和关闭数据库

启动

```shell
#mongodb 默认使用执行 mongod 命令所处盘符根目录下的 /data/db 作为自己的数据存储目录
#所以在第一次执行该命令之前先自己动手新建一个 /data/db
然后输入 mongod 启动 
```

如果想要修改默认的数据存储目录，可以：

```shell
mongod --dbpath = 数据存储目录路径
```

停止 ：

```
在开启服务的控制台，直接Ctrl+c即可停止 
或者直接关闭开启服务的控制台也可以
```

## 连接数据库

连接

```shell
#该命令默认连接本机的MongoDB服务
你需要打开另外一个cmd输入这个
mongo
```

退出

```shell
#在连接状态输入exit退出连接
exit
```

## 基本命令

- `show dbs`

  - 查看显示所有数据库

- `db`

  - 查看当前操作的数据库

- `use 数据库名称`

  - 切换到指定的数据库（如果没有会新建）

- 插入数据

  > show dbs
  > admin   0.000GB
  > config  0.000GB
  > local   0.000GB
  > use wuxin
  > switched to db wuxin
  > db
  > wuxin
  > show dbs
  > admin   0.000GB
  > config  0.000GB
  > local   0.000GB
  > db.students.insertOne({"name":"Jack"})
  > {
  >         "acknowledged" : true,
  >         "insertedId" : ObjectId("5cd81f16358fc0e9cb6df04c")
  > }
  > show dbs
  > admin   0.000GB
  > config  0.000GB
  > local   0.000GB
  > wuxin   0.000GB
  > show collections
  > students
  > db.students.find()
  > { "_id" : ObjectId("5cd81f16358fc0e9cb6df04c"), "name" : "Jack" }

## 在Node中如何操作MongoDB数据

使用官方的`mongodb`包来操作

在npmjs中搜索 mongodb

## mongoose

- mongoose

- 第三方包：`mongoose`基于MongoDB官方的`mongodb`包再一次做了封装

  官网  https://mongoosejs.com/

  官方指南 https://mongoosejs.com/docs/guide.html

  官方API文档 https://mongoosejs.com/docs/api.html

- 真正在公司进行开发，使用的是 mongoose 这个第三方包

  + 它是基于 MongoDB 官方的 mongodb 包进一步做了封装
  + 可以提高开发效率
  + 让你操作 MongoDB 数据库更方便

- 掌握使用 mongoose 对数据集合进行基本的 CRUD

- 把之前的 crud 案例改为了 MongoDB 数据库版本

- 使用 Node 操作 mysql 数据库

  ### 1起步

  ```shell
  npm i mongoose
  ```

  hello world:

  ```js
  const mongoose = require('mongoose');
  mongoose.connect('mongodb://localhost:27017/test', {useNewUrlParser: true});
  
  const Cat = mongoose.model('Cat', { name: String });
  
  const kitty = new Cat({ name: 'Zildjian' });
  kitty.save().then(() => console.log('meow'));
  ```

  ## 1.MongoDB数据库的基本概念

  - 数据库   :可以有多个数据库

  - 集合      ：一个数据库中可以有多个集合（表）

  - 文档      ：一个集合中可以有多个文档（表记录）

  - 文档结构很灵活，没有任何限制

  - MongoDB非常灵活，不需要像MySQL一样先创建数据库，表，设计表结构

    - 在这里只需要：当你需要插入数据的时候，只需要指定往哪个数据库的哪个集合操作就可以了
    - 一切都由MongoDB来帮你自动完成建库建表这件事儿

    ```
    {
    	qq:{
    		users:[
    		
    		],
    		products:[
    		
    		],
    	},
    	taobao:{
    	
    	}
    }
    ```

  ## 官方指南

  3.1设计Schema 发布 Model

  ```js
  const mongoose = require('mongoose')
  
  const Schema = mongoose.Schema
  
  //1.连接数据库    
  //指定连接的数据不需要存在，当你插入第一条数据之后就会自动被创建出来
  mongoose.connect('mongodb://localhost/test',{ useNewUrlParser: true })
  
  //2.设计结合结构（表结构）
  //字段名称就是表结构中的属性名称
  //值
  //约束的目的是为了保证数据的完整性，不要有脏数据
  let userSchema = new Schema({
     username:{
         type: String,
         required:true // 必须有
     },
     password:{
         type: String,
         required:true
     },
     email:{
         type: String
     }
    })
  
  //3.将文档结构发布为模型
  //  mongoose.model 方法就是用来讲一个架构发布为model
  //  第一个参数：传入一个大写名词参数字符串用来表示你的数据库名称
  //      mongoose会自动将大写名词的字符串生成 小写复数 的 集合名称
  //        例如这里的User最终会变为users集合名称 
  //  第二个参数： 架构Schema
  // 
  let User = mongoose.model('User', userSchema)
  
  //4.当我们有了模型构造函数之后，就可以使用这个构造函数对users集合中的数据为所欲为了
  //增删改查
  ```

  #### 3.2增加数据

  ```js
  let admin = new User({
      username: 'admin',
      password: '123456',
      email:'admin@admin.com'
  })
  
  admin.save((err,ret) => {
      if(err) console.log('保存失败')
      else console.log('保存成功') 
      console.log(ret)
  })
  ```

  #### 3.3 查询

  查询所有：

  ```js
  查询数据   //查询所有  查出来是数组
  User.find((err,ret)=>{
      if(err) console.log('查询失败')
      else console.log(ret)
  })
  ```

  按条件查询所有

  ```js
  User.find({
      username:'zs'
  },(err,ret)=>{
      if(err) console.log('查询失败')
      else console.log(ret)
  })
  ```

  按条件查询单个

  ```js
  按条件查单个   
  这个是查一个按条件查 查出来是一个对象  如果没有条件 那么查出来第一个
  User.findOne({
      username:'zs',
      password:'123456sda'
  },(err,ret)=>{
      if(err) console.log('查询失败')
      else console.log(ret)
  })
  ```

  按照id查询

  ```js
   //replace 
      //字符串模式
      //简单，但是不支持全局和忽略大小写问题
      //正则表达式模式
      //强大，支持全局和忽略大小写
      Student.findById(req.query.id.replace(/"/g,''),(err,student)=>{
          if(err){
                  return res.status(500).send('Server error')
          }
        res.render('edit.html',{
              student:student
        })
      })
  ```
  

  
##### 3.4 删除

  ```js
  删除数据 
User.remove({
      username:'zs'
},(err,ret)=>{
      if(err) console.log('删除失败')
    else console.log('删除成功')
      console.log(ret)
  })
  ```

  根据条件删除一个

  ```
  Model.findOneAndRemove(conditions, [options], [callback])
  ```

  根据id删除一个

  ```
  Model.findByIdAndRemove(id, [options], [callback])
  ```

  ##### 3.5更新数据

  根据条件更新所有

  ```js
Model.update(conditions, doc ,[options], [callback])
  ```

  根据指定条件更新一个

  ```js
  Model.findOneAndUpdate(conditions, doc ,[options], [callback])
  ```

  根据id更新一个

  ```js
  更新数据 
  User.findByIdAndUpdate('5cd831f0c7a6ac4a2470a01d',{
      password:'123'
  },(err,ret)=>{
      if(err) console.log('更新失败')
      else console.log('更新成功')
  })
  ```

## 使用Node.js操作Mysql数据库

安装：

```shell
npm install mysql
```

```js
使用方法：

var mysql = require('mysql');

//1. 创建连接
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'users' //数据库名和表名一样
});
 
//2.连接数据库  打开冰箱门
connection.connect();
 
//3.执行数据操作  把大象放冰箱
// connection.query('SELECT * FROM `users`', function (error, results, fields) {
//   if (error) throw error;
//   console.log('The solution is: ', results);
// });

connection.query('INSERT INTO users VALUES(NULL,"admin","123456")', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results);
  });
  

//4.关闭连接    关闭冰箱门
connection.end();
```

## Promise

callback hell  回调地狱 

![callbackhell](nodeimg/callbackhell.png)

无法保证顺序的代码

```js
文件越大加载越慢但是无法保证顺序
const fs = require('fs')

fs.readFile('./data/a.txt','utf8',(err,data)=>{
    if(err){
        //return console.log('读取失败')
        //抛出异常
        //  1.阻止程序的执行
        //  2.把错误消息打印到控制台
        throw err
    }
    console.log(data)
})


fs.readFile('./data/b.txt','utf8',(err,data)=>{
    if(err){
        //return console.log('读取失败')
        //抛出异常
        //  1.阻止程序的执行
        //  2.把错误消息打印到控制台
        throw err
    }
    console.log(data)
})

fs.readFile('./data/c.txt','utf8',(err,data)=>{
    if(err){
        //return console.log('读取失败')
        //抛出异常
        //  1.阻止程序的执行
        //  2.把错误消息打印到控制台
        throw err
    }
    console.log(data)
})
```

用嵌套的方法保证执行顺序   但是产生了回调地狱不美观不利于维护 

```js
const fs = require('fs')

fs.readFile('./data/a.txt','utf8',(err,data)=>{
    if(err){
        //return console.log('读取失败')
        //抛出异常
        //  1.阻止程序的执行
        //  2.把错误消息打印到控制台
        throw err
    }
    console.log(data)
    fs.readFile('./data/b.txt','utf8',(err,data)=>{
    if(err){
        //return console.log('读取失败')
        //抛出异常
        //  1.阻止程序的执行
        //  2.把错误消息打印到控制台
        throw err
    }
    console.log(data)
    fs.readFile('./data/c.txt','utf8',(err,data)=>{
    if(err){
        //return console.log('读取失败')
        //抛出异常
        //  1.阻止程序的执行
        //  2.把错误消息打印到控制台
        throw err
    }
    console.log(data)
        })
    })
})

```

为了解决以上编码方式带来的问题（回调地狱嵌套），所以在EcmaScript6中新增了一个API`promise`

- Promise的英文就是承诺，保证的意思（i promise you）

- 基本代码

- ```js
  const fs = require('fs')
  
  //创建Promise容器
  // 1 .给别人一个承诺 I promise you
  // Promise 容器一旦创建，就开始执行里面的代码
  //promise 是同步代码 内部异步代码才是异步执行
  let p1 = new Promise((res,rej)=>{
      fs.readFile('./data/a.txt','utf8',(err,data)=>{
          if(err) rej(err) // 失败了 承诺容器中的任务失败了 把容器的Pending状态变成Rejected
          res(data)   //成功了 把容器的Pending状态变成Resolved
          //也就是说这里你调用的resolve方法实际上就是then方法传递的那个function
      })    
  })
  //then方法接受的function就是容器中的resolve函数 
  p1.then((res)=>{
      console.log(res)
  },(rej)=>{
      console.log(rej)
  })
  ```

  封装异步Promise 

  ```js
  const fs = require('fs')
  
  let pReadFile = (filePath)=>{
      return new Promise((res,rej)=>{
      fs.readFile(filePath,'utf8',(err,data)=>{
          if(err) rej(err) 
          res(data)  
          })    
      })
  }
  
  pReadFile('./data/a.txt')
      .then((res)=>{
          console.log(res)
          return pReadFile('./data/b.txt')
      })
      .then((res)=>{
          console.log(res)
          return pReadFile('./data/c.txt')
      })
     
  
  ```

  接口服务器 真好用啊  JSON Server

  https://www.npmjs.com/package/json-server

  ```shell
  Getting started
  Install JSON Server
  
  npm install -g json-server
  Create a db.json file with some data
  
  {
    "posts": [
      { "id": 1, "title": "json-server", "author": "typicode" }
    ],
    "comments": [
      { "id": 1, "body": "some comment", "postId": 1 }
    ],
    "profile": { "name": "typicode" }
  }
  Start JSON Server
  
  json-server --watch db.json
  Now if you go to http://localhost:3000/posts/1, you'll get
  
  { "id": 1, "title": "json-server", "author": "typicode" }
  ```

  