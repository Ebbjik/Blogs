---
title: ES6_学习
date: 2025-06-12 22:36:03
tags: [前端, js]
categories: 学习
---

let 与 const

<!-- more -->

[文档链接🔗](https://tony-code.github.io/javascript-ES6/book/docs/let.html)

# let 命令

ES6中新增了`let`命令，用法与`var`类似，主要区别就是作用域不同

- `var`如果在函数中写是函数作用域声明，如果不在，那就是全局作用域
- `let`是块级作用域声明

## 函数作用域

即`var`声明的变量在整个**函数内部**都有效，可以跨越代码块`{}`，例如

```
function testVar() {
  if (true) {
    var x = 1;
  }
  console.log(x); // ✅ 输出 1，即使 x 是在 if 块里声明的
}
```

## 块级作用域

`let`声明的变量只在最近的一对`{}`花括号中有效，这种声明可以有效避免变脸‘泄漏’例如

```
function testLet() {
  if (true) {
    let y = 2;
  }
  console.log(y); // ❌ 报错：y is not defined
}
```

ES6允许块级作用域的任意嵌套

```
{{{{
  {let insane = 'Hello World'}
  console.log(insane); // 报错
}}}};
```

外层作用域无法读取内层作用域的变量，但内层在一些情况可以访问上层变量

```
{{{{
  let insane = 'Hello World out';
  {
    let insane = 'Hello World in'
    console.log(insane) //Hello World in
  }
}}}};
```

内层作用域可以定义外层作用域的同名变量，且在使用变量时会优先使用当前作用域的，如果没有，则会向上层查找

但是`var`不支持块级作用域，在代码块`{}`中声明的变量会被**提升**到函数顶部或全局作用域

### 变量提升

`var`声明的变量会被提升到作用域顶部，但不会被初始化
例如：

```
console.log(a); // undefined
if (false) {
  var a = 10;
}
console.log(a); // undefined
if (true) {
  var a = 20;
}
console.log(a); // 20
```

等价于：

```
var a; // 声明被提升到顶部

console.log(a); // undefined（已声明但未赋值）
if (false) {
  a = 10; // 不会执行
}
console.log(a); // 还是 undefined
if (true) {
  a = 20; // 执行了，a 被赋值为 20
}
console.log(a); // 输出 20
```

`let` 不存在变量变量提升，如果试图在变量声明前调用它的话，就会报错

## 全局作用域

如果`var`不在函数中声明，那他就是全局作用变量，即所有地方都可访问到他

```
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```

这样的循环可以像这样展开

```

var a = [];
var i = 0;

a[i] = function () { console.log(i); }; i++;
a[i] = function () { console.log(i); }; i++;
a[i] = function () { console.log(i); }; i++;
...
```

## 暂时性死区(TDZ)

只要在块级作用域中用`let`声明了变量，这个变量就会‘绑定’这个区域，不再受外部影响
即：这个变量名在作用域中只能是`let`声明的那个，不存在说使用同名的全局变量

```
var tmp = 123;
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```

## 不允许重复声明

`let`不允许在相同作用域内重复声明同一个变量

```
// 报错
function func() {
  let a = 10;
  var a = 1;
}

// 报错
function func() {
  let a = 10;
  let a = 1;
}
```

因此在很函数内重新声明参数也是不对的，因为JavaScript 会在函数作用域内，自动为每个参数名（如 arg）创建一个变量绑定

```
function func(arg) {
  let arg; // 报错
}

function func(arg) {
  {
    let arg; // 不报错
  }
}
```

# const

`const`的作用是声明一个只读常量，一旦声明，不可改变

```
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

因为一旦声明就不能改变，那就意味着声明的同时就必须初始化，不能留到后面再赋值
即：

```
const foo;
// SyntaxError: Missing initializer in const declaration
```

在作用域方面，`cosnt`与`let`相同，同样是**块级作用域**，同样是存在**暂时性死区**，同样是**不可提升**

`cosnt`也不可以重复重复声明

```
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```

## 本质

`const`声明常量不可改变，实际上保证的不是变量的值不可改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，const只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。

即：

```
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```

这是另一个数组的例子：

```
const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
a = ['Dave'];    // 报错
```

# ES6声明变量的6种方法

1. `var`声明变量
2. `function`声明函数
3. `let`声明变量
4. `const`声明变量
5. `import`声明模块变量
6. `class`声明类

--TODO: 续写
