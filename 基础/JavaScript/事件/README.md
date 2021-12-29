<!--
 * @Description: 事件
 * @Author: shenxh
 * @Date: 2021-12-29 11:13:37
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-29 15:53:17
-->

- [事件](#事件)
  - [用法示例](#用法示例)
  - [addEventListener() 和 removeEventListener()](#addeventlistener-和-removeeventlistener)
  - [阻止默认行为](#阻止默认行为)
  - [事件冒泡及捕获](#事件冒泡及捕获)
  - [事件委托](#事件委托)
  - [常用事件总结](#常用事件总结)
    - [资源事件](#资源事件)
    - [网络事件](#网络事件)
    - [焦点事件](#焦点事件)
    - [WebSocket 事件](#websocket-事件)
    - [表单事件](#表单事件)
    - [视图事件](#视图事件)
    - [剪贴板事件](#剪贴板事件)
    - [键盘事件](#键盘事件)
    - [鼠标事件](#鼠标事件)
    - [拖放事件](#拖放事件)

# 事件

> 附 [MDN 事件参考文档](https://developer.mozilla.org/zh-CN/docs/Web/Events)

在 Web 中, 事件在浏览器窗口中被触发并且通常被绑定到窗口内部的特定部分 — 可能是一个元素、一系列元素、被加载到这个窗口的 HTML 代码或者是整个浏览器窗口。

## 用法示例
```
<button onclick="handleBtn()">按钮</button>
```
```
function handleBtn() {
  console.log('点击事件触发');
}
```

## addEventListener() 和 removeEventListener()
`addEventListener()` 方法将指定的监听器注册到 EventTarget 上，当该对象触发指定的事件时，指定的回调函数就会被执行。事件目标可以是一个文档上的元素 Element, Document 和 Window 或者任何其他支持事件的对象。

`addEventListener()` 常用参数:
- type: 表示监听事件类型的字符串
- listener: 当所监听的事件类型触发时，可以是一个对象或函数
- options: 可选. 一个指定有关 listener 属性的可选参数对象

如下所示:

```
<button id="btn">按钮</button>
```
```
const myBtn = document.getElementById('btn');

myBtn.addEventListener('click', handleBtn);

function handleBtn(evt) {
  console.log('点击事件触发');
  console.log('事件对象:', evt);
}
```
有时候在事件处理函数内部，您可能会看到一个固定指定名称的参数，例如 event，evt 或简单的 e。 这被称为**事件对象**，它被自动传递给事件处理函数，以提供额外的功能和信息。

这个机制带来了一些相较于旧方式的优点。有一个相对应的方法，`removeEventListener()`，这个方法移除事件监听器，参数与 `addEventListener()` 相同。

例如，下面的代码将会移除上个代码块中的事件监听器：

```
myBtn.removeEventListener('click', handleBtn);

// 此时再点击按钮就不会触发点击事件了
```

## 阻止默认行为
有时，你会遇到一些情况，你希望事件不执行它的默认行为。 

最常见的例子是Web表单，例如自定义注册表单。当你填写详细信息并按提交按钮时，自然行为是将数据提交到服务器上的指定页面进行处理，并将浏览器重定向到某种“成功消息”页面（或相同的页面，如果另一个没有指定）

当用户没有正确提交数据时，麻烦就来了。作为开发人员，你希望停止提交信息给服务器，并给他们一个错误提示，告诉他们什么做错了，以及需要做些什么来修正错误。

一些浏览器支持自动的表单数据验证功能，但由于许多浏览器不支持，因此建议你不要依赖这些功能，并实现自己的验证检查。 我们来看一个简单的例子：

首先，一个简单的HTML表单，需要你填入名（first name）和姓（last name）

```
<form>
  <div>
    <label for="username">用户名: </label>
    <input id="username" type="text">
  </div>
  <div>
    <label for="password">密码: </label>
    <input id="password" type="password">
  </div>
  <div>
    <input id="submit" type="submit" value="提交">
  </div>
</form>
```

这里我们用一个 `onsubmit` 事件处理程序（在提交的时候，在一个表单上发起 submit 事件）来实现一个非常简单的检查，用于测试文本字段是否为空。

如果是，我们在事件对象上调用 `preventDefault()` 函数，这样就停止了表单提交，然后在我们表单下面的段落中显示一条错误消息，告诉用户什么是错误的：

```
const form = document.querySelector('form');
const username = document.getElementById('username');
const password = document.getElementById('password');

form.onsubmit = function(e) {
  if (username.value === '' || password.value === '') {
    alert('请输入用户名和密码');

    阻止默认行为
    e.preventDefault();
  }
}
```

## 事件冒泡及捕获
最后即将介绍的这个主题你常常不会深究，但如果你不理解这个主题，就会十分痛苦。

事件冒泡和捕捉是两种机制，主要描述当在一个元素上有两个相同类型的事件处理器被激活会发生什么。

为了容易理解，我们来看一个例子：

```
<div id="wrap" class="wrap">
  <button id="btn">按钮</button>
</div>
```
```
const wrap = document.getElementById('wrap');
const myBtn = document.getElementById('btn');

wrap.addEventListener('click', handleWrap);
myBtn.addEventListener('click', handleBtn);

function handleWrap() {
  console.log('点击 Wrap');
}
function handleBtn() {
  console.log('点击按钮');
}

// 点击按钮
// 点击 Wrap
```
当点击按钮时，你会发现同时触发了包裹它的其他元素事件。

这是令人讨厌的行为，但有一种方法来解决它！标准事件对象具有可用的名为 `stopPropagation()` 的函数, 当在事件对象上调用该函数时，它只会让当前事件处理程序运行，但事件不会在冒泡链上进一步扩大，因此将不会有更多事件处理器被运行(不会向上冒泡)。所以，我们可以通过改变前面代码块中的第二个处理函数来解决当前的问题:

```
function handleBtn(e) {
  console.log('点击按钮');

  // 阻止冒泡
  e.stopPropagation();
}

// 点击按钮
```

## 事件委托
冒泡还允许我们利用事件委托——这个概念依赖于这样一个事实,如果你想要在大量子元素中单击任何一个都可以运行一段代码，您可以将事件监听器设置在其父节点上，并让子节点上发生的事件冒泡到父节点上，而不是每个子节点单独设置事件监听器。

一个很好的例子是一系列列表项，如果你想让每个列表项被点击时弹出一条信息，您可以将 `click` 单击事件监听器设置在父元素 `<ul>` 上，这样事件就会从列表项冒泡到其父元素 `<ul>` 上。

## 常用事件总结

### 资源事件
|事件名称|何时触发|
|-|-|
|error|资源加载失败时|
|abort|正在加载资源已经被中止时|
|load|资源及其相关资源已完成加载|
|beforeunload|window，document 及其资源即将被卸载|
|unload|文档或一个依赖资源正在被卸载|

### 网络事件
|事件名称|何时触发|
|-|-|
|online|浏览器已获得网络访问|
|offline|浏览器已失去网络访问|

### 焦点事件
|事件名称|何时触发|
|-|-|
|focus|元素获得焦点（不会冒泡）|
|blur|元素失去焦点（不会冒泡）|

### WebSocket 事件
|事件名称|何时触发|
|-|-|
|open|WebSocket 连接已建立|
|message|通过 WebSocket 接收到一条消息|
|error|WebSocket 连接异常被关闭（比如有些数据无法发送）|
|close|WebSocket 连接已关闭|

### 表单事件
|事件名称|何时触发|
|-|-|
|reset|点击重置按钮时|
|submit|点击提交按钮|

### 视图事件
|事件名称|何时触发|
|-|-|
|fullscreenchange|全屏模式 (F11)|
|fullscreenerror|无法在全屏模式下查看元素时，即使它已被请求|
|resize|视图大小改变时|
|scroll|页面滚动时|

### 剪贴板事件
|事件名称|何时触发|
|-|-|
|cut|已经剪贴选中的文本内容并且复制到了剪贴板|
|copy|已经把选中的文本内容复制到了剪贴板|
|paste|从剪贴板复制的文本内容被粘贴|

### 键盘事件
|事件名称|何时触发|
|-|-|
|keydown|按下任意按键|
|keypress|除 Shift、Fn、CapsLock 外的任意键被按住（连续触发）|
|keyup|释放任意按键|

### 鼠标事件
|事件名称|何时触发|
|-|-|
|click|在元素上按下并释放任意鼠标按键|
|contextmenu|右键点击（在右键菜单显示前触发）|
|dblclick|在元素上双击鼠标按钮|
|mousedown|在元素上按下任意鼠标按钮|
|mouseenter|指针移到有事件监听的元素内|
|mouseleave|指针移出元素范围外（不冒泡）|
|mousemove|指针在元素内移动时持续触发|
|mouseover|指针移到有事件监听的元素或者它的子元素内|
|mouseout|指针移出元素，或者移到它的子元素上|
|mouseup|在元素上释放任意鼠标按键|
|pointerlockchange|鼠标被锁定或者解除锁定发生时|
|pointerlockerror|可能因为一些技术的原因鼠标锁定被禁止时|
|select|有文本被选中|
|wheel|滚轮向任意方向滚动|

### 拖放事件
|事件名称|何时触发|
|-|-|
|drag|正在拖动元素或文本选区（在此过程中持续触发，每 350ms 触发一次）|
|dragend|拖放操作结束。（松开鼠标按钮或按下 Esc 键）|
|dragenter|被拖动的元素或文本选区移入有效释放目标区|
|dragstart|用户开始拖动HTML元素或选中的文本|
|dragleave|被拖动的元素或文本选区移出有效释放目标区|
|dragover|被拖动的元素或文本选区正在有效释放目标上被拖动 （在此过程中持续触发，每350ms触发一次）|
|drop|元素在有效释放目标区上释放|
