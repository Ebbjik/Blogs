---
title: Ubuntu24.04设置默认终端为kitty
date: 2025-04-24 12:34:03
tags:
  [linux, Ubuntu]
categories:
  教程
---


这篇文章用于记录如何在ubuntu24.04中安装kitty并将其设置为默认终端

<!-- more -->

# 前言
ubuntu默认的终端不支持图片预览，因此想要更换

# 安装kitty

[官方文档](https://sw.kovidgoyal.net/kitty/binary/#binary-install)写的十分详细,只需要两个步骤即可完成安装

1. 在终端中运行如下指令
```bash
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```

2. 运行以下指令以创建快捷方式（可选）

```bash
# Create symbolic links to add kitty and kitten to PATH (assuming ~/.local/bin is in
# your system-wide PATH)
ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten ~/.local/bin/
# Place the kitty.desktop file somewhere it can be found by the OS
cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/
# If you want to open text files and images in kitty via your file manager also add the kitty-open.desktop file
cp ~/.local/kitty.app/share/applications/kitty-open.desktop ~/.local/share/applications/
# Update the paths to the kitty and its icon in the kitty desktop file(s)
sed -i "s|Icon=kitty|Icon=$(readlink -f ~)/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty*.desktop
sed -i "s|Exec=kitty|Exec=$(readlink -f ~)/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty*.desktop
# Make xdg-terminal-exec (and hence desktop environments that support it use kitty)
echo 'kitty.desktop' > ~/.config/xdg-terminals.list
```

至此kitty就已经安装成功了

# 设置kitty为默认终端

虽然现在已经安装了kitty，但是点击快捷键`ctrl+alt+t`呼出的还是ubuntu默认的快捷键

这就需要更换默认终端

1. 查找kitty的位置

软件默认安装在`/home/{用户名}/.local/kitty.app/bin/kitty`
如果路径不对，就全局搜索名字为`kitty`的文件，找到那个点击就可以运行终端的文件的路径

2. 注册 kitty 作为终端选项

运行这个命令
```bash
sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator /usr/bin/kitty 50
// /usr/bin/kitty 代表第一步中找到的文件的路径，更换为真实路径
```

3. 选择kitty为默认终端

在终端运行这个命令
```bash
sudo update-alternatives --config x-terminal-emulator
```
会看到以下页面
![](image.png)

选择kitty即可（键入1）

至此，成功安装了kitty并将其设置为了默认终端，用终端快捷键`ctrl+alt+t`检查，呼出的是kitty终端，操作结束

# 后记-4.26

kitty不支持fcitx4，有相关需要的注意