docker可道云怎么挂载移动硬盘_玩客云刷机系统之armbian挂载U盘增加空间

解忧子 2021-01-07 15:04:25  510  收藏 1
文章标签： docker可道云怎么挂载移动硬盘
版权

点击上方蓝字关注我们

回顾前几期和大家分享了玩客云刷机电视盒子、armbian系统、宝塔面板(5.9)、wrodpress博客。后面我准备搭建可道云做nas以方便给大家固件分享。但是因为 玩客云内存只有8G做nas远远不够所以就有了今天的 玩客云armbian系统挂载U盘/硬盘步骤的分享！ (如果确实对你有帮助记得帮我转发或者点下文字最方的转发哦) 准备工作 在正式操作之前我们首先了解一下如下几个linux命令以帮助我们更好的理解挂载步骤。 1. fdisk —— 是一个创建和维护分区表的程序，它兼容DOS类型的分区表、BSD或者SUN类型的磁盘列表。
语法
fdisk [必要参数][选择参数]
必要参数：

-l 列出所有分区表

-u 与"-l"搭配使用，显示分区数目

这里用到的命令为 fdisk -l 来查看当前分区情况。
2. mkfs.ext4 —— 创建ext4文件系统硬盘格式化。

命令语法
mkfs.ext4 [选项] [设备]

例如：将/dev/sda1分区格式化成ext4文件系统，命令为：

mkfs.ext4 /dev/sda1

3. blkid —— 查看块设备的文件系统类型、LABEL、UUID等信息。

语法

blkid -L | -U
blkid [-c ] [-ghlLv] [-o] [-s ][-t ] -[w ] [ ...]
blkid -p [-s ] [-O ] [-S ][-o] ...
blkid -i [-s ] [-o] ...
例如：显示指定设备dev/sda1的UUID：

sudo blkid -s UUID /dev/sda1
4.chmod ——控制文件如何被他人所调用，可以理解为给用户使用权限。
语法
chmod [-cfvR] [--help] [--version] mode file...
这里用到的命令为  chmod -R 777 来给创建目录最高权限。
其次还需要了解fstab文件： /etc/fstab 文件负责配置Linux开机时自动挂载的分区，某些时候当Linux系统下划分了新的分区后，需要将这些分区设置为开机自动挂载，否则，linux是无法使用新建的分区的。磁盘分区都必须挂载到目录树中的某个具体的目录上才能进行读写操作，而fstab正是负责这一配置。
开始挂载U盘/硬盘操作

一、U盘/硬盘接入USB接口。

二、用 fdisk -l 命令查看刚刚接入USB的U盘/硬盘并记下其设备名称，例如下图：

![107b1ad399a170a9954864b6119b6989.png](https://img-blog.csdnimg.cn/img_convert/107b1ad399a170a9954864b6119b6989.png)

三、用mkfs.ext4命令格式化硬盘位ext4格式，例如下图：

![f0f51bbbe3dee5d0877eb17768298bdc.png](https://img-blog.csdnimg.cn/img_convert/f0f51bbbe3dee5d0877eb17768298bdc.png)

格式化硬盘速度根据硬盘容量大于时间不同，一般的1T硬盘格式好大约需要15分钟左右。

四、用blkid 命令查看所需要挂载硬盘的UUID，并复制保存UUID。例如下图：

![f41de1f2d9d1427909baf9345f6df981.png](https://img-blog.csdnimg.cn/img_convert/f41de1f2d9d1427909baf9345f6df981.png)

图中使用的命令blkid /dev/sda1中的/dev/sda1为你需要挂载的设备名称。

五、挂载目录：

利用cd命令切换到要挂载的目标目录，然后利用mkdir命令创建挂载目录 ，也可以使用WinSCP软件直接目标目录下创建挂载目录。例如下图：

![f4dc8f4c010cfa1763d744dbfb6a4b6f.png](https://img-blog.csdnimg.cn/img_convert/f4dc8f4c010cfa1763d744dbfb6a4b6f.png)





![db8280bc735452a8534f24e5982858a2.png](https://img-blog.csdnimg.cn/img_convert/db8280bc735452a8534f24e5982858a2.png)六、打开/etc/fstab文件，在最后行追加(记住是追加，原有的内容不要动)下面内容：

UUID=a63dfbda-29c8-478f-a88e-55796514c961   /mnt/diskyingpan/   ext4    defaults    0 0

注意：

“06dc25bf-539f-4131-ac58-59cc45722dec”为你刚记录的UUID

“/mnt/diskyingpan/”为你创建的挂载目录，其他的不用改变。

七、给创建的拐杖目录权限

 chmod -R 777 /mnt/diskyingpan/

![94575bd6fc92e37695c9e08ce2693bf3.png](https://img-blog.csdnimg.cn/img_convert/94575bd6fc92e37695c9e08ce2693bf3.png)

注意：“/mnt/diskyingpan/”为你创建的挂载目录，这里的权限范围根据自己需要设置，不一定非得最高权限。

八、重启玩客云

使用命令reboot 重启一次系统，如果/mnt/diskyingpan目录下有一个lost+found目录说明挂载成功，那么挂载USB硬盘的工作就顺利完成。

![a53eb55715702b17c22458edd80cea9e.png](https://img-blog.csdnimg.cn/img_convert/a53eb55715702b17c22458edd80cea9e.png)

关注大毛爱分享获取更多资源哦！

关注大毛爱分享



下期预告：玩客云搭建宝塔面板7.3系统

点个“在看”表示朕

已阅

相关资源：玩客云综合工具(矿机监工)V1.1绿色免费版