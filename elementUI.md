# Vue ElementUI 如何修改消息提示框样式

![96](https://upload.jianshu.io/users/upload_avatars/14961787/5d6d5dad-e260-4435-89fe-e2d3b26e0770?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96)

 

[陌上花開丶](https://www.jianshu.com/u/76822f40192d)

 

关注

 0.5 2019.04.18 14:59* 字数 119 阅读 610评论 0喜欢 1

## 一、前言

在窄屏模式下（移动端），提示框的宽度太宽，希望降低宽度。
**应当如何修改 ElementUI 的样式呢**？

## 二、情景还原

```
// 弹出注销提示框
this.$confirm('确认注销吗?', '提示', {
}).then(() => {
  this.$message({
    message: '已成功注销',
    type: 'success'
  })
}).catch(() => { /* 用户取消注销 */ })
...
<style scoped>
  ...
  .message-logout {
    width: 350px;
  }
</style>
// 弹出注销提示框
this.$confirm('确认注销吗?', '提示', {
}).then(() => {
  this.$message({
    message: '已成功注销',
    type: 'success'
  })
}).catch(() => { /* 用户取消注销 */ })
...
<style scoped>
  ...
  .el-message-box {
    width: 350px;
  }
</style>
```





![img](https://upload-images.jianshu.io/upload_images/14961787-435b7c5e48c3d77e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/826/format/webp)

image.png

此时在scoped的style中写是无效的，因为ElementUI组件不可以给样式添加scoped，因此必须去掉scoped；但是去掉scoped后不满足单组件的CSS。



## 三、解决方案

#### 1、附加在没有scoped的style中

```
<style scoped>
  ...
</style>
<style>
  ...
  .el-message-box {
    width: 350px;
  }
</style>
```



![img](https://upload-images.jianshu.io/upload_images/14961787-4d67a52f87e4ab4b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/827/format/webp)

image.png

#### 2、给消息提示框加类名（荐）

更加推荐为这个messageBox添加一个类名，比较科学并且不会影响到其他。



![img](https://upload-images.jianshu.io/upload_images/14961787-9876367255faea70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/887/format/webp)

组件 | Element

```
// 弹出注销提示框
this.$confirm('确认注销吗?', '提示', {
  customClass: 'message-logout'
}).then(() => {
  this.$message({
    message: '已成功注销',
    type: 'success'
  })
}).catch(() => { /* 用户取消注销 */ })
...
<style scoped>
  ...
</style>
<style>
  ...
  .message-logout {
    width: 350px;
  }
</style>
```



![img](https://upload-images.jianshu.io/upload_images/14961787-e5dcde1469357124.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/829/format/webp)

image.png

