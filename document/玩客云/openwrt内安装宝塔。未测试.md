[宝塔面板：探索openwrt安装宝塔，搭建web网站论坛社区网校](http://52youguan.com/56781.html)

- ![有关](http://52youguan.com/wp-content/themes/zibll/img/avatar-default.png)

-  

- - [有关](http://52youguan.com/author/2)

    1月前发布

-  

- [关注](javascript:;)



[0](http://52youguan.com/56781.html#respond)420

*本帖最后由 离人难拥 于 2021-2-20 09:08 编辑*

本人小白新手，linux命令也不熟悉，学习，有老师的话请指教

先认识一下openwrt

> OpenWrt 可以被描述为一个嵌入式的 Linux 发行版。（主流路由器固件有 dd-wrt,tomato,openwrt,padavan四类）对比一个单一的、静态的系统，OpenWrt的包管理提供了一个完全可写的文件系统，从应用程序供应商提供的选择和配置，并允许您自定义的设备，以适应任何应用程序。
> 对于开发人员，OpenWrt 是使用框架来构建应用程序，而无需建立一个完整的固件来支持；对于用户来说，这意味着其拥有完全定制的能力，可以用前所未有的方式使用该设备。

所以很多linux命令是可以使用的。但是这个系统非常精简。

**网上参考链接只有两个**

> 网上唯一的参考只有两个
> 1：https://www.right.com.cn/forum/thread-785028-1-1.html
> 描述看，好像是啊openwrt上面装debian，也有一些错误，感觉比较不稳定，仔细学习看了
> 2：https://www.right.com.cn/forum/thread-4061094-1-1.html
> 这个是装docker容器，利用容器装Debian唯一的参考只有两个

根据思路第一种思路直接安装宝塔。第二种思路用docker容器安装宝塔

![img]()
**第一步，硬件刷openwrt，自行百度教程安装。**
**第二步，尝试安装宝塔。**
1.安装宝塔前，发现硬盘储存太小，于是按照宝塔论坛的帖子，挂载了一下U盘，没通过openwrt自带的挂载点挂载，我的设备识别不了

> 参考帖:https://www.bt.cn/bbs/thread-50002-1-1.html

1. mkdir -p /www
2. mkfs.ext4 /dev/sdb1 # sdb1自己的磁名 格式化当前分区
3. echo “/dev/sdb1 /www ext4 defaults 0 0” >> /etc/fstab #这句的时候openwrt挂了，顶掉了openwrt默认web访问页面

*复制代码*
通过宝塔官方提供的SSH宝塔终端照常访问SSH，既然挂掉了，索性直接尝试安装宝塔
![img](http://52youguan.com/wp-content/uploads/97/75f3bd5a403b7d0698c5709a49ef8f.png)

前天 11:47 上传


提示已有Web环境，安装宝塔可能影响现有站点
![img](http://52youguan.com/wp-content/uploads/8b/50dd9ea3901272fa9de51e4f7afeb6.png)

前天 11:49 上传


安装失败，重刷硬件，重新安装openwrt，下午继续更新………![img]()

![img]()

重装openwrt以后，继续，

2.好像解决了 U盘根目录扩容的问题。

> 参考链接：http://www.mamicode.com/info-detail-3039766.html

3.既然扩容解决了。根据思路一、继续安装宝塔。首先看了看，装debian系统就算了。
官方的几种系统安装方法都试试。
![img](http://52youguan.com/wp-content/uploads/45/abdaace16606b49c84ab53911948fe.png)

前天 15:09 上传



过分了，

> 官方手册：https://www.kancloud.cn/chudong/bt2017/424206

要求是512M内存最低，我这硬件只有256M内存，换个硬件，N1合适。

第二种思路是需要。安装docker，但是docker也需要内存，内存不足。
贴出我探索的部分，A，先在openwrt官方的软件库里有没有docker，opkg命令更新列表，查找列表

> 参考链接：https://www.bilibili.com/video/av970595502/

等我换个硬件继续更新……
![img]()
新淘了个台电的windo本。功耗非常小，适合架设小服务器。发现直接安装centos7了……
脱离了openwrt装宝塔的主题，等我继续淘个，目前来说，最适合的应该是N1……



© 版权声明