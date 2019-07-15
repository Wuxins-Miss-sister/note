创建

<https://blog.csdn.net/weiwenwen6/article/details/83120115>

# [vue-cli 中使用 TypeScript](https://segmentfault.com/a/1190000012361988)



 

- [vue.js](https://segmentfault.com/t/vue.js/blogs)
-  

- [typescript](https://segmentfault.com/t/typescript/blogs)
-  

- [前端](https://segmentfault.com/t/前端/blogs)

 

6.2k 次阅读  ·  读完需要 14 分钟

1













学以致用，这篇文章是对在 vue-cli 中使用 TypeScript 的一次小结。

## 环境

npm

```
// typescript
npm install typescript --save-dev

// ts-loader
npm install ts-loader --save-dev
```

webpack.base.conf.js

```
module.exports = {
  // 修改入口文件
  entry: './src/main.ts',
  // 引入 ts/tsx 文件时不必后缀 
  resolve: {
    extensions: ['.js', '.vue', '.json', '.ts', '.tsx'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
    }
  },
  module: {
    // 对 ts 使用 ts-loader
    {
      test: /\.tsx?$/,
      exclude: /node_modules/,
      use: [
        "babel-loader",
        {
          loader: "ts-loader",
          options: { appendTsxSuffixTo: [/\.vue$/] }
        }
      ]
    }
    // ...其他
  }
}
```

创建一个 .d.ts 文件让 TypeScript 识别 .vue 文件，在此项目中，我放到了 src/typings 文件夹下：

```
declare module '*.vue' {
  import Vue from 'vue'
  export default Vue
}
```

根目录下添加 tsconfig.json 配置文件，配置参数参考：[https://zhongsp.gitbooks.io/t...](https://zhongsp.gitbooks.io/typescript-handbook/content/doc/handbook/Compiler Options.html) ，项目内有一份配置，就不贴出来了。

## JavaScript 校验

很遗憾，如果你使用 TypeScript，在vue-cli(2.9.1) 里并不能使用 ESlint 校验 .vue 文件了，很常见的一个报错：

![img](https://segmentfault.com/img/remote/1460000012361993?w=1388&h=774)

在 .vue 文件内，并不识别 .d.ts 声明文件内的类型。

ESlint 不能用，TSlint 怎么样？
折腾了一会，在 .vue 文件内也有坑（可能是功力不够），最后决定先放弃。

webpack.base.conf.js

![img](https://segmentfault.com/img/remote/1460000012361994?w=1028&h=142)

## 关于插件

由于在 Vue 中使用 TypeScript 还不是很普及，大部分插件都缺少声明文件：

![img](https://segmentfault.com/img/remote/1460000012361995?w=1118&h=384)

此时必须添加新声明。
不过还好，[Vue](https://github.com/vuejs/vue/tree/dev/types), [Vue Router](https://github.com/vuejs/vue-router/tree/dev/types), [Vuex](https://github.com/vuejs/vuex/tree/dev/types), [Element](https://github.com/ElemeFE/element/tree/dev/types)，都提供了相应的声明文件。

## 开始修改

### .vue 文件

当然，首先要让 webpack 识别为 TypeScript 而不是 JavaScript，在 script 标签上加上 lang="ts"：

```
<template>
// ...
</template>
<script lang="ts">
// ...
<script>
```

有个官方维护的插件 [vue-class-component](https://github.com/vuejs/vue-class-component) ，可以写成下面方式：

```
import Vue from 'vue'
import Component from 'vue-class-component'

@Component({
  // 所有组件选项可以写这里
})
export default class Hello extends Vue {}
```

更多的实例可以看 [https://github.com/vuejs/vue-...](https://github.com/vuejs/vue-class-component) 。
此外，还有另一个基于 vue-class-component 的 [vue-property-decorator](https://github.com/kaorun343/vue-property-decorator) 插件，提供了如 Watch、Prop、Emit 等修饰器，于是可以写成下面方式：

```
import { Component, Vue, Watch, Prop } from 'vue-property-decorator'

@Component
export default class Hello extends Vue {
  @Watch('someValue')
  valueChange(val, oldVal) {}
  
  @Prop()
  propA: number
}
```

### Vue Router

Vue Router 的修改比较容易，在 router/index.ts 内为变量添加相应 interface 即可：

```
import Vue, { AsyncComponent } from 'vue'
import Router, { RouteConfig, Route, NavigationGuard } from 'vue-router'

import home: AsyncComponent = (): any => import(/* webpackChunkName: "home" */ '@/pages/home/index.vue')
// ... 其他组件

const routers: RouteConfig[] = [
  {
    path: '/home',
    comment: 'home'
  }
  // ...其他 routers
]
```

如果你想组件内使用 Vue Router 导航钩子，你必须注册一次：

```
import Component from 'vue-class-component'

// Register the router hooks with their names
Component.registerHooks([
  'beforeRouteEnter',
  'beforeRouteLeave',
  'beforeRouteUpdate' // for vue-router 2.2+
])
```

其他插件提供的钩子，也可以这么使用。
必须在使用之前注册，我把它放到了 main.ts 里。

### Vuex

Vuex 修改相对麻烦一点。

一个简单的栗子

```
import Vue from 'vue'

// 需要使用 Vuex 的 interface 
import Vuex, { ActionTree, MutationTree } from 'vuex'

Vue.use(Vuex)

interface State = {
  name: String;
}

const state: State = {
  name: ''
}

const action: ActionTree<State, any> = {
  changName (
    { commit },
    name: String
  ): void {
    commit('CHANGE_NAME', name)
  }
}

const mutations: MutationTree<State> = {
  'CHANGE_NAME' (
    state: State,
    name: String
  ): void {
    state.name = name
  }
}

export default new Vuex.Store({
  state,
  actions,
  mutations
})
```

如果你想在组件里面使用 vuex 的辅助函数，可以使用这个插件 [vuex-class](https://github.com/ktsn/vuex-class) 。由于我不习惯使用辅助函数，这里也就不再赘述了。