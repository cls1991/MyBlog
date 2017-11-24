---
layout: post
title: 获取golang.org安装包
date: 2017-11-24 11:49:48
categories: golang
tags:
  - golang.org
  - polipo
  - socks5 proxy
---


## 目前, [golang.org](https://golang.org/)仍被GFW封锁, 导致部分golang包无法安装.

### 1. github下载安装包

	$ cd $GOPATH/src
    $ git clone https://github.com/golang/net golang.org/x/net

### 2. 添加http代理

	$ sudo polipo socksParentProxy=localhost:1080 &
    $ https_proxy=http://localhost:8123 go get golang.org/x/net

<!-- more -->

推荐后者, 灵活方便.

ps: [polipo传送门](https://github.com/shadowsocks/shadowsocks/wiki/Convert-Shadowsocks-into-an-HTTP-proxy)


