<!--
 * @Author: shenxh
 * @Date: 2021-12-16 13:32:42
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-16 13:32:52
 * @Description: HTML 快速创建多个标签
-->

- [手册](#手册)
  - [嵌套操作](#嵌套操作)
    - [子操作符: `>`](#子操作符-)
    - [并列操作符: `+`](#并列操作符-)
    - [上级操作符: `^`](#上级操作符-)
    - [重复操作符: `*`](#重复操作符-)
    - [分组操作符: `()`](#分组操作符-)
  - [属性操作](#属性操作)
    - [选择器: `id` 和 `class`](#选择器-id-和-class)
    - [属性值: `[key=value]`](#属性值-keyvalue)
    - [数列值: <code>$</code>](#数列值-)
    - [数列操作符: `@`](#数列操作符-)
  - [字符操作](#字符操作)
    - [字符操作: `{}`](#字符操作-)
- [总结](#总结)
  - [可省略标签的元素](#可省略标签的元素)
    - [`div`](#div)
    - [`li`](#li)
    - [`tr` `th` `td`](#tr-th-td)

> 使用说明: 在编辑器中输入快捷指令后, 按"Tab"键即可快速生成对应的标签组

# 手册

## 嵌套操作

### 子操作符: `>`
+ `ul>li`
```
<ul>
  <li></li>
</ul>
```

### 并列操作符: `+`
+ `div+span`
```
<div></div>
<span></span>
```

### 上级操作符: `^`
+ `div>h1^span`
```
<div>
  <h1></h1>
</div>
<span></span>
```
+ `div>ul>li>i^^span`
```
<div>
  <ul>
    <li><i></i></li>
  </ul>
  <span></span>
</div>
```

### 重复操作符: `*`
+ `ul>li*3`
```
<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

### 分组操作符: `()`
+ `div>(p>span)*2`
```
<div>
  <p><span></span></p>
  <p><span></span></p>
</div>
```

## 属性操作

### 选择器: `id` 和 `class`
+ `div#header+div.main+div#footer`
```
<div id="header"></div>
<div class="main"></div>
<div id="footer"></div>
```

### 属性值: `[key=value]`
+ `a[title=test target=_blank]`
```
<a href="" title="test" target="_blank"></a>
```

### 数列值: <code>$</code>
+ `h$.title$*5`

```
<h1 class="title1"></h1>
<h2 class="title2"></h2>
<h3 class="title3"></h3>
<h4 class="title4"></h4>
<h5 class="title5"></h5>
```
+ `h$.title$$*5`
```
<h1 class="title01"></h1>
<h2 class="title02"></h2>
<h3 class="title03"></h3>
<h4 class="title04"></h4>
<h5 class="title05"></h5>
```

### 数列操作符: `@`
+ `h$@-*3`
+ `h$@-1*3`
```
<h3></h3>
<h2></h2>
<h1></h1>
```
+ `h$@2*3`
```
<h2></h2>
<h3></h3>
<h4></h4>
```
+ `h$@-2*3`
```
<h4></h4>
<h3></h3>
<h2></h2>
```

## 字符操作

### 字符操作: `{}`
+ `span{文本内容}`
```
<span>文本内容</span>
```

# 总结

## 可省略标签的元素

### `div`
+ `.header+.footer` 等价于 `div.header+div.footer`
```
<div class="header"></div>
<div class="footer"></div>
```

### `li`
+ `ul>.item*3` 等价于 `ul>li.item*3`
```
<ul>
  <li class="item"></li>
  <li class="item"></li>
  <li class="item"></li>
</ul>
```

### `tr` `th` `td`
+ `table>(.row>.col-h*3)+(.row*2>.col-d*3)` 等价于 `table>(tr.row>th.col-h*3)+(tr.row*2>td.col-d*3)`
```
<table>
  <tr class="row">
    <td class="col-h"></td>
    <td class="col-h"></td>
    <td class="col-h"></td>
  </tr>
  <tr class="row">
    <td class="col-d"></td>
    <td class="col-d"></td>
    <td class="col-d"></td>
  </tr>
  <tr class="row">
    <td class="col-d"></td>
    <td class="col-d"></td>
    <td class="col-d"></td>
  </tr>
</table>
```
