## Vue路由![]()

```js
router.ts
import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'
import Router1 from './views/router1.vue'

Vue.use(Router)

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/router1/:name',
      name: 'router1',
      component : Router1,
      
    },
    {
      path: '/about',
      name: 'about',
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
    }
  ]
})

```

实验组件

```js
<template>
    <div id="ts">
        <p>可怜的路由测试机器</p>
        <p>{{this.$route.query.id}}</p>
    </div>
</template>

<script lang="ts">
import { Prop,Component,Vue} from 'vue-property-decorator'
@Component
export default class router1 extends Vue{
   
        created () {
            // alert(this.$route.query.id)
            alert(this.$route.params.name)
        }
    
   
        // console.log(this.$route.params.id)
        // console.log(this.$route.query.id)
   
}
</script>

<style>

</style>

```

实验组件的地方

```js
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <!-- <router-link :to="{ name:'router1',path:'/router1',query:{id:1}}">Router</router-link> -->
      <router-link :to="{ name:'router1',path:'/router1',params:{name:'无心'}}">Router</router-link>
    </div>
    <router-view/>
  </div>
</template>
```

## Vue注册子组件

```js
父组件
<template>
    <div id="ts">
        <p>可怜的路由测试机器</p>
        <router2></router2>
 		<router3></router3>
    </div>
</template>

<script lang="ts">
import { Prop,Component,Vue} from 'vue-property-decorator'
import router2 from '@/views/router2.vue';
import router3 from '@/components/router3.vue';

@Component({    
    components:{
        router2,
        router3,
    }
})
export default class router1 extends Vue{
   
}
277
子组件
<template>
  <div class="router3">
    <h1>{{ msg }}</h1>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
  private msg : string = '第二个试验品';
}
</script>
```

Vue子父组件传值

```js
父组件传值  
<router2 msg="中野三玖"></router2>
<router3 v-bind:zara ='zara'></router3>

子组件接受值 
        <p>{{msg}}</p>
<script lang="ts">
import { Prop,Component,Vue} from 'vue-property-decorator'
@Component

export default class Router2 extends Vue{
    @Prop() private msg!: string;
}
子组件接受值 
 <h1>{{ zara }}</h1>

import { Component, Prop, Vue } from 'vue-property-decorator';
@Component

export default class HelloWorld extends Vue {
  @Prop() private zara!: string ; 
}
```

```js
子向父传值  emit装饰器的使用
子组件
<button @click="pass">emit装饰器的使用</button>
<script lang="ts">
import { Component, Prop, Vue , Emit} from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
  @Emit('welcome') private pass() : string{
      console.log('bindNoArg')
      return 'typescript'
  }
}
</script>
父组件
<router3 v-bind:zara ='zara' @welcome="sayHi"></router3>
前面是绑定传值 后面的welcome方法是获取事件传递过来的值
<script lang="ts">
import { Prop,Component,Vue} from 'vue-property-decorator'
import router2 from '@/views/router2.vue';
import router3 from '@/components/router3.vue';

@Component({    
    components:{
        router2,
        router3,
    }
})
export default class router1 extends Vue{   
        public bindNo : string = ''
	  private sayHi(arg: string): void {
        console.log(arg);
        this.bindNo = arg;
      }
}
</script>
```

公共兄弟组件传值 

```js
先在src下创建Pub.ts
import Vue from "vue"
export default new Vue()


发送的组件
<button @click="send">发送组件传值</button>
import Pub from '../Pub'
  send(){
      Pub.$emit('val',"公共组件传值牛逼")
  }

接收的组件
import Pub from '../Pub'
 mounted() {
      var vm = this
      // 用$on事件来接收参数
      Pub.$on('val', (data:string) => {
        console.log(data)
        vm.name = data
      })
    }
```

## @model装饰器

