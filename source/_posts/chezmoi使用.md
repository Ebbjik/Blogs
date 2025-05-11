---
title: chezmoi使用
date: 2025-05-11 22:10:58
tags: [chezmoi, linux]
categories: 教程
---

这篇文章学习如何安装和使用`chezmoi`

<!-- more -->

# chezmoi的安装

[官方文档](https://www.chezmoi.io/install/)

官方给了很多安装方法
~我还是用brew~
在终端运行以下代码

```
brew install chezmoi
```

# chezmoi的使用

## 初始化chezmoi

当安装好后，运行以下命令来初始化`chezmoi`

```
chezmoi init
```

这将在 ~/.local/share/chezmoi 中创建一个新的 git 本地仓库，chezmoi 将在其中存储其源状态。默认情况下，chezmoi 仅修改工作副本中的文件。

## 用chezmoi管理文件

#### 把文件添加到chezmoi

```
chezmoi add ~/.bashrc
```

这会将 `~/.bashrc` 复制到 `~/.local/share/chezmoi/dot_bashrc` .

#### 修改文件

```
chezmoi edit ~/.bashrc
```

~也不是非要用这个，可以先改源文件，然后重新运行添加命令~

#### 集成github

```
chezmoi cd //这会跳转到~/.local/share/chezmoi/
git init
git remote add origin git@github.com:yourname/dotfiles.git
git add .
git commit -m "Initial chezmoi dotfiles"
git push -u origin main
```

通过这些命令，把数据同步到github
~记得创建私有仓库~

### 在另一台电脑应用配置

```
chezmoi init https://github.com/$GITHUB_USERNAME/dotfiles.git
chezmoi apply
```

在`init`时带上仓库url，chezmoi会自动克隆远程仓库中的文件

#### 初始化后获取最新配置

```
chezmoi update
```

---

通过chezmoi,我们可以方便的配置`nvim`,`.zshrc`之类的配置
