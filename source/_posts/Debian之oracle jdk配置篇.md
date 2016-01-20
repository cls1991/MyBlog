debian7.9默认安装openjdk6.0, 平时也够用, 以防万一, 最好还是切换到oracle jdk上.
jdk官方下载(http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
选择需要的版本下载.

jdk配置:
1.解压tar.gz文件

    cp ~/Downloads/jdk-8u71-linux-x64.tar.gz /opt/
    cd /opt
    mkdir jdk && cd jdk
    tar zxvf jdk-8u71-linux-x64.tar.gz
    rm jdk-8u71-linux-x64.tar.gz

2.替换openjdk

    update-alternatives --config java         // 查看所有jdk配置(主要知道openjdk的优先级)
    sudo update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_71/bin/java 1200      // 设置oracle jdk的优先级(只要比openjdk的数字大就行)
    sudo update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_71/bin/javac 1200   // 设置javac的优先级
    update-alternatives --display java     // 查看当前java配置
    update-alternatives --display javac    // 查看当前javac配置
    java -version
    javac -version

3.升级oracle jdk
可以多个版本共存或者删除老版本, 仅保留最新版本
同上操作, 以版本号区分jdk新旧, 设置优先级.
