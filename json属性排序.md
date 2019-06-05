# [js中json对象数组按对象属性排序（sort方法）---2（根据拼音排序汉字和排序英文）](https://www.cnblogs.com/taohuaya/p/10049341.html)





> **目录**
>
> [localeCompare() 方法](https://www.cnblogs.com/taohuaya/p/10049341.html#localecompare-方法)
> [  定义和用法](https://www.cnblogs.com/taohuaya/p/10049341.html#定义和用法)
> [  语法](https://www.cnblogs.com/taohuaya/p/10049341.html#语法)
> [  返回值](https://www.cnblogs.com/taohuaya/p/10049341.html#返回值)
> [  说明](https://www.cnblogs.com/taohuaya/p/10049341.html#说明)

本例主要实现 中文汉字按拼音排序的方法和英文按照首字母排序的方法。

 

要排序的数据：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//要排序的数据
let data = [
        {chinese: '蔡司', english: 'Chase'},
        {chinese: '艾伦', english: 'Allen'},    
        {chinese: '左拉', english: 'Zola'},
        {chinese: '贝克', english: 'Baker'},    
        {chinese: '伯格', english: 'Berg'},    
        {chinese: '菲奇', english: 'Fitch'},    
        {chinese: '迪安', english: 'Dean'},    
        {chinese: '厄尔', english: 'Earle'},        
        {chinese: '亨利', english: 'Henry'},
        
    ]
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

根据汉字拼音排序

这里要用到一个字符串方法：

# localeCompare() 方法

## 定义和用法

用本地特定的顺序来比较两个字符串。

### 语法

```
stringObject.localeCompare(target)
```

| 参数   | 描述                                                 |
| ------ | ---------------------------------------------------- |
| target | 要以本地特定的顺序与 stringObject 进行比较的字符串。 |

### 返回值

说明比较结果的数字。如果 stringObject 小于 target，则 localeCompare() 返回小于 0 的数。如果 stringObject 大于 target，则该方法返回大于 0 的数。如果两个字符串相等，或根据本地排序规则没有区别，该方法返回 0。

### 说明

把 < 和 > 运算符应用到字符串时，它们只用字符的 Unicode 编码比较字符串，而不考虑当地的排序规则。以这种方法生成的顺序不一定是正确的。例如，在西班牙语中，其中字符 “ch” 通常作为出现在字母 “c” 和 “d” 之间的字符来排序。

localeCompare() 方法提供的比较字符串的方法，考虑了默认的本地排序规则。ECMAscript 标准并没有规定如何进行本地特定的比较操作，它只规定该函数采用底层操作系统提供的排序规则。

 

可是排序：

 

从z~a

```
    //根据汉字首字母排序
    //使用箭头函数
    //【注】localeCompare() 是js内置方法
     data.sort((a, b)=> b.chinese.localeCompare(a.chinese, 'zh')); //z~a 排序
```

从a~z

```
     data.sort((a, b)=> a.chinese.localeCompare(b.chinese, 'zh')); //a~z 排序    
```

根据英文首字母的ASCLL码进行排序

从z~a

```
    //根据英文排序 比较 首字母ASCLL码
    //使用箭头函数
    data.sort((a, b) => b.english.charCodeAt(0) - a.english.charCodeAt(0)); //z~a 排序
```

 

从a~z

```
    data.sort((a, b) => a.english.charCodeAt(0) - b.english.charCodeAt(0)); //a~z 排序    
```

 

完整演示代码：



[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//要排序的数据
let data = [
        {chinese: '蔡司', english: 'Chase'},
        {chinese: '艾伦', english: 'Allen'},    
        {chinese: '左拉', english: 'Zola'},
        {chinese: '贝克', english: 'Baker'},    
        {chinese: '伯格', english: 'Berg'},    
        {chinese: '菲奇', english: 'Fitch'},    
        {chinese: '迪安', english: 'Dean'},    
        {chinese: '厄尔', english: 'Earle'},        
        {chinese: '亨利', english: 'Henry'},
        
    ]

    //根据汉字首字母排序
    //使用箭头函数
    //【注】localeCompare() 是js内置方法
    // data.sort((a, b)=> b.chinese.localeCompare(a.chinese, 'zh')); //z~a 排序
    // data.sort((a, b)=> a.chinese.localeCompare(b.chinese, 'zh')); //a~z 排序    
    // console.log(data);

    //根据英文排序 比较 首字母ASCLL码
    //// console.log(data[0].english.charCodeAt(0));
    // data.sort((a, b) => b.english.charCodeAt(0) - a.english.charCodeAt(0)); //z~a 排序
    data.sort((a, b) => a.english.charCodeAt(0) - b.english.charCodeAt(0)); //a~z 排序    

    console.log(data);
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

控制台输出效果（英文从a~z的效果）：

![img](https://img2018.cnblogs.com/blog/1249006/201812/1249006-20181201142302985-1951266132.png)