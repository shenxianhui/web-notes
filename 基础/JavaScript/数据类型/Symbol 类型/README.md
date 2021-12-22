<!--
 * @Description: Symbol 类型
 * @Author: shenxh
 * @Date: 2021-12-22 15:41:07
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-22 15:43:55
-->

- [Symbol (符号) 类型](#symbol-符号-类型)

# Symbol (符号) 类型
Symbol（符号）是 ECMAScript 6 新增的数据类型。符号是原始值，且符号实例是唯一、不可变的。

符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险。

尽管听起来跟私有属性有点类似，但符号并不是为了提供私有属性的行为才增加的（尤其是因为
Object API 提供了方法，可以更方便地发现符号属性）。

相反，符号就是用来创建唯一记号，进而用作非字符串形式的对象属性。

[Symbol 文档](https://es6.ruanyifeng.com/#docs/symbol)
