<!--
 * @Description: 浏览器缓存
 * @Author: shenxh
 * @Date: 2021-12-29 16:07:46
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-29 16:21:05
-->

- [浏览器缓存](#浏览器缓存)
  - [localstorage 和 sessionstorage](#localstorage-和-sessionstorage)
    - [储存数据](#储存数据)
    - [取出数据](#取出数据)
    - [修改数据](#修改数据)
    - [删除数据](#删除数据)
    - [清除数据](#清除数据)
  - [cookie](#cookie)
    - [储存数据](#储存数据-1)
    - [取出数据](#取出数据-1)

# 浏览器缓存
当用户登录后, 我们一般把登录者的信息统一储存在缓存中 (F12 调试工具 > Application > Storage 中查看)

常用的方式一般有三种: `localStorage`、`sessionStorage` 和 `Cookie`, 它们区别如下:
- `localStorage`: `localStorage` 的生命周期是永久的，关闭页面或浏览器之后 `localStorage` 中的数据也不会消失。`localStorage` **除非主动删除数据，否则数据永远不会消失**
- `sessionStorage`: `sessionStorage` 的生命周期是仅在当前会话下有效。`sessionStorage` 引入了一个“浏览器窗口”的概念，`sessionStorage` 是在同源的窗口中始终存在的数据。只要这个浏览器窗口没有关闭，即使刷新页面或者进入同源另一个页面，数据依然存在。但是 `sessionStorage` **在关闭了浏览器窗口后就会被销毁**。同时独立的打开同一个窗口同一个页面，`sessionStorage` 也是不一样的
- `cookie`: `cookie` 生命期为只在设置的 `cookie` 过期时间之前一直有效，即使窗口或浏览器关闭。存放数据大小为4K左右, 有个数限制（各浏览器不同），一般不能超过20个。缺点是**不能储存大数据且不易读取**

## localstorage 和 sessionstorage
首先要判断浏览器是否支持 `localStorage` / `sessionStorage`

比如判断 `localStorage` :
```
if (window.localStorage) {
    alert('浏览支持 localStorage');
} else {
    alert('浏览暂不支持 localStorage');
}
```

### 储存数据

用途: 将 `value` 存储到 `key` 字段

用法: `setItem(key, value)`

代码示例

```
sessionStorage.setItem('name', '张三');
localStorage.setItem('name', '张三');
```

> 注: 如果需要储存数组或对象的话, 可以用 JSON格 式传入

### 取出数据

用途: 获取指定 `key` 本地存储的值

用法: `getItem(key)`

代码示例

```
sessionStorage.getItem('name'); // 张三
localStorage.getItem('name'); // 张三
```

### 修改数据

用途: 修改指定 `key` 本地存储的值

用法: `setItem(key)`

代码示例

```
sessionStorage.setItem('name', '李四');
localStorage.setItem('name', '李四');
```

### 删除数据

用途: 删除指定 `key` 本地存储的值

用法: `removeItem(key)`

代码示例

```
sessionStorage.removeItem('name');
localStorage.removeItem('name');
```

### 清除数据

用途: 清除所有本地存储的数据

用法: `clear()`

代码示例

```
sessionStorage.clear();
localStorage.clear();
```

## [cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie)

### 储存数据

```
window.document.cookie = 'key=val';
```

### 取出数据

```
document.cookie
```

示例

```
// 设置 Cookie
setCookie(key, val, days) {
  let date = new Date(); // 获取时间
  date.setTime(date.getTime() + 24 * 60 * 60 * 1000 * days);
  // 字符串拼接 Cookie
  window.document.cookie = `${key}=${val};path=/;expires=${date.toGMTString()};`;
}
```
```
// 获取 Cookie
getCookie() {
  let cookie = document.cookie.split(';');
}
```
```
// 清除Cookie
clearCookie() {
  this.setCookie('', '', -1);
}
```
