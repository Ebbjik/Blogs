---
title: dom_学习
date: 2025-06-14 21:43:33
tags: [前端, js]
categories: 学习
---

# 概念

什么是dom,dom全名**Document Object Model（文档对象模型）**，是浏览器提供的**以编程方式操作网页内容的接口**

例如：

```html
<p id="intro">你好，世界！</p>
```

```js
const para = document.getElementById("intro");
para.textContent = "你好，DOM！";
```

这段代码就会把网页中的文字“你好，世界！”变成“你好，DOM！”。

在网页开发中，较多的用法是通过特定接口获取dom,再对其添加或是删去类名，以动态修改其样式

# 方法

## 从`EventTarget`继承

### `addEventListener()`

这个方法将指定的监听器注册到 EventTarget 上，当该对象触发指定的事件时，指定的回调函数就会被执行。事件目标可以是一个文档上的元素 Element、Document 和 Window，也可以是任何支持事件的对象（比如 XMLHttpRequest）

```js
addEventListener(type, listener);
addEventListener(type, listener, options);
addEventListener(type, listener, useCapture);
```

- type
  字符串，表示监听的事件类型，比如`click`、`keydown`、`DOMContentLoaded`

- listener
  回调函数，事件发生时被调用

- options 可选
  一个对象
  ```JSON
  {
  capture: Boolean, //表示 listener 会在该类型的事件捕获阶段传播到该 EventTarget 时触发
  once: Boolean, // 表示 listener 只会触发一次，执行后自动移除
  passive: Boolean, // 表示 listener 永远不会调用preventDefault()，用于提升滚动性能
  signal: AbortSignal // 表示当关联的 AbortController 的 abort() 被调用时，移除该 listener
  }
  ```
- useCapture 可选
  跟上面`options`中的`capture`属性一样

# 事件

## 加载和卸载事件

### DOMContentLoaded

HTML 文档被完全加载和解析完成，但图片、CSS、视频等资源可能还没加载完，此时这个事件就会被触发

在使用方法上它类似vue3中的`mounted`，都表示【现在你可以安全的访问和操作DOM元素了】
不然就容易出现这种问题

```html
<head>
  <script>
    const p = document.getElementById("text");
    p.textContent = "Hi"; // ❌ 此时页面还没加载 <p>，报错或无效
  </script>
</head>
<body>
  <p id="text">Hello</p>
</body>
```

为了避免这种报错，我们要这么做

```js
document.addEventListener("DOMContentLoaded", function () {
  // 所有 DOM 元素都已准备好，可以安全操作
  const p = document.getElementById("text");
  p.textContent = "Hi, DOM!";
});
```

-- TODO:续写
