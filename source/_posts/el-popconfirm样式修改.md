---
title: el-popconfirm样式修改
date: 2025-04-03 14:52:28
tags:
  [ElementPlus, vue3]
---

这篇文章用于记录如何修改el-popconfirm的弹窗样式

<!-- more -->

# 问题1

在项目中使用el-popconfirm时，发现默认的弹窗样式与项目中的样式不符，需要进行修改

# 解决1

这个问题很好解决，打开F12，很容易就可以找到弹窗的div结构，如下

```html
<div class="ant-popover-inner" role="tooltip">
    <!---->
    <div class="ant-popover-inner-content">
        <div class="ant-popconfirm-inner-content">
            <div class="ant-popconfirm-message">
                <span class="ant-popconfirm-message-icon">
                    <span role="img" aria-label="exclamation-circle" class="anticon anticon-exclamation-circle">
                        <svg focusable="false" data-icon="exclamation-circle" width="1em" height="1em"
                            fill="currentColor" aria-hidden="true" viewBox="64 64 896 896">
                            <path
                                d="M512 64C264.6 64 64 264.6 64 512s200.6 448 448 448 448-200.6 448-448S759.4 64 512 64zm-32 232c0-4.4 3.6-8 8-8h48c4.4 0 8 3.6 8 8v272c0 4.4-3.6 8-8 8h-48c-4.4 0-8-3.6-8-8V296zm32 440a48.01 48.01 0 010-96 48.01 48.01 0 010 96z">

                            </path>
                        </svg>
                        <!---->
                    </span>
                </span>
                <div class="ant-popconfirm-message-title">确认删除当前系统？</div>
            </div><!---->
            <div class="ant-popconfirm-buttons"><button
                    class="css-dev-only-do-not-override-1g91or ant-btn ant-btn-default ant-btn-sm"
                    type="button"><!----><span>取 消</span></button><button
                    class="css-dev-only-do-not-override-1g91or ant-btn ant-btn-primary ant-btn-sm"
                    type="button"><!----><span>确 认</span></button>
            </div>
        </div>
    </div>
</div>
```

那想要修改样式就很简单了，只需要修改对应的css样式即可，例如我想要修改确认按钮的背景色为红色，只需要修改如下css样式即可

```css
.ant-btn-primary {
    background-color: red;
}
```

但是不总是这么顺利的

# 问题2

项目中可能有很多的弹窗，而上面这种方法会修改所有的弹窗，导致其他弹窗的样式也发生了变化，那怎么办呢？

# 解决2

这种时候我们一定会想到给弹窗加一个唯一的class，然后修改这个class的样式，例如

```css
.red-popconfirm {
    .ant-btn-primary {
        background-color: red;
    }
}
```

这样就可以只修改指定弹窗的样式了

在查看[官方文档](https://element-plus.org/zh-CN/component/popconfirm.html#api)后，并没有找到给弹窗添加class的方法

但是我们看到这样一句话

> Popconfirm 的属性与 Popover 很类似， 因此对于重复属性，请参考 Popover 的文档，在此文档中不做详尽解释。

于是我们转到[Popover的文档](https://element-plus.org/zh-CN/component/popover.html#api)，在文档中找到了`popper-class`属性，如下

`popper-class` 为 popper 添加类名 `string`

于是我们就可以给弹窗添加一个唯一的class，如下

```vue
<el-popconfirm popper-class="red-popconfirm">
    <el-button>点击</el-button>
</el-popconfirm>
```

这样就可以给弹窗添加一个唯一的class了

