layout: post
title: Debian之vim配置篇
categories: Linux
date: 2016-01-20 21:57:07
tags:
- Linux
- Debian
- vim
- terminator
---

##安装vim替换debian自带的vi

    apt-get install vim

不需要从零开始学习配置vim, 直接用牛人的配置文件, 省得折腾.
[vimrc](https://github.com/amix/vimrc), 按照文档操作即可.

##安装terminator替换字体自带的terminal

    apt-get install terminator

##配置terminator颜色以及主题
[terminator-solarized](https://github.com/ghuntley/terminator-solarized)
美中不足的是, ls显示的文件和目录都是灰蒙蒙的, 这是因为默认情况下solarized各种bright方案基本都是灰色, 而系统默认显示目录和文件时多用bright色.
<!-- more -->
需要配置dircolors才能显示出彩色的文件和目录.
[dircolors-solarized](https://github.com/seebi/dircolors-solarized)
对照文档完成配置.
##最终效果:
![terminator](https://github.com/cls1991/MyBlog/raw/master/img/terminator.png)
