<!--
 * @Description: WebSocket
 * @Author: shenxh
 * @Date: 2021-12-30 11:48:19
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-31 10:05:16
-->

- [WebSocket](#websocket)
  - [构造函数 WebSocket()](#构造函数-websocket)
    - [语法](#语法)
    - [参数](#参数)
  - [属性](#属性)
  - [方法](#方法)
  - [事件](#事件)
  - [示例](#示例)

# WebSocket
WebSocket 对象提供了用于创建和管理 WebSocket 连接，以及可以通过该连接发送和接收数据的 API。

使用 `WebSocket()` 构造函数来构造一个 WebSocket 。

## 构造函数 WebSocket()

### 语法
```
let ws = new WebSocket(url [, protocols]);
```

### 参数
- url
  - 要连接的URL；这应该是WebSocket服务器将响应的URL。
- protocols (可选)
  - 一个协议字符串或者一个包含协议字符串的数组。这些字符串用于指定子协议，这样单个服务器可以实现多个WebSocket子协议（例如，您可能希望一台服务器能够根据指定的协议（protocol）处理不同类型的交互）。如果不指定协议字符串，则假定为空字符串。

## 属性
|名称|说明|
|-|-|
|WebSocket.binaryType|使用二进制的数据类型连接|
|WebSocket.onclose|用于指定连接关闭后的回调函数|
|WebSocket.onerror|用于指定连接失败后的回调函数|
|WebSocket.onmessage|用于指定当从服务器接受到信息时的回调函数|
|WebSocket.onopen|用于指定连接成功后的回调函数|

## 方法
|名称|说明|
|-|-|
|WebSocket.close()|关闭当前链接|
|WebSocket.send(data)|对要传输的数据进行排队|

## 事件
使用 `addEventListener()` 或将一个事件监听器赋值给本接口的 `oneventname` 属性，来监听下面的事件。

|名称|说明|
|-|-|
|close|当一个 WebSocket 连接被关闭时触发<br />也可以通过 `onclose` 属性来设置|
|error|当一个 WebSocket 连接因错误而关闭时触发，例如无法发送数据时<br />也可以通过 `onerror` 属性来设置|
|message|当通过 WebSocket 收到数据时触发<br />也可以通过 onmessage 属性来设置|
|open|当一个 WebSocket 连接成功时触发<br />也可以通过 `onopen` 属性来设置|

## 示例
```
// 创建 WebSocket 实例
const ws = new WebSocket('ws://localhost:8080');

// 开启
ws.onopen = () => {
  console.log('WebSocket 已开启');
}

// 发送消息
ws.send('这是一条消息');

// 获取消息
ws.onmessage = data => {
  console.log(data); // '这是一条消息'
}

// 关闭
ws.onclose = () => {
  console.log('WebSocket 已关闭');
}
```
