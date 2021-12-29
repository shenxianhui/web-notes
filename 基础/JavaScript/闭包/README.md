<!--
 * @Description: 闭包
 * @Author: shenxh
 * @Date: 2021-12-29 11:08:49
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-29 11:08:50
-->

- [定义](#定义)
- [扩展](#扩展)

# 定义
闭包是指有权访问另一个函数作用域中的变量的函数

我的理解是，函数内的函数使用到外层函数的变量延长变量的生存时间，造成常驻内存

例子见下：
```
function foo() {
  var a = 2;
  return function() {
    a += 1;
    console.log(a);
  }
}

var baz = foo();

baz(); // 3
baz(); // 4
baz(); // 5
baz(); // 6
```
上面的例子中，外部的函数 `foo()` 执行完成之后，正常的情况下应该销毁 a 变量的，但是内部的返回的匿名函数使用到该变量，不能销毁

如果需要销毁的话，可以改写成下面：
```
function foo() {
  var a = 2;
  return function() {
    a += 1;
    console.log(a);
  }
}
var baz = foo();
baz(); // 3

baz = null; // 将内部的匿名函数赋值为空
```

# 扩展
谈到了闭包，这让我想起了不久前刷知乎看到一篇[文章](https://zhuanlan.zhihu.com/p/25855075)。自己整理如下：
```
for (var i = 0 ; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000)
}
console.log(i);

// 5,5,5,5,5,5
```
上面的代码是输出了6个5，而这6个5是这样执行的，先输出全局中的 `console.log(i)`，然后是过了1秒种后，瞬间输出了5个5（为什么用瞬间这个词呢，怕看者理解为每过一秒输出一个5）

解读上面的代码的话，可以通过狭义范围 (es5) 的理解：同步 => 异步 => 回调 （回调也是属于异步的范畴，所以我这里指明了狭义啦）

先是执行同步的 `for`, 遇到异步的 `setTimeout`(`setTimeout` 和 `setInterval` 属于异步) 后将其放入队列中等待，接着往下执行全局的 `console.log(i)`，将其执行完成后执行异步的队列

改写上面的代码，期望输出的结果为：5 => 0,1,2,3,4

+ 方法1
```
for (var i = 0; i < 5; i++) {
  (function(j){
    setTimeout(function() {
      console.log(j);
    }, 1000);
  })(i);
}
console.log(i);

// 5,0,1,2,3,4
```
上面的代码巧妙的利用 IIFE (Immediately Invoked Function Expression: 声明即执行的函数表达式) 来解决闭包造成的问题，闭包的解析看上面

+ 方法2

利用js中基本类型的参数传递是按值传递的特征
```
var output = function(i) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
};
for (var i = 0; i < 5; i++) {
  output(i); // 这里传过去的i值被复制了
}
console.log(i);

// 5,0,1,2,3,4
```
上面改造的两个方法都是执行代码后先输出5，然后过了一秒种依次输出 0,1,2,3,4

+ 方法3

如果不要考虑全局中的 console.log(i) 输出的5，而是循环中输出的 0,1,2,3,4。你还可以使用 ES6 的 `let` 块级作用域语法, 实现超级简单:
```
for (let i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}

// 0,1,2,3,4
```
上面是过了一秒钟后，依次输出 0,1,2,3,4。这种做法类似于无形中添加了闭包。那么，如果使用ES6语法的话，会怎样实现 5,0,1,2,3,4 呢？

改造刚开始的代码使得输出的结果是每隔一秒输出0,1,2,3,4，大概第五秒输出5

在不使用ES6的情况下：
```
for (var i = 0; i < 5; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j);
    }, 1000*j);
  })(i);
}
setTimeout(function() {
  console.log(i);
}, 1000*i);

// 0,1,2,3,4,5
```

上面的代码简单粗暴，但是不推荐。看题目是每隔一秒输出一个值，再回调实现最后的 5 输出，这个时候应该使用 ES6 语法来考虑，应该使用 `Promise` 方案：
```
const tasks = [];
for (var i = 0; i < 5; i++) { // 这里的i声明不能改成 let，改成 let 的话请看下一段代码
  (j => {
    tasks.push(new Promise(resolve => { // 执行tasks
      setTimeout(()=> {
        console.log(j);
        resolve(); // 这里一定要resolve,否则代码不会按照预期执行
      }, 1000*j);
    }))
  })(i);
}

Promise.all(tasks).then(()=>{ // 执行完tasks，回调
  setTimeout(() => {
    console.log(i);
  }, 1000);
});

// 符合要求的每隔一秒输出
// 0,1,2,3,4,5
```

如果是使用 `let`，我的改造如下：
```
const tasks = [];
for (let i = 0; i < 5; i++) {
  tasks.push(new Promise((resolve) => {
    setTimeout(() => {
      console.log(i);
      resolve();
    }, 1000 * i);
  }));
}

Promise.all(tasks).then(() => {
  setTimeout(() => {
    console.log(tasks.length);
  }, 1000);
});

// 0,1,2,3,4,5
```

上面的代码比较庞杂，可以将其颗粒话，模块化。对上面两段代码的带 `var` 那段进行改造后如下：
```
const tasks = []; // 这里存放异步操作的Promise
const output = i => new Promise(resolve => {
  setTimeout(() => {
    console.log(i);
  }, 1000*i);
});

// 生成全部的异步操作
for (var i = 0; i < 5; i++) {
  tasks.push(output(i));
}
// 异步操作完成之后，输出最后的i
Promise.all(tasks).then(() => {
  setTimeout(() => {
    console.log(i);
  }, 1000);
});

// 符合要求的每隔一秒输出
// 0,1,2,3,4,5
```

+ 方法4

既然ES6的 `Promise` 可以写，那么 ES7 是否可以写呢，从而让代码更加简洁易读？那就使用到到了异步操作的 `async await` 特性啦
```
// 模拟其他语言中的sleep，实际上可以是任何异步操作
const sleep = time => new Promise(resolve => {
  setTimeout(resolve, time);
});

(async () => {
  for (var i = 0; i < 5; i++) {
    await sleep(1000);
    console.log(i);
  }
	
  await sleep(1000);
  console.log(i);
})();

// 符合要求的每隔一秒输出
// 0,1,2,3,4,5
```
