---
title: SvelteKit-day2
date: 2025-05-11 14:29:00
tags: [sveltekit, 前端]
categories: 学习
---

这篇文章学习`svelte`中的`Runes`

<!-- more -->

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

### Classes

`$state`同样可以在类`class`中使用,无论是公有类还是私有类

[关于class](/2025/05/13/js中的类/)

```
class Todo {
	done = $state(false);
	text = $state();

	constructor(text) {
		this.text = text;
	}

	reset() {
		this.text = '';
		this.done = false;
	}
}
```

<div class="alert">
编译器将 done 和 text 这类用$state创建的响应式变量转换为引用私有字段的类原型上的 get / set 方法。这意味着属性是不可枚举的。
</div>

当你用 `for...in`、`Object.keys()` 之类的方法去遍历对象属性时，done 和 text 这两个属性不会被枚举

<div class="alert">
  在 JavaScript 中调用方法时，this 的值很重要
</div>

## 下面两种调用方法，第一种会报错

```
<button onclick={todo.reset}>
	reset
</button>
```

```
<button onclick={() => todo.reset()}>
	reset
</button>
```

或者在类中定义方法时使用箭头函数

```
class Todo {
	done = $state(false);
	text = $state();

	constructor(text) {
		this.text = text;
	}

	reset = () => {
		this.text = '';
		this.done = false;
	}
}
```

-- TODO: 关于不同函数的blog

为什么报错，见[函数之间的区别](/functions)

## $state.raw

如果你不希望对象和数组深度响应式，可以使用`$state.raw`。

使用`$state.raw` 声明的 State 不能被改变;它只能重新分配。换句话说，如果您想更新对象或数组，而不是分配给对象的属性，或使用 push 等数组方法：

```
let person = $state.raw({
	name: 'Heraclitus',
	age: 49
});

// this will have no effect
//这不会起作用
person.age += 1;

// this will work, because we're creating a new person
//这会起作用，因为创建了一个新对象
person = {
	name: 'Heraclitus',
	age: 50
};
```

## $state.snapshot

要拍摄深度反应式`$state`代理的静态快照，请使用`$state.snapshot`
<span class="side">实际意思就是为了返回静态对象而不是Proxy</span>

```
<script>
	let counter = $state({ count: 0 });

	function onclick() {
		// Will log `{ count: ... }` rather than `Proxy { ... }`
		console.log($state.snapshot(counter));
	}
  let counter = $state({ count: 0 });
  console.log(counter); // 输出的是 Proxy { ... }
  console.log($state.snapshot(counter));
  // 输出的是普通对象：{ count: 0 }
</script>
```

## 把state传递给函数

<div class='alert'>JavaScript 是一种按值传递的语言 — 当你调用一个函数时，参数是值而不是变量 。</div>

```
function add(a: number, b: number) {
	return a + b;
}

let a = 1;
let b = 2;
let total = add(a, b);
console.log(total); // 3

a = 3;
b = 4;
console.log(total); // still 3!
```

实际意思就是，即使传入的变量定义为`$state`，传入函数中的值也是`$state`的当前值

```
function add(a: number, b: number) {
	return a + b;
}

let a = $state(1);
let b = $state(2);
let total = add(a, b);
console.log(total); // 3

a++;
b++;
console.log(total); // still 3!
```

## 跨模块传递

<div class="alert"> 您可以在 .svelte.js 和 .svelte.ts 文件中声明状态，但只有在未直接重新分配该状态的情况下才能导出该状态。</div>

即这样做是错误的

```
export let count = $state(0);

export function increment() {
	count += 1;
}
```

如果跨模块导出，会导致这样的问题

```

// state.svelte.js
export let count = $state(0);

// another-file.js
import { count } from './state.svelte.js';
console.log(count); // 是一个对象，不是数字
```

如果你把`count`导出到别的文件中，Svelte编译器无法知道这个`count`是响应式的，所以它不会自动处理`$.get()`和`$.set()`，就会出错或行为不符合预期。

### 避免出错的方法

1. 不要重新赋值整个状态对象

```
// state.svelte.js
export const counter = $state({
	count: 0
});

export function increment() {
	counter.count += 1; // ✅ 只修改对象内部属性，不重新赋值
}
```

这种方式可以导出响应式对象，只要你不对整个对象重新赋值（即不写`counter = {...}`），Svelte 编译器可以处理。

2. 不导出状态本身，而是导出访问器函数

```
// state.svelte.js
let count = $state(0);

export function getCount() {
	return count;
}

export function increment() {
	count += 1;
}
```

在这种方式中，`count`是模块内私有的，外部不能直接访问，只能通过函数间接访问和修改。这样 Svelte 编译器仍能正确转换状态操作。

# $derived

--TODO: derived

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
.alert {
  padding: 12px 16px;
  border-radius: 8px;
  margin-bottom: 12px;
  font-size: 14px;
  line-height: 1.4;
  border: 1px solid transparent;
  display: flex;
  align-items: center;
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
  background-color: #fffbea; /* very light yellow */
}
</style>
