<!--
 * @Description: Object 类型
 * @Author: shenxh
 * @Date: 2021-12-21 15:49:57
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-22 16:16:09
-->

- [Object (对象) 类型](#object-对象-类型)
  - [构造函数](#构造函数)
  - [字面量](#字面量)

# Object (对象) 类型
对象其实就是一组数据和功能的集合。创建对象的常用方法有以下几种:

## 构造函数
通过 `new` 操作符后跟对象类型的名称来创建, 然后再给对象添加属性和方法：

```
let obj = new Object();

obj.name = '张三';
obj.age = 18;
```

## 字面量
对象字面量是对象定义的一种简写形式, 目的在于简化创建包含大量属性的对象的过程, 性质其实和第一种一样, 只是写法不同而已:

```
let obj = {};

obj.name = '张三';
obj.age = 18;
```

或者你可以这样写 (推荐):
```
let obj = {
  name: '张三',
  age: 18
}
```
