---
title: nvim实现剪切板与系统互通
date: 2025-05-07 15:40:21
tags:
  [linux,nvim]
categories:
  教程
---

这篇文章用于记录如何配置nivm的剪切板功能

<!-- more -->

# 首先需要确保系统中安装了xclip
~我使用Ubuntu~
linux安装`xclip`
在命令行中运行如下命令
```
sudo apt install xclip   # Debian/Ubuntu
sudo pacman -S xclip     # Arch
```

# 配置快捷键
~我使用lazyvim~
故执行需要`/home/prawn/.config/nvim/lua/config`在中添加以下配置
```
-- 复制到剪贴板
vim.keymap.set("v", "<leader>y", '"+y', { desc = "复制到剪贴板" })
vim.keymap.set("n", "<leader>Y", '"+yg_', { desc = "复制整行到剪贴板" })
vim.keymap.set("n", "<leader>y", '"+y', { desc = "复制光标位置后的内容到剪贴板" })
vim.keymap.set("n", "<leader>yy", '"+yy', { desc = "复制整行到剪贴板" })

-- 从剪贴板粘贴
vim.keymap.set("n", "<leader>p", '"+p', { desc = "从剪贴板粘贴" })
vim.keymap.set("n", "<leader>P", '"+P', { desc = "从剪贴板粘贴到光标前" })
vim.keymap.set("v", "<leader>p", '"+p', { desc = "粘贴到选中的区域" })
vim.keymap.set("v", "<leader>P", '"+P', { desc = "粘贴到选中的区域" })
```

这样之后nvim和系统之间的剪切板就是通用的了
