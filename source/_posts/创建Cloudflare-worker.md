---
title: 创建Cloudflare_worker
date: 2025-07-08 17:01:43
tags: [后端, js]
categories: 学习
---

# 目的

创建一个基于Cloudflare的轻量后端

# 步骤

## 注册`Cloudflare`账号

## 安装开发工具

1. 安装

```bash
npm install -g wrangler
```

2. 登陆

```bash
wrangler login
```

运行这个命令后会打开一个浏览器页面，正常登录

## 创建一个`Worker`项目

```bash
wrangler init my-worker
cd my-worker
```

根据自己的需求进行选择，即可创建项目
