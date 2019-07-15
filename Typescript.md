## 配置自动编译ts

```js
第一步 tsc --init 生成ts配置文件 

找到这个更改命令更改ts同时可以编译ts "outDir": "./js",    

第二部 任务 - 运行任务  监视 tsconfig.json
```

## TypeScript中的数据类型

​		typescript中为了使编写的代码更规范，更有利于维护，增加了类型校验，在typescript中主要有以下数据类型

```
Object
布尔boolean类型
数字number类型
字符串类型string类型
数组类型array类型
元组类型tuple类型
枚举类型enum类型
任意类型any类型
null 和 undefined
void类型
never类型
```

//写ts代码必须指定类型 



## Object

`object`表示非原始类型，也就是除`number`，`string`，`boolean`，`symbol`，`null`或`undefined`之外的类型。

使用`object`类型，就可以更好的表示像`Object.create`这样的API。例如：

```ts
declare function create(o: object | null): void;

create({ prop: 0 }); // OK
create(null); // OK

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```

//布尔类型

​    // var aaa = true

​    // flag = 456

//

// var flag:boolean = true;

//flag = 123; //错误写法

//flag = false; //正确写法

//数字类型(number)

​    // var num:number = 123;

​    // num = 456;

​    // console.log(num)

​    // num = 'str' //错误写法

//字符串类型string类型

​    // var str:string = 12212 //错误写法

​    // var str:string = '12212'

//数组类型array类型  ts定义数组有两种方式

​    //第一种定义数组的方式

​    //es5定义数组

​    //var arr = ['1','2']

​    //1.第一种定义数组的方式

​    // var arr:number[] = [11,12,13];

​    // console.log(arr);

​    //2.第二种定义数组的方式

​        // var arr:Array<number> = [11,22,33]

​        // console.log(arr);

​    //3.第三种定数组的方式 

​    // var arr:any[] = [11,'ss',33]

​    //     console.log(arr);

//元组类型tuple类型  属于数组的一种 

//可以给数组每一个位置指定一个类型 

​    //   let arr:[number,string] = [123,'this is ts']

​    //   console.log(arr);

//枚举类型enum类型

​    // enum 枚举名{

​    //     标识符[=整性常数],

​    //     标识符[=整型常数],

​    //     。。。

​    //     标识符[=整型常数],

​    // }

​    

​    // enum Flag{

​    //     success = 1,error = 2

​    // }

​    // let s:Flag = Flag.success;

​    // console.log(s);

​    // let f:Flag = Flag.error;

​    // console.log(f);

​    // enum Color {blue,red,'orange'};

​    // var c:Color = Color.red;

​    // console.log(c); //1 如果表示符没有赋值  它的值就是下标

​    //  enum Color {blue,red=3,'orange'}; // 赋值 

​    //  var c:Color = Color.orange;

​    //  console.log(c); // 4

​    //用到最多表示状态码 

​    // enum Err {'undefined' = -1,'null' = -2,'success' = 1 };

​    // var e:Err = Err.success;

​    // console.log(e)

//任意类型any类型

​    // var  num:any = 123;

​    // num = 'str';

​    // num = true;

​    // console.log(num)

​    // var oBox:any = document.querySelector('#box')

​    // oBox.style.background = 'red';

//null 和 undefined 其他数据类型的子类型   子类型=(never类型)

​    // var num:number;

​    // console.log(num) // 输出undefined  报错 

​    // var num:undefined;

​    // console.log(num) // 输出undefined  正确

​    //定义没有赋值就是undefined

​    // var num:number | undefined

​    // console.log(num);

​    // var num:null;

​    // num = null;

​    //一个元素可能是number类型 可能是null 可能是undefined

​    // var num:number | null | undefined;

​    // num = 1234;

​    // console.log(num)

//void类型 typescript中的void表示没有任何类型,一般用于定义方法的时候方法没有返回值

​    //es5定义方法

​    // function run(){

​    //     console.log('run')

​    // }

​    // run()

​    //表示方法没有返回任何类型

​    // function run():void{

​    //     console.log('run')

​    // }

​    // run()

​    //错误写法

​    // function run():undefined{

​    //     console.log('run')

​    // }

​    // run()

​    //正确写法

​    // function run():number{

​    //     console.log('run')

​    //     return 123

​    // }

​    // run()

//never类型 是其他类型 (包括 null 和 undefined) 的子类型,代表从不会出现的值,这意味着

//声明never的变量只能被never类型所赋值

   

​    // var a:undefined;

​    // a = undefined;

​    // var b:null;

​    // b = null;

​    // var a:never;

​     //a=123 // 错误的写法

​    // a = (()=>{

​    //     throw new Error('错误');

​    // })()

## TypeScript函数

  //函数的定义

​    //es5

​    //函数声明法

​    // function run(){

​    //     return 'run';

​    // }

​    //匿名函数 

​    // var run2 = function(){

​    //     return 'run2';

​    // }

​    //ts中定义函数的方法 

​    //正确

​    // function run():string{

​    //     return 'run';

​    // }

​    //错误 

​    // function run():string{

