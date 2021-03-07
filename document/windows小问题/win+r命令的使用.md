# 快速入门Win+R命令（附图）

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Lindark](https://blog.csdn.net/qq_40287093) 2018-09-21 21:52:53 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 98349 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 145

分类专栏： [计算机](https://blog.csdn.net/qq_40287093/category_8076808.html) 文章标签： [windows](https://www.csdn.net/tags/MtTaEg0sNTAxMTMtYmxvZwO0O0OO0O0O.html) [Win R](https://so.csdn.net/so/search/s.do?q=Win R&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

最近在学习Linux，被命令行深深吸引了，陷入其中不能自拔，考虑到Windows上也有cmd命令行，但对新人来说不是很友好。这次我们就先讲一下Win+R运行框里的快捷键，绝对能提高不少效率！

### 什么是Win+R

防止有些小白看不懂，所以说明一些，使用Windows+R快捷键就可以打开如下图的运行窗口，在里面输入命令可以方便快捷地打开很多东西，而且本文的所有操作都是在这个运行框里输入的，不要与cmd弄混了。

 

![img](https://img-blog.csdn.net/20180921214443306?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjg3MDkz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

###  

### **计算机管理**

在Win+R运行框里输入compmgmt.msc，就会弹出Windows自带的计算机管理器，日常用到它的情况也比较多，如下图。

![img](https://img-blog.csdn.net/20180921204238504?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjg3MDkz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

为什么说它重要呢，连它的每一个小的分项都自带命令！而且这些命令也很常用，部分如下：

> - lusrmgr.msc（本机用户和用户）：用于设置用户的权限等信息。
> - devmgmt.msc（设备管理）：计算**机的硬**件设备以及安装的驱动管理。
> - diskmgmt.msc（磁盘管理）：可以看到磁盘的分区等信息，也可以自己开辟分区。
> - services.msc（本地服务设置）：有些程序只有开启了相关的服务才能运行，就在这里设置。
> - perfmon.msc（性能监视器）：性能监视器，作用不大。
> - eventvwr（事件查看器）：查看计算机最近执行的事件，如果蓝屏，可以重启后打开这个看是由于什么事件引起的。

###  

### 管理信息

这里的命令分类其实不是很准确，只是觉得这些易于理解，而且后面两个命令比较常用，特别是涉及到计算机的一些深层次的东西的时候往往会用到。

> - explorer（文件资源管理器）：不常用，没Win+E来的方便。
> - taskmgr（任务管理器）：还行，也有快捷键Esc+Shift+Ctrl，哪个方便因人而异。
> - certmgr.msc（证书管理器）：查看电脑上的所有证书，不常用。
> - secpol.msc（本地安全策略）：电脑安全方面的设置，不常用。
> - regedit/regedt（注册表编辑器）：删除某些程序的时候用的到。
> - gpedit.msc（组策略编辑器）：好像只有windows专业版才有的命令。

###  

### 快速打开文件和软件

一般的我们通过Win+R能直接打开的是office软件，但输入的命令名并不完全是这三个软件的名字，而是winword，excel，powerpnt。只有输入上面的三个命令才能打开正确的软件！

如果你想能进一步提高效率，想要快捷地打开自己安装的软件的话，不妨看看这篇博主的文章[如何使用Win+R快速打开程序](https://blog.csdn.net/bat67/article/details/76396321)，里面详细地说明了如何实现这样的操作。

除此之外，还有几个打开文件的小命令

> - . （打开本机用户文件的目录）
> - \ （打开资源管理器下的C盘）
> - %temp%（打开临时文件夹）

 

### 控制面板

在Win+R运行框里输入control命令就会进入到控制面板，这个命令特别好用，尤其是升级到Win10后，控制面板的入口不好找到，直接输入命令方便快捷，速度甩了别人几条街有木有！

![img](https://img-blog.csdn.net/20180921214120497?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjg3MDkz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

如果你想拥有更高的效率的话，不妨试试下面的命令，这些命令基本也是控制面板下的常见设置的命令。

> - desk.cpl（桌面设置）
> - main.cpl（鼠标设置）
> - inetcpl.cpl（Internet属性）
> - ncpa.cpl（网络连接）
> - mmsys.cpl（声音和音频设备）
> - powercfg.cpl（电源选项）
> - sysdm.cpl（系统属性）
> - firewall.cpl（防火墙）

###  

### 系统自带工具

还有一些常用的系统自带的小工具，有时候想用但找了半天不知道在哪儿，所以记住这些命令还是有点作用的。

> - calc（计算器）
> - osk（虚拟键盘）
> - write（写字板）
> - notepad（记事本）
> - mspaint（画图）
> - magnify（放大镜）

###  

### 其他命令

其实我也不知道到底还有什么命令可写，因为有好多的命令用不到，有的命令也是专业人士才用的到，所以这里就放一些我觉得有用的命令吧。也欢迎大家有什么好玩的命令在评论区里分享

> - mstsc（远程桌面连接）
> - cleanmgr（磁盘清理）
> - winver（Windows版本查看）
> - mmc（控制台）
> - nslookup（IP地址检测器）

喜欢文章的话不妨点个赞哦~

 

 PS：下次更新写cmd啦~