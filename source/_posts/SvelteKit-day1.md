---
title: SvelteKit学习-day1
date: 2025-03-22 21:51:39
tags:
  sveltekit
  前端
categories:
  学习
---

此篇文章介绍如何创建一个sveltekit项目

<!-- more -->

# 创建一个sveltekit项目

只需运行命令`npx sv create %项目名%`即可开始创建

随后在弹出的命令行按需选择即可

1. 选择生成的框架类型
![](1.png)
   1. SvelteKit demo app
特点：创建一个简单的用于展示的 Demo 项目，通常包含一个猜谜游戏等示例内容。
适用场景：主要用于学习和演示 SvelteKit 的基本功能，帮助开发者快速了解其工作方式。
项目结构：会包含一些预设的页面和功能，方便用户直接运行和查看效果。
   2. Skeleton project
特点：生成一个基本的应用骨架，包含最基础的文件和目录结构，没有过多的预设内容。
适用场景：适合正式的项目开发，开发者可以根据自己的需求自由添加页面、组件和功能。
项目结构：通常包含基本的 src 目录、routes 文件夹、app.html 等，适合从零开始构建项目。
   3. Library skeleton project
特点：用于创建 Svelte 组件库或其他库项目，提供了一个适合开发库的基础结构。
适用场景：如果需要开发一个可复用的 UI 组件库或其他库，这个类型是最佳选择。
项目结构：会包含一些用于构建和打包库的配置文件和目录结构，支持通过 svelte-package 插件进行分发。

2. 选择是否在项目中添加 TypeScript 的类型检查功能
![](2.png)
   1. Yes, using TypeScript syntax
   选择这个选项会将项目转换为使用 TypeScript 语法。这意味着你的代码文件将从 .js 扩展名改为 .tsx 或 .ts（取决于是否使用了 React），并且你可以利用 TypeScript 提供的类型系统来增强代码的可读性和可维护性。
   2. Yes, using JavaScript with JSDoc comments
   选择这个选项会在项目中使用 JavaScript 语法，但通过 JSDoc 注释来提供类型信息。JSDoc 是一种在 JavaScript 代码中添加文档注释的方式，这些注释可以用来描述函数、变量等的类型信息。这种方式不需要将代码转换为 TypeScript 语法，但仍然可以提供一定程度的类型检查。
   3. No
   选择这个选项表示不添加类型检查。项目将继续保持使用纯 JavaScript 语法，不使用 TypeScript 或 JSDoc 注释来提供类型信息。

3. 根据需求预装插件
![](3.png)
可使用方向键移动，空格键选择，回车键进入下一步
   - prettier：一个流行的代码格式化工具，可以帮助开发者以一致的风格格式化代码。它支持多种编程语言，并且可以通过配置文件自定义格式化规则。
   - eslint：一个 JavaScript 代码质量和代码风格检查工具。它可以帮助开发者发现代码中的错误，并且可以配置规则来强制执行特定的代码风格。（这个插件比prettier更加严格，严格到可以规定使用单引号还是双引号）
   - vitest：一个快速的单元测试框架，用于测试 JavaScript 和 TypeScript 代码。
   - playwright：一个用于自动化浏览器测试的工具，支持多种浏览器和多种测试场景。
   - tailwindcss：一个实用优先的 CSS 框架，用于快速构建自定义设计的工具。
   - sveltekit-adapter：SvelteKit 的适配器，用于部署 SvelteKit 应用。
   - drizzle：一个用于构建和连接数据库的库，通常与 Next.js 一起使用。
   - lucia：一个用于构建用户界面的库，可能是一个特定项目的内部工具或库。
   - mdsvex：一个将 Markdown 文件转换为 Svelte 组件的工具，常用于构建静态网站。
   - paraglide：一个用于适配多种语言的插件。
   - storybook：一个前端组件开发环境，允许开发者在隔离的环境中开发和测试 UI 组件

4. 选择包管理器
![](4.png)
关于各种包管理器的比较有很多，这里不多赘述

至此，项目创建完成，运行以下命令即可运行

```
1: cd 项目名                                                               
2: git init && git add -A && git commit -m "Initial commit" (optional)  
3: npm run dev -- --open
```