​    //     return 123;

​    // }

​    //匿名函数 

​    // var fun2 = function():number{

​    //     return 123;

​    // }

​    // alert(fun2()) /*调用方法 */

​    //ts中定义方法传参 

​        //函数声明法

​        // function getInfo(name:string,age:number):string{

​        //     return `${name} --- ${age}`

​        // }

​        // alert(getInfo('lisi',20))

​        //匿名函数 

​        // var getInfo=function(name:string,age:number):string{

​        //     return `${name} --- ${age}`;

​        // }

​        // alert(getInfo('zhangsan',20));

​        //没有返回值的方法

​            // function run():void{

​            //     console.log('run')

​            // }

​            // run()

​        

​        //方法可选参数 

​        //es5里面方法的实参和形参可以不一样，但是ts中必须一样，

​        //如果不一样就需要配置可选参数

​        // function getInfo(name:string,age?:number):string{

​             

​        //     if(age){

​        //         return `${name} --- ${age}`

​        //     }

​        //     return `${name} --- 年龄保密`

​               

​        //     }

​        //     alert(getInfo('lisi'))

​        //     alert(getInfo('lisi',12))

​        //可选参数必须配置到参数的最后面 

​        

​        // function getInfo(age?:number,name:string):string{

​        //    错误写法

​        //     if(age){

​        //         return `${name} --- ${age}`

​        //     }

​        //     return `${name} --- 年龄保密`

​               

​        //     }

​        //     alert(getInfo('lisi'))

​        //     alert(getInfo('lisi',12))

​        //默认参数

​        //es5里面设置默认参数es6和ts中都可以设置默认参数

​        // function getInfo(name:string,age:number=20):string{

​        //     if(age){

​        //         return `${name} --- ${age}`

​        //     }

​        //     return `${name} --- 年龄保密`

​        // }

​        // alert(getInfo('张三')); // 张三 20

​        // function sum(a:number,b:number,c:number,d:number):number{

​        //     return a+b+c+d

​        // }

​        // alert(sum(1,2,3,4))

​        //拓展运算符

​        // function sum(a:number,...result:number[]):number{

​        //     var sum = 0;

​        //     for(var i=0;i<result.length;i++){

​        //         sum+=result[i]

​        //     }

​        //     return sum;

​        // }

​        // alert(sum(1,2,3,4,5,6));

​        //ts函数重载 

​        //java中方法的重载,重载指的是两个或者两个以上的同名函数，但他们的参数不一样，

​        //这时会出现函数重载的情况

​        //typescript中的重载,通过为同一个函数提供多个函数类型定义来试下多种功能的目的

​        //ts为了兼容es5 以及 es6 重载的写法和java有区别

​        //es5中出现同名方法,下面的会替换上面的方法

​        // function css(config){

​        // }

​        // function css(config,value){

​        // }

​        //ts中的重载 

​        // function getInfo(name:string):string;

​        // function getInfo(age:number):string;

​        // function getInfo(str:any):any{

​        //     if(typeof str === 'string'){

​        //         return '我叫' + str

​        //     }else{

​        //         return  '我的年龄是' + str

​        //     }

​        // }

​        // alert(getInfo('张三'))  都是正确的写法

​        // alert(getInfo(20))      都是正确的写法

​        // alert(getInfo(true)) // 错误写法

​        //多个参数的重载

​        // function getInfo(name:string):string;

​        // function getInfo(name:string,age:number):string;

​        // function getInfo(name:any,age?:any):any{

​        //     if(age){

​        //         return `我叫:${name}我的年龄是${age}`

​        //     }else{

​        //         return `我叫${name}`

​        //     }

​        // }

​        // alert(getInfo('zhangsan')) //正确

​        // alert(getInfo(123)) //错误

​        // alert(getInfo('zhangsan',20));

​        //箭头函数 es6

​        //this指向的问题  箭头函数里面的this指向上下文 

​        // setTimeout(()=>{

​        //     alert('ts')

​        // },1000)

## Es5上的类

  //1.最简单的类

​        // function Person(){

​        //     this.name = '张三';

​        //     this.age = 20

​        // }

​        // var p = new Person();

​        // alert(p.name)

​        //2.构造函数和原型链增加方法

​        // function Person(){

​        //         this.name = '张三';属性

​        //         this.age = 20;

​        //         this.run = function(){ 实例方法

​        //             alert(this.name + '在运动')

​        //         }

​        //     }

​        // Person.getInfo = function(){

​        //     alert('我是静态方法')

​        // }

​        //原型链上的属性会被多个实例共享  构造函数不会 

​        // Person.prototype.sex = '男';

​        // Person.prototype.work = function(){

​        //     alert(this.name + '在工作')

​        // }

​        //     var p = new Person();

​        //     alert(p.name)

​        //     p.run();

​        //     p.work()

​        //3.类里面的静态方法 

​        //调用静态方法

​        // Person.getInfo()

​        //4.es5里面的继承 

​        //Web类 继承Person类 原型链+对象冒充的组合继承模式 

​        // function Web(){

​        //     Person.call(this) //对象冒充实现继承 

