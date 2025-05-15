---
title: flex用法
date: 2025-05-14 22:33:24
tags: [css, 前端]
categories: 学习
css: flex用法
---

这篇文章学习怎么使用`css`中的`flex`用法

<!-- more -->

[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox)

# 概念

`flex`，全名为Flexible Box模型，通常被称为`flexbox`，是一种一维的布局模型
我们说 flexbox 是一种一维的布局，是因为一个 flexbox 一次只能处理一个维度上的元素布局，一行或者一列。作为对比的是另外一个二维布局 CSS Grid Layout，可以同时处理行和列上的布局。

--TODO: 写一篇关于grid的blog

# 轴线

`flex`具有两条轴线--主轴和交叉轴

## 主轴

主轴由`flex-direction`定义，可取四个枚举值

- `row`
- `row-reverse`
- `column`
- `column-reverse`

两两分组，当设置为前两个时，主轴将沿着**行向**延伸，这时盒子中的元素就会全部排成一行

```

<div style={{ display: 'flex', gap: '10px' }}>
  <div style={{ background: 'lightblue', padding: '10px' }}>子项 1</div>
  <div style={{ background: 'lightgreen', padding: '10px' }}>子项 2</div>
  <div style={{ background: 'lightcoral', padding: '10px' }}>子项 3</div>
</div>
```

<div style="display: flex; gap: 10px;">
  <div style="background: lightblue; padding: 10px;">子项 1</div>
  <div style="background: lightgreen; padding: 10px;">子项 2</div>
  <div style="background: lightcoral; padding: 10px;">子项 3</div>
</div>

相对的，设置为后两个时，主轴沿着页面的上下方向延伸--也就是**块向**，此时盒子里的每个元素都会独占一行

```

<div style="display: flex; flex-direction: column; gap: 10px;">
  <div style="background: lightblue; padding: 10px;">子项 1</div>
  <div style="background: lightgreen; padding: 10px;">子项 2</div>
  <div style="background: lightcoral; padding: 10px;">子项 3</div>
</div>
```

<div style="display: flex; flex-direction: column; gap: 10px;">
  <div style="background: lightblue; padding: 10px;">子项 1</div>
  <div style="background: lightgreen; padding: 10px;">子项 2</div>
  <div style="background: lightcoral; padding: 10px;">子项 3</div>
</div>

## 交叉轴

交叉轴就是垂直于主轴的一条轴线
所以如果你的`flex-direction`（主轴）设成了 `row` 或者 `row-reverse` 的话，交叉轴的方向就是沿着上下方向延伸的。
如果主轴方向设成了 `column` 或者 `column-reverse`，交叉轴就是水平方向。

# Flex容器

文档中采用了 flexbox 的区域就叫做 flex 容器。为了创建`flex` 容器，我们把一个容器的`display`属性值改为`flex`或者`inline-flex`。完成这一步之后，容器中的直系子元素就会变为**flex** 元素。由于所有 CSS 属性都会有一个初始值，所以 flex 容器中的所有 flex 元素都会有下列行为：

- 元素排列成一行(`flex-direction`初始值为`row`)
- 元素从主轴的起始线开始
- 元素不会在主维度方向拉伸，但是可以缩小
- `flex-basis`属性为`auto`
- `flex-wrap`属性为`nowrap`

<div class="box">
  <div>One</div>
  <div>Two</div>
  <div>Three <br />has <br />extra <br />text</div>
</div>

```html
<div class="box">
  <div>One</div>
  <div>Two</div>
  <div>Three <br />has <br />extra <br />text</div>
</div>
```

```css
.box > * {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
}

.box {
  border: 2px dotted rgb(96 139 168);
  display: flex;
}
```

<style>

.box > * {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
}

.box {
  border: 2px dotted rgb(96 139 168);
  display: flex;
}
</style>
