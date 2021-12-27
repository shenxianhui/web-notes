<!--
 * @Description: Math 数学
 * @Author: shenxh
 * @Date: 2021-12-27 15:04:55
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-27 16:07:52
-->

- [Math 数学](#math-数学)
  - [min() 和 max() 方法](#min-和-max-方法)
  - [舍入方法](#舍入方法)
  - [random() 方法](#random-方法)
  - [其他方法](#其他方法)

# Math 数学
ECMAScript 提供了 Math 对象作为保存数学公式、信息和计算的地方。Math 对象提供了一些辅助计算的属性和方法。

> 注: Math 对象上提供的计算要比直接在 JavaScript 实现的快得多，因为 Math 对象上的计算使用了 JavaScript 引擎中更高效的实现和处理器指令。但使用 Math 计算的问题是精度会因浏览器、操作系统、指令集和硬件而异。

## min() 和 max() 方法
Math 对象也提供了很多辅助执行简单或复杂数学计算的方法。

`min()` 和 `max()`方法用于确定一组数值中的最小值和最大值。这两个方法都接收任意多个参数，如下面的例子所示：

```
let max = Math.max(3, 54, 32, 16);
let min = Math.min(3, 54, 32, 16);

console.log(max); // 54
console.log(min); // 3 
```

要知道数组中的最大值和最小值，可以像下面这样使用扩展操作符：

```
let values = [1, 2, 3, 4, 5, 6, 7, 8];
let max = Math.max(...values);
```

## 舍入方法
接下来是用于把小数值舍入为整数的 4 个方法：`Math.ceil()`、`Math.floor()`、`Math.round()` 和 `Math.fround()`。这几个方法处理舍入的方式如下所述。
+ `Math.ceil()` 方法始终向上舍入为最接近的整数
+ `Math.floor()` 方法始终向下舍入为最接近的整数
+ `Math.round()` 方法执行四舍五入取整
+ `Math.fround()` 方法返回数值最接近的单精度（32 位）浮点值表示

以下示例展示了这些方法的用法：

```
console.log(Math.ceil(25.9)); // 26
console.log(Math.ceil(25.5)); // 26
console.log(Math.ceil(25.1)); // 26

console.log(Math.round(25.9)); // 26
console.log(Math.round(25.5)); // 26
console.log(Math.round(25.1)); // 25

console.log(Math.fround(0.4)); // 0.4000000059604645
console.log(Math.fround(0.5)); // 0.5
console.log(Math.fround(25.9)); // 25.899999618530273

console.log(Math.floor(25.9)); // 25
console.log(Math.floor(25.5)); // 25
console.log(Math.floor(25.1)); // 25
```

## random() 方法
`Math.random()` 方法返回一个 0~1 范围内的随机数，其中**包含 0 但不包含 1**。

如果想从 1~10 范围内随机选择一个数，代码就是这样的：

```
let num = Math.round(Math.random() * 9 + 1); 
```

## 其他方法
|方法|说明|
|-|-|
|`Math.abs(x)`|返回 x 的绝对值|
|`Math.exp(x)`|返回 Math.E 的 x 次幂|
|`Math.expm1(x)`|等于 Math.exp(x) - 1|
|`Math.log(x)`|返回 x 的自然对数|
|`Math.log1p(x)`|等于 1 + Math.log(x)|
|`Math.pow(x, power)`|返回 x 的 power 次幂|
|`Math.hypot(...nums)`|返回 nums 中每个数平方和的平方根|
|`Math.clz32(x)`|返回 32 位整数 x 的前置零的数量|
|`Math.sign(x)`|返回表示 x 符号的 1、0、-0 或-1|
|`Math.trunc(x)`|返回 x 的整数部分，删除所有小数|
|`Math.sqrt(x)`|返回 x 的平方根|
|`Math.cbrt(x)`|返回 x 的立方根|
|`Math.acos(x)`|返回 x 的反余弦|
|`Math.acosh(x)`|返回 x 的反双曲余弦|
|`Math.asin(x)`|返回 x 的反正弦|
|`Math.asinh(x)`|返回 x 的反双曲正弦|
|`Math.atan(x)`|返回 x 的反正切|
|`Math.atanh(x)`|返回 x 的反双曲正切|
|`Math.atan2(y, x)`|返回 y/x 的反正切|
|`Math.cos(x)`|返回 x 的余弦|
|`Math.sin(x)`|返回 x 的正弦|
|`Math.tan(x)`|返回 x 的正切|
