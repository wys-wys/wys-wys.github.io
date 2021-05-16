#  Linux(SLES)挂载NTFS移动硬盘实践

| [日期：2014-04-21] | 来源：Linux社区 作者：wsgzao | [字体：[大](javascript:ContentSize(16)) [中](javascript:ContentSize(0)) [小](javascript:ContentSize(12))] |
| ------------------ | ---------------------------- | ------------------------------------------------------------ |
|                    |                              |                                                              |

**问题描述：**

由于通过测试环境导出的dmp过大，但要求尽快导入至生产服务器，请网络室打通防火墙后发现测试网络为100M而生产网络贵为1000M却无法发挥任何作用即使通过networklink效率也太低，考虑到两台设备物理位置距离较远无法通过千兆线直连的情况下，最后选择通过移动硬盘作为中转传输介质。

**解决方案：**

Linux挂载NTFS格式硬盘时会报错**unknown filesystem type 'ntfs'**，这时就需要用到第三方的插NTFS-3G来加载NTFS格式硬盘。其中NTFS-3G是一个开源软件，支持在Linux, FreeBSD, Mac OS X, NetBSD, Haiku操作系统下读写NTFS格式的分区。主要的操作步骤如下：

**1.安装gcc等编译环境(前提准备)

2.下载安装NTFS-3G(建议使用stable version)**

ntfs-3g下载地址：

**免费下载地址在** http://linux.linuxidc.com/

**用户名与密码都是**www.linuxidc.com

**具体下载目录在** /2012年资料/7月/10日/ntfs-3g加载NTFS分区工具/

下载方法见 [http://www.linuxidc.com/Linux/2013-07/87684.htm](https://www.linuxidc.com/Linux/2013-07/87684.htm)

**3.安装步骤(root用户)**
tar –xvzf ntfs-3g_ntfsprogs*.tgz
cd ntfs-3g_ntfsprogs*
./configure
make
make install

**4. 检查NTFS硬盘分区信息(sd\*1注意实际情况)**
fdisk -l
\---------------------------------
Device Boot Start End Blocks Id System
/dev/sdg1 2048 1953525163 976761558 7 HPFS/NTFS/exFAT

**4.挂载分区**
mkdir /mnt/ntfs
mount -t ntfs-3g /dev/sdg1 /mnt/ntfs
\#分区挂载完成，此时进入/mnt/ntfs目录，即是移动硬盘的分区

**5.卸载分区**
umount /dev/sdg1

**6.开机自动挂载移动硬盘，编辑/etc/fstab文件**
\#更改之前先备份
cp /etc/fstab /etc/fstabbak
\#编辑，在最后添加以下信息，以读写方式挂载磁盘
vi /etc/fstab
\---------------------------------
/dev/sdg1 /mnt/ntfs ntfs-3g defaults 0 0
\#保存，退出
:x
\#重启机器就会自动挂载移动硬盘

**7.取消挂载umount的时候出现如下提示：**
device is busy.
\#解决方法：fuser
\#可以显示出当前哪个程序在使用磁盘上的某个文件、挂载点、甚至网络端口，并给出程序进程的详细信息。
fuser -m -v /media/SLES100_001
\---------------------------------
USER PID ACCESS COMMAND
/media/SLES100_001: root 8153 ..c.. bash

\#然后可以添加一个 -k 参数把占用的进程给干掉！
fuser -m -k /media/SLES100_001
\---------------------------------
/media/SLES100_001: 8153c

**本文永久更新链接地址**：[http://www.linuxidc.com/Linux/2014-04/100542.htm](https://www.linuxidc.com/Linux/2014-04/100542.htm)

[![linux](https://www.linuxidc.com/linuxfile/logo.gif)](http://www.linuxidc.com/)

# linux环境下挂载NTFS

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[weixin_33897722](https://blog.csdn.net/weixin_33897722) 2009-03-25 13:40:27 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 101 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

文章标签： [php](https://www.csdn.net/tags/NtDagg1sNTQwLWJsb2cO0O0O.html)

版权

*linux*环境下挂载*NTFS<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" />*



*1.* 查看自己系统的内核版本*
\#uname -a*



*#uname -r*



*2.* 找合适自己系统内核和 *CPU* 的 *NTFS* 模块下载 *:
*比如我的 *:kernel-module-ntfs-<?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" />2.6.18-53.el5*



*google* 搜索 *,* 找到后下载 *.
*我在 *[[url\]http://sourceforge.net/project/showfiles.php?group_id=13956[/url]](http://sourceforge.net/project/showfiles.php?group_id=13956)* 页面找到*
[[url\]http://jaist.dl.sourceforge.net/[/url]](http://jaist.dl.sourceforge.net/) ... 0.rr.10.11.i686.rpm*



*3.* 安装*
*运行 *rpm -ihv kernel-module-ntfs-2.6.18-53.el5-2.1.27-0.rr.10.11.i686.rpm* ，安装此 *RPM* 包。*
*运行 */sbin/modprobe ntfs* 加载内核模块。*
*运行 *dmesg | grep NTFS* ，可以查看 *NTFS* 驱动版本。显示*
[root@localhost src]# dmesg | grep NTFS
NTFS driver 2.1.27 [Flags: R/W MODULE].
*可以运行 *cat /proc/filesystems* 看到已经支持 *ntfs* 文件系统了。*
*出现*
nodev autofs
ntfs
*表示已经支持 *ntfs* 了！



*4.* 挂载分区*
(1).fdisk -l* 查看分区信息*
Disk /dev/hda: 80.0 GB, 80000000000 bytes
255 heads, 63 sectors/track, 9726 cylinders
Units = cylinders of 16065 \* 512 = 8225280 bytes*



*Device Boot Start End Blocks Id System
/dev/hda1 \* 1 1912 15358108+ 7 HPFS/NTFS
/dev/hda2 1913 9725 62757922+ f W95 Ext'd (LBA)
/dev/hda5 1913 4462 20482843+ b W95 FAT32
/dev/hda6 4463 7012 20482843+ 7 HPFS/NTFS
/dev/hda7 7013 7025 104391 83 Linux
/dev/hda8 7026 9725 21687718+ 8e Linux LVM*



*(2).* 建立挂载目录*
mkdir /mnt/c
mkdir /mnt/d
mkdir /mnt/e*



*(3).Mount windwos* 下的所有分区*
ntfs* 用 *mount -t ntfs /dev/hda6 /mnt/c
vfat* 用 *mount -t vfat /dev/hda5 /mnt/d*



使用 *df -h* 查看是否被 *mount* 上来



*(4).* 设置启动自动挂载分区*
*修改 */etc/fstab
*添加如下信息：*
/dev/hda1 /mnt/c ntfs umask=000,nls=utf8
/dev/hda5 /mnt/d vfat umask=000,nls=utf8
/dev/hda6 /mnt/e ntfs umask=000,nls=utf8
*重启下试下吧！



*5.* 卸载 *NTFS* 模块*
rpm -qa|grep -i ntfs* 查看所安装的版本*
rpm -e kernel-module-ntfs-2.6.18-53.el5-2.1.27-0.rr.10.11.i686
*即可卸载。





 

转载于:https://blog.51cto.com/wangping258/142298