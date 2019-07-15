以下题目请使用TypeScript编写代码，不得使用noImplicitAny选项

1. 找出数组 arr: number[] 中重复出现过的元素 

**输入例子:**`duplicates([1, 2, 4, 4, 3, 3, 1, 5, 3]).sort()`
**输出例子:**`[1, 3, 4]`

2. 获取数字 num 二进制形式第 bit 位的值。注意：bit 从 1 开始；返回 0 或 1；举例：2 的二进制为 10，第 1 位为 0，第 2 位为 1 

**输入例子:**`valueAtBit(128, 8)`
**输出例子:**`1`

3. 将给定字符串的每一个字符都转换%XX形式(类似于urlencode，但不仅仅转换特殊字符)。 

**输入例子:**`encode('abc xyz')`
**输出例子:**`%61%62%63%20%78%79%7a`

4. 找出对象 obj 不在原型链上的属性(注意这题测试例子的冒号后面也有一个空格~)

- 返回数组，格式为 key: value，结果数组不要求顺序 

  输入例子:

  ```javascript
  var C = function() {
    this.foo = 'bar';
    this.baz = 'bim';
  };
  C.prototype.bop = 'bip';
  iterate(new C());
  ```

  输出例子:

  `["foo: bar", "baz: bim"]`


5. (Node.js) 读取文件input.txt，将文件中的行排序后输出到output.txt
6. 获取Moment.js库，配置相应的d.ts声明，编写代码将当前时间的下一周周一的凌晨3点一刻输出到console
7. 按以下要求编写代码：
* 编写一个Stack类，参考任意数据结构书上的相应抽象数据类型(ADT)，要求实现为泛型，底层可使用Array
* 编写一个成员方法修饰器(Decorator)，使用该修饰器的成员函数，被调用时输出函数名字、使用的参数和开始时间，调用结束后输出函数返回值、结束时间和总耗费时间。
* 前面的Stack类中增加一个multiPop(num)函数，从Stack中一次移出num个成员，并将移出的成员以数组形式返回
* 使用前面的decorrator修饰前面的multiPop函数，向一个Stack中push从1到10万共10万个数字，然后multiPop10个数字，再multiPop100个数字
* 
