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

## `Function`构造函数

--TODO: 续写
