<!--
 * @Description: Array 数组
 * @Author: shenxh
 * @Date: 2021-12-28 10:08:10
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-28 16:52:20
-->

- [Array](#array)
  - [创建数组](#创建数组)
  - [数组索引](#数组索引)
- [数组方法总结](#数组方法总结)
  - [检测数组](#检测数组)
    - [isArray()](#isarray)
  - [迭代器方法](#迭代器方法)
    - [keys()、values() 和 entries()](#keysvalues-和-entries)
  - [复制和填充方法](#复制和填充方法)
    - [copyWithin() 和 fill()](#copywithin-和-fill)
  - [转换方法](#转换方法)
    - [toString() 和 valueOf()](#tostring-和-valueof)
    - [join()](#join)
  - [栈方法](#栈方法)
    - [push()](#push)
    - [pop()](#pop)
  - [队列方法](#队列方法)
    - [unshift()](#unshift)
    - [shift()](#shift)
  - [排序方法](#排序方法)
    - [reverse()](#reverse)
    - [sort()](#sort)
  - [操作方法](#操作方法)
    - [concat()](#concat)
    - [slice()](#slice)
    - [splice()](#splice)
  - [搜索和位置方法](#搜索和位置方法)
    - [indexOf()、lastIndexOf() 和 includes()](#indexoflastindexof-和-includes)
    - [find() 和 findIndex()](#find-和-findindex)
  - [迭代方法](#迭代方法)
    - [every()](#every)
    - [filter()](#filter)
    - [forEach()](#foreach)
    - [map()](#map)
    - [some()](#some)
  - [归并方法](#归并方法)
    - [reduce() 和 reduceRight()](#reduce-和-reduceright)

# Array
除了 Object，Array 应该就是 ECMAScript 中最常用的类型了。

ECMAScript 数组跟其他编程语言的数组有很大区别。跟其他语言中的数组一样，ECMAScript 数组也是一组有序的数据，但跟其他语言不同的是，数组中每个槽位可以存储**任意类型**的数据。这意味着可以创建一个数组，它的第一个元素是字符串，第二个元素是数值，第三个是对象。ECMAScript 数组也是动态大小的，会随着数据添加而自动增长。

## 创建数组
有几种基本的方式可以创建数组。一种是使用 Array 构造函数，比如：

```
let colors = new Array("red", "blue", "green");

console.log(colors); // ['red', 'blue', 'green']
```

另一种创建数组的方式是使用数组字面量表示法。数组字面量是在中括号中包含以逗号分隔的元素列表，如下面的例子所示：

```
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个元素的数组
let names = []; // 创建一个空数组

console.log(colors); // ['red', 'blue', 'green']
console.log(names); // []
```

## 数组索引
要取得或设置数组的值，需要使用中括号并提供相应值的数字索引，如下所示：

```
let colors = ["red", "blue", "green"]; // 定义一个字符串数组

// 显示第一项
console.log(colors[0]); // red
// 修改第三项
colors[2] = "black"; // ['red', 'blue', 'black']
// 添加第四项
colors[3] = "brown"; // ['red', 'blue', 'black', 'brown']
```

在中括号中提供的索引表示要访问的值。如果索引小于数组包含的元素数，则返回存储在相应位置的元素，就像示例中 colors[0] 显示"red"一样。设置数组的值方法也是一样的，就是替换指定位置的值。如果把一个值设置给超过数组最大索引的索引，就像示例中的 colors[3]，则数组长度会自动扩展到该索引值加 1（示例中设置的索引 3，所以数组长度变成了 4）。

数组中元素的数量保存在 length 属性中，这个属性始终返回 0 或大于 0 的值，如下例所示：

```
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
let names = []; // 创建一个空数组

console.log(colors.length); // 3
console.log(names.length); // 0
```

数组 length 属性的独特之处在于，它不是只读的。通过修改 length 属性，可以从数组末尾删除或添加元素。来看下面的例子：

```
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组

colors.length = 2;
console.log(colors[2]); // undefined
```

这里，数组 colors 一开始有 3 个值。将 `length` 设置为 2，就删除了最后一个（位置 2 的）值，因此 colors[2] 就没有值了。如果将 `length` 设置为大于数组元素数的值，则新添加的元素都将以 `undefined` 填充，如下例所示：

```
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组

colors.length = 4;
console.log(colors[3]); // undefined
```

这里将数组 colors 的 `length` 设置为 4，虽然数组只包含 3 个元素。位置 3 在数组中不存在，因此访问其值会返回特殊值 `undefined`。

使用 `length` 属性可以方便地向数组末尾添加元素，如下例所示：

```
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组

// 添加一种颜色（位置 3）
colors[colors.length] = "black"; // ['red', 'blue', 'green', 'black']
// 再添加一种颜色（位置 4）
colors[colors.length] = "brown"; // ['red', 'blue', 'green', 'black', 'brown']
```

数组中最后一个元素的索引始终是 length - 1，因此下一个新增槽位的索引就是 `length`。每次在数组最后一个元素后面新增一项，数组的 `length` 属性都会自动更新，以反映变化。这意味着第二行的 colors[colors.length] 会在位置 3 添加一个新元素，下一行则会在位置 4 添加一个新元素。新的长度会在新增元素被添加到当前数组外部的位置上时自动更新。

# 数组方法总结
|方法|描述|备注|
|-|-|-|
|[isArray()](#isarray)|判断某个变量是否是一个数组对象|数组检测|
|[keys()](#keysvalues-和-entries)|返回一个包含数组中每个索引键的对象||
|[values()](#keysvalues-和-entries)|返回一个新的对象，该对象包含数组每个索引的值||
|[entries()](#keysvalues-和-entries)|返回一个新的对象，该对象包含数组中每个索引的键/值对||
|[copyWithin()](#copywithin-和-fill)|浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度||
|[fill()](#copywithin-和-fill)|用一个固定值填充一个数组中从起始索引到终止索引内的全部元素||
|[toString()](#tostring-和-valueof)|返回一个字符串表示指定的数组及其元素|数组转字符串|
|[valueOf()](#tostring-和-valueof)|返回数组对象的原始值||
|[join()](#join)|将一个数组的所有元素连接成一个字符串并返回这个字符串|数组转字符串|
|[push()](#push)|将一个或多个元素添加到数组的末尾，并返回该数组的新长度||
|[pop()](#pop)|从数组中删除最后一个元素，并返回该元素的值||
|[unshift()](#unshift)|将一个或多个元素添加到数组的头部，并返回该数组的新长度||
|[shift()](#shift)|从数组中删除第一个元素，并返回该元素的值||
|[reverse()](#reverse)|将数组中元素的位置颠倒，并返回该数组。该方法会改变原数组||
|[sort()](#sort)|对数组元素进行原地排序并返回此数组||
|[concat()](#concat)|用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组||
|[slice()](#slice)|提取源数组的一部分并返回一个新数组||
|[splice()](#splice)|通过删除或替换现有元素或者原地添加新的元素来修改数组，并以数组形式返回被修改的内容||
|[indexOf()](#indexoflastindexof-和-includes)|返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回 -1||
|[lastIndexOf()](#indexoflastindexof-和-includes)|返回指定元素在数组中的最后一个的索引，如果不存在则返回 -1||
|[includes()](#indexoflastindexof-和-includes)|判断一个数组是否包含一个指定的值，如果包含则返回 `true`，否则返回 `false`||
|[find()](#find-和-findindex)|返回数组中满足提供的测试函数的第一个元素的值。否则返回 `undefined`||
|[findIndex()](#find-和-findindex)|返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回 -1||
|[every()](#every)|测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值|遍历|
|[filter()](#filter)|创建一个新数组, 其包含通过所提供函数实现的测试的所有元素|遍历|
|[forEach()](#foreach)|对数组的每个元素执行一次给定的函数|遍历|
|[map()](#map)|返回一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值|遍历|
|[some()](#some)|测试数组中是不是至少有一个元素通过了被提供的函数测试|遍历|
|[reduce()](#reduce-和-reduceright)|对数组中的每个元素执行一个由您提供的函数（升序执行），将其结果汇总为单个返回值||
|[reduceRight()](#reduce-和-reduceright)|对数组中的每个元素执行一个由您提供的函数（降序执行），将其结果汇总为单个返回值||

## 检测数组

### isArray()
判断对象是否为数组

```
let arr = [];
let str = '';
let num = 0;

console.log(Array.isArray(arr)); // true
console.log(Array.isArray(str)); // false
console.log(Array.isArray(num)); // false
```

## 迭代器方法

### keys()、values() 和 entries()
在 ES6 中，Array 的原型上暴露了 3 个用于检索数组内容的方法：`keys()`、`values()` 和 `entries()`。`keys()` 返回数组索引的迭代器，`values()` 返回数组元素的迭代器，而 `entries()` 返回索引/值对的迭代器：

```
let a = ["foo", "bar", "baz", "qux"];

// 因为这些方法都返回迭代器，所以可以将它们的内容
// 通过 Array.from()直接转换为数组实例
let aKeys = Array.from(a.keys());
let aValues = Array.from(a.values());
let aEntries = Array.from(a.entries());

console.log(aKeys); // [0, 1, 2, 3]
console.log(aValues); // ["foo", "bar", "baz", "qux"]
console.log(aEntries); // [[0, "foo"], [1, "bar"], [2, "baz"], [3, "qux"]]
```

## 复制和填充方法

### copyWithin() 和 fill()
ES6 新增了两个方法：批量复制方法 `copyWithin()`，以及填充数组方法 `fill()`。

这两个方法的函数签名类似，都需要指定既有数组实例上的一个范围，包含开始索引，不包含结束索引。使用这个方法不会改变数组的大小。

使用 `fill()` 方法可以向一个已有的数组中插入全部或部分相同的值。开始索引用于指定开始填充的位置，它是可选的。如果不提供结束索引，则一直填充到数组末尾。负值索引从数组末尾开始计算。也可以将负索引想象成数组长度加上它得到的一个正索引：

```
let zeroes = [0, 0, 0, 0, 0];

// 用 5 填充整个数组
zeroes.fill(5);
console.log(zeroes); // [5, 5, 5, 5, 5]
zeroes.fill(0); // 重置

// 用 6 填充索引大于等于 3 的元素
zeroes.fill(6, 3);
console.log(zeroes); // [0, 0, 0, 6, 6]
zeroes.fill(0); // 重置

// 用 7 填充索引大于等于 1 且小于 3 的元素
zeroes.fill(7, 1, 3);
console.log(zeroes); // [0, 7, 7, 0, 0];
zeroes.fill(0); // 重置
```

`copyWithin()` 方法浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度。如下所示：

```
let array1 = ['a', 'b', 'c', 'd', 'e'];

// 将索引 3 (不包括) 之后的元素复制到索引 0
[1, 2, 3, 4, 5].copyWithin(0, 3); // [4, 5, 3, 4, 5]

// 将索引 3 (包括) 和 索引 4 (不包括) 之间的元素复制到索引 0
[1, 2, 3, 4, 5].copyWithin(0, 3, 4); // [4, 2, 3, 4, 5]
```

## 转换方法

### toString() 和 valueOf()
`valueOf()` 返回的是数组本身，而 `toString()` 返回由数组中每个值的等效字符串拼接而成的一个逗号分隔的字符串。也就是说，对数组的每个值都会调用其 `toString()` 方法，以得到最终的字符串。来看下面的例子：

```
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组

console.log(colors.toString()); // red,blue,green
console.log(colors.valueOf()); // ['red', 'blue', 'green']
console.log(colors); // ['red', 'blue', 'green']
```

### join()
如果想使用不同的分隔符，则可以使用 `join()` 方法。`join()` 方法接收一个参数，即字符串分隔符，返回包含所有项的字符串。来看下面的例子：

```
let colors = ["red", "green", "blue"];

console.log(colors.join()); // red,green,blue
console.log(colors.join(",")); // red,green,blue
console.log(colors.join("||")); // red||green||blue 
```

这里在 colors 数组上调用了 `join()` 方法，得到了与调用 `toString()` 方法相同的结果。传入逗号，结果就是逗号分隔的字符串。最后一行给 `join()` 传入了双竖线，得到了字符串 "red||green||blue"。如果不给 `join()` 传入任何参数，或者传入 `undefined`，则仍然使用逗号作为分隔符。

## 栈方法

### push()
`push()` 方法接收任意数量的参数，并将它们添加到数组末尾，返回数组的最新长度。

```
let colors = ["red"];
let count = colors.push("blue", "green"); // 数组末尾添加两项

console.log(count); // 3
console.log(colors); // ['red', 'blue', 'green']
```

### pop()
`pop()` 方法用于删除数组的最后一项并返回它，然后数组长度减 1。

```
let colors = ["red", "blue", "green"];
let item = colors.pop(); // 数组末尾删除一项

console.log(item); // green
console.log(colors); // ['red', 'blue']
```

## 队列方法

### unshift()
`unshift()` 方法接收任意数量的参数，并将它们添加到数组开头，返回数组的最新长度。

```
let colors = ["green"];
let count = colors.unshift("red", "blue"); // 数组开头添加两项

console.log(count); // 3
console.log(colors); // ['red', 'blue', 'green']
```

### shift()
`shift()` 方法用于删除数组的第一项并返回它，然后数组长度减 1。

```
let colors = ["red", "blue", "green"];
let item = colors.shift(); // 数组开头删除一项

console.log(item); // red
console.log(colors); // ['blue', 'green']
```

## 排序方法

### reverse()
`reverse()` 方法就是将数组元素反向排列。比如：

```
let values = [1, 2, 3, 4, 5];
values.reverse();

console.log(values); // [5, 4, 3, 2, 1]
```


### sort()
默认情况下，`sort()` 会按照升序重新排列数组元素，即最小的值在前面，最大的值在后面。为此，`sort()` 会在每一项上调用 `String()` 转型函数，然后比较字符串来决定顺序。即使数组的元素都是数值，也会先把数组转换为字符串再比较、排序。比如：

```
let values = [0, 1, 5, 10, 15];
values.sort();

console.log(values); // [0, 1, 10, 15, 5]
```

一开始数组中数值的顺序是正确的，但调用 `sort()` 会按照这些数值的字符串形式重新排序。因此，即使 5 小于 10，但字符串"10"在字符串"5"的前头，所以 10 还是会排到 5 前面。很明显，这在多数情况下都不是最合适的。为此，`sort()` 方法可以接收一个比较函数，用于判断哪个值应该排在前面。

比较函数接收两个参数，如果第一个参数应该排在第二个参数前面，就返回负值；如果两个参数相等，就返回 0；如果第一个参数应该排在第二个参数后面，就返回正值。下面是使用简单比较函数的一个例子：

```
let values = [0, 1, 5, 10, 15];

values.sort(function (value1, value2) {
  if (value1 < value2) {
    return -1;
  } else if (value1 > value2) {
    return 1;
  } else {
    return 0;
  }
});

console.log(values); // [0, 1, 5, 10, 15]
```

在给 `sort()` 方法传入比较函数后，数组中的数值在排序后保持了正确的顺序。当然，比较函数也可以产生降序效果，只要把返回值交换一下即可：

```
let values = [0, 1, 5, 10, 15];

values.sort(function (value1, value2) {
  if (value1 < value2) {
    return 1;
  } else if (value1 > value2) {
    return -1;
  } else {
    return 0;
  }
});

console.log(values); // [15, 10, 5, 1, 0]
```

如果数组的元素是数值，或者是其 `valueOf()` 方法返回数值的对象（如 Date 对象），这个比较函数还可以写得更简单，因为这时可以直接用第二个值减去第一个值：

```
let values = [0, 1, 5, 10, 15];

values.sort(function (value1, value2) {
  return value1 - value2
});

console.log(values); // [0, 1, 5, 10, 15]
```

推荐使用箭头函数：

```
let values = [0, 1, 5, 10, 15];

values.sort((value1, value2) => value1 - value2);

console.log(values); // [0, 1, 5, 10, 15]
```

比较函数就是要返回小于 0、0 和大于 0 的数值，因此减法操作完全可以满足要求。

## 操作方法

### concat()
`concat()` 方法可以在现有数组全部元素基础上创建一个新数组。它首先会创建一个当前数组的副本，然后再把它的参数添加到副本末尾，最后返回这个新构建的数组。如果传入一个或多个数组，则 `concat()` 会把这些数组的每一项都添加到结果数组。如果参数不是数组，则直接把它们添加到结果数组末尾。来看下面的例子：

```
let colors = ["red", "green", "blue"];
let colors2 = colors.concat("yellow", ["black", "brown"]);

console.log(colors); // ['red', 'green', 'blue']
console.log(colors2); // ['red', 'green', 'blue', 'yellow', 'black', 'brown']
```

这里先创建一个包含 3个值的数组 colors。然后 colors 调用 `concat()` 方法，传入字符串 "yellow" 和一个包含"black"和"brown"的数组。保存在 colors2 中的结果就是['red', 'green', 'blue', 'yellow', 'black', 'brown']。原始数组 colors 保持不变。

### slice()
方法 `slice()` 用于创建一个包含原有数组中一个或多个元素的新数组。

`slice()` 方法可以接收一个或两个参数：返回元素的开始索引和结束索引。

如果只有一个参数，则 `slice()` 会返回该索引到数组末尾的所有元素。如果有两个参数，则 `slice()` 返回从开始索引到结束索引对应的所有元素，其中不包含结束索引对应的元素。记住，这个操作不影响原始数组。来看下面的例子：

```
let colors = ["red", "green", "blue", "yellow", "purple"];
let colors2 = colors.slice(1);
let colors3 = colors.slice(1, 4);

console.log(colors2); // ['green', 'blue', 'yellow', 'purple']
console.log(colors3); // ['green', 'blue', 'yellow']
console.log(colors); // ['red', 'green', 'blue', 'yellow', 'purple']
```

这里，colors 数组一开始有 5 个元素。调用 `slice()` 传入 1 会得到包含 4 个元素的新数组。其中不包括"red"，这是因为拆分操作要从位置 1 开始，即从"green"开始。得到的 colors2 数组包含"green"、"blue"、"yellow"和"purple"。colors3 数组是通过调用 `slice()` 并传入 1 和 4 得到的，即从位置 1 开始复制到位置 3。因此 colors3 包含"green"、"blue"和"yellow"。

### splice()
或许最强大的数组方法就属 `splice()` 了，使用它的方式可以有很多种。`splice()` 的主要目的是在数组中间插入元素，但有 3 种不同的方式使用这个方法。
- 删除。需要给 `splice()` 传 2 个参数：要删除的第一个元素的位置和要删除的元素数量。可以从数组中删除任意多个元素，比如 splice(0, 2)会删除前两个元素。
- 插入。需要给 `splice()` 传 3 个参数：开始位置、0（要删除的元素数量）和要插入的元素，可以在数组中指定的位置插入元素。第三个参数之后还可以传第四个、第五个参数，乃至任意多个要插入的元素。比如，splice(2, 0, "red", "green") 会从数组位置 2 开始插入字符串"red"和"green"。
- 替换。`splice()` 在删除元素的同时可以在指定位置插入新元素，同样要传入 3 个参数：开始位置、要删除元素的数量和要插入的任意多个元素。要插入的元素数量不一定跟删除的元素数量一致。比如，splice(2, 1, "red", "green") 会在位置 2 删除一个元素，然后从该位置开始向数组中插入"red"和"green"。

`splice()` 方法始终返回这样一个数组，它包含从数组中被删除的元素（如果没有删除元素，则返回空数组）。以下示例展示了上述 3 种使用方式。

```
let colors = ["red", "green", "blue"];
let removed = colors.splice(0, 1); // 删除第一项

console.log(colors); // ['green', 'blue']
console.log(removed); // ['red']

// 在位置 1 插入两个元素
removed = colors.splice(1, 0, "yellow", "orange");

console.log(colors); // ['green', 'yellow', 'orange', 'blue']
console.log(removed); // []

// 插入两个值，删除一个元素
removed = colors.splice(1, 1, "red", "purple");

console.log(colors); // ['green', 'red', 'purple', 'orange', 'blue']
console.log(removed); // ['yellow']
```

这个例子中，colors 数组一开始包含 3 个元素。

第一次调用 `splice()` 时，只删除了第一项，colors 中还有"green"和"blue"。

第二次调用 `slice()` 时，在位置 1 插入两项，然后 colors 包含"green"、"yellow"、"orange"和"blue"。这次没删除任何项，因此返回空数组。

最后一次调用 `splice()` 时删除了位置 1 上的一项，同时又插入了"red"和"purple"。

最后，colors 数组包含"green"、"red"、"purple"、"orange"和"blue"。

## 搜索和位置方法

### indexOf()、lastIndexOf() 和 includes()
ECMAScript 提供了 3 个严格相等的搜索方法：`indexOf()`、`lastIndexOf()` 和 `includes()`。

这些方法都接收两个参数：要查找的元素和一个可选的起始搜索位置。`indexOf()` 和 `includes()` 方法从数组前头（第一项）开始向后搜索，而 `lastIndexOf()` 从数组末尾（最后一项）开始向前搜索。

`indexOf()` 和 `lastIndexOf()` 都返回要查找的元素在数组中的位置，如果没找到则返回1。`includes()` 返回布尔值，表示是否至少找到一个与指定元素匹配的项。在比较第一个参数跟数组每一项时，会使用全等（`===`）比较，也就是说两项必须严格相等。下面来看一些例子：

```
let numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];

console.log(numbers.indexOf(4)); // 3
console.log(numbers.lastIndexOf(4)); // 5
console.log(numbers.includes(4)); // true

console.log(numbers.indexOf(4, 4)); // 5
console.log(numbers.lastIndexOf(4, 4)); // 3
console.log(numbers.includes(4, 7)); // false

let person = { name: "Nicholas" };
let people = [{ name: "Nicholas" }];
let morePeople = [person];

console.log(people.indexOf(person)); // -1
console.log(morePeople.indexOf(person)); // 0
console.log(people.includes(person)); // false
console.log(morePeople.includes(person)); // true 
```

### find() 和 findIndex()
ECMAScript 也允许按照定义的断言函数搜索数组，每个索引都会调用这个函数。断言函数的返回值决定了相应索引的元素是否被认为匹配。

断言函数接收 3 个参数：元素、索引和数组本身。其中元素是数组中当前搜索的元素，索引是当前元素的索引，而数组就是正在搜索的数组。断言函数返回真值，表示是否匹配。

`find()` 和 `findIndex()` 方法使用了断言函数。这两个方法都从数组的最小索引开始。`find()` 返回第一个匹配的元素，`findIndex()` 返回第一个匹配元素的索引。这两个方法也都接收第二个可选的参数，用于指定断言函数内部 `this` 的值。找到匹配项后，这两个方法都**不再继续搜索**。

```
let arr = [5, 12, 8, 130, 44];
let findFn = function (element) {
  return element > 10
};
let arrFind = arr.find(findFn);
let arrFindIdx = arr.findIndex(findFn);

console.log(arrFind); // 12
console.log(arrFindIdx); // 1
```

## 迭代方法
ECMAScript 为数组定义了 5 个迭代方法。这些方法都不改变调用它们的数组。

他们的参数如下：
- `callback`：用来测试每个元素的函数，它可以接收三个参数：
  - `item`：正在处理的当前元素
  - `index`：可选。用于测试的当前值的索引
  - `array`：可选。当前正在操作的数组
- `thisArg`：可选。当执行回调函数 `callback` 时，用作 `this` 的值

### every()
`every()` 方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。

> 注：若收到一个空数组，此方法在一切情况下都会返回 true。

```
let arr = [1, 30, 39, 29, 10, 13];
let result1 = arr.every(item => item < 40);
let result2 = arr.every(item => item > 5);

console.log(result1); // true
console.log(result2); // false
```

### filter()
`filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

```
let arr = [1, 30, 39, 29, 10, 13];
let result = arr.filter(item => item > 20);

console.log(result); // [30, 39, 29]
```

### forEach()
`forEach()` 方法对数组的每个元素执行一次给定的函数。

```
let arr = ['a', 'b', 'c'];

arr.forEach((item, index) => console.log(item, index));

// a 0
// b 1
// c 2
```

### map()
`map()` 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。

```
let arr = [1, 4, 9, 16];
let newArr = arr.map(item => item * 2);

console.log(newArr); // [2, 8, 18, 32]
```

### some()
`some()` 方法测试数组中是不是至少有1个元素通过了被提供的函数测试。它返回的是一个 Boolean 类型的值。

> 注：如果用一个空数组进行测试，在任何情况下它返回的都是 false。

```
let arr = [1, 30, 39, 29, 10, 13];
let result1 = arr.some(item => item > 30);
let result2 = arr.some(item => item < 1);

console.log(result1); // true
console.log(result2); // false
```

## 归并方法

### reduce() 和 reduceRight()
这两个方法都会迭代数组的所有项，并在此基础上构建一个最终返回值。`reduce()` 方法从数组第一项开始遍历到最后一项。而 `reduceRight()` 从最后一项开始遍历至第一项。

这两个方法都接收两个参数：对每一项都会运行的归并函数，以及可选的以之为归并起点的初始值。传给 `reduce()` 和 `reduceRight()` 的函数接收 4 个参数：上一个归并值、当前项、当前项的索引和数组本身。

这个函数返回的任何值都会作为下一次调用同一个函数的第一个参数。如果没有给这两个方法传入可选的第二个参数（作为归并起点值），则第一次迭代将从数组的第二项开始，因此传给归并函数的第一个参数是数组的第一项，第二个参数是数组的第二项。

```
let arr = [1, 2, 3, 4, 5];
let sum = arr.reduce((prev, cur, index, array) => prev + cur);

console.log(sum); // 15 
```

第一次执行归并函数时，prev 是 1，cur 是 2。第二次执行时，prev 是 3（1 + 2），cur 是 3（数组第三项）。如此递进，直到把所有项都遍历一次，最后返回归并结果。

`reduceRight()` 方法与之类似，只是方向相反。来看下面的例子：

```
let arr = [1, 2, 3, 4, 5];
let sum = arr.reduceRight((prev, cur, index, array) => prev + cur);

console.log(sum); // 15
```

在这里，第一次调用归并函数时 prev 是 5，而 cur 是 4。当然，最终结果相同，因为归并操作都是简单的加法。

究竟是使用 `reduce()` 还是 `reduceRight()`，只取决于遍历数组元素的方向。除此之外，这两个方法没什么区别。
