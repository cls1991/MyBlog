打开终端, 通过ssh连接到Linux主机进行开发, 正常退出ssh后, Linux主机上的后台程序仍然会继续执行下去; 如果此时直接关闭终端或者遇到断电等异常情形, ssh退出了, 对应Linux主机上的后台服务也会退出, 解决方案可以是: 使用nohup命令屏蔽掉所有的挂断信号, 这样后台程序会一直执行, 不会被打断.

    测试用例: ping www.baidu.com

测试结果截图展示:
![ssh_problem_01](https://github.com/cls1991/MyBlog/raw/master/img/ssh_problem_01.png)
![ssh_problem_02](https://github.com/cls1991/MyBlog/raw/master/img/ssh_problem_02.png)
![ssh_p:roblem_03](https://github.com/cls1991/MyBlog/raw/master/img/ssh_problem_03.png)
