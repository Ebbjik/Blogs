---
title: js中的函数
date: 2025-06-15 16:15:14
tags: [前端, js]
categories: 学习
---

# 本质

函数实际上是一个`Function`对象

函数不定义`return`默认返回`undefined`

# 定义函数方法

有多种方法可以定义函数

## 函数声明(函数语句)

```js
function name([param[, param[, ... param]]]) { statements }

function sayHello() {
  console.log("Hello");
}
```

## 函数表达式

函数表表达式可以看作是**把函数作为值**的一种用法

```js
const sayHi = function greet() {
  console.log("Hi");
};

const sayHi = function () {
  console.log("Hi");
};

function greet(name, callback) {
  console.log("Hello, " + name + "!");
  callback(); // 调用传入的函数
}

function sayBye() {
  console.log("Goodbye!");
}

// 把 sayBye 函数作为参数传进去
greet("Alice", sayBye);
```

把函数传给变量，常量当值是函数表达式，传给函数当参数值也是函数表达式

❓：那为什么要具名定义函数呢，既然赋值给变量了，那都写成`function (){}`不就好了
💡：因为有时会定义递归函数，像是这样

```js
const factorial = function fact(n) {
  if (n <= 1) return 1;
  return n * fact(n - 1);
};

console.log(factorial(5)); // 120
```

在写法上这两种非常行接近，区别重要在提升和作用域方面

- 函数声明定义的函数是可以在定义前调用的，因为在执行前会被提升到当前作用域的顶部，相对的函数表达式不会提升，所以在定义前调用会报错

## 函数生成器声明

## 函数生成器表达式

## 箭头函数表达式

写法

```js
const ceshi = () => {
  console.log("nihao");
};
```

其中括号中的是参数，支持剩余参数、默认参数和解构，始终需要括号

- 剩余参数

```js
const f = (a, b, ...r) => [a, b, r];
f(1, 2, 3, 4, 5); // [1, 2, [3, 4, 5]]
```

其中`a`、`b`是普通参数,`...r`表示接受剩余的所有参数，组成一个数组

- 默认参数

当函数未传入对应参数或是传入`undefined`时，他将会使用默认的值

```js
function foo(a = 100) {
  console.log(a);
}

foo(); // 输出 100
foo(undefined); // 输出 100
foo(0); // 输出 0（不会使用默认值）
```

只有`undefined`可以，其余的假值是不起作用的
把带默认值的参数放到前面再试图跳过他是不合法的，像是这样

```js
function f(a = 1, b = 2, c = 3) { ... }
f(1, , 3); // ❌ 语法错误
f(1,undefined,3); //必须显式的传递`undefined`
```

但可以把带默认值的参数放到最后

```js
function foo(a, b = 20) {
  console.log(a, b);
}

foo(10); // ✅ 输出：10 20
```

- 解构赋值

  数组解构

  - 基本用法

  ```js
  const arr = [1, 2, 3];
  const [a, b, c] = arr;
  console.log(a); // 1
  console.log(b); // 2
  console.log(c); // 3
  ```

  - 跳过元素

  ```js
  const [x, , z] = [10, 20, 30];
  console.log(x, z); // 10 30
  ```

  - 默认值

  ```js
  const [a = 100, b = 200] = [1];
  console.log(a, b); // 1 200
  ```

  - 嵌套解构

  ```js
  const [a, [b, c]] = [1, [2, 3]];
  console.log(a, b, c); // 1 2 3
  ```

箭头函数没有独立的 `this`、`arguments` 和 `super` 绑定，并且不可被用作方法。

`this`的值取决于它出现的上下文：函数、类或全局

- 函数上下文
  在函数内部，this 的值取决于函数如何被调用，`this`的值不是拥有此函数作为自己属性的对象，而是用于调用此函数的对象。

  ```js
  const obj4 = {
    name: "obj4",
    getThis() {
      return this;
    },
  };
  const obj5 = { name: "obj5" };
  obj6.getThis = obj4.getThis;
  console.log(obj5.getThis()); // { name: 'obj5', getThis: [Function: getThis] }
  ```

  普通函数的`this`是‘调用时决定的’，而箭头函数的`this`是‘定义时决定的’，永远集成自外层作用域，不能改变

  ```js
  const obj = {
    name: "Alice",
    sayHi1: function () {
      console.log(this.name); // this 指向 obj，输出 "Alice"
    },
    sayHi2: () => {
      console.log(this.name); // this 不是 obj，而是外部（window/undefined）
    },
  };
  obj.sayHi1(); // "Alice"
  obj.sayHi2(); // undefined（不是你期望的）
  ```

  上面的`obj`只是一个变量对象，箭头函数从他那里得不到`this`，只能再往上，也就是全局

`arguments`同样从上层继承~~事实上只有函数~~，`arguments`是一个对应于传递给函数的参数的类数组对象。
在[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)中，推荐编写兼容ES6的代码时使用**剩余参数**

`super`从它被定义的上下文获取~~包含它的类~~

这三个东西，都要从外层作用域继承，是因为ES6设计箭头函数时，目的就是**简洁、闭包友好、绑定外层this**，因此：

- 它**不创建自己的执行上下文**
- 它**直接使用它定义时的“父作用域”的上下文**。
- 所以，它也就没有自己的 `this`、`arguments`、`super`、`new.target`。

而方法，通常需要操作调用函数的对象，像是`console.log(this.name)`，从上下文继承`this`的箭头函数自然不能用
当说`F`是`O`的一个方法时，通常意味着`F`将`O`作为其`this`绑定。没有根据它们的`thi` 值具有不同行为的函数属性（或者根本没有动态`this`绑定的函数——比如绑定函数和箭头函数）可能不被普遍认为是方法。

箭头函数不能用作构造函数。使用`new`调用它们会引发`TypeError`。它们也无法访问`new.target`关键字。

箭头函数不能在其主体中使用`yield`，也不能作为生成器函数创建。

箭头函数既可以使用**表达式体**，也可以使用**表达式体**

```js
const func = (x) => x * x;
// 表达式体语法，隐含返回值

const func2 = (x, y) => {
  return x + y;
};
// 块体语法，需要明确返回值
```

但用表达式体直接返回对象是不能正常工作的`(params) => { object: literal }`
这是因为只有当箭头后面的标记不是左括号时，JavaScript 才会将箭头函数视为表达式体，因此括号（{}）内的代码会被解析为一系列语句，而在没有`return`，所以默认返回`undefined`，要解决这个问题，这么做

```js
const func = () => ({ foo: 1 });
```

用括号把对象包起来

箭头函数的参数与箭头之间不能换行，实际是`) =>`必须保持在一行

## `Function`构造函数

--TODO: 续写