```js
三、 @Model 装饰器
@Model 装饰器是用以组件上实现双向绑定。

1）父组件
	<template>
	  <div>
	    <h1>@Model - 组件上实现双向绑定</h1>
		<el-button type="primary" @click="onAlterFoo">父组件改变foo</el-button>
	    <ModelSub v-model="foo"></ModelSub>
	  </div>
	</template>
	
	<script lang="ts">
	import { Vue, Component, Model } from 'vue-property-decorator';
	import ModelSub from '@/components/decorator/property_decorator/ModelSub.vue';
	
	@Component({ components: { ModelSub } })
	export default class ModelComponent extends Vue {
	  private foo: boolean = true;
	
	  private onAlterFoo() {
	    this.foo = !this.foo;
	  }
	}
	</script>

2）子组件
	<template>
	  <div>
	    <input type="checkbox" v-bind:checked="checked" 
	    	v-on:change="$emit('balabala', $event.target.checked)"
	    >
	  </div>
	</template>
	
	<script lang="ts">
	import { Vue, Component, Model, Prop } from 'vue-property-decorator';
	
	@Component
	export default class ModelComponent extends Vue {
	  @Model('balabala', { type: Boolean }) private checked!: boolean;
	}
	</script>
```

## @Provide 装饰器 和 @Inject 装饰器

@Provide 装饰器是用以注入数据，@Inject 装饰器是用以获取注入的数据

静态注入就一次不同步感觉一般 

```js


1）父组件 @Provide
	<template>
	  <div>
	    <h1>@Provide/@Inject - 接收来自父组件的数据</h1>
	    父组件通过依赖注入赋予的值是：{{ foo }}
	    <ProvideInject></ProvideInject>
	  </div>
	</template>
	
	<script lang="ts">
	import { Component, Vue, Provide } from 'vue-property-decorator';
	import ProvideInject from '@/components/decorator/property_decorator/ProvideInject.vue';
	
	@Component({ components: { ProvideInject } })
	export default class Home extends Vue {
	  @Provide('bar') private foo = '111';
	}
	</script>

2）子组件 @Inject
<template>
  <div>
    子组件通过依赖注入接收的值是：{{ bar }}
  </div>
</template>

<script lang="ts">
import { Component, Vue, Inject } from 'vue-property-decorator';

@Component
export default class ProvideInject extends Vue {
  @Inject() private readonly bar!: string;
}
</script>

```

## 

## @Watch 装饰器是用以监控数据是否改变。

```js
	<template>
	  <div>
	    <h1>@Watch - 监控数据是否改变</h1>
	    <input v-model="child" placeholder="请输入内容"></input>
	    <p>当前值：{{ val }} 原来值：{{ oldVal }}</p>
	  </div>
	</template>
	
	<script lang="ts">
	import { Component, Vue, Inject, Watch } from 'vue-property-decorator';
	
	@Component
	export default class ProvideInject extends Vue {
	  private child: number | null = null;
	  private val: number | null = null;
	  private oldVal: number | null = null;
	
	  @Watch('child')
	  private onChildChanged(val: number, oldVal: number): void {
	    this.val = val;
	    this.oldVal = oldVal;
	  }
	}
	</script>

```

## VueX部分

一、安装 npm 包

使用下面三条命令行进行包的安装

```
npm install vuex --save
npm install vuex-module-decorators -s
npm install vuex-class -s
```

## vue3.0+node跨域

```js
module.exports = {
    devServer: {
        proxy: {
            '/api': {
                target: 'http://192.168.3.167:3000/', 
                ws: true,  
                changeOrigin: true,  
                pathRewrite: {
                    '^/api': ''  
                }
            },
        }, 
    }
};


export default class M3 extends Vue{
    public data : any = 'asdas'

    created () {
    axios.get('/api/users')
    .then(res =>{ // 注册成功
        console.log(res);
        this.data = res;
	
	})  //  在http全局配置了catch所以这边是不用配置的
    }
}

node去官网自己找骨架开发
var express = require('express');
var router = express.Router();

/* GET users listing. */
router.get('/', function(req, res, next) {
  res.send('respond with a resource'); 
});

module.exports = router;

```



###### 

