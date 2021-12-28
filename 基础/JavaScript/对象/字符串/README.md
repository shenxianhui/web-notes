<!--
 * @Description: String 字符串
 * @Author: shenxh
 * @Date: 2021-12-27 09:51:47
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-28 09:21:24
-->

- [String](#string)
- [字符串方法总结](#字符串方法总结)
  - [JavaScript 字符](#javascript-字符)
    - [charAt()](#charat)
    - [charCodeAt()](#charcodeat)
  - [字符串操作方法](#字符串操作方法)
    - [concat()](#concat)
    - [slice()、substr() 和 substring()](#slicesubstr-和-substring)
  - [字符串位置方法](#字符串位置方法)
    - [indexOf() 和 lastIndexOf()](#indexof-和-lastindexof)
  - [字符串包含方法](#字符串包含方法)
    - [startsWith()、endsWith() 和 includes()](#startswithendswith-和-includes)
  - [trim() 方法](#trim-方法)
  - [repeat() 方法](#repeat-方法)
  - [padStart() 和 padEnd() 方法](#padstart-和-padend-方法)
  - [字符串迭代与解构](#字符串迭代与解构)
  - [字符串大小写转换](#字符串大小写转换)
    - [toLowerCase()](#tolowercase)
    - [toUpperCase()](#touppercase)
  - [字符串模式匹配方法](#字符串模式匹配方法)
    - [match()](#match)
    - [search()](#search)
    - [replace()](#replace)
    - [split()](#split)
  - [localeCompare() 方法](#localecompare-方法)

# String
String 是对应字符串的引用类型。要创建一个 String 对象，使用 String 构造函数并传入一个数值，如下例所示：

```
let stringObject = new String("hello world");

// 实际开发中, 我们一般这样写:
let myStr = "hello world";
```

每个 String 对象都有一个 `length` 属性，表示字符串的长度 (字符的数量)。来看下面的例子：

```
let stringValue = "hello world";
console.log(stringValue.length); // 11
```

这个例子输出了字符串"hello world"中包含的字符数量：11。

# 字符串方法总结
|方法|描述|备注|
|-|-|-|
|[charAt()](#charat)|返回指定位置的字符||
|[charCodeAt()](#charcodeat)|返回指定位置的字符的 Unicode 编码||
|[concat()](#concat)|字符串拼接, 返回拼接得到的新字符串||
|[slice()](#slicesubstr-和-substring)|提取字符串的片断，并在新的字符串中返回被提取的部分||
|[substr()](#slicesubstr-和-substring)|从起始索引号提取字符串中指定数目的字符 (包前不包后)||
|[substring()](#slicesubstr-和-substring)|提取字符串中两个指定的索引号之间的字符 (包前不包后)||
|[indexOf()](#indexof-和-lastindexof)|返回某个指定的字符串值在字符串中首次出现的位置||
|[lastIndexOf()](#indexof-和-lastindexof)|从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置||
|[startsWith()](#startswithendswith-和-includes)|确定一个字符串是否在另一个字符串头部|ES6|
|[endsWith()](#startswithendswith-和-includes)|确定一个字符串是否在另一个字符串尾部|ES6|
|[includes()](#startswithendswith-和-includes)|确定一个字符串是否包含在另一个字符串中|ES6|
|[trim()](#trim-方法)|去除字符串两边的空白||
|[repeat()](#repeat-方法)|重复原字符串|ES6|
|[padStart()](#padstart-和-padend-方法)|在头部补全字符串|ES6|
|[padEnd()](#padstart-和-padend-方法)|在尾部补全字符串|ES6|
|[toLowerCase()](#tolowercase)|把字符串转换为小写||
|[toUpperCase()](#touppercase)|把字符串转换为大写||
|[match()](#match)|查找找到一个或多个正则表达式的匹配||
|[search()](#search)|返回字符串中第一个匹配项的索引如果没有找到匹配项, 则返回 -1||
|[replace()](#replace)|在字符串中查找匹配的子串，并替换与正则表达式匹配的子串||
|[split()](#split)|把字符串分割为字符串数组|字符串转数组|
|[localeCompare()](#localecompare-方法)|比较两个字符串的字符顺序||

## JavaScript 字符

### charAt()
`charAt()` 方法返回给定索引位置的字符，由传给方法的整数参数指定：

```
let message = "abcde";

console.log(message.charAt(2)); // "c" 
```

### charCodeAt()
JavaScript 字符串使用了两种 Unicode 编码混合的策略：UCS-2 和 UTF-16。对于可以采用 16 位编码的字符（U+0000~U+FFFF），这两种编码实际上是一样的。

使用 `charCodeAt()` 方法可以查看指定码元的字符编码。这个方法返回指定索引位置的码元值，索引以整数指定。比如：

```
let message = "abcde";

// Unicode "Latin small letter C"的编码是 U+0063
console.log(message.charCodeAt(2)); // 99
// 十进制 99 等于十六进制 63
console.log(99 === 0x63); // true
```

## 字符串操作方法

### concat()
`concat()` 用于将一个或多个字符串拼接成一个新字符串。来看下面的例子：

```
let stringValue = "hello ";
let result = stringValue.concat("world");

console.log(result); // "hello world"
console.log(stringValue); // "hello"
```

在这个例子中，对 stringValue 调 用 concat()方法的结果是得到"hello world"， 但
stringValue 的值保持不变。concat()方法可以接收任意多个参数，因此可以一次性拼接多个字符串，如下所示：

```
let stringValue = "hello ";
let result = stringValue.concat("world", "!");

console.log(result); // "hello world!"
console.log(stringValue); // "hello"
```

这个修改后的例子将字符串"world"和"!"追加到了"hello "后面。

虽然 `concat()` 方法可以拼接字符串，但更常用的方式是使用加号操作符（`+`）。而且多数情况下，对于拼接多个字符串来说，使用加号更方便：

```
let stringValue = "hello ";
let result = stringValue + "world";

console.log(result); // "hello world"
```

### slice()、substr() 和 substring()
ECMAScript 提供了 3 个从字符串中提取子字符串的方法：`slice()`、`substr()` 和 `substring()`。

这3个方法都返回调用它们的字符串的一个子字符串，而且都接收一或两个参数。第一个参数表示子字符串开始的位置，第二个参数表示子字符串结束的位置。

对 `slice()` 和 `substring()` 而言，第二个参数是提取结束的位置（即该位置之前的字符会被提取出来）。对 `substr()` 而言，第二个参数表示返回的子字符串数量。任何情况下，省略第二个参数都意味着提取到字符串末尾。

与 `concat()` 方法一样，`slice()`、`substr()` 和 `substring()` 也不会修改调用它们的字符串，而只会返回提取到的原始新字符串值。

来看下面的例子：

```
let stringValue = "hello world";

console.log(stringValue.slice(3)); // "lo world"
console.log(stringValue.substring(3)); // "lo world"
console.log(stringValue.substr(3)); // "lo world"
console.log(stringValue.slice(3, 7)); // "lo w"
console.log(stringValue.substring(3,7)); // "lo w"
console.log(stringValue.substr(3, 7)); // "lo worl"
```

在这个例子中，`slice()`、`substr()` 和 `substring()` 是以相同方式被调用的，而且多数情况下返回的值也相同。如果只传一个参数 3，则所有方法都将返回"lo world"，因为"hello"中"l"位置为 3。如果传入两个参数 3 和 7，则 `slice()` 和 `substring()` 返回"lo w"（因为"world"中"o"在位置 7，不包含），而 `substr()` 返回"lo worl"，因为第二个参数对它而言表示返回的字符数。

当某个参数是负值时，这 3 个方法的行为又有不同。比如，`slice()` 方法将所有负值参数都当成字符串长度加上负参数值。

而 `substr()` 方法将第一个负参数值当成字符串长度加上该值，将第二个负参数值转换为 0。
`substring()` 方法会将所有负参数值都转换为 0。看下面的例子：

```
let stringValue = "hello world";

console.log(stringValue.slice(-3)); // "rld"
console.log(stringValue.substring(-3)); // "hello world"
console.log(stringValue.substr(-3)); // "rld"
console.log(stringValue.slice(3, -4)); // "lo w"
console.log(stringValue.substring(3, -4)); // "hel"
console.log(stringValue.substr(3, -4)); // ""
```

这个例子明确演示了 3 个方法的差异。在给 `slice()` 和 `substr()` 传入负参数时，它们的返回结果相同。这是因为-3 会被转换为 8（长度加上负参数），实际上调用的是 `slice(8)` 和 `substr(8)`。而 `substring()` 方法返回整个字符串，因为-3 会转换为 0。

在第二个参数是负值时，这 3 个方法各不相同。`slice()` 方法将第二个参数转换为 7，实际上相当于调用 `slice(3, 7)`，因此返回"lo w"。而 `substring()` 方法会将第二个参数转换为 0，相当于调用 `substring(3, 0)`，等价于 `substring(0, 3)`，这是因为这个方法会将较小的参数作为起点，将较大的参数作为终点。对 `substr()` 来说，第二个参数会被转换为 0，意味着返回的字符串包含零个字符，因而会返回一个空字符串。

## 字符串位置方法

### indexOf() 和 lastIndexOf()
有两个方法用于在字符串中定位子字符串：`indexOf()` 和 `lastIndexOf()`。这两个方法从字符串中搜索传入的字符串，并返回位置（如果没找到，则返回-1）。

两者的区别在于，`indexOf()` 方法从字符串开头开始查找子字符串，而 `lastIndexOf()` 方法从字符串末尾开始查找子字符串。来看下面的例子：

```
let stringValue = "hello world";

console.log(stringValue.indexOf("o")); // 4
console.log(stringValue.lastIndexOf("o")); // 7
```

这里，字符串中第一个"o"的位置是 4，即"hello"中的"o"。最后一个"o"的位置是 7，即"world"
中的"o"。如果字符串中只有一个"o"，则 `indexOf()` 和 `lastIndexOf()` 返回同一个位置。

这两个方法都可以接收可选的第二个参数，表示开始搜索的位置。这意味着，`indexOf()` 会从这个参数指定的位置开始向字符串末尾搜索，忽略该位置之前的字符；`lastIndexOf()` 则会从这个参数指定的位置开始向字符串开头搜索，忽略该位置之后直到字符串末尾的字符。下面看一个例子：

```
let stringValue = "hello world";

console.log(stringValue.indexOf("o", 6)); // 7
console.log(stringValue.lastIndexOf("o", 6)); // 4
```

在传入第二个参数 6 以后，结果跟前面的例子恰好相反。这一次，`indexOf()` 返回 7，因为它从位置 6（字符"w"）开始向后搜索字符串，在位置 7 找到了"o"。而 `lastIndexOf()` 返回 4，因为它从位置 6 开始反向搜索至字符串开头，因此找到了"hello"中的"o"。

## 字符串包含方法

### startsWith()、endsWith() 和 includes()
这些方法都会从字符串中搜索传入的字符串，并返回一个表示是否包含的布尔值。它们的区别在于，`startsWith()` 检查开始于索引 0 的匹配项，`endsWith()` 检查开始于索引 (string.length - substring.length) 的匹配项，而 `includes()` 检查整个字符串：

```
let message = "foobarbaz";

console.log(message.startsWith("foo")); // true
console.log(message.startsWith("bar")); // false
console.log(message.endsWith("baz")); // true
console.log(message.endsWith("bar")); // false
console.log(message.includes("bar")); // true
console.log(message.includes("qux")); // false
```

`startsWith()` 和 `includes()` 方法接收可选的第二个参数，表示开始搜索的位置。如果传入第二个参数，则意味着这两个方法会从指定位置向着字符串末尾搜索，忽略该位置之前的所有字符。下面是一个例子：

```
let message = "foobarbaz";

console.log(message.startsWith("foo")); // true
console.log(message.startsWith("foo", 1)); // false
console.log(message.includes("bar")); // true
console.log(message.includes("bar", 4)); // false
```

`endsWith()` 方法接收可选的第二个参数，表示应该当作字符串末尾的位置。如果不提供这个参数，那么默认就是字符串长度。如果提供这个参数，那么就好像字符串只有那么多字符一样：

```
let message = "foobarbaz";

console.log(message.endsWith("bar")); // false
console.log(message.endsWith("bar", 6)); // true 
```

## trim() 方法
所有字符串上都提供了 `trim()` 方法。这个方法会创建字符串的一个副本，删除前、后所有空格符，再返回结果。比如：

```
let stringValue = " hello world ";
let trimmedStringValue = stringValue.trim();

console.log(stringValue); // " hello world "
console.log(trimmedStringValue); // "hello world" 
```

由于 `trim()` 返回的是字符串的副本，因此原始字符串不受影响，即原本的前、后空格符都会保留。

另外，`trimLeft()` 和 `trimRight()` 方法分别用于清理字符串开头和末尾的空格符。

##  repeat() 方法
所有字符串上都提供了 `repeat()` 方法。这个方法接收一个整数参数，表示要将字符串复制多少次，然后返回拼接所有副本后的结果。

```
let stringValue = "na ";

console.log(stringValue.repeat(16) + "batman");
// na na na na na na na na na na na na na na na na batman
```

## padStart() 和 padEnd() 方法
`padStart()` 和 `padEnd()` 方法会复制字符串，如果小于指定长度，则在相应一边填充字符，直至满足长度条件。这两个方法的第一个参数是长度，第二个参数是可选的填充字符串，默认为空格

```
let stringValue = "foo";

console.log(stringValue.padStart(6)); // "   foo"
console.log(stringValue.padStart(9, ".")); // "......foo"
console.log(stringValue.padEnd(6)); // "foo   "
console.log(stringValue.padEnd(9, ".")); // "foo......" 
```

可选的第二个参数并不限于一个字符。如果提供了多个字符的字符串，则会将其拼接并截断以匹配指定长度。此外，如果长度小于或等于字符串长度，则会返回原始字符串。

```
let stringValue = "foo";

console.log(stringValue.padStart(8, "bar")); // "barbafoo"
console.log(stringValue.padStart(2)); // "foo"
console.log(stringValue.padEnd(8, "bar")); // "foobarba"
console.log(stringValue.padEnd(2)); // "foo" 
```

## 字符串迭代与解构
在 for-of 循环中可以通过这个迭代器按序访问每个字符：

```
for (const item of "abcde") {
  console.log(item);
}

// a
// b
// c
// d
// e 
```

有了这个迭代器之后，字符串就可以通过解构操作符来解构了。比如，可以更方便地把字符串分割为字符数组：

```
let message = "abcde";

console.log([...message]); // ["a", "b", "c", "d", "e"]
```

## 字符串大小写转换

### toLowerCase()
用于把字符串转换为小写

```
let msg = "Hello World";

console.log(msg.toLowerCase()); // "hello world"
```

### toUpperCase()
用于把字符串转换为大写

```
let msg = "Hello World";

console.log(msg.toUpperCase()); // "HELLO WORLD"
```

## 字符串模式匹配方法

### match()
`match()` 方法接收一个参数，可以是一个正则表达式字符串，也可以是一个 RegExp 对象。来看下面的例子：

```
let text = "cat, bat, sat, fat";
let pattern = /.at/;
let matches = text.match(pattern);

console.log(matches.index); // 0
console.log(matches[0]); // "cat"
```

### search()
这个方法唯一的参数与 `match()` 方法一样：正则表达式字符串或 RegExp 对象。这个方法返回模式第一个匹配的位置索引，如果没找到则返回 -1。`search()` 始终从字符串开头向后匹配模式。看下面的例子：

```
let text = "cat, bat, sat, fat";
let pos = text.search(/at/);

console.log(pos); // 1 
```

这里，`search(/at/)` 返回 1，即"at"的第一个字符在字符串中的位置。


### replace()
为简化子字符串替换操作，JavaScript 提供了 `replace()` 方法。

这个方法接收两个参数，第一个参数可以是一个 RegExp 对象或一个字符串（这个字符串不会转换为正则表达式），第二个参数可以是一个字符串或一个函数。

如果第一个参数是字符串，那么只会替换第一个子字符串。要想替换所有子字符串，第一个参数必须为正则表达式并且带全局标记，如下面的例子所示：

```
let text = "cat, bat, sat, fat";
let result = text.replace("at", "ond");

console.log(result); // "cond, bat, sat, fat"
result = text.replace(/at/g, "ond");
console.log(result); // "cond, bond, sond, fond"
```

在这个例子中，字符串"at"先传给 `replace()` 函数，而替换文本是"ond"。结果是"cat"被修改为"cond"，而字符串的剩余部分保持不变。通过将第一个参数改为带全局标记的正则表达式，字符串中的所有"at"都被替换成了"ond"。

### split()
`split()` 方法会根据传入的分隔符将字符串拆分成数组。

作为分隔符的参数可以是字符串，也可以是 RegExp 对象。（字符串分隔符不会被这个方法当成正则表达式。）还可以传入第二个参数，即数组大小，确保返回的数组不会超过指定大小。

来看下面的例子：

```
let colorText = "red,blue,green,yellow";
let colors1 = colorText.split(","); // ["red", "blue", "green", "yellow"]
let colors2 = colorText.split(",", 2); // ["red", "blue"]
```

在这里，字符串 colorText 是一个逗号分隔的颜色名称符串。调用 `split(",")` 会得到包含这些颜色名的数组，基于逗号进行拆分。要把数组元素限制为 2 个，传入第二个参数 2 即可。

## localeCompare() 方法
最后一个方法是 `localeCompare()`，这个方法比较两个字符串，返回如下 3 个值中的一个
+ 如果按照字母表顺序，字符串应该排在字符串参数前头，则返回负值。（通常是 -1，具体还要看与实际值相关的实现。）
+ 如果字符串与字符串参数相等，则返回 0。
+ 如果按照字母表顺序，字符串应该排在字符串参数后头，则返回正值。（通常是 1，具体还要看与实际值相关的实现。）

`localeCompare()` 区分大小写, 同字母小写在前, 大写在后

下面是一个例子：

```
let stringValue = "bcd";

stringValue.localeCompare("abc"); // 1
stringValue.localeCompare("bc"); // 1
stringValue.localeCompare("bcd"); // 0
stringValue.localeCompare("bcde"); // -1
stringValue.localeCompare("cd"); // -1
stringValue.localeCompare("Bcd"); // -1
```
