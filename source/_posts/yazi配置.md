---
title: yazi配置
date: 2025-05-09 09:57:37
tags:
  [linux,yazi]
categories:
  教程
---

这篇文章用于记录如何在ubuntu24.04中配装和配置yazi

<!-- more -->

# yazi的安装

[官方文档](https://yazi-rs.github.io/docs/installation)

我选择brew安装
在终端中运行以下命令
```
brew install yazi ffmpeg sevenzip jq poppler fd ripgrep fzf zoxide resvg imagemagick font-symbols-only-nerd-font
```

除了`yazi`外这个命令还安装了必要的依赖项，可以删掉，但是可能会对功能造成影响

~brew真的是很好的包管理器~

# yazi的配置

## 配置启动命令

[官方文档](https://yazi-rs.github.io/docs/quick-start)

在安装完成后在命令行运行`yazi`就可以启动程序
但这还不够

在终端配置文件`.zshrc`,也可能是其他，添加以下

```
function y() {
	local tmp="$(mktemp -t "yazi-cwd.XXXXXX")" cwd
	yazi "$@" --cwd-file="$tmp"
	if cwd="$(command cat -- "$tmp")" && [ -n "$cwd" ] && [ "$cwd" != "$PWD" ]; then
		builtin cd -- "$cwd"
	fi
	rm -f -- "$tmp"
}
```

这可以让我们只用一个`y`就可以启动`yazi`，更重要的是在这样配置后，我们在`yazi`中跳转到某个位置退出后，终端会同步位置

## 配置启动器

[官方文档](https://yazi-rs.github.io/docs/faq/#why-cant-edit)

在`yazi`中，快捷键`o`可以打开文件，而在linux中默认的`EDITOR`是`vim`

将其更改为`nvim`

进行以下配置
```
# yazu Setup
export EDITOR='nvim'
```

至此，`yazi`就可以使用了

