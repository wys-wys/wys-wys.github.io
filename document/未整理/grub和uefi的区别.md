- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/tanrong/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/RongT)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/banlieue13/images/xml.gif)](https://www.cnblogs.com/tanrong/rss/)

随笔- 254 文章- 0 评论- 28 

# [Grub 和 UEFI启动](https://www.cnblogs.com/tanrong/p/7764285.html)

# 一、Grub

 

GNU GRUB 和GRUB是GRand Unified Bootloader的缩写，它是一个多重操作系统启动管理器。用来引导不同系统，如windows，linux。

开机出现GRUB引导主要原因是，一般现在的电脑现在都不再是legacy BIOS引导，而是UEFI这种快速启动的引导方式，在硬件的BOOT权限设置时，一般有legacy first和UEFI first这两个选项，**若是采用legacy first的话一般是不会出现GRUB界面的**，因为grub多用于引导LINUX系统，此时boot是优先导入LINUX。但是如果改为UEFI first的话，开机GRUB丢失引导项，出现GRUB界面。

 

 

# **二、UEFI**

**uefi**是一种更快捷快速的电脑**启动配置**，它的全称是“统一可扩展固件接口”(Unified Extensible Firmware Interface)

 

要详细了解uefi之前，我们不得不从bios说起。大家都知道电脑中有一个bios设置，它主要负责**开机时检测硬件功能和引导操作系统启动**的功能。而uefi则是用于操作系统自动从预启动的操作环境，加载到一种操作系统上从而节省开机时间。

![img](https://images2017.cnblogs.com/blog/1152413/201710/1152413-20171031224642388-563403799.png)

 

uefi启动是一种**新的主板引导项**，它被看做是bios的继任者。uefi最主要的特点是**图形界面**，更利于用户对象图形化的操作选择。

 ![img](https://images2017.cnblogs.com/blog/1152413/201710/1152413-20171031224750576-1795258646.png)

 

简单的来说uefi启动是新一代的bios，功能更加强大，而且它是以图形图像模式显示，让用户更便捷的直观操作。当然也会产生一些问题

 

如今很多新产品的电脑都支持uefi启动模式，甚至有的电脑都已抛弃bios而仅支持uefi启动。这不难看出uefi正在取代传统的bios启动。

 

参考链接：http://www.uqidong.com/uefi.html

 

# 三、UEFI/Legacy启动模式区分

(1)进入系统查看
运行cmd，然后输入 bcdedit /enum {current} 执行，如果 path 中给出的路径是 winload.efi ，则说明系统是通过 UEFI 模式启动的了
(2)开机时查看
在开机的时候，如果显示开机画面是主板的logo，底下加上一个转圈，这应该就是UEFI启动。如果是出现系统开机画面时才出现转圈则是传统BIOS启动
(3)进入系统查看
首先同时按下电脑的win键和r键，打开“运行”(或者直接在开始菜单中打开“运行”）
然后再输入msinfo32，点击确定。
然后就打开了系统信息的窗口。
查看 ”BIOS模式”，写的是UEFI就是UEFI，legacy就是传统BIOS启动。*
*

 

参考链接：[UEFI/Legacy两种启动模式下安装Win10/Ubuntu双系统](https://blog.csdn.net/GJXS2017/article/details/80296267)

 

 

分类: [其他](https://www.cnblogs.com/tanrong/category/1003900.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)