<!--
 * @Description: Number 数字
 * @Author: shenxh
 * @Date: 2021-12-27 09:41:36
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-27 09:47:03
-->

- [Number](#number)

# Number
Number 是对应数值的引用类型。要创建一个 Number 对象，就使用 Number 构造函数并传入一个数值，如下例所示：

```
let numberObject = new Number(10);

// 实际开发中, 我们一般这样写:
let myNum = 10;
```

除了继承的方法，Number 类型还提供了几个用于将数值格式化为字符串的方法。

`toFixed()` 方法返回包含指定小数点位数的数值字符串，如：

```
let num = 10;

console.log(num.toFixed(2)); // "10.00"
```

这里的 `toFixed()` 方法接收了参数 2，表示返回的数值字符串要包含两位小数。结果返回值为"10.00"，小数位填充了 0。如果数值本身的小数位超过了参数指定的位数，则四舍五入到最接近的小数位：

```
let num = 10.005;

console.log(num.toFixed(2)); // "10.01" 
```

`toFixed()` 自动舍入的特点可以用于处理货币。不过要注意的是，多个浮点数值的数学计算不一定得到精确的结果。比如，0.1 + 0.2 = 0.30000000000000004。
