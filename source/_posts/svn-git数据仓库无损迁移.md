title: svn/git数据仓库无损迁移
date: 2016-07-16 22:15:27
tags:
- svn
- git
- gitlab
- commit log
- 无损迁移
- 提交记录
- 数据仓库
---

前几天，公司的ubuntu desktop出现不定期死机，上面托管着公司的项目代码(git管理)，美术资源(svn管理), 以及bug追踪系统(禅道管理), 排查了不是内存/cpu故障, 最终定位貌似是硬件故障. 为了一劳永逸, 干脆拿出一台古董机安装了mini版的centos server, 接下来的工作就是数据仓库迁移了. 

1.svn

配置文件迁移: 直接拷贝故障机器上svn的配置文件, 确保用户/权限分配正常; 数据迁移: 考虑到需要保留提交记录, 采用原生的svnadmin进行操作.

	svnadmin dump oldRepository > dumpfile       // 备份数据仓库
	svnadmin create newRepository               // 新建数据仓库
	svnadmin load newRepository < dumpfile      // 还原数据仓库

2.git

使用gitlab搭建内部git管理平台, 为了保留提交记录, 使用内置的gitlab-rake工具进行数据仓库迁移的工作.

<!-- more -->

数据仓库备份:

	gitlab-rake gitlab:backup:create         // 备份整个数据仓库

使用以上命令会在/var/opt/gitlab/backups目录下创建一个名称类似为1393513186_gitlab_backup.tar的压缩包, 这个压缩包就是Gitlab整个的完整部分, 其中开头的1596713186是备份创建的日期.

数据仓库还原:
	
	# 停止gitlab相关数据连接服务
	gitlab-ctl stop unicorn
	gitlab-ctl stop sidekiq
	
	# 从1596713186编号备份中恢复
	gitlab-rake gitlab:backup:restore BACKUP=1596713186

	# 启动gitlab
	sudo gitlab-ctl start

需要注意的是新服务器上的gitlab的版本必须与创建备份时的gitlab版本号相同.
	
	
	

