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

```html

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

```html
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

### 属性

1. align-items
   `align-items` 属性用于设置 Flex 容器中子元素在交叉轴（垂直轴）上的对齐方式。它包含很多枚举值,flex布局中常用的有以下四种：
   更多的见[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/align-items)

   - **stretch** (默认值)  
     当子元素没有指定固定尺寸时，子元素会沿着交叉轴方向拉伸，填满父容器在该方向上的空间。
   - **center**  
     flex 元素的外边距框在交叉轴上居中对齐。如果元素的交叉轴尺寸大于 flex 容器，它将在两个方向上等距溢出。
   - **self-start**  
     将元素与容器的主轴起点或交叉轴起点对齐，轴起点的方向对应于元素的起始方向。
   - **self-end**  
      将元素与容器的主轴末端或交叉轴末端对齐，轴末端的方向对应于元素的结尾方向。

2. justify-content
   `justify-content` 属性用于设置 Flex 容器中子元素在主轴上的对齐方式。它包含很多枚举值,flex布局中常用的有以下几种：
   更多的见[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-content)

   - **stretch**  
     如果元素沿主轴的组合尺寸小于对齐容器的尺寸，任何尺寸设置为`auto`的元素都会等比例地增加其尺寸（而不是按比例增加），同时仍然遵守由`max-height`/`max-width`（或相应功能）施加的约束，以便沿主轴完全填充对齐容器的组合尺寸。
   - **center**  
     伸缩元素向每行中点排列。每行第一个元素到行首的距离将与每行最后一个元素到行尾的距离相同。
   - **self-start** (默认值)
     元素紧密地排列在弹性容器的主轴起始侧。仅应用于弹性布局的项目。对于不是弹性容器里的元素，此值将被视为`start`。
   - **self-end**  
     元素紧密地排列在弹性容器的主轴结束侧。仅应用于弹性布局的元素。对于不是弹性容器里的元素，此值将被视为`end`。
   - **space-around**  
     在每行上均匀分配弹性元素。相邻元素间距离相同。每行第一个元素到行首的距离和每行最后一个元素到行尾的距离将会是相邻元素之间距离的一半。
   - **space-between**  
     在每行上均匀分配弹性元素。相邻元素间距离相同。每行第一个元素与行首对齐，每行最后一个元素与行尾对齐。

# Flex容器

文档中采用了 flexbox 的区域就叫做 flex 容器。为了创建`flex` 容器，我们把一个容器的`display`属性值改为`flex`或者`inline-flex`。完成这一步之后，容器中的直系子元素就会变为**flex** 元素。由于所有 CSS 属性都会有一个初始值，所以 flex 容器中的所有 flex 元素都会有下列行为：

- 元素排列成一行(`flex-direction`初始值为`row`)
- 元素从主轴的起始线开始
- 元素不会在主维度方向拉伸，但是可以缩小
- `flex-basis`属性为`auto`
- `flex-wrap`属性为`nowrap`

## Flex容器的子元素默认有这样的属性`flex: 0 1 auto`

```
flex: <flex-grow> <flex-shrink> <flex-basis>;
```

- flex-grow
  元素是否可以扩张
- flex-shrink
  元素是否可以收缩
- flex-basis
  元素的默认大小

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

`row-reverse`和`column-reverse`属性的效果是在原基础上起始线和终止线位置互换

<div class="box-reverse">
  <div>One</div>
  <div>Two</div>
  <div>Three <br />has <br />extra <br />text</div>
</div>

```html
<div class="box-reverse">
  <div>One</div>
  <div>Two</div>
  <div>Three <br />has <br />extra <br />text</div>
</div>
```

```css
.box-reverse > * {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
}

.box-reverse {
  border: 2px dotted rgb(96 139 168);
  display: flex;
  flex-direction: row-reverse;
}
```

# 用`flex-wrap`实现多行Flex容器

`flex-wrap`切换为`wrap`后，元素会自动换行

<div class="box-wrap">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
</div>

```html
<div class="box-wrap">
  <div>One</div>
  <div>Two</div>
  <div>Three <br />has <br />extra <br />text</div>
</div>
```

```css
.box-wrap > * {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  width: 200px;
}

.box-wrap {
  width: 500px;
  border: 2px dotted rgb(96 139 168);
  display: flex;
  flex-wrap: wrap;
}
```

# 简写属性`flex-flow`

[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-flow)

`flex-direction`和`flex-wrap`可以被组合简写为`flex-flow`

