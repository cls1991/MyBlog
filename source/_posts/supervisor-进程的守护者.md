---
title: supervisor--进程的守护者
categories: Linux
date: 2016-04-20 13:53:34
tags:
- supervisor
- python
- process
---

##为什么推荐supervisor
接触过后台开发的人, 应该对以下内容不陌生.
比如, 你开发了一个服务, 放在服务器上运行, 供客户端调用. 你会这样做, 以python程序为例说明:

	pyenv activate env_AntiCheat_2.7.9                                // 激活python虚拟环境
	nohup python AntiCheat.py > AntiCheat.log 2>&1 &                 // 以后台形式运行服务

如果代码有更新, 需要重新部署服务, 不得不找到进程id, 杀死.

	ps aux | grep AntiCheat.py                     // 找出进程id
    kill -9 xxx								   // 杀死进程

每次都重复着这样的操作, 实在是浪费时间, 当然你也可以针对每一个程序写一份脚本, 一旦服务数量很多, 重复性的劳动就会越来越多. 这时候就需要有一个程序能够统一管理目标服务.
<!-- more -->
## 安装supervisor

	pip install supervisor

手动编译安装亦可, 根据自己的需要选择一种安装途径.

## 配置supervisor
官方提供的样例配置[sample.conf](https://github.com/Supervisor/supervisor/blob/master/supervisor/skel/sample.conf)
我们只需要在其基础上进行修改即可使用.

	; Sample supervisor config file.
    ;
    ; For more information on the config file, please see:
    ; http://supervisord.org/configuration.html
    ;
    ; Notes:
    ;  - Shell expansion ("~" or "$HOME") is not supported.  Environment
    ;    variables can be expanded using this syntax: "%(ENV_HOME)s".
    ;  - Comments must have a leading space: "a=b ;comment" not "a=b;comment".
    ;  - Quotes around values are not supported, except in the case of
    ;    the environment= options as shown below.

    [unix_http_server]
    file=/tmp/supervisor.sock   ; (the path to the socket file)
    ;chmod=0700                 ; socket file mode (default 0700)
    ;chown=nobody:nogroup       ; socket file uid:gid owner
    ;username=user              ; (default is no username (open server))
    ;password=123               ; (default is no password (open server))

    ;[inet_http_server]         ; inet (TCP) server disabled by default
    ;port=127.0.0.1:9001        ; (ip_address:port specifier, *:port for all iface)
    username=cls1991              ; (default is no username (open server))
    password=asd123               ; (default is no password (open server))

    [supervisord]
    logfile=/tmp/supervisord.log ; (main log file;default $CWD/supervisord.log)
    logfile_maxbytes=50MB        ; (max main logfile bytes b4 rotation;default 50MB)
    logfile_backups=10           ; (num of main logfile rotation backups;default 10)
    loglevel=info                ; (log level;default info; others: debug,warn,trace)
    pidfile=/tmp/supervisord.pid ; (supervisord pidfile;default supervisord.pid)
    nodaemon=false               ; (start in foreground if true;default false)
    minfds=1024                  ; (min. avail startup file descriptors;default 1024)
    minprocs=200                 ; (min. avail process descriptors;default 200)
    ;umask=022                   ; (process file creation umask;default 022)
    ;user=chrism                 ; (default is current user, required if root)
    ;identifier=supervisor       ; (supervisord identifier, default is 'supervisor')
    ;directory=/tmp              ; (default is not to cd during start)
    ;nocleanup=true              ; (don't clean up tempfiles at start;default false)
    ;childlogdir=/tmp            ; ('AUTO' child log dir, default $TEMP)
    ;environment=KEY="value"     ; (key value pairs to add to environment)
    ;strip_ansi=false            ; (strip ansi escape codes in logs; def. false)

    ; the below section must remain in the config file for RPC
    ; (supervisorctl/web interface) to work, additional interfaces may be
    ; added by defining them in separate rpcinterface: sections
    [rpcinterface:supervisor]
    supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

    [supervisorctl]
    serverurl=unix:///tmp/supervisor.sock ; use a unix:// URL  for a unix socket
    ;serverurl=http://127.0.0.1:9001 ; use an http:// url to specify an inet socket
    ;username=chris              ; should be same as http_username if set
    ;password=123                ; should be same as http_password if set
    ;prompt=mysupervisor         ; cmd line prompt (default "supervisor")
    ;history_file=~/.sc_history  ; use readline history if available

    ; The below sample program section shows all possible program subsection values,
    ; create one or more 'real' program: sections to be able to control them under
    ; supervisor.

    ;[program:AntiCheat]
    ;command=python AntiCheat.py              ; the program (relative uses PATH, can take args)
    ;process_name=%(program_name)s ; process_name expr (default %(program_name)s)
    ;numprocs=1                    ; number of processes copies to start (def 1)
    directory=/home/taozhengkai/Developer/mygit/github/ThirdPlatform                ; directory to cwd to before exec (def no cwd)
    ;umask=022                     ; umask for process (default None)
    ;priority=999                  ; the relative start priority (default 999)
    ;autostart=true                ; start at supervisord start (default: true)
    ;startsecs=1                   ; # of secs prog must stay up to be running (def. 1)
    ;startretries=3                ; max # of serial start failures when starting (default 3)
    ;autorestart=unexpected        ; when to restart if exited after running (def: unexpected)
    ;exitcodes=0,2                 ; 'expected' exit codes used with autorestart (default 0,2)
    ;stopsignal=QUIT               ; signal used to kill process (default TERM)
    ;stopwaitsecs=10               ; max num secs to wait b4 SIGKILL (default 10)
    ;stopasgroup=false             ; send stop signal to the UNIX process group (default false)
    ;killasgroup=false             ; SIGKILL the UNIX process group (def false)
    ;user=chrism                   ; setuid to this UNIX account to run the program
    ;redirect_stderr=true          ; redirect proc stderr to stdout (default false)
    ;stdout_logfile=/a/path        ; stdout log path, NONE for none; default AUTO
    ;stdout_logfile_maxbytes=1MB   ; max # logfile bytes b4 rotation (default 50MB)
    ;stdout_logfile_backups=10     ; # of stdout logfile backups (default 10)
    ;stdout_capture_maxbytes=1MB   ; number of bytes in 'capturemode' (default 0)
    ;stdout_events_enabled=false   ; emit events on stdout writes (default false)
    ;stderr_logfile=/a/path        ; stderr log path, NONE for none; default AUTO
    ;stderr_logfile_maxbytes=1MB   ; max # logfile bytes b4 rotation (default 50MB)
    ;stderr_logfile_backups=10     ; # of stderr logfile backups (default 10)
    ;stderr_capture_maxbytes=1MB   ; number of bytes in 'capturemode' (default 0)
    ;stderr_events_enabled=false   ; emit events on stderr writes (default false)
    environment=PATH="/home/taozhengkai/.pyenv/versions/env_AntiCheat_2.7.9/bin"       ; process environment additions (def no adds)
    ;serverurl=AUTO                ; override serverurl computation (childutils)

    ; The below sample eventlistener section shows all possible
    ; eventlistener subsection values, create one or more 'real'
    ; eventlistener: sections to be able to handle event notifications
    ; sent by supervisor.

    ; The below sample group section shows all possible group values,
    ; create one or more 'real' group: sections to create "heterogeneous"
    ; process groups.

    ;[group:thegroupname]
    programs=AntiCheat  ; each refers to 'x' in [program:x] definitions
    ;priority=999                  ; the relative start priority (default 999)

    ; The [include] section can just contain the "files" setting.  This
    ; setting can list multiple files (separated by whitespace or
    ; newlines).  It can also contain wildcards.  The filenames are
    ; interpreted as relative to this file.  Included files *cannot*
    ; include files themselves.

    ;[include]
    ;files = relative/directory/*.ini

配置完毕之后, 启动supervisor服务

	supervisord -c supervisord.conf                     // 从指定的配置文件启动supervisor

如果配置了web管理接口, 直接访问http://127.0.0.1:9001(默认配置), 用户名和密码默认或者自定义都行:

        [inet_http_server]         ; inet (TCP) server disabled by default
        port=127.0.0.1:9001        ; (ip_address:port specifier, *:port for all iface)
        username=cls1991              ; (default is no username (open server))
        password=asd123               ; (default is no password (open server))

代码更新之后, 可以利用web管理页面重新部署进程, 便利不少. 想更深入了解supervisor, 请访问[supervisor官网](http://supervisord.org/).