​        // }

​        // var w = new Web();

​        // w.run(); //对象冒充可以继承构造函数里面的属性和方法

​        // w.work(); //对象冒充可以继承构造函数里面的属性和方法 但是没法继承原型链上的属性和方法

​        //原型链继承 

​        //可以继承构造函数里面的属性和方法 也可以继承原型链上的属性和方法

​        // Web.prototype = new Person()//原型链实现继承 

​        // var w = new Web();

​        // w.run();

​        // w.work();

​        //原型链继承问题 

​        //  function Person(){

​        //             this.name = '张三';//属性

​        //             this.age = 20;

​        //             this.run = function(){ //实例方法

​        //                 alert(this.name + '在运动')

​        //             }

​        //         }

​        // Person.prototype.sex = '男';

​        // Person.prototype.work = function(){

​        //     alert(this.name + '在工作')

​        // }

​        // function Web(name,age){

​        // }

​        // Web.prototype = new Person();

​        // var w = new Web('赵四',20); //实例化子类的时候没法给父类传参

​        // w.run();

​        // var w1 = new Web('王五',22) 

​        //对象冒充继承模式 

​        //  function Person(name,age){

​        //             this.name = name;//属性

​        //             this.age = age;

​        //             this.run = function(){ //实例方法

​        //                 alert(this.name + '在运动')

​        //             }

​        //         }

​        // Person.prototype.sex = '男';

​        // Person.prototype.work = function(){

​        //     alert(this.name + '在工作')

​        // }

​        // function Web(name,age){

​        //     Person.call(this,name,age)//对象冒充继承 实例化子类可以给父类传参

​        // }

​        // Web.prototype = new Person();

​        // var w = new Web('赵四',20); //实例化子类的时候没法给父类传参

​        // w.work();

​      

​        //原型链+对象冒充继承的另一种方法  可以继承构造函数里面的属性和方法

​        

​        // function Person(name,age){

​        //             this.name = name;//属性

​        //             this.age = age;

​        //             this.run = function(){ //实例方法

​        //                 alert(this.name + '在运动')

​        //             }

​        //         }

​        // Person.prototype.sex = '男';

​        // Person.prototype.work = function(){

​        //     alert(this.name + '在工作')

​        // }

​        // function Web(name,age){

​        //     Person.call(this,name,age)//对象冒充继承 实例化子类可以给父类传参

​        // }

​        // Web.prototype = Person.prototype;

​        // var w = new Web('赵四',20); //实例化子类的时候没法给父类传参

​        // w.work();

## Typescript上的类

​     //ts类

​        // class Person{

​        //         name:string //属性 前面省略了public关键字

​    

​        //         constructor(name:string){ //构造函数  实例化类的时候触发的方法

​        //             this.name = name;

​        //         }

​    

​        //         getName():string{

​        //             return this.name;

​        //         }

​        //         setName(name:string):void{

​        //             this.name = name;

​        //         }

​        //     }

​        //     var p = new Person('张三');

​        //     alert(p.getName())

​        //     p.setName('李四')

​        //     alert(p.getName())

​        //ts中实现继承 extends ，super

​        // class Person{

​        //     name:string

​        //     constructor(name:string){

​        //         this.name = name; 

​        //     }

​        //     run():string{

​        //         return `${this.name}在运动`

​        //     }

​        // }

​        // // var p = new Person('王五');

​        // // alert(p.run());

​        // class Web extends Person{

​        //     constructor(name:string){

​        //         super(name); //初始父类的构造函数 

​        //     }

​        // }

​        // var w = new Web('李四');

​        // alert(w.run());

​        //ts继承中父类和子类方法的探讨

​        // class Person{

​        //     name:string

​        //     constructor(name:string){

​        //         this.name = name; 

​        //     }

​        //     run():string{

​        //         return `${this.name}在运动`

​        //     }

​        // }

​        // var p = new Person('王五');

​        // alert(p.run());

​        // class Web extends Person{

​        //     constructor(name:string){

​        //         super(name); //初始父类的构造函数 

​        //     }

​        //     run():string{

​        //         return `${this.name}在运动子类`

​        //     }

​        //     work(){

​        //         alert(`${this.name}在工作`)

​        //     }

​        // }

​        // var w = new Web('李四');

​        // alert(w.run());

​        // w.work();

## 类里面的修饰符 

​        //类里面的修饰符 typescript里面定义属性的时候给我们提供了三种修饰符 

​        //public  公有   在类里面，子类，类外面都可以访问

​        //protected  保护类型    在类里面子类里面可以访问，在类外部没法访问

​        //private   私有    在类里面可以访问，子类，类外部都没法访问

​        //属性没有默认为 public

​        // public  公有   在类里面，子类，类外面都可以访问

​        //  class Person{

​        //         public name:string //公有属性

​    

​        //         constructor(name:string){

​        //             this.name = name; 

​        //         }

​        //         run():string{

​        //             return `${this.name}在运动`

​        //         }

​        //     }

​        //     var p = new Person('王五');

​        //     alert(p.run());

​    

​        //     class Web extends Person{

