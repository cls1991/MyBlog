安装Debian7.9(wheezy)记录
----
###1. 刻录启动盘
1.镜像下载(http://cdimage.debian.org/mirror/cdimage/archive/7.9.0/amd64/iso-dvd/), 直接下载DVD_1.iso即可, 32位系统去相应目录下载.
2.Windows平台下制作启动盘
可供选择的软件比较多, 推荐2款自己平时常用的
ultraiso官网(https://www.ezbsystems.com/ultraiso/download.htm)
poweriso官网(http://www.poweriso.com/download.php)
选择对应版本安装即可, 软件具体使用方法百度/谷歌一下.
3.Linux平台下制作启动盘
推荐dd命令

    dd if=/path/to/debian.iso of=/dev/sdb bs=1M    // 替换成你的实际路径

###2. 安装Debian
1.可以选择文本安装/图形界面安装, 推荐新手使用后者, 操作更直观.
2.系统语言选择, 推荐英文系统
3.磁盘分区
Debian内置多种分区方案
1.使用整块磁盘, lvm支持
优点: lvm方便之后拓展分区大小
缺点: 单系统, 想装Windows/Linux多系统的不用考虑
2.手动选择磁盘
1.系统自动分区有2种方案
1.仅划分一个分区
优点: 简单, 不易犯错
缺点: 安全性低, 分区挂了, 系统也完了
2.划分/, /home, /usr, /var, /tmp分区以及swap空间
优点: 安全性高, 便于备份重要数据
缺点: 早期的分区太小, 后期只能不停的转移数据, 甚至是重装系统
2.手动分区(推荐)
考虑到系统自动分区, 部分分区大小可能不够用, 还是自己手动来.
预装Debian的磁盘大小: 304G
划分方案:
/: 15G
/usr: 40G
/var: 25G
/tmp: 5G
/home: 211G
swap: 8G(内存的2倍)
4.安装系统, 安装过程不要联网, 直接从启动盘安装软件; 可能会出现无线网卡固件缺失的情况, 不用管, 之后会处理;
按照默认规格安装, 经过一段时间的等待, 完成安装.

###3. 问题解决
1. 无线网卡驱动

    lspci                      // 找到无线网卡型号

比如, 我机器的无线网卡就是BCM43225, 有了这个, 问题就好办了.
访问Debian Wiki(https://wiki.debian.org/brcm80211)，查找解决方案.

2. 中文输入法
ibus:(https://wiki.debian.org/I18n/ibus)
fcitx: (https://wiki.debian.org/gnome-chinese-input)
参照文档操作即可, 需要注销或者重启电脑.

3. 谷歌浏览器书签和tab页标题中文乱码

    sudo apt-get install ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy

安装相应的字体库, 重启chrome.

4. lantern无法启动
官网(https://getlantern.org/)被墙, 打不开.
Github(https://github.com/getlantern/lantern), 下载对应版本的lantern, 安装即可.

    /.lantern/bin/lantern： error while loading shared libraries： libappindicator3.so.1： cannot open shared object file： No such file or directory

解决方案:

    apt-cache search libappindicator3

安装缺失的库:

    apt-get install ibappindicator3-1

