---
title: setTimeout方法
date: 2025-06-30 15:55:01
tags: [js, 前端]
categories: 学习
---

[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout)

`setTimeout()`方法设置一个定时器，一旦定时器到期，就会执行一个函数或指定的代码片段

# 语法

```js
setTimeout(code);
setTimeout(code, delay);

setTimeout(functionRef);
setTimeout(functionRef, delay);
setTimeout(functionRef, delay, param1);
setTimeout(functionRef, delay, param1, param2);
setTimeout(functionRef, delay, param1, param2, /* …, */ paramN);
```

# 参数

- `functionRef`
  当定时器到期后要执行的函数
- `code`
  这是一个代替语法，允许你包含在定时器到期后编译和执行的字符串而非函数。这个语法**不推荐使用**。

  ```js
  setTimeout("alert('Hello World')", 1000);
  ```

  不推荐的原因：

  1. 安全风险：字符串可能来自用户输入，容易导致XSS
  2. 调试困难：调试器对匿名 eval 脚本支持不佳。
  3. 性能差：JavaScript 引擎无法优化 eval 和字符串执行的代码。

- `delay`
  代表定时器在执行指定的函数或代码之前应该等待的时间，单位是毫秒，默认值为0，即如果跳过此参数，意味着‘立即’执行，或者应该说是在下一个事件循环执行

- `param`
  会被传递给由`functionRef`指定的函数的附加参数。
  例子

  ```js
  function greet(context, name, time) {
    console.log(`Good ${time}, ${name}!`);
  }
  setTimeout(greet, 2000, null, "Alice", "evening");
  ```

  两秒后执行`greet(null, "Alice", "evening")`
  注意不能这么写

  ```js
  setTimeout(greet(null, "Alice", "evening"), 2000);
  ```

  这会立即调用`greet(null, "Alice", "evening")`并把它的**返回值（不是函数)**传给`setTimeout`

# 返回值

返回值`timeoutID`是一个正整数，表示由`setTimeout()`调用创建的定时器的标识符。可以将这个值传递给`clearTimeout()`来取消该定时器。
