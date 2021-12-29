<!--
 * @Description: JSON
 * @Author: shenxh
 * @Date: 2021-12-29 16:32:01
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-29 17:06:32
-->

- [JSON](#json)
  - [转换方法](#转换方法)
    - [对象转 JSON](#对象转-json)
    - [JSON 转对象](#json-转对象)

# JSON
JSON 是 "JavaScript Object Notation" 的首字母缩写，单词的意思是 JavaScript 对象表示法。

这里说的 JSON 指的是类似于 JavaScript 对象的一种数据格式，目前这种数据格式比较流行，逐渐替换掉了传统的xml数据格式。

示例如下：

```
{
  "name": "张三",
  "age": 35,
  "star": true,
  "children": [
    {
      "name": "李四",
      "age": 18,
      "star": false,
      "children": null
    }
  ]
}
```

也可以是一个数组：

```
["a", "b", "c", 1, 2, 3, { "name": "张三" }]
```

与对象不同的是，JSON 格式的**属性名称**和**字符串值**需要用**双引号**引起来，用单引号或者不用引号会导致读取错误

合法符号如下：
- `{`
- `}`
- `"`
- `:`
- `,`
- `[`
- `]`

## 转换方法

### 对象转 JSON
`JSON.stringify()` 方法将一个 JavaScript 对象或值转换为 JSON 字符串

```
let num = 123;
let str = 'abc';
let obj = {
  name: '张三',
  age: 18
};
let arr = ['a', 'b', 'c', 1, 2, 3];

JSON.stringify(num); // '123'
JSON.stringify(str); // '"abc"'
JSON.stringify(obj); // '{"name":"张三","age":18}'
JSON.stringify(arr); // '["a","b","c",1,2,3]'
```

### JSON 转对象
`JSON.parse()` 方法可以解析 JSON 字符串, 将数据转换为 JavaScript 对象

我们用上面的 JSON 数据做演示：

```
let jsonNum = '123';
let jsonStr = '"abc"';
let jsonObj = '{"name":"张三","age":18}';
let jsonArr = '["a","b","c",1,2,3]';

JSON.parse(jsonNum); // 123
JSON.parse(jsonStr); // 'abc'
JSON.parse(jsonObj); // {name: '张三', age: 18}
JSON.parse(jsonArr); // ['a', 'b', 'c', 1, 2, 3]
```
