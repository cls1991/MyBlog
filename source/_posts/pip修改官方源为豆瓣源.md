title: pip修改官方源为豆瓣源
date: 2015-11-29 20:14:45
tags:
- pip
- python
---

使用pip安装python依赖库, 经常网速很慢, 甚至被墙, 无法完成安装. 好在国内有较为成熟的pip镜像站, 这里选择豆瓣源.

编辑配置文件, 如果没有, 新建一份:
	
	vi ~/.pip/pip.conf

<!-- more -->

添加内容如下:
	
	[global]
	index-url = http://pypi.douban.com/simple
	trusted-host = pypi.douban.com

另外, 使用setup.py安装依赖库, 还是会从默认的http://pypi.python.org下载, 解决方案如下:

编辑配置文件, 如果没有, 新建一份:
	
 	vi ~/.pydistutils.cfg
 
 添加内容如下:
 	
 	[easy_install]
	index_url = http://pypi.douban.com/simple
	trusted-host = pypi.douban.com

之后便可以安装需要的依赖库了.

ps: 下面是国内几个常见的pip源, 大家根据自己的地理位置, 选择对应的源.

	http://pypi.hustunique.com/ 华中理工大学
	http://pypi.sdutlinux.org/ 山东理工大学
	http://pypi.mirrors.ustc.edu.cn/ 中国科学技术大学


