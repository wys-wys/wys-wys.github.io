作者：橘子
链接：https://www.zhihu.com/question/26190694/answer/61118139
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



BusyBox 包含了一些简单的工具，例如 cat 和 echo，还包含了一些更大、更复杂的工具，例如 grep、find、mount 以及 telnet。简单的说BusyBox就好像是个大工具箱，它集成压缩了 Linux 的许多工具和命令。（摘自百度百科）一般用在Android上，解决[adbshell命令不全](https://link.zhihu.com/?target=http%3A//blog.csdn.net/lhj0711010212/article/details/9273107)在Android安装BusyBox：先要把手机给Root了，具体教程这里就不提供了，网上有很多。1.下载BusyBox的binary，打开这个地址 [Index of /downloads/binaries](https://link.zhihu.com/?target=http%3A//www.busybox.net/downloads/binaries) ，选择最新版本，然后下载对应你的设备架构的版本，这里我下载了busybox-armv6l，下面将以这个文件名为示例。2. 需要有一个命令行的环境，在电脑上使用adb或在手机上使用terminal emulator。3. 连接手机和电脑，手机的USB Mode设置成None（仅充电），并且开启USB调试模式。安装：1. 将busybox-armv6l重命名为busybox2. 将busybox传入手机的SD卡，可以使用下面的命令或自己想其他办法。打开terminal（Linux，Mac）或cmd（Windows）
adbpush ~/Desktop/busybox /mnt/sdcard

其中的~/Desktop请根据自己的情况替换成正确的路径3. 输入以下命令，为了在/system目录写入文件
adb shell
su
mount -o remount,rw -t yaffs2 /dev/block/mtdblock3 /system
使用 ls 检查一下 /system 里是否有 xbin 目录，没有的话输入 mkdir xbin 创建，因为本示例是要把busybox安装到 /system/xbin 。4. 复制 busybox 文件到 /system/xbin，并为其分配“可执行”的权限
cp /mnt/sdcard/busybox /system/xbin
chmod 755 busybox
\5. 这时就可以使用 busybox 的命令了，例如以前没有清屏的clear命令，现在只需输入 busybox clear 就可以实现清屏功能，使用完整版的 ls 只需输入 busybox ls 。但是每次前面都加上个busybox太麻烦了，所以我们还要继续完成安装。在 /system/xbin 下输入
busybox --install .
如果想安装到别的目录，则把点替换成别的路径。至此就安装完成了，比较一下原来的 ls 命令和 busybox 里的 ls 命令。常见错误：1. 如果安装时出现这样的错误，busybox: /bin/zcat: No such file or directorybusybox: /sbin/zcip: Invalid cross-device link说明没有输入安装路径，正确的示例 busybox --install /system/xbin2. 如果出现这样的错误，cp: /system/xbin/busybox: Read-only file system说明没有正确输入上面第三步的mount命令。小技巧：1. busybox 里有 ash 和 hush 还有 sh 这几种 shell，在命令行输入 ash 或 hush，可以像在 bash 里那样，通过按上下键选择刚才输入的命令。2. android系统本身就有ls命令，busybox里也有ls，输入ls时调用的是android的ls，那么想用busybox的ls就要每次都在前面加个busybox吗？不用，使用alias命令可以搞定。
alias ls='busybox ls'
同样的，cp、mv等二者都有的命令都可以这样搞定。也可以通过修改 /init.rc 来解决。
([android busybox解决adbshell命令不全](https://link.zhihu.com/?target=http%3A//blog.csdn.net/lhj0711010212/article/details/9273107))

[编辑于 2015-08-27](http://www.zhihu.com/question/26190694/answer/61118139)

赞同 244 条评论

分享

收藏喜欢



收起

继续浏览内容

![img](https://gitee.com/wys-wys/picgo/raw/master/picgo/v2-10e18ff65a640175ad058b4b5dfd2867_1440w.png)

知乎

发现更大的世界

打开

![img](https://gitee.com/wys-wys/picgo/raw/master/picgo/v2-a448b133c0201b59631ccfa93cb650f3_1440w.png)

Chrome

继续



[![张良怀](https://pic1.zhimg.com/v2-f1f638747d3e4f5e1aeda26df46c7d3b_xs.jpg?source=1940ef5c)](https://gitee.com/wys-wys/picgo/raw/master/picgo/brisyramshere)

[张良怀](https://gitee.com/wys-wys/picgo/raw/master/picgo/brisyramshere)[](https://www.zhihu.com/question/48510028)

西安交通大学 生物医学工程硕士

7 人赞同了该回答创建于: 2014-11-18 15:15:19  编辑于: 2014-11-18 15:15:19

安卓虽然是基于linux，但是精简了很多linux工具，很多常用的linux指令不能使用。
busybox相当于一个打包的工具箱，打包了很多的常用的linux可执行文件和其依赖。安装了busybox你就可以在安卓下下载一个模拟终端然后在里面运行一些之前不能运行的指令。
当然还有如果你想在安卓上探索更多有关它的linux的本质，安装上这个有必要。

[发布于 2014-11-18](http://www.zhihu.com/question/26190694/answer/33597226)

赞同 7添加评论

分享

收藏喜欢



继续浏览内容

![img](https://gitee.com/wys-wys/picgo/raw/master/picgo/v2-10e18ff65a640175ad058b4b5dfd2867_1440w.png)

知乎

发现更大的世界

打开

![img](https://gitee.com/wys-wys/picgo/raw/master/picgo/v2-a448b133c0201b59631ccfa93cb650f3_1440w.png)

Chrome

继续



[![王小Y](https://pic2.zhimg.com/da8e974dc_xs.jpg?source=1940ef5c)](https://gitee.com/wys-wys/picgo/raw/master/picgo/wang-xiao-y-38)

[王小Y](https://gitee.com/wys-wys/picgo/raw/master/picgo/wang-xiao-y-38)

1 人赞同了该回答创建于: 2015-08-28 14:32:49  编辑于: 2015-08-28 14:32:49

个人理解busybox应该就是独特的封装的linux驱动的工具箱，linux的常用命令基本都是可以使用的，楼上不知道为什么会说不能使用，专业版的功能能够在手机上完成很多事情，详情参照：[Linux工具箱使用说明,Linux工具箱使用教程](https://link.zhihu.com/?target=http%3A//www.anruan.com/news/10093.html)。