title: proxychains为python脚本穿越GW
date: 2015-11-26 15:26:34
tags:
- shadowsocks
- proxychains
- python
---
安装环境:
- ubuntu 14.10
- python 2.7.6

----------

经常执行python脚本, 碍于防火墙GW, 很多请求都被屏蔽了, 因此, 需要像proxychains这样的神器, 帮助我们透过GW, 获取我们想要的资源. 
<!-- more  -->

###1. 安装shadowsocks
这里只介绍shadowsocks在ubuntu上的配置, 至于vps或vpn的搭建, 大家可以移步[版瓦工](https://bandwagonhost.com/), 套餐自己选择. 

	sudo apt-get install shadowsocks     # 安装shadowsocks

修改shadowsocks配置文件:
	
	sudo vim /etc/shadowsocks/config.json

编辑配置文件, 类似如下形式:
	
	{ 
	    "server": "107.182.xxx.xx", 
	    "server_port": 12035, 
	    "local_address": "127.0.0.1",
	    "local_port": 1080, 
	    "password": "ZmJkYWJlxxx", 
	    "timeout": 512, 
	    "method": "aes-256-cfb", 
	    "fast_open": false, 
	    "workers": 1 
	}

其中, server, server_port, local_port, password修改成自己对应的服务器配置即可.

运行shadowsocks服务:
	
	sslocal -c /etc/shadowsocks/config.json

###2. 安装proxychains
ubuntu安装proxychains, 这里直接通过软件源安装
	
	sudo apt-get install proxychains

修改proxychains配置文件:
	
	sudo vim /etc/proxychains.conf

编辑配置文件, 类似如下形式:
	
	socks5 127.0.0.1 1080      # 这里1080端口为shadowsocks配置文件中的local_port项

测试一下, proxychains服务是否可用.

	proxychains curl https://twitter.com/

proxychains执行python脚本的示例, 请移步[github demo](https://github.com/cls1991/DataKit.git).