​        //         constructor(name:string){

​        //             super(name); //初始父类的构造函数 

​        //         }

​        //         run():string{

​        //             return `${this.name}在运动子类`

​        //         }

​        //         work(){

​        //             alert(`${this.name}在工作`)

​        //         }

​        //     }

​    

​        //     var w = new Web('李四');

​           

​        //     w.work();

​            

​        // 类外访问共有属性

​        // class Person{

​        //     public name:string //公有属性

​        //     constructor(name:string){

​        //         this.name = name; 

​        //     }

​        //     run():string{

​        //         return `${this.name}在运动`

​        //     }

​        // }

​        // var p = new Person('王五');

​        // alert(p.name)

​        //protected  保护类型    在类里面子类里面可以访问，在类外部没法访问

​        // class Person{

​        //             protected name:string //保护属性

​        

​        //             constructor(name:string){

​        //                 this.name = name; 

​        //             }

​        //             run():string{

​        //                 return `${this.name}在运动`

​        //             }

​        //         }

​        //         class Web extends Person{

​        //             constructor(name:string){

​        //                 super(name); //初始父类的构造函数 

​        //             }

​        //             work(){

​        //                 alert(`${this.name}在工作`)

​        //             }

​        //         }

​        

​        //         var w = new Web('李四11');

​               

​        //         w.work();

​        //         alert(w.run());

​         // 类外访问共有属性

​        //类外部没法访问保护类型属性

​        // class Person{

​        //     protected name:string //保护属性

​        //     constructor(name:string){

​        //         this.name = name; 

​        //     }

​        //     run():string{

​        //         return `${this.name}在运动`

​        //     }

​        // }

​        // var p = new Person('王五');

​        // alert(p.name)  //报错 

​                

​        //private   私有    在类里面可以访问，子类，类外部都没法访问

​        // class Person{

​        //             private name:string //私有属性

​        

​        //             constructor(name:string){

​        //                 this.name = name; 

​        //             }

​        //             run():string{

​        //                 return `${this.name}在运动`

​        //             }

​        //         }

​        //         class Web extends Person{

​        //             constructor(name:string){

​        //                 super(name); //初始父类的构造函数 

​        //             }

​        //             work(){

​        //                 alert(`${this.name}在工作`)

​        //             }

​        //         }

​        

​        //         var w = new Web('李四11');

​               

​        //         w.work();

​        //         alert(w.run());

​         // 类外访问共有属性

​        //类外部没法访问私有类型属性

​        // class Person{

​        //     private name:string //私有属性

​        //     constructor(name:string){

​        //         this.name = name; 

​        //     }

​        //     run():string{

​        //         return `${this.name}在运动`

​        //     }

​        // }

​        // var p = new Person('王五');

​        // alert(p.name)  //报错     

​        //当前类可以访问

## 静态属性静态属性，方法

 //静态属性  静态方法

​        //es5

​        // function Person(){

​        //     this.run1 = function(){

​        //     }

​        // }

​        // Person.name = "hahha"

​        // Person.run2 = function(){ //静态方法

​        // }

​        // var p = new Person();

​        // Person.run2() //静态方法的调用 

​        // class Person{

​        //     public name:string

​        //     //静态属性

​        //     static age:number = 20

​        //     constructor(name:string){

​        //         this.name = name 

​        //     }

​        //     run(){

​        //         alert(`${this.name}在运动`)

​        //     }

​        //     work(){

​        //         alert(`${this.name}在工作`)

​        //     }

​        //     static print(){  //静态方法 里面没法直接调用类里面的属性

​        //         alert('print方法'+Person.age)

​        //     }

​        // }

​        // var p = new Person('张三');

​        // p.run();

​        // Person.print()

## 多态

class Animal{

​        //     name:string

​        //     constructor(name:string){

​        //         this.name = name;

​        //     }

​        //     eat(){ //具体吃什么 不知道 具体吃什么继承他的子类去实现，每一个子类的表现不一样

​        //         console.log('吃的方法')

​        //     }

​        // }

​        // class Dog extends Animal{

​        //     constructor(name:string){

​        //         super(name)

​        //     }

​        //     eat(){

​        //         return this.name+'吃肉'

​        //     }

​        // }

​        // class Cat extends Animal{

​        //     constructor(name:string){

​        //         super(name)

​        //     }

​        //     eat(){

​        //         return this.name+'吃鱼'

​        //     }

​        // }

## 抽象类

