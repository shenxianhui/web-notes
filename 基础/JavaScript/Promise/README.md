<!--
 * @Description: Promise
 * @Author: shenxh
 * @Date: 2021-12-31 10:23:05
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-31 10:56:52
-->

- [Promise 的含义](#promise-的含义)
- [基本用法](#基本用法)
  - [创建](#创建)
  - [使用](#使用)
- [实战](#实战)

# Promise 的含义
所谓 `Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，`Promise` 是一个对象，从它可以获取异步操作的消息。`Promise` 提供统一的 API，各种异步操作都可以用同样的方法进行处理。 

`Promise` 对象有以下两个特点：
- 对象的状态不受外界影响
- 一旦状态改变，就不会再变，任何时候都可以得到这个结果

`Promise` 也有一些缺点：
- 一旦新建它就会立即执行，无法中途取消
- 如果不设置回调函数，`Promise` 内部抛出的错误，不会反应到外部
- 当处于 `pending` 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

有了 `Promise` 对象，就可以将**异步**操作以**同步**操作的流程表达出来，避免了层层嵌套的回调函数。

# 基本用法
ES6 规定，`Promise` 对象是一个构造函数，用来生成 `Promise` 实例

## 创建
首先, 我们来创建一个 `Promise` 实例

```
const promise = new Promise((resolve, reject) => {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

`Promise` 构造函数接受一个函数作为参数，该函数的两个参数分别是 `resolve` 和 `reject`。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

`resolve` 函数的作用是，将 `Promise` 对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；`reject` 函数的作用是，将 `Promise` 对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

## 使用
`Promise` 实例生成以后，可以用 `then` 和 `catch` 方法分别指定 `resolved` 状态和 `rejected` 状态的回调函数。

```
promise.then(res => {
  // success
}).catch(err => {
  // error
});
```

# 实战
举个栗子:

现在有个需求: 有两个函数 fn1 和 fn2, 需要等 fn1 执行完后再执行 fn2, 按照下面的写法显然是无法实现的

```
const fn1 = () => {
  setTimeout(() => {
    console.log('fn1 执行完毕');
  }, 500);
}

const fn2 = () => {
  fn1();

  console.log('fn2 执行完毕');
}

fn2();

// fn2 执行完毕
// fn1 执行完毕
```

这种情况我们可以借助 `Promise` 实现:

```
// 将 fn1 改成 Promise 实例
const fn1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('fn1 执行完毕');

      resolve(); // 操作成功
    }, 500);
  });
}

// fn1 使用 then 方法实现代码同步执行
const fn2 = () => {
  fn1().then(res => {
    console.log('fn2 执行完毕');
  });
}

fn2();

// fn1 执行完毕
// fn2 执行完毕
```

> 附 [Promise 文档](https://es6.ruanyifeng.com/#docs/promise)
