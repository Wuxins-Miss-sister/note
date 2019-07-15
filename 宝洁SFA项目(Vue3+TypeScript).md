项目地址

https://github.com/malun666?tdsourcetag=s_pcqq_aiomsg

```js
按需引入
借助 babel-plugin-component，我们可以只引入需要的组件，以达到减小项目体积的目的。

首先，安装 babel-plugin-component：

npm install babel-plugin-component -D

然后，将 .babelrc 修改为：

{
  "presets": [
    ["es2015", { "modules": false }]
  ],
  "plugins": [["component", [
    {
      "libraryName": "mint-ui",
      "style": true
    }
  ]]]
}
```

接口网站   模拟接口<http://yapi.demo.qunar.com/group/57051>

全局守卫

未登录不允许注入

获取对象类型方法.....

Object.prototype.toString.call()

一个是全局守卫挡不住 还有 样式 和报错 