像这样

```
flex-flow: <flex-direction> <flex-wrap>
```

实例：

<div class="flex-flow-box">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
</div>

```

.flex-flow-box > * {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  width: 200px;
}

.flex-flow-box {
  width: 500px;
  border: 2px dotted rgb(96 139 168);
  display: flex;
  flex-flow: row wrap;
}
```

# flex元素上的属性

为了更好地控制 flex 元素，有三个属性可以作用于它们：

- [flex-grow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-grow)
- [flex-shrink](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-shrink)
- [flex-basis](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-basis)

这几个flex属性的作用其实就是改变了flex容器中可用空间的行为

## 可用空间

假设在 1 个 500px 的容器中，我们有 3 个 100px 宽的元素，那么这 3 个元素需要占 300px 的宽，剩下 200px 的可用空间。在默认情况下，flexbox 的行为会把这 200px 的空间留在最后一个元素的后面。

如果期望这些元素能自动地扩展去填充满剩下的空间，那么我们需要去控制可用空间在这几个元素间如何分配，这就是元素上的那些`flex`属性要做的事。

## `flex-basis`

`flex-basis`定义元素的**空间大小**，默认值为`auto`，其实就是子元素在主轴方向上的大小，它决定了在浏览器分配剩余空间之前，Flex子元素本来的尺寸

- 默认值为`auto`，意味着如果没有显式的设置`flex-basis`，浏览器会根据内容大小或`width`或`height`来决定元素的初始尺寸

- `flex-basis`为`auto`的基础上，如果用`width`或`height`设置了主轴方向上的尺寸，`flex-basis`就会采用它

- 但如果显式的设置了`flex-basis`，它会覆盖`width`或`height`

总结：flex容器中的子元素在主轴方向的尺寸 flex-basis > width/height > 内容
即，没有设置`flex-basis`的话，按`width`/`height`来，`width`/`height`也没有设置，按内容来

## `flex-grow`

`flex-grow`定义了在主轴方向上元素如何'扩展'来填充容器的可用空间

它接受正数赋值，这个数字不是像素值，而是「比例」，它的默认值是0，此时它不会扩展，设置为正数时，就会拓展以占据可用空间，当有多个元素被设置`flex-grow`时，他们会按照`flex-grow`来按比例划分可用区域

例子：

1. 元素均等扩展

```css
.item {
  flex-grow: 1;
}
```

此时，如果容器主轴上有 300px 可用空间，三个子元素会各占：

- 每个元素分得：300 / 3 = 100px

2. 元素按比例扩展

```css
.item1 {
  flex-grow: 2;
}
.item2,
.item3 {
  flex-grow: 1;
}
```

如果有 400px 可用空间，则总比例是 2 + 1 + 1 = 4：

- item1 分得：400 × (2/4) = 200px

- item2 和 .item3 各分得：400 × (1/4) = 100px

## `flex-shrink`

`flex-shrink`定义了当Flex容器空间不足时，子元素在主轴方向上如何收缩
即空间不足时：谁先让，让多少

- 它的默认值是1，代表允许收缩，
- `0`代表允许收缩
- 整个正整数同样代表比例，当多个元素都具有这个正整数值时，数值越大，收缩越多

例子：

1. 元素均等收缩

```css
.item {
  flex-shrink: 1;
  flex-basis: 200px;
}
```

此时，如果容器主轴上宽度为300px，但三个子元素共占据600px，所以他们都要收缩，共需要收缩300px
因为`flex-shrink`都是1，所以均分，各收缩100px

2. 元素按比例收缩

```css
.item1 {
  flex-shrink: 2;
  flex-basis: 200px;
}
.item2,
.item3 {
  flex-shrink: 1;
  flex-basis: 200px;
}
```

同样共需要收缩300px，但是按比例，`item1`收缩四分之二，即100px，`item2,item3`各占四分之一，即100px

但元素不会无限制的收缩，最小尺寸会限制它

- `min-height`/`min-width`
- 内容自动撑开的尺寸，像是文字或图片

## Flex属性的简写

以上三种样式可以像这样合并写到一起

```
flex: <flex-grow> <flex-shrink> <flex-basis>
```

还有预定义的简写形式

- flex: initial
  相当于`flex: 0 1 auto`
- flex: auto
  相当于`flex: 1 1 auto`
- flex: none
  相当于`flex: 0 0 auto`
- flex: \<positive-number\>
  相当于`flex: positive-number 1 0`
