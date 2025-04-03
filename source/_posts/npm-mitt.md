---
title: npm_mitt
date: 2025-03-28 15:54:11
tags:
  [npm, vue3]
---

这篇文章用于记录一个很有用的组件间通信的库==mitt

<!-- more -->

# 什么是mitt

mitt是一个轻量级的、零依赖的、事件驱动的库，用于在组件之间进行通信。它提供了一个简单的方式来发送和接收事件，而不需要依赖复杂的框架或库。

可以做到：

- 组件间通信
- 父子组件通信
- 兄弟组件通信
- 跨级组件通信

# 安装

```bash
npm install --save mitt
```

# 使用

```js
import mitt from 'mitt'  // 引入mitt

const emitter = mitt()  // 创建emitter实例

// 发送事件
emitter.emit('test', 'hello')

// 监听事件
emitter.on('test', (data) => {
  console.log(data)
})
```

具体解释：

- 监听事件：emitter.on('test', (data) => {
  console.log(data)
})

  其中test是事件名，这个名字可以自定义，(data) => {
    console.log(data)
  }是事件回调函数，即在其他地方通过这个名字，就可以触发这个回调函数
  也可以写成这样：

  ```js
  const fn = (data) => {
    console.log(data)
  }

  emitter.on('test', fn)
  ```

- 发送事件：emitter.emit('test', 'hello')

  其中test是事件名，hello是事件参数

  根据事件名，可以发送多个参数，视监听时间时绑定的函数而定
