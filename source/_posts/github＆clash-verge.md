---
title: github＆clash-verge
date: 2025-03-17 14:38:48
tags:
  github
categories:
  教程
---
# 问题描述

因为众所周知的原因，国内无法直连github

这就导致国内的开发者很难使用github的服务，在一些情况下，clash这样的代理软件打开后虽然浏览器可以访问github，但是 `git push`和 `git pull`这些命令却不能正常使用

# 问题解决

## 代理查询

首先我们在输入以下命令

```
git config --global http.proxy
git config --global https.proxy
```

这可以检测我们是否使用了git 代理

## 代理取消

如果使用了的话，我们需要先取消它们
通过以下命令实现

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

运行完成后再次使用代理检测中的命令检测是否取消成功

## 重新设置代理

首先我们要知道自己的代理软件的服务器地址，一般为 `127.0.0.1:****`
`****`为端口号，这个需要查看自己的软件，不能照搬
![](1742198026901.png)
从这里可以看出我的端口是 `7897`，则需要运行以下命令

```
git config --global http.proxy 127.0.0.1:7897
git config --global https.proxy 127.0.0.1:7897
```

命令运行后可再次运行检测代理命令来查看是否设置成功

## 设置完成

至此，设置完成，就可以正常推送拉取
