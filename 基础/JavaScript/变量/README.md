<!--
 * @Author: shenxh
 * @Date: 2021-12-17 14:37:55
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-17 16:52:50
 * @Description: 变量
-->

- [变量](#变量)
  - [var 关键字](#var-关键字)
  - [let 声明与 const 声明](#let-声明与-const-声明)

# 变量
变量是松散类型的，意思是变量可以用于保存任何类型的数据

每个变量只不过是一个用于保存任意值的命名占位符

有 3 个关键字可以声明变量：`var`、`let` 和 `const`

## var 关键字
要定义变量，可以使用 `var` 操作符（注意 `var` 是一个关键字），后跟变量名（即标识符，如前所述）：
```
var message;
```

这行代码定义了一个名为 `message` 的变量，可以用它保存任何类型的值。（不初始化的情况下，变量会保存一个特殊值 `undefined`，下一节讨论数据类型时会谈到。）

可以同时定义变量并设置它的值：
```
var message = "hi";
```

这里，`message` 被定义为一个保存字符串值 `hi` 的变量。随后，不仅可以改变保存的值，也可以改变值的类型：
```
var message = "hi";
message = 100; // 合法，但不推荐
```

在这个例子中，变量 `message` 首先被定义为一个保存字符串值 `hi` 的变量，然后又被重写为保存了数值 100。虽然不推荐改变变量保存值的类型，但这在 JavaScript 中是完全有效的。

还可以在一条语句中声明很多变量。该语句以 `var` 开头，并使用逗号分隔变量即可：
```
var lastname="Doe", age=30, job="carpenter";
```

声明也可横跨多行：
```
var lastname="Doe",
age=30,
job="carpenter";
```

## let 声明与 const 声明
`let` 与 `const` 为 ES6 新增命令

[查看详情](https://es6.ruanyifeng.com/#docs/let)
