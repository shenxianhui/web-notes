<!--
 * @Description: Null 类型
 * @Author: shenxh
 * @Date: 2021-12-22 11:23:34
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-22 11:28:57
-->

- [Null (空) 类型](#null-空-类型)

# Null (空) 类型
Null 类型同样只有一个值，即特殊值 `null`。逻辑上讲，`null` 值表示一个空对象指针，这也是给 `typeof` 传一个 `null` 会返回 "object" 的原因：

```
let car = null;

console.log(typeof car); // "object"
```

`null` 是一个假值。因此，如果需要，可以用更简洁的方式检测它。不过要记住，也有很多其他可能的值同样是假值。所以一定要明确自己想检测的就是 `null` 这个字面值，而不仅仅是假值。

```
let message = null;

if (message) {
 // 这个块不会执行
}
if (!message) {
 // 这个块会执行
}
```
