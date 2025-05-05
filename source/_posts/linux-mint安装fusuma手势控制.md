---
title: linux-mint安装fusuma手势控制
date: 2025-05-05 11:31:25
tags:
  [linux,linux-mint,fusuma]
categories:
  教程
---

这篇文章用于记录如何在linuxmint中安装fusuma来用触控板手势触发快捷键

<!-- more -->

# 安装必要的库
安装必要的包，终端输入：
```
sudo apt-get install libinput-tools
sudo apt-get install xdotool
sudo gem install fusuma
```
第三个命令中`gem`需要`Ruby`环境
输入以下命令安装环境
```
sudo apt-get install ruby
```
## 安装完成后输入命令以检测是否安装成功
```
sudo fusuma
```
![](测试fusuma.png)
出现这样的输出证明安装成功

# 书写配置文件

## 配置文件路径

```
~/.config/fusuma/config.yml
```

## 默认配置
```yml
swipe:
  3:
    left:
      command: 'xdotool key alt+Right'  # 切换到下一个工作区或窗口
    right:
      command: 'xdotool key alt+Left'   # 切换到上一个工作区或窗口
    up:
      command: 'xdotool key ctrl+t'     # 打开新标签页
    down:
      command: 'xdotool key ctrl+w'     # 关闭当前标签页
  4:
    left:
      command: 'xdotool key ctrl+alt+Right'  # 切换到下一个虚拟桌面
    right:
      command: 'xdotool key ctrl+alt+Left'   # 切换到上一个虚拟桌面
    up:
      command: 'xdotool key ctrl+alt+Down'   # 打开窗口切换器或访问不同的虚拟桌面
    down:
      command: 'xdotool key ctrl+alt+Up'     # 切换到上一个虚拟桌面或打开窗口切换器

pinch:
  2:
    in:
      command: 'xdotool key ctrl+equal'  # 放大
    out:
      command: 'xdotool key ctrl+minus'  # 缩小
  4:
    in:
      command: 'xdotool key ctrl+v'      # 粘贴剪贴板内容
    out:
      command: 'xdotool key alt+F10'     # 最大化窗口

threshold:
  swipe: 0.5  # 滑动手势的阈值设置为 50%
  pinch: 0.5  # 捏合手势的阈值设置为 50%

interval:
  swipe: 0.5  # 滑动手势的时间间隔设置为 0.5 秒
  pinch: 0.5  # 捏合手势的时间间隔设置为 0.5 秒

```
随后只需更改对应的快捷键即可