 //typescript中的抽象类,他是提供其他继承的基类，不能直接实例化

​        //用abstract关键字定义抽象类和抽象方法，抽象类中的抽象方法不包含具体实现并且必须在派生类中实现

​        //abstract抽象方法只能放在抽象类里面

​        //抽象类和抽象方法用来定义标准

​        //抽象类和抽象方法用来定义标准,标准Animal 这个类要求子类必须包含eat方法

​        //标准 

​        //其他方法可以不实现

​        // abstract class Animal{

​        //     public name:string;

​        //     constructor(name:string){

​        //         this.name = name;

​        //     }

​        //     abstract eat():any;

​        // }

​        // var a = new Animal() //错误的写法

​        // class Dog extends Animal{

​             //抽象类的子类必须实现抽象类里面的抽象方法

​        //     constructor(name:any) {

​        //         super(name)

​        //     }

​        //     eat(){

​        //         console.log(this.name+'吃粮食')

​        //     }

​        // }

​        // var d = new Dog('小黑')

​        // d.eat();

## 接口

//ts中的接口 

//接口的作用,在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范，在程序设计里面，

//接口起到一种限制和规范的作用。接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部状态数据，

//也不关心这些类里方法的实现细节，他只规定这批类里必须提供某些方法，提供这些方法的类就可以满足实际需要。

//typescript中的接口类似于java，同时还增加了更灵活的接口类型，包括属性，函数，可索引和类等

//定义标准

// 属性类接口

// 函数类型接口

// 可索引接口

// 类类型接口

// 接口扩展

//属性接口    

//ts中自定义方法传入参数 对json的约束

// function printLabel(labelInfo:{label:string}):void{

//     console.log('print')

// }

// printLabel('hahha'); //错误写法

// printLabel({name:"张三"}) //错误的写法

// printLabel({label:'张三'}) //正确的写法

//接口 对批量方法传入参数进行约束

// interface FullName{

//     firstName:string; // 注意;结束 

//     secondName:string;

// }

// function printName(name:FullName){

​     //必须传入对象  firstName  secondName

//     console.log(name.firstName+ '----' + name.secondName)

// }

// printName('1112')//错误

// var obj = {

//     age:20,

//     firstName:'张',

//     secondName: '三'

// }

// printName(obj)

//接口：行为和动作的规范，对批量方法进行约束 

// interface FullName{

//         firstName:string; // 注意;结束 

//         secondName:string;

//     }

​    

//     function printName(name:FullName){

//         //  必须传入对象  firstName  secondName

//         console.log(name.firstName+ '----' + name.secondName)

//     }

​    

//     function printInfo(info:FullName){

//         // 必须传入对象  firstName  secondName

//        console.log(info.firstName+ '----' + info.secondName)

//    }

//     //值要严格跟接口对应

//     var obj = {

//         age:20,

//         firstName:'张',

//         secondName: '三'

//     }

//     printName(obj)

//     var info = {

//         age:20,

//         firstName:'李',

//         secondName: '四'

//     }

//     printInfo(info)

//接口  可选属性

​    // interface FullName{

​    //     firstName:string;

​    //     secondName?:string;

​    // }

​    // function getName(name:FullName){

​    //     console.log(name)

​    // }

​    // //参数的顺序可以不一样

​    // getName({

​       

​    //     firstName: 'one'

​    // })

##    原生js封装ajax例子 

​    // $.ajax({

​    //     type: "GET",

​    //     url: "test.json",

​    //     data: {username:$("#username").val(),content:$("#content").val()},

​    //     dataType:"json"

​    // })

​    //属性类型接口简单例子

​    // interface Config{

​    //     type: string;

​    //     url: string;

​    //     data ?:string;

​    //     dataType:string;

​    // }

​    // function ajax(config:Config){

​    //     var xhr = new XMLHttpRequest();

​    //     xhr.open(config.type,config.url,true);

​    //     xhr.send(config.data);

​    //     xhr.onreadystatechange = function(){

​    //         if(xhr.readyState == 4 && xhr.status == 200){

​    //             console.log('chenggong')

​    //             if(config.dataType == 'json'){

​    //                 console.log(JSON.parse(xhr.responseText)) 

​    //             }else{

​    //                 console.log(xhr.responseText)

​    //             }

​    //         }

​    //     }

​    // }

​    // ajax({

​    //     type:'get',

​    //     data:"name=zhangsan",

​    //     url:"http://a.itying.com/api/productlist",

​    //     dataType:"json"

​    // })



## 函数类型接口 对方法传入的参数 以及返回值进行约束  批量约束

​    //加密的函数类型接口 

​    // interface encrypt{

​    //     (ket:string,value:string):string

​    // }

​    // var md5:encrypt=function(key:string,value:string):string{

​    //     //模拟操作      接口是这样函数必须是这样

​    //     return key+value;

​    // }

​    // console.log(md5('name','zhangsan')) 

## 可索引接口类类型接口

//可索引接口,数组的约束 对象的约束(不常用)

​    //ts定义数组 

​    // var arr:number[] = [2,1551]

​    // var arr:Array<number> = [1111]

​    //可索引接口对数组的约束 

​    // interface UserArr{

​    //     [index:number]:string

​    // }

​    // var arr:UserArr = ['aaa','bbb'];

​    // console.log(arr[0]);

​    //可索引接口对对象的约束 

​    // interface UserObj{

​    //     [index:string]:string

​    // }

​    // var arr:UserObj = {name:"张三"}



