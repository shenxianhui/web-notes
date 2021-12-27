<!--
 * @Description: RegExp 正则
 * @Author: shenxh
 * @Date: 2021-12-24 14:10:48
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-27 16:14:03
-->

- [RegExp](#regexp)

# RegExp
ECMAScript 通过 RegExp 类型支持正则表达式。正则表达式使用类似 Perl 的简洁语法来创建：

```
let expression = /pattern/flags;
```

这个正则表达式的 pattern（模式）可以是任何简单或复杂的正则表达式，包括字符类、限定符、分组、向前查找和反向引用。每个正则表达式可以带零个或多个 flags（标记），用于控制正则表达式的行为。下面给出了表示匹配模式的标记。
+ g：全局模式，表示查找字符串的全部内容，而不是找到第一个匹配的内容就结束
+ i：不区分大小写，表示在查找匹配时忽略 pattern 和字符串的大小写
+ m：多行模式，表示查找到一行文本末尾时会继续查找
+ y：粘附模式，表示只查找从 lastIndex 开始及之后的字符串
+ u：Unicode 模式，启用 Unicode 匹配
+ s：dotAll 模式，表示元字符.匹配任何字符（包括 `\n` 或 `\r`）

使用不同模式和标记可以创建出各种正则表达式，比如：

```
// 匹配字符串中的所有"at"
let pattern1 = /at/g;

// 匹配第一个"bat"或"cat"，忽略大小写
let pattern2 = /[bc]at/i;

// 匹配所有以"at"结尾的三字符组合，忽略大小写
let pattern3 = /.at/gi; 
```

与其他语言中的正则表达式类似，所有元字符在模式中也必须转义，包括

`(` `[` `{` `\` `^` `$` `|` `)` `]` `}` `?` `*` `+` `.`

元字符在正则表达式中都有一种或多种特殊功能，所以要匹配上面这些字符本身，就必须使用反斜杠来转义。下面是几个例子：

```
// 匹配第一个"bat"或"cat"，忽略大小写
let pattern1 = /[bc]at/i;

// 匹配第一个"[bc]at"，忽略大小写
let pattern2 = /\[bc\]at/i;

// 匹配所有以"at"结尾的三字符组合，忽略大小写
let pattern3 = /.at/gi;

// 匹配所有".at"，忽略大小写
let pattern4 = /\.at/gi;
```

这里的 pattern1 匹配 "bat" 或 "cat"，不区分大小写。要直接匹配 "[bc]at"，左右中括号都必须像 pattern2 中那样使用反斜杠转义。在 pattern3 中，点号表示 "at" 前面的任意字符都可以匹配。如果想匹配 ".at"，那么要像 pattern4 中那样对点号进行转义。

前面例子中的正则表达式都是使用字面量形式定义的。正则表达式也可以使用 `RegExp` 构造函数来创建，它接收两个参数：模式字符串和（可选的）标记字符串。任何使用字面量定义的正则表达式也可以通过构造函数来创建，比如：

```
// 匹配第一个"bat"或"cat"，忽略大小写
let pattern1 = /[bc]at/i;

// 跟 pattern1 一样，只不过是用构造函数创建的
let pattern2 = new RegExp("[bc]at", "i");
```

附: [正则表达式速查表](https://www.jb51.net/shouce/jquery1.82/regexp.html)
