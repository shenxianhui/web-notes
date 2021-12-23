<!--
 * @Description: 语句
 * @Author: shenxh
 * @Date: 2021-12-23 14:10:54
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-23 15:34:06
-->

- [if 语句](#if-语句)
- [for 语句](#for-语句)
- [for-in 语句](#for-in-语句)
- [for-of 语句](#for-of-语句)
- [break 和 continue 语句](#break-和-continue-语句)
- [switch 语句](#switch-语句)

# if 语句
if 语句是使用最频繁的语句之一，如下所示：

```
if (age < 18) {
  console.log('未成年');
} else {
  console.log('已成年');
} 
```

可以像这样连续使用多个 `if` 语句：

```
if (weight < 40) {
  console.log('体重最小为 40 kg');
} else if (weight > 60) {
  console.log('体重最大为 60 kg');
} else {
  console.log('体重合格!');
} 
```


# for 语句
for 语句也是先测试语句，只不过增加了进入循环之前的初始化代码，以及循环执行后要执行的表达式，如下所示：

```
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

以上代码在循环开始前定义了变量 i 的初始值为 0。然后求值条件表达式，如果求值结果为 `true`（i < 10），则执行循环体。因此循环体也可能不会被执行。如果循环体被执行了，则循环后表达式也会执行，以便递增变量 i。

# for-in 语句
for-in 语句是一种严格的迭代语句，用于枚举对象中的非符号键属性，如下所示：

```
let obj = {
  name: '张三',
  age: 18
}

for (let propName in obj) {
  console.log(propName);
}

// 打印结果:
// name
// age
```

JavaScript 中对象的属性是无序的，因此 for-in 语句不能保证返回对象属性的顺序。换句话说，所有可枚举的属性都会返回一次，但返回的顺序可能会因浏览器而异

如果 for-in 循环要迭代的变量是 `null` 或 `undefined`，则不执行循环体。

# for-of 语句
for-of 语句是一种严格的迭代语句，用于遍历可迭代对象 (数组) 的元素，语法如下：

```
let arr = ['张三', '李四', '王五', '赵六'];

for (let item in arr) {
  console.log(item);
} 

// 打印结果:
// 0
// 1
// 2
// 3
```

for-of 循环会按照可迭代对象的 `next()` 方法产生值的顺序迭代元素。

# break 和 continue 语句
break 和 continue 语句为执行循环代码提供了更严格的控制手段。其中，break 语句用于立即退出循环，强制执行循环后的下一条语句。而 continue 语句也用于立即退出循环，但会再次从循环顶部开始执行。下面看一个例子：


```
let num = 0;

for (let i = 1; i < 10; i++) {
  if (i % 5 == 0) {
    break;
  }
  num++;
}

console.log(num); // 4 
```

在上面的代码中，for 循环会将变量 i 由 1 递增到 10。而在循环体内，有一个 if 语句用于检查 i 能否被 5 整除（使用取模操作符）。如果是，则执行 break 语句，退出循环。变量 num 的初始值为 0，表示循环在退出前执行了多少次。当 break 语句执行后，下一行执行的代码是 console.log(num)，显示 4。之所以循环执行了 4 次，是因为当 i 等于 5 时，break 语句会导致循环退出，该次循环不会执行递增 num 的代码。

如果将 break 换成 continue，则会出现不同的效果：

```
let num = 0;

for (let i = 1; i < 10; i++) {
  if (i % 5 == 0) {
    continue;
  }
  num++;
}

console.log(num); // 8
```

这一次，console.log 显示 8，即循环被完整执行了 8 次。当 i 等于 5 时，循环会在递增 num 之前退出，但会执行下一次迭代，此时 i 是 6。然后，循环会一直执行到自然结束，即 i 等于 10。最终 num 的值是 8 而不是 9，是因为 continue 语句导致它少递增了一次。

# switch 语句
switch 语句是与 if 语句紧密相关的一种流控制语句，如下所示：

```
switch (expression) {
  case value1:
    statement;
    break;
  case value2:
    statement;
    break;
  case value3:
    statement;
    break;
  case value4:
    statement;
    break;
  default:
    statement;
}
```

这里的每个 case（条件/分支）相当于：“如果表达式等于后面的值，则执行下面的语句。” break 关键字会导致代码执行跳出 switch 语句。如果没有 break，则代码会继续匹配下一个条件。default 关键字用于在任何条件都没有满足时指定默认执行的语句（相当于 else 语句）。

有了 switch 语句，开发者就用不着写类似这样的代码了：

```
if (i == 25) {
  console.log("25");
} else if (i == 35) {
  console.log("35");
} else if (i == 45) {
  console.log("45");
} else {
  console.log("Other");
} 
```

而是可以这样写：

```
switch (i) {
  case 25:
    console.log('25');
    break;
  case 35:
    console.log('35');
    break;
  case 45:
    console.log('45');
    break;
  default:
    console.log('Other');
}
```