 //类类型接口 对类的约束 和 抽象类抽象方法有点类似 

​    

​    interface Animal{

​        name:string;

​        eat(str:string):void;

​    }

​    class Dog implements Animal{

​        name:string;

​        constructor(name:string){

​            this.name = name;

​        }

​        eat(){

​            console.log(this.name+'吃粮食')

​        }

​    }

​    

​    var d = new Dog('小黑')

​    d.eat();

​    class Cat implements Animal{

​        name:string;

​        constructor(name:string){

​            this.name = name;

​        }

​        eat(){

​            console.log(this.name+'吃老鼠')

​        }

​    }

​    var c = new Cat('笑话')

​    c.eat();

## Typescript接口的扩展接口的继承

 //接口的扩展，接口的继承 

​    interface Animal{

​        eat():void;

​    }

​    interface Person extends Animal{

​        work():void;

​    }

​    class Programmer{

​        public name:string;

​        constructor(name:string){

​            this.name = name;

​        }

​        coding(code:string){

​            console.log(this.name+code)

​        }

​    }

​    class Web extends Programmer implements Person{

​        // public name:string;

​        constructor(name:string){

​            super(name)

​            this.name = name

​        }

   

​    eat(){

​        console.log(this.name+'喜欢吃馒头')

​    }

​    work(){

​        console.log(this.name+'写代码')

​    }

}

​    var w = new Web('小李');

​    w.eat();

​    w.coding('写ts代码')

## TS中的泛型

//Typescript中的泛型

//通俗理解就是解决类 接口 方法的复用性,以及对不特定数据类型的支持

//只能返回 string类型的数据 

// function getData(value:string):string{

   

//     return value;

// }

//同时返回string类型和number类型 代码冗余

// function getData(value:string):string{

   

//     return value;

// }

// function getData1(value:number):number{

   

//     return value;

// }

//同时返回 string类型和number类型 any可以解决这个问题  但是放弃了对类型的控制 

​    // function getData(value:any):any{

​    //     return '哈哈哈'

​    // }

​    // getData(123);

​    // getData('str');

​    //any放弃了类型检查,传入什么 返回什么 比如 传入number类型必须返回number类型 传入string

​    //类型必须返回string类型

​    //传入的类型可以和返回的类型不一致 

​    //泛型可以支持不特定的数据类型  ， 要求传入的参数和返回的参数一致 

​    //T表示泛型,具体是什么是调用这个方法决定的 

​        // function getData<T>(value:T):T{

​        //     return value;

​        // }

​        // getData<number>(123);

​        

​        // getData<string>('2112');  

​        // getData<number>('2112'); //错误的写法

​        

​        // function getData<T>(value:T):any{

​        //         return value;

​        //     }

​    

​        //     getData<number>(123); //参数必须是number

​            

​        //     getData<string>('这是一个泛型');  

​    

​        //泛型类 比如有个最小对算法,需要同时支持返回数组和字符串两种类型、通过类的泛型来实现 

​        // class MinClass{

​        //     public list:number[] = [] ;

​        //     add(num:number){

​        //         this.list.push(num)

​        //     }

​        //     min():number{

​        //         var minNum = this.list[0];

​        //         for(var i=0;i<this.list.length;i++){

​        //             if(minNum>this.list[i]){

​        //                 minNum = this.list[i];

​        //             }

​        //         }

​        //         return minNum;

​        //     }

​        // }

​        // var m = new MinClass();

​        // m.add(2);

​        // m.add(5);

​        // m.add(33);

​        // m.add(6);

​        // m.add(88);

​        // alert(m.min())

​        // 类的泛型

​        // class MinClass<T>{

​        //     public list:T[] = [] ;

​        //     add(num:T){

​        //         this.list.push(num)

​        //     }

​        //     min():T{

​        //         var minNum = this.list[0];

​        //         for(var i=0;i<this.list.length;i++){

​        //             if(minNum>this.list[i]){

​        //                 minNum = this.list[i];

​        //             }

​        //         }

​        //         return minNum;

​        //     }

​        // }

​        // var m = new MinClass<number>(); //实例化类并且指定了类的T代表的类型是number

​        // m.add(2);

​        // m.add(5);

​        // m.add(33);

​        // m.add(6);

​        // m.add(88);

​        // alert(m.min())

## TS泛型接口泛型类接口

 //typescript中的泛型

​        //普通函数接口

​        // interface ConfigFn{

​        //     (value:string,value2:string):string;

​        // }

​        // var setData:ConfigFn = function(value:string,value2:string):string{

​        //     return value+value2;

​        // }

​        // setData('name','张三')

​        //1.泛型接口

​        

​        // interface ConfigFn{

​        //         <T>(value:T):T

​        // }

​        // var getData:ConfigFn = function<T>(value:T):T{

​        //     return value;

​        // }

​        // getData<string>('张三')

​        // getData<string>(1234) ///错误

​         //2.泛型接口

​        

​    //     interface ConfigFn<T>{

​    //            (value:T):T

​    //     }

​    //    function getData<T>(value:T):T{

​    //             return value;

​    //     }

​    //     var myGetData:ConfigFn<string>=getData;

​    //     myGetData('20') //正确

​        // myGetData(20) //错误

## 泛型类

// 泛型类：泛型可以帮助我们避免重复的代码以及对不特定的数局类型的支持(类型校验),下面我们看看把类当作参数的泛型类

​    //定义个类

​    //把类作为参数来约束数据传入的类型

​    //定义一个User的类这个类的作用就是映射数据库字段，然后定义一个MysqlDb的类用于操作数据库

​    //然后把User类作为参数传入到MysqlDb中

