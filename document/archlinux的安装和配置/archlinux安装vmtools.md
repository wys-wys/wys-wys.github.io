# [Archlinux里面安装VMware Tools](https://www.cnblogs.com/liangxiaofeng/p/4953966.html)

用虚拟机学习linux确实很方便，但是和主机的文件共享是个大问题，VMWARE TOOLS可以很好的解决这个问题，但是在ARCH里却不能向大多数linux那样方便的安装，在查了很多帖子试了无数遍之后，终于安装成功，现将过程简单的记录一下，希望能对被这个问题困扰的朋友们有些帮助！

工作环境如下：
linux：archlinux 2.6.25
vmware 6.03

VMWARE的linux TOOLS 可以去如下网址下载：http://www.vmware.cn/Soft/1053.html

Download VMware Workstation 6.0.3 VMware tools大全

关键字：VMware,Workstation,VMCN,精简,绿色版

简介: 
VMware Workstation 6.0.3 VMware tools大全，配合精简绿色版使用。绿色版为减小体积，VMware tools只包含了windows.iso，用于其他系统的VMware tools，可以从这里下载。

下载地址: http://www.vmware.cn/Soft/ShowSoftDown.asp?UrlID=4&SoftID=1053

1、准备工作
创建如下目录：(在中端输入)
mkdir -p /etc/vmware-tools/init.d
cd /etc/vmware-tools
mkdir rc0.d
mkdir rc1.d
mkdir rc2.d
mkdir rc3.d
mkdir rc4.d
mkdir rc5.d 
mkdir rc6.d

创建一个连接
ln -s /etc/rc.d/network /etc/vmware-tools/init.d/network

修改version.h文件
路径在/usr/src/linux-2.6.25-ARCH/include/linux/version.h

注意：linux-2.6.25-ARCH这个目录名可能会根据你的系统内核版本不同而区别，可以先去父目录查看，或使用uname命令来查看系统版本来确定目录名

将version.h添加一行内容：#define UTS_RELEASE "2.6.25-ARCH"

version.h内容变为：
\#define LINUX_VERSION_CODE 132627
\#define KERNEL_VERSION(a,b,c) (((a) << 16) + ((b) << 8) + (c))
\#define UTS_RELEASE "2.6.25-ARCH"

2、开始安装程序
进入vmware菜单，选择安装vmware tools，如果此时虚拟机的光驱内未自动读取linux.iso，可手动制定路径eg：E:\vmware\linux.iso

进入archlinux，以root用户进行如下操作
cd / 
mount -t iso9660 /dev/cdrom /mnt 
cp /mnt/cdrom/VMwareTools-6.0.3-45731.tar.gz /tmp 
umount /dev/cdrom

解压缩在 /tmp 中的 VMware Tools tar 文件，然后安装它。

cd /tmp 
tar zxf vmware-linux-tools.tar.gz
cd vmware-linux-tools
cd ~/vmware-tools-distrib
./vmware-install.pl

安装会自动进行，之后会有如下提示：一下来自archwiki，很简单就不翻译了，根据屏幕上显示的问题安下面的说明填写路径并键入yes即可继续

"In which directory do you want to install the binary files?": /opt/vmware-tools/bin
"What is the directory that contains the init directories ... ?": /etc/vmware-tools
For the rest accept default locations and say yes when a directory creation is needed.
When the installer asks you to run vmware-config-tools.pl answer 'no'

出现enjoy done等字样，就说明安装成功了

以上安装部分完成！

3、配置vmware tools 
这一部分我也不是很明白，依葫芦画瓢有如下步骤：

运行配置脚本

运行 /opt/vmware-tools/bin/vmware-config-tools.pl

这个脚本提问 'What is the location of the directory of C header files that match your running kernel? [/usr/src/linux/include]'. 回答如下:

/usr/src/linux-2.6.25-ARCH/include

脚本将编译一些东西，基本按提示选yes就行啦，到Xorg部分，提示选择一个X屏幕分辨率。你需要已经安装好Xorg在你的系统里面来让X配置正常工作。

