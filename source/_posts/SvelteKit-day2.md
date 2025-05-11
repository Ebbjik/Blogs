---
title: SvelteKit-day2
date: 2025-05-11 14:29:00
tags: [sveltekit, 前端]
categories: 学习
---

这篇文章学习`svelte`中的`Runes`

<!-- more -->

  <link rel="stylesheet" href="../css/day2.css">

# 什么是Runes

[官方文档](https://svelte.dev/docs/svelte/what-are-runes)

他是一类以`$`符号开头的特殊符号，有以下几种

- $state
- $derived
- $effect
- $props
- $bindable
- $inspect
- $host

下面分别讲解

# $state

[官方文档](https://svelte.dev/docs/svelte/$state)

这个符文的作用是创建一个响应式变量<span class="side">响应式就是页面会随着变量的改变自行更改</span>。

类似于`Vue3`中的`ref`，`reactive`

不同的是他没有用于交互的api，像是`ref`的`.value`

举例：

```
<script>
	let count = $state(0);
</script>

<button onclick={() => count++}>
	clicks: {count}
</button>
```

即在使用上它没有不同

## 深度状态 Deep state

### 什么是深度状态

简单来说，Deep state 指的是组件或应用中「嵌套层级较深的状态数据结构」，比如嵌套对象或数组中的数据，而不仅仅是表层的简单变量。
**例子：**

```
let user = {
  name: "Alice",
  address: {
    city: "Beijing",
    street: "Main St"
  }
};
```

这里，`user.address.city` 就是「深层状态」。

`svelte`允许我们创建这样一个响应式对象

```
let todos = $state([
	{
		done: false,
		text: 'add more todos'
	}
]);

```

`$state`允许我们用数组和简单对象，但像集合和图这样的类不能被代理，但`svelte`提供了内置的响应式实现，可以从[svelte/reactivity](https://svelte.dev/docs/svelte/svelte-reactivity)引入

此时，修改`todos`中的某一个变量，ui中依赖他的内容都会随之改变

如果推送一个对象到数组中，这个对象同样是响应式的

```
todos.push({
	done: false,
	text: 'eat lunch'
});
```

但是如果你解构一个响应式的值，得到的引用不会是响应式的

```
let { done, text } = todos[0];

todos[0].done = !todos[0].done;
```

像这样得到的`done`和`text`就只是普通的js变量

-- TODO: class部分

<style>
.side {
  display: inline-block;
  font-size: 12px;
  margin-left: 4px;
  background-color: #e0f0ff;
  color: #003366;
  padding: 1px 2px;
  border-radius: 4px;
  border: 1px solid #555;
}
</style>
