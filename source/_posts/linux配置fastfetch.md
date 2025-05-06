---
title: linux配置fastfetch
date: 2025-05-06 14:31:37
tags:
  [linux,fastfetch]
categories:
  教程
---

这篇文章用于记录如何在ubuntu24.04中安装kitty并将其设置为默认终端

<!-- more -->

# 美化样式

## 创建配置文件

路径为 `~/.config/fastfetch/config.toml`

个人比较喜欢这一套，直接复制即可

```
{
    "$schema": "https://github.com/fastfetch-cli/fastfetch/raw/dev/doc/json_schema.json",
    "logo": {
        "type": "small",
        "padding": {
            "top": 1
        }
    },
    "display": {
        "separator": " "
    },
    "modules": [
        {
            "key": "╭───────────╮",
            "type": "custom"
        },
        {
            "key": "│  user    │",
            "type": "title",
            "format": "{user-name}"
        },
        {
            "key": "│ 󰇅 hname   │",
            "type": "title",
            "format": "{host-name}"
        },
        {
            "key": "│ 󰅐 uptime  │",
            "type": "uptime"
        },
        {
            "key": "│ {icon} distro  │",
            "type": "os"
        },
        {
            "key": "│  kernel  │",
            "type": "kernel"
        },
        {
            "key": "│ 󰇄 desktop │",
            "type": "de"
        },
        {
            "key": "│  term    │",
            "type": "terminal"
        },
        {
            "key": "│  shell   │",
            "type": "shell"
        },
        {
            "key": "│ 󰍛 cpu     │",
            "type": "cpu",
            "showPeCoreCount": true
        },
       /* {
            "key": "│ 󰍹 gpu     │",  // ★ GPU 模块
            "type": "gpu"
        },*/
        {
            "key": "│ 󰉉 disk    │",
            "type": "disk",
            "folders": "/"
        },
        {
            "key": "│  memory  │",
            "type": "memory"
        },
        {
            "key": "│ 󰩟 network │",
            "type": "localip",
            "format": "{ipv4} ({ifname})"
        },
        {
            "key": "├───────────┤",
            "type": "custom"
        },
        {
            "key": "│  colors  │",
            "type": "colors",
            "symbol": "circle"
        },
        {
            "key": "╰───────────╯",
            "type": "custom"
        }
    ]
}
```

# 配置启动规则

我使用zsh，因此配置在`~/.zshrc`

## 打开终端自动运行fastfetch

只需要在文件中添加
```
fastfetch
```
这一行即可

但是这会引出其他问题,我并不希望在任何地方，一打开终端就运行它，就比如vscode，cursor,nvim中

## 配置启动规则

为了不让fastfetch在任何地方都启动，需要添加规则

把配置文件中的`fastfetch`更改为下面这一段

```
# fastfetch
# Run fastfetch only when NOT in VSCode terminal or nvim
if [[ "$TERM_PROGRAM" != "vscode" && -z "$VSCODE_INJECTION" && -z "$NVIM" ]]; then
  fastfetch
fi
```
这样就可以保证fastfetch只有在打开终端软件时才会运行
