---
title: Ubuntu24.04用终端启动cursor
date: 2025-04-26 14:01:14
tags:
  [linux, Ubuntu, cursor]
categories:
  教程
---

此篇文章介绍如何在ubuntu24.04中用终端终端启动cursor

<!-- more -->

# 下载cursor

前往[官网](https://www.cursor.com/cn/downloads)，根据自己的设备下载对应版本的cursor即可

~~Ubuntu24自然下载的就是Appimage~~

# 安装 libfuse2

```bash
sudo apt update
sudo apt install libfuse2
```

~~其实我不用这个~~

有一个名为[星火软件商店](https://www.spark-app.store/download)的软件
性质比较像archlinux的aur，是一个第三方的软件库，用户们会自行打包上传软件
里面就有旧版本的cursor，安装后就有了运行环境

# 给Appimage执行权限

- 命令行方法

找到Appimage文件的位置并运行如下命令

```bash
cd /way/to/cusor/father
chmod +x cursor.AppImage
```

- 图形化方法

打开文件管理器，找到appimage文件位置，右键文件，在属性中启用允许执行

![](PE.png)

给予执行权限后双击Appimage就可以启动cursor
或者使用命令行启动`cursor.AppImage --no-sandbox`

# 添加cursor快捷方式到命令行

方法来源于cursor论坛中的[这篇帖子](https://forum.cursor.com/t/how-to-open-cursor-from-terminal/3757)

如果终端是zsh
```bash
 nvim ~/.zshrc
```

然后添加这么一段
```
function cursor {
  (nohup /path/to/cursor.appimage "$@" > /dev/null 2>&1 &)
}
```

如果是bash
```bash
nvim ~/.bashrc
```
然后添加这么一段
```
cursor() {
    /home/user/path_to_appimage/Cursor.AppImage "$@"
}
```

修改完成后运行
```
source ~/.zshrc
或是
source ~/.bashrc
```

至此，就可以运行cursor . 
来在cursor中打开当前文件夹了
***

相关文档：[在 Ubuntu 24.04 上安装 Cursor AI 代码编辑器](https://gist.github.com/evgenyneu/5c5c37ca68886bf1bea38026f60603b6)
这篇文章里面还提到了如何制作快捷方式