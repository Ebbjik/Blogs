---
title: Ubuntu24.04安装搜狗输入法
date: 2025-04-19 11:39:17
tags:
---

此篇文章介绍如何在ubuntu24.04中安装搜狗输入法

<!-- more -->

# 更换fcitx版本

目前搜狗输入法官网的linux版适用于fcitx4，而ubuntu24.04自带fcitx5（且二者不兼容）所以首先要做的是更换fcitx版本

1. 卸载ubuntu原有的fcitx5

```
sudo apt purge fcitx5
```

2. 更新

```
sudo apt update
sudo apt upgrade 
```

3. 此时系统应该会提醒有未卸载的fcitx5依赖项,卸载这些依赖包

```
sudo apt autoremove 
```

4. 此时再安装fcitx

```
sudo apt install fcitx
```

- **此时应该会提示未完全卸载的** `“fcitx5-chinese-addons-data : 冲突: fcitx-data 但是 1:4.2.9.9-2build2 正要被安装”`

- 卸载`fcitx5-chinese-addons-data`即可
```
sudo apt remove fcitx5-chinese-addons-data
```

- 此时再运行安装命令,即可完成安装

```
sudo apt install fcitx
```

# 更换输入法框架

在语言支持中，更换输入法框架为`fcitx4`

![](更换输入法框架.png)

# 安装搜狗输入法

前往[搜狗输入法官网](https://shurufa.sogou.com/linux)下载对应的deb安装包即可

点击下载后会弹出[官方教程](https://shurufa.sogou.com/linux/guide)

deb安装包下载好后可以直接双击安装包进行安装，也可以通过命令行

```
sudo dpkg -i sogoupinyin_4.2.1.145_amd64.deb 
```

即可完成安装

安装好后这样配置

![](添加搜狗输入法.png)

# 配置默认激活输入法

经过上述步骤后，搜狗输入法已经安装完成，但是存在一个问题，输入法默认是没有激活的

这导致我们每次开机后要点击**ctrl+space**以激活输入法

开机后进入fcitx配置

![](配置输入法默认激活.png)

经过这样的设置后，开机搜狗输入法就会默认激活了


***

参考链接：[24.04的搜狗输入法安装](https://blog.csdn.net/weixin_44009267/article/details/144539057)