```js
<template>
  <div class="searchpage">
    <div class="search-box">
      <van-search placeholder="联系人姓名" class="search" v-model="value"/>
      <div class="search-text">
        <p>取消</p>
      </div>
    </div>
    <div class="search-content">
      <p>搜索到的联系人</p>
    </div>
    <div class="search-res">
      <ul>
        <li v-for="arr in testarr" :key="arr.id">
          <div class="search-res-imgbox">
            <div class="search-res-img">
              <div class="res-img"></div>
            </div>
            <div class="search-res-info">
              <p class="search-res-name">{{arr.name}}</p>
              <p class="search-res-num">{{arr.phone}}</p>
            </div>
          </div>
          <hr>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang='ts'>
import { Vue, Component , Watch } from 'vue-property-decorator';
import { Search } from 'vant';
import axios from 'axios';
Vue.use(Search);
@Component
export default class SearchPage extends Vue {
  public value: string = '';
  public testarr: any [] = [];
  public CancelToken : any = axios.CancelToken;
  public cancel : string | Function  = 'function';
  cancelRequest(){
            if(typeof this.cancel ==='function'){
                this.cancel('终止请求')
            }
        }
  
  @Watch('value')
    private onChildChanged(val: number): void {
      let that = this;
      this.cancelRequest();
      axios.get('/api/search?searchname=' + this.value,{
         cancelToken: new axios.CancelToken(function executor(c:any) {
           that.cancel = c;
         })
      })
      .then((res) => {
        console.log(res);
        if (res.data) {
          this.testarr = res.data;
        }
      }).catch(function (thrown) {
        if (axios.isCancel(thrown)) {
          console.log('Request canceled', thrown.message);
        } else {
          // handle error
          console.log(thrown);
        };
      })
}
}
</script>


<style lang='scss' scoped>
.searchpage {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;

  .search-box {
    display: flex;
    flex-grow: 1;
    max-height: 0.44rem;
    background: white;
    .search {
      width: 85.068%;
      padding: 0.1rem 0rem 0.1rem 0.15rem;
      .van-search__content {
        display: flex;
        border-radius: 13.5px;
        line-height: 0.27rem;
        height: 0.27rem;
        line-height: 0.27rem;
        align-items: center;
        background: #f1f1f1 100%;
      }
    }
    .search-text {
      display: flex;
      text-align: center;
      padding-left: -0.26rem; 
      margin: auto;
      height: 100%;
      align-items: center;
      p {
        line-height: 0.14rem;
        height: 0.14rem;
        font-size: 14px;
        color: #333333;
        text-align: center;
      }
    }
  }
  .search-content {
    display: flex;
    height: 0.32rem;
    align-items: center;
    p {
      color: #999999;
      height: 0.12rem;
      line-height: 0.12rem;
      font-size: 12px;
      margin-left: 0.15rem;
    }
  }
  .search-res {
    height: 2.84rem;
    ul {
      width: 100%;
      background: #ffffff 100%;
      li {
        hr{
          width: 3.45rem;
          margin: 0 auto;
          border: 0.005rem solid #eeeeee;
        } 
        .search-res-imgbox {
          height: 0.565rem;
          display: flex;
          .search-res-img {
            width: 0.36rem;
            height: 0.36rem;
            margin: 0.1rem 0.05rem 0.1rem 0.15rem;
            .res-img {
              width: 0.36rem;
              height: 0.36rem;
              border: transparent solid 0.0001px;
              border-radius: 50%;
              background: #ccc;
            }
          }
          .search-res-info {
            display: flex;
            flex-direction: column;
            height: 0.31rem;
            width: 0.98rem;
            margin: 0.13rem 0;
            justify-content: center;
            .search-res-name {
              height: 0.14rem;
              width: 0.98rem;
              line-height: 0.14rem;
              font-size: 14px;
              color: #333333;
              padding-bottom: 0.05rem;
            }
            .search-res-num {
              flex: auto;
              height: 0.12rem;
              width: 0.71rem;
              font-size: 12px;
              color: #999999;
            }
          }
        }
      }
      li:last-child hr{
        display: none;
      }
    }
  }
}
</style>

```

