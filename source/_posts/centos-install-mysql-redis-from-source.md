---
title: 'centos源码安装mysql, redis'
categories: Linux
tags:
  - mysql
  - redis
  - source
  - centos
  - mysql server
  - redis server
date: 2016-11-08 15:35:19
---



## 为什么选择源代码安装
选择源码安装, 主要原因在于维护开发/生产环境的一致, 另外也便于使用mysql, redis的一些新特性.

## 安装mysql
以mysql-5.5.24为例, 下载地址[mysql-5.5.24.tar.gz](http://120.52.72.24/cdn.mysql.com/c3pr90ntc0td/archives/mysql-5.5/mysql-5.5.24.tar.gz)

安装编译所需库:

	yum -y install make gcc-c++ cmake bison-devel  ncurses-devel

<!-- more -->
编译选项设置:

	cmake \
    -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
	-DMYSQL_DATADIR=/data/mysql/data \
	-DSYSCONFDIR=/etc \
	-DWITH_MYISAM_STORAGE_ENGINE=1 \
	-DWITH_INNOBASE_STORAGE_ENGINE=1 \
	-DWITH_MEMORY_STORAGE_ENGINE=1 \
	-DWITH_READLINE=1 \
	-DMYSQL_UNIX_ADDR=/var/lib/mysql/mysql.sock \
	-DMYSQL_TCP_PORT=3306 \
	-DENABLED_LOCAL_INFILE=1 \
	-DWITH_PARTITION_STORAGE_ENGINE=1 \
	-DEXTRA_CHARSETS=all \
	-DDEFAULT_CHARSET=utf8 \
	-DDEFAULT_COLLATION=utf8_general_ci

一般设置这些就够用了, 如果想了解更多, 请参考[MySQL Source-Configuration Options](http://dev.mysql.com/doc/refman/5.5/en/source-configuration-options.html)

安装:

	make && make install

## 配置mysql

	// 设置权限
	groupadd mysql
	useradd -g mysql mysql
    chown -R mysql:mysql /usr/local/mysql
    chown -R mysql:mysql /data/mysql/data

	// 初始化配置
    cd /usr/local/mysql
    ./scripts/mysql_install_db --user=mysql --datadir=/data/mysql/data

	// 拷贝配置文件
    cp support-files/my-large.cnf /etc/my.cnf

	// mysql开机启动
	cp support-files/mysql.server /etc/init.d/mysqld
    chkconfig --level 35 mysqld on

    // 启动mysql
    service mysqld start

	// 设置密码
    mysqladmin -uroot password "your password"

	// 允许root账户远程访问
	GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.169.%' IDENTIFIED BY 'your password' WITH GRANT OPTION;

	// 添加访客用户, 并授权
    CREATE USER 'guest'@'192.168.%' IDENTIFIED BY 'your password';
    GRANT SELECT ON your_database.your_table TO 'guest'@'192.168.%';

    // 取消授权(可选)
    INVOKE SELECT ON your_database.your_table FROM 'guest'@'192.168.%';

	// 防火期(/etc/sysconfig/iptables)
    -A INPUT -m state --state NEW -m tcp -p -dport 3306 -j ACCEPT
    service iptables restart
    iptables -L -n

## 安装redis
以redis-2.8.5为例, 下载地址[redis-2.8.5.tar.gz](http://download.redis.io/releases/redis-2.8.5.tar.gz)

编译安装:

	make && make install

## 配置redis

	// 拷贝配置文件
    mkdir /etc/redis
    cp redis.conf /etc/redis/6379.conf

	// 设置数据存储目录
    mkdir -p /data/redis/6379

	// 编辑配置文件, 修改以下4行
    daemonize yes
    pidfile /var/run/redis_6379.pid
    logfile /var/log/redis_6379.log
    dir /data/redis/6379

	// 系统配置(/etc/sysctl.conf), 添加1行
    vm.overcommit_memory=1

	sysctl vm.overcommit_memory=1
    sysctl -w fs.file-max=100000

	// redis开机启动
    cp utils/redis_init_script /etc/init.d/redis_6379
    // 编辑启动脚本(/etc/init.d/redis_6379), 添加3行(可参考/etc/init.d/mysqld)
    # Comments to support chkconfig on RedHat Linux
	# chkconfig: 2345 64 36
	# description:  Redis is a persistent key-value database

	chkconfig --level 345 redis_6379 on

	// 启动redis
    service redis_6379 start

后期, 主机/服务器上需要运行多个redis实例, 指定不同端口就行, 很方便.
