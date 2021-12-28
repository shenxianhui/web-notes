<!--
 * @Description: Object 对象
 * @Author: shenxh
 * @Date: 2021-12-27 16:27:31
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-28 09:44:42
-->

- [Object](#object)
  - [属性值简写](#属性值简写)
  - [简写方法名](#简写方法名)
  - [对象解构](#对象解构)
- [静态方法](#静态方法)

# Object
到目前为止，大多数引用值的示例使用的是 Object 类型。Object 是 ECMAScript 中最常用的类型之一。虽然 Object 的实例没有多少功能，但很适合存储和在应用程序间交换数据。

显式地创建 Object 的实例有两种方式。第一种是使用 new 操作符和 Object 构造函数，如下所示：

```
let person = new Object();

person.name = "Nicholas";
person.age = 29;
```

另一种方式是使用对象字面量表示法。对象字面量是对象定义的简写形式，目的是为了简化包含大量属性的对象的创建。比如，下面的代码定义了与前面示例相同的 person 对象，但使用的是对象字面量表示法：

```
let person = {
  name: "Nicholas",
  age: 29
}; 
```

虽然属性一般是通过点语法来存取的，这也是面向对象语言的惯例，但也可以使用中括号来存取属性。在使用中括号时，要在括号内使用属性名的字符串形式，比如：

```
console.log(person["name"]); // "Nicholas"
console.log(person.name); // "Nicholas"
```

从功能上讲，这两种存取属性的方式没有区别。使用中括号的主要优势就是可以通过变量访问属性，就像下面这个例子中一样：

```
let propertyName = "name";

console.log(person[propertyName]); // "Nicholas"
```

另外，如果属性名中包含可能会导致语法错误的字符，或者包含关键字/保留字时，也可以使用中括号语法。比如：

```
person["first name"] = "Nicholas";
```

因为"first name"中包含一个空格，所以不能使用点语法来访问。不过，属性名中是可以包含非字母数字字符的，这时候只要用中括号语法存取它们就行了。

通常，点语法是首选的属性存取方式，除非访问属性时必须使用变量。

## 属性值简写
在给对象添加变量的时候，开发者经常会发现属性名和变量名是一样的。例如：

```
let name = 'Matt';
let person = {
  name: name
};

console.log(person); // { name: 'Matt' }
```

为此，简写属性名语法出现了。简写属性名只要使用变量名（不用再写冒号）就会自动被解释为同名的属性键。如果没有找到同名变量，则会抛出 ReferenceError。

以下代码和之前的代码是等价的：

```
let name = 'Matt';
let person = {
  name
};

console.log(person); // { name: 'Matt' }
```

## 简写方法名
在给对象定义方法时，通常都要写一个方法名、冒号，然后再引用一个匿名函数表达式，如下所示：

```
let person = {
  sayName: function(name) {
    console.log(`My name is ${name}`);
  }
};

person.sayName('Matt'); // My name is Matt
```

新的简写方法的语法遵循同样的模式，但开发者要放弃给函数表达式命名（不过给作为方法的函数命名通常没什么用）。相应地，这样也可以明显缩短方法声明。

以下代码和之前的代码在行为上是等价的：

```
let person = {
  sayName(name) {
    console.log(`My name is ${name}`);
  }
};

person.sayName('Matt'); // My name is Matt
```

## 对象解构
ECMAScript 6 新增了对象解构语法，可以在一条语句中使用嵌套数据实现一个或多个赋值操作。简单地说，对象解构就是使用与对象匹配的结构来实现对象属性赋值。

下面的例子展示了两段等价的代码，首先是不使用对象解构的：

```
// 不使用对象解构
let person = {
  name: 'Matt',
  age: 27
};
let personName = person.name;
let personAge = person.age;

console.log(personName); // Matt
console.log(personAge); // 27
```

然后，是使用对象解构的：

```
// 使用对象解构
let person = {
  name: 'Matt',
  age: 27
};
let { name: personName, age: personAge } = person;

console.log(personName); // Matt
console.log(personAge); // 27 
```

使用解构，可以在一个类似对象字面量的结构中，声明多个变量，同时执行多个赋值操作。如果想让变量直接使用属性的名称，那么可以使用简写语法，比如：

```
let person = {
  name: 'Matt',
  age: 27
};
let { name, age } = person;

console.log(name); // Matt
console.log(age); // 27 
```


# 静态方法

|方法|说明|
|-|-|
|[Object.assign()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/Object)|通过复制一个或多个对象来创建一个新的对象|
|[Object.create()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)|使用指定的原型对象和属性创建一个新对象|
|[Object.defineProperty()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)|给对象添加一个属性并指定该属性的配置|
|[Object.defineProperties()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)|给对象添加多个属性并分别指定它们的配置|
|[Object.entries()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)|返回给定对象自身可枚举属性的 `[key, value]` 数组|
|[Object.freeze()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)|冻结对象：其他代码不能删除或更改任何属性|
|[Object.getOwnPropertyDescriptor()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor)|返回对象指定的属性配置|
|[Object.getOwnPropertyNames()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames)|返回一个数组，它包含了指定对象所有的可枚举或不可枚举的属性名|
|[Object.getOwnPropertySymbols()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols)|返回一个数组，它包含了指定对象自身所有的符号属性|
|[Object.getPrototypeOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/GetPrototypeOf)|返回指定对象的原型对象|
|[Object.is()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is)|比较两个值是否相同。所有 NaN 值都相等（这与==和===不同）|
|[Object.isExtensible()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isExtensible)|判断对象是否可扩展|
|[Object.isFrozen()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isFrozen)|判断对象是否已经冻结|
|[Object.isSealed()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isSealed)|判断对象是否已经密封|
|[Object.keys()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)|返回一个包含所有给定对象**自身**可枚举属性名称的数组|
|[Object.preventExtensions()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)|防止对象的任何扩展|
|[Object.seal()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)|防止其他代码删除对象的属性|
|[Object.setPrototypeOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf)|设置对象的原型（即内部 `[[Prototype]]` 属性）|
|[Object.values()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/values)|返回给定对象自身可枚举值的数组|