安装xorg可以见上篇帖子，简单来说如下：
pacman -S xorg-server xorg-xkb-utils xorg-xauth xorg-server-utils xorg-xinit
pacman -S xf86-video-vesa xf86-input-mouse xf86-input-keyboard
pacman -S hwd
hwd -x
mv /etc/X11/xorg.conf.hwd /etc/X11/xorg.conf

安装
pacman -S xf86-video-vmware xf86-input-vmmouse

修改一下配置文件

编辑/etc/X11/xorg.conf
寻找 
Section "InputDevice"
Identifier "Mouse1"

改成下面： 
Driver "vmmouse"
Option "Device" "/dev/psaux"

注：这里我改的是USB Mouse这个Section，我用的U口的鼠标

在/etc/ rc.conf 里面迅早 MODULES= 这一行然后禁用 pcnet32 模块然后启用vmware模块，就类似下面的：

MODULES=(!pcnet32 vmblock vmxnet vmmemctl vmhgfs)

为了保证日期和时间能和主机同步，vmware-guestd程序必须在运行。这个程序可以在开机时候通过下面步骤开启：

cd /etc/rc.d 
ln -s /etc/vmware-tools/init.d/vmware-tools vmware-tools

然后在 rc.conf 里面寻找 DAEMONS= 这一行然后把 vmware-tools 添加进去

额外的，为了能复制／粘贴能在X和主机之间工作，你必须开启 'vmware-user' 程序。添加下面一行到你的配置文件中，.xinitrc 或者 .xsession (任何你的程序能在X启动的时候启动的地方):

路径在/etc/X11/xinit，在xinitrc最后加入/opt/vmware-tools/bin/vmware-user &

保存退出

重启，然后所有功能应该能正常工作了。

注意：有时启动后vmware-tools的功能会变得无法使用，我的解决办法是重新配置一下：

运行 /opt/vmware-tools/bin/vmware-config-tools.pl 基本选no再走一遍过程就好了，希望有高手能指点一下！

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

# BlackArch Linux安装VMware Tools教程

其实，只要是Linux系统，安装VMware Tools都是大同小异，我曾经也给大家分享过一篇文章：

