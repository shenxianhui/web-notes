<!--
 * @Author: shenxh
 * @Date: 2021-12-17 11:02:24
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-17 13:38:56
 * @Description: 创建
-->

- [行内脚本/内联脚本](#行内脚本内联脚本)
- [内嵌式/嵌入式](#内嵌式嵌入式)
- [外链式 (推荐)](#外链式-推荐)

# 行内脚本/内联脚本
要在行内创建的话, 要在属性值内用 `javascript`

比如, 我们给一个按钮赋予一个行为弹窗
```
<button onclick="javascript: alert('来咬我啊, 笨蛋~')">点我</button>
```

> 注: 由于要将脚本和内容混杂在一起，内联脚本会损失掉脚本表的许多优势, 请**慎用**这种方法

# 内嵌式/嵌入式
使用 `<script>` 标签在文档尾部定义
```
<button onclick="handleBtn()">点我</button>
```
```
<script>
    // 按钮点击事件
    function handleBtn() {
        alert('来咬我啊, 笨蛋~');
    }
</script>
```

# 外链式 (推荐)
使用 `<script>` 标签在文档尾部定义, 同一个页面可以插入多个

当脚本需要应用于很多页面时，外部脚本表将是理想的选择

项目开发中使用外链式将利于维护

+ 演示文件 `index.html`
```
<!DOCTYPE html>
<html lang="en">
    <body>
        <button onclick="handleBtn()">点我</button>

        <script src="./myJavaScript.js"></script>
    </body>
</html>

```
+ 脚本文件 `myJavaScript.js`
```
// 按钮点击事件
function handleBtn() {
    alert('来咬我啊, 笨蛋~');
}
```

> 注: 无论内嵌式还是外链式, 原则上来说, 将 `<script>` 标签插入至 `<head>` 中和 `<body>` 中都可以, 但页面会先加载 `<head>` 部分, 所以当脚本内容过大时, 会影响页面渲染速度, 此时在页面内容出来之前, 会有一段时间的"白屏", 所以我们一般将 `<script>` 标签插入至 `<body>` 结尾, 以保证页面内容出来后再加载脚本文件, 提高用户体验