<!--
 * @Author: shenxh
 * @Date: 2021-12-13 17:06:50
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-15 15:51:22
 * @Description: CSS 创建
-->

- [插入样式表的方法](#插入样式表的方法)
  - [行内样式/内联样式](#行内样式内联样式)
  - [内嵌式/嵌入式](#内嵌式嵌入式)
  - [外链式 (推荐)](#外链式-推荐)
- [样式优先级](#样式优先级)

# 插入样式表的方法
## 行内样式/内联样式
要使用行内样式，需要在相关标签内使用 `style` 属性

```
<div style="font-size: 28px; color: #f00;">示例</div>
```

> 注: 由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势, 请**慎用**这种方法

## 内嵌式/嵌入式
当单个文档需要特殊的样式时，就应该使用内嵌式

可以使用 `<style>` 标签在文档头部定义内部样式表

```
<style>
    div {
        font-size: 28px;
        color: #f00;
    }
</style>
```

## 外链式 (推荐)
当样式需要应用于很多页面时，外部样式表将是理想的选择

项目开发中使用外链式将利于维护

每个页面使用 `<link>` 标签链接到样式表, `<link>` 标签在（文档的）头部

+ 样式文件 `myStyle.css`
```
div {
  font-size: 28px;
  color: #f00;
}
```
+ 演示文件 `index.html`
```
<!DOCTYPE html>
<html lang="en">
    <head>
        <!-- 引入公共样式 -->
        <link rel="stylesheet" href="./myStyle.css" />
    </head>
    <body>
        <div>示例</div>
    </body>
</html>

```

# 样式优先级
不考虑 `!important`, 从高到低依次为:
+ 行内样式
+ 内嵌式
+ 外链式

