<!--
 * @Description: Function 函数
 * @Author: shenxh
 * @Date: 2021-12-28 17:05:34
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-29 10:37:41
-->

- [函数](#函数)
  - [参数](#参数)
  - [箭头函数](#箭头函数)
  - [构造函数](#构造函数)
  - [函数声明与函数表达式](#函数声明与函数表达式)
  - [函数内部](#函数内部)
    - [arguments](#arguments)
    - [this](#this)
      - [标准函数中的 this](#标准函数中的-this)
      - [箭头函数中的 this](#箭头函数中的-this)
  - [递归](#递归)

# 函数
函数是 ECMAScript 中最有意思的部分之一，这主要是因为函数实际上是对象。

每个函数都是 Function 类型的实例，而 Function 也有属性和方法，跟其他引用类型一样。

因为函数是对象，所以函数名就是指向函数对象的指针，而且不一定与函数本身紧密绑定。

函数通常以函数声明的方式定义，比如：

```
function sum(num1, num2) {
  return num1 + num2;
}
```

注意函数定义最后没有加分号。

另一种定义函数的语法是函数表达式。函数表达式与函数声明几乎是等价的：

```
let sum = function(num1, num2) {
  return num1 + num2;
}; 
```

这里，代码定义了一个变量 sum 并将其初始化为一个函数。注意 function 关键字后面没有名称，因为不需要。这个函数可以通过变量 sum 来引用。

还有一种定义函数的方式与函数表达式很像，叫作“箭头函数”，如下所示：

```
let sum = (num1, num2) => {
  return num1 + num2;
}; 
```

## 参数
参数分为"形参"和"实参"两种：
+ 形参：在函数的定义阶段，括号内写的变量名，叫做该函数的形式参数，简称形参
+ 实参：在函数的调用阶段，括号内实际传入的值，叫做实际参数，简称实参

比如：

```
// 定义函数时, 括号内的参数为形参, 相当于变量名
function sum(num1, num2) {
  return num1 + num2;
}

// 调用函数时, 括号内的参数为实参
console.log(sum(2, 5)); // 7
```

也可以给参数设置默认值, 比如：

```
// 函数调用时, 如果不传入实参的话, 就会使用默认参数
function sum(num1 = 3, num2 = 4) {
  return num1 + num2;
}

// 此时只传入了第一个参数 2, 所以第二个参数就会使用默认的 4
console.log(sum(2)); // 6
```

## 箭头函数
ECMAScript 6 新增了使用箭头（`=>`）语法定义函数表达式的能力。

很大程度上，箭头函数实例化的函数对象与正式的函数表达式创建的函数对象行为是相同的。任何可以使用函数表达式的地方，都可以使用箭头函数：

```
let arrowSum = (a, b) => {
  return a + b;
};

let fnSum = function(a, b) {
  return a + b;
};

console.log(arrowSum(5, 8)); // 13
console.log(fnSum(5, 8)); // 13
```

如果只有一个参数，那也可以不用括号。只有没有参数，或者多个参数的情况下，才需要使用括号：

```
// 只有一个参数时, 以下两种写法都有效
let double = (x) => { return 2 * x; };
let triple = x => { return 3 * x; };

// 没有参数需要括号
let getRandom = () => { return Math.random(); };

// 多个参数需要括号
let sum = (a, b) => { return a + b; };

// 无效的写法：
let multiply = a, b => { return a * b; }; 
```

箭头函数也可以不用大括号，但这样会改变函数的行为。使用大括号就说明包含“函数体”，可以在一个函数中包含多条语句，跟常规的函数一样。

如果不使用大括号，那么箭头后面就只能有一行代码，比如一个赋值操作，或者一个表达式。而且，省略大括号会隐式返回这行代码的值：

```
// 以下两种写法都有效，而且返回相应的值
let double = (x) => { return 2 * x; };
let triple = (x) => 3 * x;

// 可以赋值
let value = {};
let setName = (x) => x.name = "Matt";

setName(value);
console.log(value.name); // "Matt"

// 无效的写法：
let multiply = (a, b) => return a * b;
```

箭头函数虽然语法简洁，但也有很多场合不适用。箭头函数不能使用 `arguments`、`super` 和 `new.target`，也不能用作构造函数。此外，箭头函数也没有 `prototype` 属性。

## 构造函数
- 构造函数也是一个普通函数，创建方式和普通函数一样，但构造函数习惯上**首字母大写**
- 构造函数与普通函数调用方式不一样
  - 普通函数直接调用：`sum();`
  - 构造函数需要使用 `new` 关键字调用：`new Sum();`
- 构造函数用来创建**实例对象**
- 构造函数的函数名与类名相同
  - 比如 `Sum()` 这个构造函数, Sum 既是函数名, 又是这个对象的类名
- 构造函数内部用 `this` 来构造属性和方法
  - 在构造函数内部，`this` 指向的是构造出来的新对象
  - 在普通函数内部，`this` 指向的是 `window` 全局对象
- 构造函数默认不用 `return` 返回值；普通函数一般都有 `return` 返回值
  - 构造函数会默认返回 `this`，也就是新的实例对象
  - 普通函数如果没有 `return` 值的话，返回 `undefined`
  - 如果使用了 `return`，那返回值会根据 `return` 值的类型而有所不同  
- 构造函数的执行流程
  - 在堆内存中创建一个新的对象
  - 将新建的对象设置为函数中的 `this`
  - 执行构造函数中的代码
  - 返回新建的对象

```
function Sum(num1, num2) {
  this.num1 = num1;
  this.num2 = num2;
}

let getSum = new Sum();

console.log(getSum);
```

## 函数声明与函数表达式
JavaScript 引擎在任何代码执行之前，会先读取函数声明，并在执行上下文中生成函数定义。而函数表达式必须等到代码执行到它那一行，才会在执行上下文中生成函数定义。来看下面的例子：

```
// 这样写没问题
console.log(sum(10, 10));

function sum(num1, num2) {
  return num1 + num2;
}
```

以上代码可以正常运行，因为函数声明会在任何代码执行之前先被读取并添加到执行上下文。这个过程叫作**函数声明提升**。

在执行代码时，JavaScript 引擎会先执行一遍扫描，把发现的函数声明提升到源代码树的顶部。因此即使函数定义出现在调用它们的代码之后，引擎也会把函数声明提升到顶部。

如果把前面代码中的函数声明改为等价的函数表达式，那么执行的时候就会出错：

```
// 这样写会出错
console.log(sum(10, 10));

let sum = function(num1, num2) {
  return num1 + num2;
}; 
```

上面的代码之所以会出错，是因为这个函数定义包含在一个变量初始化语句中，而不是函数声明中。代码从上往下执行时, 并没有发现已声明的函数, 所以会报错。

## 函数内部

### arguments
`arguments` 对象是一个类数组对象 (结构与数组相同, 有 `length` 属性, 但没有数组的方法)，包含调用函数时传入的所有参数。这个对象只有以 function 关键字定义函数时才会有（箭头函数没有）。

```
function sum() {
  return arguments[0] + arguments[1];
}

console.log(sum(2, 3)); // 5
```

当不确定实参个数的时候, 我们可以用 `arguments` 来接收, 比如：

```
function sum() {
  let num = 0;

  for (let i = 0; i < arguments.length; i++) {
    num += arguments[i]
  }

  return num;
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

### this
另一个特殊的对象是 `this`，它在标准函数和箭头函数中有不同的行为。


#### 标准函数中的 this
在标准函数中，`this` 引用的是把函数当成方法调用的上下文对象，这时候通常称其为 `this` 值（在网页的全局上下文中调用函数时，`this` 指向 `windows`）。来看下面的例子：


```
window.color = 'red';

let o = {
  color: 'blue'
};

function sayColor() {
  console.log(this.color);
}

sayColor(); // 'red'
o.sayColor = sayColor;
o.sayColor(); // 'blue'
```

定义在全局上下文中的函数 sayColor() 引用了 `this` 对象。这个 `this` 到底引用哪个对象必须到函数被调用时才能确定。因此这个值在代码执行的过程中可能会变。

如果在全局上下文中调用 sayColor()，这结果会输出"red"，因为 `this` 指向 `window`，而 this.color 相当于 window.color。

而在把 sayColor() 赋值给 o 之后再调用 o.sayColor()，`this` 会指向 o，即 this.color 相当于 o.color，所以会显示"blue"。

#### 箭头函数中的 this
对于普通函数来说，内部的 `this` 指向函数运行时所在的对象，但是这一点对箭头函数不成立。它没有自己的 `this` 对象，内部的 `this` 就是定义时上层作用域中的 `this`。也就是说，箭头函数内部的 `this` 指向是固定的，相比之下，普通函数的 `this` 指向是可变的。

下面的例子演示了这一点。在对 sayColor() 的两次调用中，`this` 引用的都是 `window` 对象，因为这个箭头函数是在 `window` 上下文中定义的：

```
window.color = 'red';

let o = {
  color: 'blue'
};
let sayColor = () => console.log(this.color);

sayColor(); // 'red'
o.sayColor = sayColor;
o.sayColor(); // 'red' 
```

> 注：函数名只是保存指针的变量。因此全局定义的 sayColor() 函数和 o.sayColor() 是同一个函数，只不过执行的上下文不同。

在事件回调或定时回调中调用某个函数时，`this` 值指向的并非想要的对象。此时将回调函数写成箭头函数就可以解决问题。这是因为箭头函数中的 `this` 会保留定义该函数时的上下文：

```
function King() {
  this.royaltyName = 'Henry';
  // this 引用 King 的实例
  setTimeout(() => console.log(this.royaltyName), 1000);
}
function Queen() {
  this.royaltyName = 'Elizabeth';
  // this 引用 window 对象
  setTimeout(function() {
    console.log(this.royaltyName);
  }, 1000);
}

new King(); // Henry
new Queen(); // undefined
```

## 递归
递归函数通常的形式是一个函数通过名称调用自己，如下面的例子所示：

```
function factorial(num) {
  if (num <= 1) {
    return 1;
  } else {
    return num * factorial(num - 1);
  }
} 
```