   //  // var user = new user({

   //  //     username : '张三',

   //  //     password:'123456'

   //  // }) 

  //   // var Db = new MysqlDb();

  //   // Db.add(user);

​    //把类作为参数来约束数据传入的类型

​    // class User{

​    //     username:string | undefined;

​    //     password : string | undefined;

​    // }

​    // class MysqlDb{

​    //     add(user:User):boolean{

​    //         console.log(user)

​    //         return true;

​    //     }

​    // }

​    // var u = new User();

​    // u.username = '张三';

​    // u.password = '123456';

​    // var Db = new MysqlDb();

​    // Db.add(u)

​    // class ArticleCate{

​    //         title:string | undefined;

​    //         desc : string | undefined;

​    //         status:number | undefined;

​    //     }

​    

​    //     class MysqlDb{

​    //         add(info:ArticleCate):boolean{

​    //             console.log(info)

​    //             return true;

​    //         }

​    //     }

​    

​    //     var a = new ArticleCate();

​    //     a.title = '国内';

​    //     a.desc = '国内新闻';

​    //     a.status = 1

​    //     var Db = new MysqlDb();

​    //     Db.add(a)

   //定义操作数据库的泛型类

class MysqlDb<T>{

​    add(info:T):boolean{

​        console.log(info);       

​        return true;

​    }

​    updated(info:T,id:number):boolean {

​        console.log(info);  

​        

​        console.log(id); 

​        return true;

​    }

}

//想给User表增加数据

// 1、定义一个User类 和数据库进行映射

// class User{

//     username:string | undefined;

//     pasword:string | undefined;

// }

// var u=new User();

// u.username='张三';

// u.pasword='123456';

// var Db=new MysqlDb<User>();

// Db.add(u);

//2、相关ArticleCate增加数据  定义一个ArticleCate类 和数据库进行映射

class ArticleCate{

​    title:string | undefined;

​    desc:string | undefined;

​    status:number | undefined;

​    constructor(params:{

​        title:string | undefined,

​        desc:string | undefined,

​        status?:number | undefined

​    }){

​        this.title=params.title;

​        this.desc=params.desc;

​        this.status=params.status;

​    }

}

//增加操作

// var a=new ArticleCate({

//     title:'分类',

//     desc:'1111',

//     status:1

// });

// //类当做参数的泛型类

// var Db=new MysqlDb<ArticleCate>();

// Db.add(a);

//修改数据

var a=new ArticleCate({

​        title:'分类111',

​        desc:'2222'      

});

a.status=0;

var Db=new MysqlDb<ArticleCate>();

Db.updated(a,12);



## 类接口什么的综合使用

// interface DBI<T>{

//     add(info:T):boolean;

//     update(info:T,id:number):boolean;

//     delete(id:number):boolean;

//     get(id:number):any[];

// }

// //定义一个操作mysql数据库的类    注意：要实现泛型接口，这个类也应该是一个泛型类

// class MysqlDb<T> implements DBI<T>{

//     constructor(){

//         console.log('数据库建立链接')

//     }

//     add(info: T): boolean {

//         console.log(info)

//        return true

//     }    

//     update(info: T, id: number): boolean {

//         throw new Error("Method not implemented.");

//     }

//     delete(id: number): boolean {

//         throw new Error("Method not implemented.");

//     }

//     get(id: number): any[] {

//         var list = [

//             {

//                 title:'xxx',

//                 desc:'xxxx'

//             },

//             {

//                 title:'xxx',

//                 desc:'xxxxxxxxx'

//             },

//         ]

//         return list;

//     }

​    

// }

// //定义一个操作mssql数据库的类

// class MsSqlDb<T> implements DBI<T>{

//     add(info: T): boolean {

//        console.log(info)

//        return true

//     }   

//     update(info: any, id: number): boolean {

//         throw new Error("Method not implemened.");

//     }

//     delete(id: number): boolean {

//         throw new Error("Method not implemented.");

//     }

//     get(id: number): any[] {

//         var list = [

//             {

//                 title:'xxx',

//                 desc:'xxxx'

//             },

//             {

//                 title:'xxx',

//                 desc:'xxxxxxxxx'

//             },

//         ]

//         return list;

//     }

​    

// }

// //操作用户表  定于一个User类和数据库表映射

// //定义数据

// // class User{

// //     username: string | undefined

// //     password: string | undefined

// // }

// // var u = new User();

// // u.username = '张三111';

// // u.password = '123456';

// // var lala = new MysqlDb<User>()

// // lala.add(u);

// class Work{

//     username: string | undefined

//     password: string | undefined

// }

// var y = new Work()

// y.username = '无心';

// y.password = '123456';

// var lala = new MsSqlDb<Work>()

// lala.add(y)

// var data = lala.get(4);

// console.log(data);

## 模块 

/*
命名空间:

    在代码量较大的情况下，为了避免各种变量命名相冲突，可将相似功能的函数、类、接口等放置到命名空间内
    
    同Java的包、.Net的命名空间一样，TypeScript的命名空间可以将代码包裹起来，只对外暴露需要在外部访问的对象。命名空间内的对象通过export关键字对外暴露。


命名空间和模块的区别：

    命名空间：内部模块，主要用于组织代码，避免命名冲突。
    
    模    块：ts的外部模块的简称，侧重代码的复用，一个模块里可能会有多个命名空间。

*/

## 命名空间

import { A, B } from './modules/db'

var d =new A.Dog('小黑');

d.eat();

```js
export namespace A{
    interface Animal {
        name: string;
        eat(): void;
    }
    export class Dog implements Animal {
        name: string;
        constructor(theName: string) {
            this.name = theName;
        }

        eat() {
            console.log(`${this.name} 在吃狗粮。`);
        }
    }
}

```

## 装饰器

装饰器：装饰器是一种特殊类型的声明，它能够被附加到类声明，方法，属性或参数上，可以修改类的行为。

通俗的讲装饰器就是一个方法，可以注入到类，方法，属性参数上来扩展类，属性，方法，参数的功能

常见的装饰器有：类装饰器，属性装饰器，方法装饰器，参数装饰器

装饰器的写法：普通装饰器（无法传参），装饰器工厂（可传参）

装饰器是过去几年中js最大的成就之一，已是Es7的标准特性之一



1.类装饰器：类装饰器在类声明之前被声明（紧靠着类声明）。类装饰器应用于类构造函数，可以用来监视，修改或替换类定义。存入一个参数 



1.类装饰器

```js
配置之后使用命令 不好使 直接 tsc
命令行:

tsc --target ES5 --experimentalDecorators
tsconfig.json:

{
    "compilerOptions": {
        "target": "ES5",
        "experimentalDecorators": true
    }
}
```

类装饰器

​	下面是一个重载构造函数的例子

​	 类装饰器表达式会在运行时当作函数被调用，类的构造函数作为其唯一的参数

​	 如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明 

//类装饰器 扩展当前类的属性或者方法    普通装饰器

// function logClass(params:any){

//     console.log(params);

