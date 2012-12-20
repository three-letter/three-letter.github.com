---
layout: post
title: "Tmux基本使用"
date: 2012-12-19 23:41
comments: true
categories: tmux 
---

由于在工作中需要经常性使用终端且有多个操作同时进行，在正常的终端下需要开多个Tab或者窗口，不停的在之间来回切换，非常的麻烦。

[Tmux]的多session和窗口可分屏机制正好完美的解决了这种问题，现在就来体验tmux。

### 安装tmux

  sudo apt-get install tmux

### 基本用法

安装完成后，在终端中直接输入 `tmux` 即可启动。
启动后窗口的最下栏左侧有该tmux当前session(默认是数字0-9)和应用(默认是~）的名字，如：[blog] 0:vim\*

#### 1.创建命名session

创建指定名称的session

    tmux new-session -s blog

成功之后便可以该新tmux窗口中进行各种操作，同时可以通过快捷键C-b d退出该窗口(只是隐藏并未关闭该session)

#### 2.查询全部的session

可查询已创建的全部tmux session

  tmux list-sessions

#### 3.打开

可根据需要打开对应的session窗口

  tmux a -t blog

#### 4.关闭session

支持关闭指定session或全部关闭

  tmux kill-session blog
  tmux kill-server

### 5.窗口分屏

打开具体session窗口后，可通过快捷键对窗口进行相应的分屏操作

	C-b ": 上下分屏 
	C-b %:  左右分屏

同时分屏后有两种方式对各屏幕进行切换跳转

	C-b o: 当前屏幕往下切换
	C-b hjkl: 当前屏幕上下左右切换


最后附一张分屏后名为blog的tmux窗口

![tmux split](/images/tmux.png)

[Tmux]: http://tmux.sourceforge.net
