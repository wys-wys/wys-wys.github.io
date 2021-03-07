[*Linux开启Swap*分区](https://blog.csdn.net/hanziyuan08/article/details/85291719)2018-12-28 23:47:54

1. 创建要作为swap分区的文件:增加1GB大小的交换分区，则命令写法如下，其中的count等于想要的块的数量（bs*count=文件大小）。

```shell
$ dd if=/dev/zero of=/root/swapfile bs=1M count=1024
```

1. 格式化为交换分区文件:

```shell
$ mkswap /root/swapfile #建立swap的文件系统
```

1. 启用交换分区文件:

```shell
$ swapon /root/swapfile #启用swap文件
```

1. 使系统开机时自启用，在文件/etc/fstab中添加一行：

```shell
/root/swapfile swap swap defaults 0 0
```

## linux上swap的查看与调整

 (2012-06-12 10:17:16)

| 标签： oracle linux swap 杂谈 | 分类： [oracle实验笔记](http://blog.sina.com.cn/s/articlelist_1835947255_3_1.html) |
| ----------------------------- | ------------------------------------------------------------ |
|                               |                                                              |

1.查看SWAP

[root@192 oc]# cat /proc/swaps
Filename                Type      Size  Used  Priority
/dev/sda3               partition   8024  104  -1
[root@192 oc]#

 

2.通过DD创建文件

[root@192 oc]# dd if=/dev/zero of=/oc/swap bs=512 count=2000000
2000000+0 records in
2000000+0 records out
1024000000 bytes (1.0 GB) copied, 23.4213 seconds, 43.7 MB/s
[root@192 oc]#
[root@192 oc]# ll
总计 1001012
drwx------ 2 root root   16384 06-03 06:56 lost+found
-rw-r--r-- 1 root root 1024000000 06-12 10:24 swap
drwxr-xr-x 4 root root   4096 06-08 16:15 tmp
[root@192 oc]#

3.转化为swap格式
[root@192 oc]# mkswap /oc/swap
Setting up swapspace version 1, size = 1023995 kB
[root@192 oc]#

[root@192 oc]# free
      total   used   free  shared  buffers  cached
Mem:   1035108  1018168   16940     0   14716  892500
-/+ buffers/cache:  110952  924156
Swap:    8024    104   7920
[root@192 oc]#
启用，加入到swap池中。

[root@192 oc]# swapon /oc/swap

[root@192 oc]# free
      total   used   free  shared  buffers  cached
Mem:   1035108  1018228   16880     0   14748  892592
-/+ buffers/cache:  110888  924220
Swap:   1008016    104  1007912
[root@192 oc]#

 

[root@192 oc]# cat /proc/swaps
Filename                Type      Size  Used  Priority
/dev/sda3               partition   8024  104  -1
/oc/swap                file      999992 0   -4
[root@192 oc]#

 

从swap池中拿掉

[root@192 oc]# swapoff /oc/swap

[root@192 oc]# free
      total   used   free  shared  buffers  cached
Mem:   1035108  1018780   16328     0   15096  892760
-/+ buffers/cache:  110924  924184
Swap:    8024    104   7920

[root@192 oc]# cat /proc/swaps
Filename                Type      Size  Used  Priority
/dev/sda3               partition   8024  104  -1
[root@192 oc]#

 

开机自动启动：

[root@192 oc]# echo "/oc/swap swap swap defaults 0 0" >> /etc/fstab

[root@192 oc]# cat /etc/fstab
LABEL=/        /           ext3  defaults    1 1
LABEL=/boot      /boot         ext3  defaults    1 2
tmpfs         /dev/shm        tmpfs defaults    0 0
devpts         /dev/pts        devpts gid=5,mode=620 0 0
sysfs         /sys          sysfs defaults    0 0
proc          /proc         proc  defaults    0 0
LABEL=SWAP-sda3    swap          swap  defaults    0 0
/dev/sdb1   /oa  ext3  defaults    0 0
/dev/sdc1   /ob  ext3  defaults    0 0
/dev/sdd1   /oc  ext3  defaults    0 0
/dev/hdc    /media/dvd   iso9660 ro,auto 0 0
/oc/swap swap swap defaults 0 0
[root@192 oc]#

 

另：

将整个设备划为swap分区

fdisk时代码为82 linux swap，

分区后：

\# mkswap /dev/sdc3
\# swapon /dev/sdc3

荐 proc文件系统，用来查看进程Swap换出的虚拟内存大小，它保存在 /proc/pid/status中的VmSwap中（推荐你执行man proc来查询其他字段的含义）。

在第二个终端中运行下面的命令，就可以查看使用Swap最多的进程。注意for、awk、sort都是最常用的Linux命令，如果你还不熟悉，可以用man来查询它们的手册，或上网搜索教程来学习。

```
# 按VmSwap使用量对进程排序，输出进程名称、进程ID以及SWAP用量



$ for file in /proc/*/status ; do awk '/VmSwap|Name|^Pid/{printf $2 " " $3}END{ print ""}' $file; done | sort -k 3 -n -r | head



dockerd 2226 10728 kB



docker-containe 2251 8516 kB



snapd 936 4020 kB



networkd-dispat 911 836 kB



polkitd 1004 44 kB
```

从这里你可以看到，使用Swap比较多的是dockerd 和 docker-containe 进程，所以，当dockerd再次访问这些换出到磁盘的内存时，也会比较慢。

这也说明了一点，虽然缓存属于可回收内存，但在类似大文件拷贝这类场景下，系统还是会用Swap机制来回收匿名内存，而不仅仅是回收占用绝大部分内存的文件页。

最后，如果你在一开始配置了 Swap，不要忘记在案例结束后关闭。你可以运行下面的命令，关闭Swap：

```
$ swapoff -a
```

实际上，关闭Swap后再重新打开，也是一种常用的Swap空间清理方法，比如：

```
$ swapoff -a && swapon -a 
```

## linux上swap的查看与调整

 (2012-06-12 10:17:16)

| 标签： oracle linux swap 杂谈 | 分类： [oracle实验笔记](http://blog.sina.com.cn/s/articlelist_1835947255_3_1.html) |
| ----------------------------- | ------------------------------------------------------------ |
|                               |                                                              |

1.查看SWAP

[root@192 oc]# cat /proc/swaps
Filename                Type      Size  Used  Priority
/dev/sda3               partition   8024  104  -1
[root@192 oc]#

 

2.通过DD创建文件

[root@192 oc]# dd if=/dev/zero of=/oc/swap bs=512 count=2000000
2000000+0 records in
2000000+0 records out
1024000000 bytes (1.0 GB) copied, 23.4213 seconds, 43.7 MB/s
[root@192 oc]#
[root@192 oc]# ll
总计 1001012
drwx------ 2 root root   16384 06-03 06:56 lost+found
-rw-r--r-- 1 root root 1024000000 06-12 10:24 swap
drwxr-xr-x 4 root root   4096 06-08 16:15 tmp
[root@192 oc]#

3.转化为swap格式
[root@192 oc]# mkswap /oc/swap
Setting up swapspace version 1, size = 1023995 kB
[root@192 oc]#

[root@192 oc]# free
      total   used   free  shared  buffers  cached
Mem:   1035108  1018168   16940     0   14716  892500
-/+ buffers/cache:  110952  924156
Swap:    8024    104   7920
[root@192 oc]#
启用，加入到swap池中。

[root@192 oc]# swapon /oc/swap

[root@192 oc]# free
      total   used   free  shared  buffers  cached
Mem:   1035108  1018228   16880     0   14748  892592
-/+ buffers/cache:  110888  924220
Swap:   1008016    104  1007912
[root@192 oc]#

 

[root@192 oc]# cat /proc/swaps
Filename                Type      Size  Used  Priority
/dev/sda3               partition   8024  104  -1
/oc/swap                file      999992 0   -4
[root@192 oc]#

 

从swap池中拿掉

[root@192 oc]# swapoff /oc/swap

[root@192 oc]# free
      total   used   free  shared  buffers  cached
Mem:   1035108  1018780   16328     0   15096  892760
-/+ buffers/cache:  110924  924184
Swap:    8024    104   7920

[root@192 oc]# cat /proc/swaps
Filename                Type      Size  Used  Priority
/dev/sda3               partition   8024  104  -1
[root@192 oc]#

 

开机自动启动：

[root@192 oc]# echo "/oc/swap swap swap defaults 0 0" >> /etc/fstab

[root@192 oc]# cat /etc/fstab
LABEL=/        /           ext3  defaults    1 1
LABEL=/boot      /boot         ext3  defaults    1 2
tmpfs         /dev/shm        tmpfs defaults    0 0
devpts         /dev/pts        devpts gid=5,mode=620 0 0
sysfs         /sys          sysfs defaults    0 0
proc          /proc         proc  defaults    0 0
LABEL=SWAP-sda3    swap          swap  defaults    0 0
/dev/sdb1   /oa  ext3  defaults    0 0
/dev/sdc1   /ob  ext3  defaults    0 0
/dev/sdd1   /oc  ext3  defaults    0 0
/dev/hdc    /media/dvd   iso9660 ro,auto 0 0
/oc/swap swap swap defaults 0 0
[root@192 oc]#

 

另：

将整个设备划为swap分区

fdisk时代码为82 linux swap，

分区后：

\# mkswap /dev/sdc3
\# swapon /dev/sdc3

 