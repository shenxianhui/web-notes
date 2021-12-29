<!--
 * @Description: 定时器
 * @Author: shenxh
 * @Date: 2021-12-29 10:42:07
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-29 11:06:33
-->

- [定时器](#定时器)
  - [setTimeout() 与 clearTimeout()](#settimeout-与-cleartimeout)
  - [setInterval() 与 clearInterval()](#setinterval-与-clearinterval)

# 定时器
JavaScript 在浏览器中是单线程执行的，但允许使用定时器指定在某个时间之后或每隔一段时间就执行相应的代码。

`setTimeout()` 用于指定在一定时间后执行某些代码，而 `setInterval()` 用于指定每隔一段时间执行某些代码。

## setTimeout() 与 clearTimeout()
`setTimeout()` 方法通常接收两个参数：要执行的代码和在执行回调函数前等待的时间（毫秒）。第一个参数可以是包含 JavaScript 代码的字符串或者一个函数，比如：

```
// 1 秒后会打印一次 "Hello world!"
setTimeout(() => console.log("Hello world!"), 1000);
```

第二个参数是要等待的毫秒数，而不是要执行代码的确切时间。

JavaScript 是单线程的，所以每次只能执行一段代码。为了调度不同代码的执行，JavaScript 维护了一个任务队列。其中的任务会按照添加到队列的先后顺序执行。`setTimeout()` 的第二个参数只是告诉 JavaScript 引擎在指定的毫秒数过后把任务添加到这个队列。如果队列是空的，则会立即执行该代码。如果队列不是空的，则代码必须等待前面的任务执行完才能执行。

调用 `setTimeout()` 时，会返回一个表示该超时排期的数值 ID。这个超时 ID 是被排期执行代码的唯一标识符，可用于取消该任务。要取消等待中的排期任务，可以调用 `clearTimeout()` 方法并传入超时 ID，如下面的例子所示：

```
// 创建定时器
let timer = setTimeout(() => console.log("Hello world!"), 1000);

// 清除定时器
clearTimeout(timer);
```

只要是在指定时间到达之前调用 `clearTimeout()`，就可以取消超时任务。在任务执行后再调用`clearTimeout()` 没有效果。

> 注: 所有超时执行的代码（函数）都会在全局作用域中的一个匿名函数中运行，因此函数中的 `this` 值在非严格模式下始终指向 `window`，而在严格模式下是 `undefined`。如果给 `setTimeout()` 提供了一个箭头函数，那么 `this` 会保留为定义它时所在的词汇作用域。

## setInterval() 与 clearInterval()
`setInterval()` 与 `setTimeout()` 的使用方法类似，只不过指定的任务会每隔指定时间就执行一次，直到取消循环定时或者页面卸载。

`setInterval()` 同样可以接收两个参数：要执行的代码（字符串或函数），以及把下一次执行定时代码的任务添加到队列要等待的时间（毫秒）。下面是一个例子：

```
// 每隔 1 秒就会打印一次 "Hello world!"
setInterval(() => console.log("Hello world!"), 1000); 
```

`setInterval()` 方法也会返回一个循环定时 ID，可以用于在未来某个时间点上取消循环定时。要取消循环定时，可以调用 `clearInterval()` 并传入定时 ID。相对于 `setTimeout()` 而言，取消定时的能力对 `setInterval()` 更加重要。毕竟，如果一直不管它，那么定时任务会一直执行到页面卸载。下面是一个常见的例子：

```
let timer = null;
let num = 0;
let max = 10;

// 创建定时器
timer = setInterval(() => {
  num++;

  // 如果达到最大值，则取消所有未执行的任务
  if (num == max) {
    console.log("Done");

    // 清除定时器
    clearInterval(timer);
  }
}, 500);
```

在这个例子中，变量 num 会每半秒递增一次，直至达到最大限制值。
