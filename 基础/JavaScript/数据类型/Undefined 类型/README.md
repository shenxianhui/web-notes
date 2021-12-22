<!--
 * @Description: Undefined 类型
 * @Author: shenxh
 * @Date: 2021-12-22 11:07:58
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-22 11:19:16
-->

- [Undefined (未定义) 类型](#undefined-未定义-类型)

# Undefined (未定义) 类型
Undefined 类型只有一个值，就是特殊值 `undefined`。当使用 `var` 或 `let` 声明了变量但没有初始化时，就相当于给变量赋予了 `undefined` 值：

```
let message;

console.log(message); // "undefined"
```

注意，包含 `undefined` 值的变量跟未定义变量是有区别的。请看下面的例子：

```
let message; // 这个变量被声明了，只是值为 undefined
// 确保没有声明过这个变量
// let age

console.log(message); // "undefined"
console.log(age); // 报错
```

`undefined` 是一个假值。因此，如果需要，可以用更简洁的方式检测它。不过要记住，也有很多其他可能的值同样是假值。所以一定要明确自己想检测的就是 `undefined` 这个字面值，而不仅仅是假值。

```
let message; // 这个变量被声明了，只是值为 undefined

// age 没有声明
if (message) {
 // 这个块不会执行
}
if (!message) {
 // 这个块会执行
}
if (age) {
 // 这里会报错
} 
```
