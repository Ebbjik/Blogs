---
title: js中的类
date: 2025-05-13 22:23:31
tags: [js, 前端]
categories: 学习
---

这篇文章学习`JavaScript`中的`Classes`

<!-- more -->

[官方文档](https://www.w3schools.com/js//js_classes.asp)

在`ES6`中，`JavaScript`中引入了`Classes`==类

# 类是什么

类是对象的模板

# 语法

```
class ClassName {
  constructor() { ... }
}
```

例子：

```
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
}
```

类中必须一直有`constructor（）`方法，这叫做构造方法

构造函数方法是一种特殊方法：

- 它具有确切的名称`constructor`
- 当新对象被创建时，这个函数自动执行
- 这个函数被用来初始化对象属性

如果没有定义构造方法，`JavaScript`会自动添加一个空的构造方法

通过构造方法，就可以通过一个类源源不断的创建对象

```
const myCar1 = new Car("Ford", 2014);
const myCar2 = new Car("Audi", 2019);
```
