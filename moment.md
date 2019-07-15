# 使用moment.js轻松管理日期和时间

2018年05月22日 10:36:47 [风灵使](https://me.csdn.net/WuLex) 阅读数：14333



\##格式化日期
当前时间：

```
moment().format('YYYY-MM-DD HH:mm:ss'); //2014-09-24 23:36:09 
1
```

今天是星期几：

```
moment().format('d'); //3 
1
```

转换当前时间的Unix时间戳：

```
moment().format('X'); 
1
```

\##相对时间

20120901相对当前日期是2年前

```
moment("20120901", "YYYYMMDD").fromNow(); //2 years ago      
1
```

7天前的日期：

```
moment().subtract('days',7).format('YYYY年MM月DD日'); //2014年10月01日
1
```

7天后的日期：

```
moment().add('days',7).format('YYYY年MM月DD日'); //2014年10月01日
1
```

9小时前的时间：

```
moment().subtract('hours',9).format('HH:mm:ss'); 
1
```

9小时后的时间：

```
moment().add('hours',9).format('HH:mm:ss'); 
1
```

`moment.js`提供了丰富的说明文档，使用它还可以创建日历项目等复杂的日期时间应用。我们日常开发中最常用的是格式化时间，下面我把常用的格式制作成表格说明供有需要的朋友查看

| 格式代码 | 说明                       | 返回值例子                 |
| -------- | -------------------------- | -------------------------- |
| M        | 数字表示的月份，没有前导零 | 1到12                      |
| MM       | 数字表示的月份，有前导零   | 01到12                     |
| MMM      | 三个字母缩写表示的月份     | Jan到Dec                   |
| MMMM     | 月份，完整的文本格式       | January到December          |
| Q        | 季度                       | 1到4                       |
| D        | 月份中的第几天，没有前导零 | 1到31                      |
| DD       | 月份中的第几天，有前导零   | 01到31                     |
| d        | 星期中的第几天，数字表示   | 0到6，0表示周日，6表示周六 |
| ddd      | 三个字母表示星期中的第几天 | Sun到Sat                   |
| dddd     | 星期几，完整的星期文本     | 从Sunday到Saturday         |
| w        | 年份中的第几周             | 如42：表示第42周           |
| YYYY     | 四位数字完整表示的年份     | 如：2014 或 2000           |
| YY       | 两位数字表示的年份         | 如：14 或 98               |
| A        | 大写的AM PM                | AM PM                      |
| a        | 小写的am pm                | am pm                      |
| HH       | 小时，24小时制，有前导零   | 00到23                     |
| H        | 小时，24小时制，无前导零   | 0到23                      |
| hh       | 小时，12小时制，有前导零   | 00到12                     |
| h        | 小时，12小时制，无前导零   | 0到12                      |
| m        | 没有前导零的分钟数         | 0到59                      |
| mm       | 有前导零的分钟数           | 00到59                     |
| s        | 没有前导零的秒数           | 1到59                      |
| ss       | 有前导零的描述             | 01到59                     |
| X        | Unix时间戳                 | 1411572969                 |

------

\#Moment.js 写法示例
Moment.js 是我用过的最好用的操作时间的工具库。它使得操作时间变得很简单。
\##创建

```
moment() // 当前时间
moment("1995-12-25") // 1995-12-25
moment("12-25-1995", "MM-DD-YYYY") // 1995-12-25
moment({ year :2010, month :3, day :5, hour :15, minute :10, second :3, millisecond :123})
moment(Date.now() - 24 * 60 * 60 * 1000) // 昨天
moment(new Date(2011, 9, 16)) // 2011-10-16
123456
```

\##格式化

```
moment().format('YYYY年MM月DD日 HH:mm:ss') // 2016年11月11日 22:05:19
moment().format('hh:m:ss') // 10:5:19
moment().format('[YYYY]') // "YYYY"。[] 里的会原样输出。
123
```

\##转化成 Date 对象

```
moment().toDate()
1
```

\##获取/设置时间信息

```
moment().second() //获得 秒
moment().second(Number) //设置 秒。0 到 59
moment().minute() //获得 分
moment().minute(Number) //设置 分。0 到 59
// 类似的用法
moment().hour() // 小时
moment().date() // 一个月里的第几天
moment().day() // 星期几
moment().dayOfYear() // 一年里的第几天
moment().week() // 一年里的第几周
moment().month() // 第几个月
moment().quarter() // 一年里的第几个季度
moment().year() // 年
moment().daysInMonth() // 当前月有多少天
1234567891011121314
```

\##操作

```
moment().add(7, 'days') // 之后的第7天。第2个参数还可以是 'months', 'years' 等。注意是复数。
moment().add(7, 'd'）// 与上面一行代码的运行结果一样。
moment().subtract(1, 'months') // 上个月

moment().startOf('week') // 这周的第一天
moment().startOf('hour') // 等效与 moment().minutes(0).seconds(0).milliseconds(0)。
// 还支持 'year'，'month' 等

moment().endOf('week')
123456789
```

\##查询

```
// 早于
moment('2010-10-20').isBefore('2010-10-21') // true
moment('2010-10-20').isBefore('2010-12-31', 'year') // false
moment('2010-10-20').isBefore('2011-01-01', 'year') // true

// 是否相等
moment('2010-10-20').isSame('2010-10-20') // true
moment('2010-10-20').isSame('2009-12-31', 'year')  // false
moment('2010-10-20').isSame('2010-01-01', 'year')  // true

// 晚于
moment('2010-10-20').isAfter('2010-10-19') // true
moment('2010-10-20').isAfter('2010-01-01', 'year') // false
moment('2010-10-20').isAfter('2009-12-31', 'year') // true

// 是否在时间范围内
moment('2010-10-20').isBetween('2010-10-19', '2010-10-25') // true
moment('2010-10-20').isBetween('2010-01-01', '2012-01-01', 'year') // false
moment('2010-10-20').isBetween('2009-12-31', '2012-01-01', 'year') // true

moment().isLeapYear() // 是否是闰年
```