[VMware虚拟机 Linux 安装VMware Tools的方法](https://www.fujieace.com/vmware/vmware-tools.html)

 

今天我用BlackArch Linux安装VMware Tools很多步骤及其原理也是来源于此文章。

> 友情提示：
>
> 通常情况下，BlackArch Linux默认已经安装了VMware Tools，具体的执行命令路径是：
>
> **/usr/bin/vmtoolsd**
>
> 如果你不想重新安装，下面的步骤有些可以完全省略。

 

1、启动**BlackArch Linux**虚拟机；

 

2、点击VMware菜单**虚拟机 - 安装VMware Tools**；

[![安装VMware Tools](https://www.fujieace.com/wp-content/uploads/2019/07/001.png?x73259)](https://www.fujieace.com/wp-content/uploads/2019/07/001.png?x73259)

 

3、弹出“客户机操作系统已将 CD-ROM门锁定，并且可能正在使用CD-ROM，这可能会导致客户机无法识别介质的更改。如果可能,请在断开连接之前从客户机内部弹出 CD-ROM。确实要断开连接并覆盖锁定设置吗?”，点击“**是**”按钮；[![客户机操作系统已将 CD-ROM门锁定,并且可能正在使用CD-ROM,这可能会导致客户机无法识别介质的更改。如果可能,请在断开连接之前从客户机内部弹出 CD-ROM。确实要断开连接并覆盖锁定设置吗?](https://www.fujieace.com/wp-content/uploads/2019/07/002.png?x73259)](https://www.fujieace.com/wp-content/uploads/2019/07/002.png?x73259)

 

**4、挂载cdrom**

```
[ blackarch ~ ]# mkdir -p /media/cdrom0
[ blackarch ~ ]# mount  -r /dev/cdrom /media/cdrom0
```

 

**5、解压VMwareTools**

```
[ blackarch ~ ]# cd /media/cdrom0
[ blackarch ~ ]# cp  VMwareTools-10.1.6-5214329.tar.gz /tmp
[ blackarch ~ ]# cd /tmp
[ blackarch ~ ]# tar vfxz VMwareTools-10.1.6-5214329.tar.gz  
```

 

**6、安装vmware tools**

```
[ blackarch ~ ]# cd vmware-tools-distrib
[ blackarch ~ ]# ./vmware-install.pl 
```

安装过程中，它会一步一步的有问题问你？此过程中，你遇到后面显示[yes]、[no]的直接输入yes，然后回车。其他的问题不管[]里面是什么，直接回车就好了，不要输入。

 

注意事项 一：

如果你在安装过程中出现了如下错误，你需要先卸载VM，可以用命令“/tmp/vmware-tools-distrib/bin/vmware-uninstall-tools.pl“来卸载；然后再删除vmtoolsd，可以直接用命令“rm -rf /usr/bin/vmtoolsd”来解决此问题。

如果不想重新安装，当然不卸载也是可以的，也可以直接运行命令” /usr/bin/vmtoolsd“来启动vmware-tools。

> The installer has detected an existint installation of open-vm-tools built from source. The pen-vm-tools executable is /usr/bin/vmtoolsd.
>
> Please uninstall the open-vm-tools then run the installer again.

中文翻译

> 安装程序检测到从源构建的open-vm-tools的现有安装。 pen-vm-tools可执行文件是/usr/bin/ vmtoolsd。请卸载open-vm-tools然后再次运行安装程序。

[![The installer has detected an existint installation of open-vm-tools built from source. The pen-vm-tools executable is /usr/bin/vmtoolsd.Please uninstall the open-vm-tools then run the installer again.](https://www.fujieace.com/wp-content/uploads/2019/07/100-3.png?x73259)](https://www.fujieace.com/wp-content/uploads/2019/07/100-3.png?x73259)

 

注意事项二：

如果你在安装过程中出现了“[What is the directory that contains the init directories (rc0.d/ to rc6.d/)?](https://www.fujieace.com/vmware/rc0-d-rc6-d.html) ”，点击此链接可以解决此问题。

 

**7、设置 VMware Tools开机自启动**

由于BlackArch Linux和其它的系统有点小区别，VMware Tools 并不会随系统自启。

因此，如果我们不设置 VMware Tools 开机启动，我们需要每次启动系统后，都需要手工执行命令“vmtoolsd ”去启动它，这是很麻烦的一件事。

```
[ blackarch ~ ]# cat /proc/version > /etc/arch-release systemctl start vmtoolsd systemctl enable vmtoolsd
```

 

**8、重启系统**

安装成功后，重启系统就可以了！

```
[ blackarch ~ ]# reboot
```

 

注意：

BlackArch Linux有两个版本，一个是Live模式的版本，别一个是安装模式的版本，根据测试：Live模式的BlackArch Linux是无法成功安装VMware Tools的。

# [ArchLinux安装开源VMware Tools](https://www.cnblogs.com/liangxiaofeng/p/5104444.html)

首先按照传统的Linux下安装VMware Tools的方法[1]]出现了很多的错误,安装过程完全没有办法进行下去.我在ArchLinux Wiki中看到这样一句说:VMware Tools for linux exists in 2 forms: the [official VMware Tools](http://packages.vmware.com/tools) and Open-VM-Tools. VMware Tools is based on a stable snapshot of Open-VM-Tools. Open-VM-Tools contains more experimental code and features.The official VMware Tools are not available for Archlinux.

从上面这段话中得知:官方的VMware Tools不能用于Archlinux(红色标注),我们应该安装Open-VM-Tools,好了有了方向,我们开始我们的安装之路.

https://wiki.archlinux.org/index.php/Installing_Arch_Linux_in_VMware

详细参考上面的链接!

1.安装VMware Tools

 

pacman -S open-vm-tools open-vm-tools-modules

```
2.安装gtkmm	

pacman -S gtkmm
```

3.修复Tools中的60秒BUG

```
nano /usr/lib/systemd/system/vmtoolsd.service
```

在[service]项的后面增加一行   KillSignal=SIGKILL

 

4.使vmware tools开机自启动

```
cat /proc/version > /etc/arch-release
systemctl start vmtoolsd
systemctl enable vmtoolsd

5.重启,在虚拟机操作面板上选择查看->自动调整大小.
```

分类: [Linux](https://www.cnblogs.com/liangxiaofeng/category/506753.html)