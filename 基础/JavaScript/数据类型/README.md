<!--
 * @Author: shenxh
 * @Date: 2021-12-17 16:53:42
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-21 20:17:49
 * @Description: 数据类型
-->

- [数据类型分类](#数据类型分类)
  - [基本数据类型 / 简单数据类型 / 原始类型](#基本数据类型--简单数据类型--原始类型)
  - [引用数据类型 / 复杂数据类型](#引用数据类型--复杂数据类型)
- [数据类型检测](#数据类型检测)
  - [`typeof` 操作符](#typeof-操作符)

# 数据类型分类
JavaScript 有 6 种简单数据类型（也称为原始类型）：`Undefined`、`Null`、`Boolean`、`Number`、`String` 和 `Symbol`。`Symbol`（符号）是 ECMAScript 6 新增的。还有一种复杂数据类型叫 `Object`（对
象）。`Object` 是一种无序名值对的集合。因为在 JavaScript 中不能定义自己的数据类型，所有值都可以用上述 7 种数据类型之一来表示

## 基本数据类型 / 简单数据类型 / 原始类型
+ [`Undefined` 未定义]()
+ [`Null` 空]()
+ [`Boolean` 布尔]()
+ [`Number` 数字](./Number%20类型/README.md)
+ [`String` 字符串](./String%20类型/README.md)
+ [`Symbol` 符号 (ES6 新增)]()

## 引用数据类型 / 复杂数据类型
+ [`Object` 对象]()

# 数据类型检测

## `typeof` 操作符
`typeof` 操作符可以检测变量属于哪种类型

对一个值使用 `typeof` 操作符会返回下列**字符串**之一：
+ "undefined" 表示值未定义
+ "boolean" 表示值为布尔值
+ "string" 表示值为字符串
+ "number" 表示值为数值
+ "object" 表示值为对象（而不是函数）或 null
+ "function" 表示值为函数
+ "symbol" 表示值为符号

举例:
```
let message = "some string";

console.log(typeof message); // "string"
console.log(typeof(message)); // "string"
console.log(typeof 95); // "number" 
```

> 注: 严格来讲，函数在 JavaScript 中被认为是对象，并不代表一种数据类型。可是，函数也有自己特殊的属性。为此，就有必要通过 `typeof` 操作符来区分函数和其他对象
