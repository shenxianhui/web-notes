<!--
 * @Description: Date 日期
 * @Author: shenxh
 * @Date: 2021-12-24 11:21:25
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-24 14:05:04
-->

- [Date](#date)
  - [日期/时间组件方法](#日期时间组件方法)

# Date
Date 类型将日期保存为自协调世界时（UTC，Universal Time Coordinated）时间 1970 年 1 月 1 日午夜（零时）至今所经过的毫秒数。使用这种存储格式，Date 类型可以精确表示 1970 年 1 月 1 日之前及之后 285 616 年的日期。

要创建日期对象，就使用 `new` 操作符来调用 `Date` 构造函数：

```
let now = new Date();
```

## 日期/时间组件方法
Date 类型常用的方法（见下表）：

|方法|说明|
|-|-|
|`getTime()`|返回当前日期的毫秒数（13 位）|
|`getFullYear()`|返回日期中的年（4 位）|
|`getMonth()`|返回日期中的月（0~11 如：0 表示 1 月，11 表示 12 月）|
|`getDate()`|返回日期中的日（1~31）|
|`getDay()`|返回日期中的周（0~6 如：0 表示周日，6 表示周六）|
|`getHours()`|返回日期中的时（0~23）|
|`getMinutes()`|返回日期中的分（0~59）|
|`getSeconds()`|返回日期中的秒（0~59）|
|`getMilliseconds()`|返回日期中的毫秒|
