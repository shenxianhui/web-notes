<!--
 * @Description: Boolean 类型
 * @Author: shenxh
 * @Date: 2021-12-22 11:31:41
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-22 15:36:46
-->

- [Boolean (布尔) 类型](#boolean-布尔-类型)

# Boolean (布尔) 类型
Boolean（布尔值）类型是 JavaScript 中使用最频繁的类型之一，有两个字面值：`true` 和 `false`。

下面是给变量赋布尔值的例子：

```
let found = true;
let lost = false; 
```

注意，布尔值字面量 `true` 和 `false` 是区分大小写的，因此 True 和 False（及其他大小混写形式）是有效的标识符，但不是布尔值。

虽然布尔值只有两个，但所有其他 JavaScript 类型的值都有相应布尔值的等价形式。要将一个其他类型的值转换为布尔值，可以调用特定的 `Boolean()` 转型函数：

```
let message = "Hello world!";
let messageAsBoolean = Boolean(message);
```

在这个例子中，字符串 message 会被转换为布尔值并保存在变量 messageAsBoolean 中。Boolean()转型函数可以在任意类型的数据上调用，而且始终返回一个布尔值。什么值能转换为 true 或 false 的规则取决于数据类型和实际的值。下表总结了不同类型与布尔值之间的转换规则。

|数据类型|转换为 `true` 的值|转换为 `false` 的值|
|-|-|-|
|Boolean|true|false|
|String|非空字符串|空字符串 ("")|
|Number|非零数值|0、NaN|
|Object|任意对象|null|
|Undefined|-|undefined|
