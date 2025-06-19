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

  1. 数组解构

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

## `Function`构造函数

--TODO: 续写
