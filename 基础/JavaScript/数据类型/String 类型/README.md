<!--
 * @Description: String 类型
 * @Author: shenxh
 * @Date: 2021-12-21 16:37:40
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-22 11:15:19
-->

- [String (字符串) 类型](#string-字符串-类型)
  - [字符字面量](#字符字面量)
  - [转换为字符串](#转换为字符串)
  - [模板字面量](#模板字面量)
  - [字符串插值](#字符串插值)

# String (字符串) 类型
String（字符串）数据类型表示零或多个 16 位 Unicode 字符序列。字符串可以使用双引号（`"`）、单引号（`'`）或反引号（<code>`</code>）标示，因此下面的代码都是合法的：

```
let name1 = "张三";
let name2 = '李四';
let name3 = `王五`;
```

要注意的是，以某种引号作为字符串开头，必须仍然以该种引号作为字符串结尾。

比如，下面的写法会导致语法错误：

```
let name = '赵六"; // 语法错误：开头和结尾的引号必须是同一种
```

## 字符字面量
字符串数据类型包含一些字符字面量，用于表示非打印字符或有其他用途的字符，如下表所示：

|字面量|含义|
|-|-|
|`\n`|换行|
|`\t`|制表|
|`\b`|退格|
|`\r`|回车|
|`\f`|换页|
|`\\`|反斜杠（\）|
|`\'`|单引号（'），在字符串以单引号标示时使用，例如 `'He said, \'hey.\''`|
|`\"`|双引号（"），在字符串以双引号标示时使用，例如 `"He said, \"hey.\""`|
|<code>\\`</code>|反引号（\`），在字符串以反引号标示时使用，例如 <code>\`He said, \\`hey.\\``</code>|

## 转换为字符串
有两种方式把一个值转换为字符串。首先是使用几乎所有值都有的 `toString()` 方法。这个方法唯一的用途就是返回当前值的字符串等价物。比如：

```
let age = 11;
let ageAsString = age.toString(); // 字符串"11"
let found = true;
let foundAsString = found.toString(); // 字符串"true" 
```

`toString()` 方法可见于数值、布尔值、对象和字符串值。（没错，字符串值也有 `toString()` 方法，该方法只是简单地返回自身的一个副本。）`null` 和 `undefined` 值没有 `toString()` 方法。

如果你不确定一个值是不是 `null` 或 `undefined`，可以使用 `String()` 转型函数，它始终会返回表示相应类型值的字符串。String()函数遵循如下规则。

+ 如果值有 `toString()` 方法，则调用该方法（不传参数）并返回结果
+ 如果值是 `null`，返回"null"
+ 如果值是 `undefined`，返回"undefined"

下面看几个例子：

```
let value1 = 10;
let value2 = true;
let value3 = null;
let value4;

console.log(String(value1)); // "10"
console.log(String(value2)); // "true"
console.log(String(value3)); // "null"
console.log(String(value4)); // "undefined"
```

> 注: 用加号操作符给一个值加上一个空字符串 `""` 也可以将其转换为字符串（加号操作符后面会介绍）。

##  模板字面量
ES6 新增了使用模板字面量定义字符串的能力。与使用单引号或双引号不同，模板字面量保留换行字符，可以跨行定义字符串：

```
let pageHTML = `
<div>
  <a href="#">
    <span>Jake</span>
  </a>
</div>`; 
```

## 字符串插值
模板字面量最常用的一个特性是支持字符串插值，也就是可以在一个连续定义中插入一个或多个值。

字符串插值通过在 `${}` 中使用一个 JavaScript 表达式实现：

```
let value = 5;
let exponent = 'second';
// 以前，字符串插值是这样实现的：
let interpolatedString = value + ' to the ' + exponent + ' power is ' + (value * value);
// 现在，可以用模板字面量这样实现：
let interpolatedTemplateLiteral = `${ value } to the ${ exponent } power is ${ value * value }`;

console.log(interpolatedString); // 5 to the second power is 25
console.log(interpolatedTemplateLiteral); // 5 to the second power is 25
```