   //params 就是当前类

//     params.prototype.apiUrl = '动态扩展的属性'

//     params.prototype.run = function(){

//         console.log('我是一个run方法')

//     }

// }

// @logClass

// class HttpClient{

//     constructor(){

//     }

//     getData(){ 

//     }

// }

// var http:any = new HttpClient()

// console.log(http.apiUrl)

// http.run()

//类装饰器 装饰器工厂（可传参）

// function logClass(params:string){

//     return function(target:any){

//         console.log(target); // 函数本身 

//         console.log(params); // hello

//         target.prototype.apiUrl = params;

//     }

// }

// @logClass('http://www.baidu.com')

// class HttpClient{

//     constructor(){

//     }

//     getData(){

//     }

// }

// var http:any = new HttpClient()

// console.log(http.apiUrl)

// 类装饰器

//     下面是一个重载构造函数的例子

//      类装饰器表达式会在运行时当作函数被调用，类的构造函数作为其唯一的参数

//      如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明 

// function logClass(target:any){

//     console.log(target);

//     return class extends target{

//         apiUrl:any='我是修改后的数据'

//         getData(){

//             this.apiUrl = this.apiUrl + '-----';

//             console.log(this.apiUrl);

//         }

//     }

// }

// @logClass

// class HttpClient{

//     public apiUrl:string | undefined;

//     constructor(){

//         this.apiUrl = '我是构造函数里面的apiUrl';

//     }

//     getData(){

//         console.log(this.apiUrl);

//     }

// }

// var http = new HttpClient();

// http.getData();

2.属性装饰器 

​	属性装饰器表达式会在运行时当作函数被调用，传入下列两个参数；

​	1.对于静态成员来说是类的构造函数，对于实例成员是类的原型对象

​	2.成员的名字 

//类装饰器

//  function logClass(params:string){

//         return function(target:any){

​            // console.log(target); // 函数本身 

​            // console.log(params); // hello

​    //     }

​    // }

//属性装饰器 

​    // function logProperty(params:any){

​    //     return function(target:any,attr:any){

​    //         console.log(target);

​    //         console.log(attr); // 属性名称 

​    //         target[attr] = params

​    //     }

​    // }    

​    // @logClass('xxx')

​    // class HttpClient{

​    //     @logProperty('http://www.baidu.com')

​    //     public url:any|undefined

​    //     constructor(){

​    

​    //     }

​    //     getData(){

​    //         console.log(this.url)

​    //     }

​    // }

​    // var http = new HttpClient();

​    // http.getData();

方法装饰器

​	它会被应用到方法的属性描述符上可以用来监视，修改或者替换方法定义

​	方法装饰会在运行时传入下列3个参数 

​		1.对于静态成员来说是类的构造函数，对于实例成员是类的原型对象

​		2.成员的名字

​		3.成员的属性描述符 

