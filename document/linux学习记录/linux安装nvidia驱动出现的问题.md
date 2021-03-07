# Centos7 安装独立显卡驱动

参考：

https://blog.csdn.net/u013378306/article/details/69229919

## 安装基础依赖环境

```
Yum install gcc kernel-delve -y
```

 

*注意事项，保证内核版本和源码版本一样，否则，安装报错误6：*

-  查看内核版本：

  ```
  ls /boot | grep vmlinu
  ```

   

- 查看源码包版本

  ```
  rpm -aq | grep kernel-devel
  ```

   

从上面的输出中可以看出内核版本号和内核源码版本。为了解决这个错误，需要从FC官方网站上下载与内核版本对应的源码包进行安装。
可以在以下网站下载并安装：
http://rpmfind.net/linux/rpm2html/search.php?query=kernel-devel

 

## 源码安装

### 1 在英伟达官网下载相应驱动

搜索出相应的驱动后，不要直接点，而是右健，Save Link as...

否则，会出现下载半天没动静的情况。

存放的路径上最好不要有中文。

我存放的路径是 ~/Downloads/NVIDIA-Linux-x86_64-346.47.run

 

### 2 屏蔽默认带有的nouveau

使用su命令切换到root用户下: su root

打开/lib/modprobe.d/dist-blacklist.conf

 

将nvidiafb注释掉。

```
#blacklist nvidiafb 
```

 

然后添加以下语句：

```
blacklist nouveau

options nouveau modeset=0
```

### 3 重建initramfs image步骤

```
mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak

dracut /boot/initramfs-$(uname -r).img $(uname -r) 
```

### 4 修改运行级别为文本模式

```
systemctl set-default multi-user.target 
```

### 5 重新启动, 使用root用户登陆

reboot

 

### 6 查看nouveau是否已经禁用

```
ls mod | grep nouveau
```

如果没有显示相关的内容，说明已禁用。

 

### 7 进入下载的驱动所在目录

```
chmod +x NVIDIA-Linux-x86_64-346.47.run

./NVIDIA-Linux-x86_64-346.47.run
```

安装过程中，选择accept

如果提示要修改xorg.conf，选择yes

### 8 修改运行级别回图形模式

```
systemctl set-default graphical.target 
```

### 9 重新启动，OK

在Applications--Other可以看见NVIDIA X Server Settings菜单。 

## 问题：

### 错误1：

```
ERROR: The Nouveau kernel driver is currently in use by your system.  This driver is incompatible with the NVIDIA driver, and must be disabled before proceeding.  Please consult the NVIDIA driver README and your Linux distribution's documentation for details on how         to correctly disable the Nouveau kernel driver.
```

解释：如果没有执行屏蔽nouveau操作，报以上错误。

 

### 错误2：

```
unable to find the development too 'cc' in you path; please make sure that you have the package 'gcc
```

解决办法：

```
yum install gcc
```

### 错误3：

### 错误4：

```
 ERROR: Unable to find the kernel source tree for the currently running kernel.  Please make sure you have installed the kernel source files for your

 kernel and that they are properly configured; on Red Hat Linux systems, for example, be sure you have the  'kernel-source' or 'kernel-devel' RPM installed.  If you know the correct kernel source files are installed, you may specify the kernel source path with the '--kernel-source-path' command line option.
```

解决办法：

```
yum install kernel-delve
```

### 错误5：

```
 ERROR: Unable to find the kernel source tree for the currently running kernel.  Please make sure you have installed the kernel source files for your kernel and that they are properly configured; on Red Hat Linux systems, for example, be sure you have the         'kernel-source' or 'kernel-devel' RPM installed.  If you know the correct kernel source files are installed, you may specify the kernel source path with the '--kernel-source-path' command line option.
```

 解决方法：

```
./NVIDIA-Linux-x86_64-390.67.run --kernel-source-path=/usr/src/kernels/3.10.0-862.3.2.el7.x86_64/ 
```

### 错误6：

```
ERROR: Unable to load the kernel module 'nvidia.ko'.  This happens most frequently when this kernel module was built against the wrong or improperly configured kernel sources, with a version of gcc that differs from the one used to build the target kernel, or if another driver, such as nouveau, is present and prevents the NVIDIA kernel module from obtaining ownership of the NVIDIA GPU(s), or no NVIDIA GPU installed in this system is supported by this NVIDIA Linux graphics driver release.

         Please see the log entries 'Kernel module load error' and 'Kernel messages' at the end of the file '/var/log/nvidia-installer.log' for more information.
```

解决办法：

- 可以通过以下方式查看内核版本和源码包版本：

  ```
  ls /boot | grep vmlinuz
  ```

- 如果上面的命令输出中有多个内核，则按grub.conf中指定的文件为准。

  ```
  rpm -aq | grep kernel-devel
  kernel-devel-2.6.35.13-92.fc14.i686
  ```

- 从上面的输出中可以看出内核版本号和内核源码版本。为了解决这个错误，需要从FC官方网站上下载与内核版本对应的源码包进行安装。

​     *可以在以下网站下载并安装：
​    http://rpmfind.net/linux/rpm2html/search.php?query=kernel-devel*

*备注：执行更新内核操作好需要重新执行屏蔽nouveau**，及重建initramfs image**步骤。*

 

### 警告：

 

```
WARNING: nvidia-installer was forced to guess the X library path '/usr/lib64' and X module path '/usr/lib64/xorg/modules'; these paths were not queryable from the system.  If X fails to find the NVIDIA X driver module, please install the `pkg-config` utility and the

           X.Org SDK/development package for your distribution and reinstall the driver.
```

字符模式安装警告信息，可忽略。

# 安装cuda

参考：https://blog.csdn.net/claroja/article/details/81034147

1. ### **错误：**

   ```
   Installing the CUDA Toolkit in /usr/local/cuda-6.5 ...
   Missing recommended library: libGLU.so
   Missing recommended library: libXmu.so
   ```

   解决：安装第三方软件

   ```
   yum install freeglut-devel libX11-devel libXi-devel libXmu-devel  \
   
   make mesa-libGLU-devel
   ```

    

2. ### 测试CUDA

   [![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

   ```
   [root@fengyun6 ~]# find / -name deviceQuery
   
   /root/NVIDIA_CUDA-9.0_Samples/1_Utilities/deviceQuery
   
   /usr/local/cuda-9.0/extras/demo_suite/deviceQuery
   
   /usr/local/cuda-9.0/samples/1_Utilities/deviceQuery
   ```

   [![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

   若出现以下信息，则表示安装成功

   [![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

   ```
   [root@fengyun6 ~]# /usr/local/cuda-9.0/extras/demo_suite/deviceQuery
   
   /usr/local/cuda-9.0/extras/demo_suite/deviceQuery Starting...
   
    
   
    CUDA Device Query (Runtime API) version (CUDART static linking)
   
    
   
   Detected 1 CUDA Capable device(s)
   
    
   
   Device 0: "GeForce GTX 1080 Ti"
   
     CUDA Driver Version / Runtime Version          9.1 / 9.0
   
     CUDA Capability Major/Minor version number:    6.1
   
     Total amount of global memory:                 11178 MBytes (11721113600 bytes)
   
     (28) Multiprocessors, (128) CUDA Cores/MP:     3584 CUDA Cores
   
     GPU Max Clock rate:                            1645 MHz (1.64 GHz)
   
     Memory Clock rate:                             5505 Mhz
   
     Memory Bus Width:                              352-bit
   
     L2 Cache Size:                                 2883584 bytes
   
     Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
   
     Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
   
     Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
   
     Total amount of constant memory:               65536 bytes
   
     Total amount of shared memory per block:       49152 bytes
   
     Total number of registers available per block: 65536
   
     Warp size:                                     32
   
     Maximum number of threads per multiprocessor:  2048
   
     Maximum number of threads per block:           1024
   
     Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
   
     Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
   
     Maximum memory pitch:                          2147483647 bytes
   
     Texture alignment:                             512 bytes
   
     Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
   
     Run time limit on kernels:                     No
   
     Integrated GPU sharing Host Memory:            No
   
     Support host page-locked memory mapping:       Yes
   
     Alignment requirement for Surfaces:            Yes
   
     Device has ECC support:                        Disabled
   
     Device supports Unified Addressing (UVA):      Yes
   
     Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
   
     Compute Mode:
   
        < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >
   
    
   
   deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 9.1, CUDA Runtime Version = 9.0, NumDevs = 1, Device0 = GeForce GT
   
   X 1080 TiResult = PASS
   ```

   [![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

# 安装cudnn

参考：https://www.cnblogs.com/mar-q/p/7482720.html

下载：https://developer.nvidia.com/rdp/cudnn-archive

### 安装cudnn

```
tar -xvf cudnn-8.0-linux-x64-v6.0.tgz -C /usr/local/
```

 

分类: [Linux](https://www.cnblogs.com/2012blog/category/1142171.html)

标签: [显卡](https://www.cnblogs.com/2012blog/tag/显卡/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/sample_face.gif)](https://home.cnblogs.com/u/2012blog/)

[总管](https://home.cnblogs.com/u/2012blog/)
[关注 - 0](https://home.cnblogs.com/u/2012blog/followees/)
[粉丝 - 0](https://home.cnblogs.com/u/2012blog/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/2012blog/p/9303682.html)上一篇： [centos同步yum源到本地](https://www.cnblogs.com/2012blog/p/9303682.html)
[» ](https://www.cnblogs.com/2012blog/p/9431716.html)下一篇： [jenkins各种触发方式介绍](https://www.cnblogs.com/2012blog/p/9431716.html)

posted @ 2018-08-06 17:20 [总管](https://www.cnblogs.com/2012blog/) 阅读(9776) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=9431432) [收藏](javascript:void(0))

# kali 2016.2rolling版更新源（找不到内核头文件的解决办法）

[![img](https://upload.jianshu.io/users/upload_avatars/4170354/12b44a2f9a47.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/eea6acda4b25)

[g0](https://www.jianshu.com/u/eea6acda4b25)关注

2017.01.10 13:27:27字数 475阅读 1,026

root@g0:~# leafpad /etc/apt/sources.list



#### ~~#kali官方源 ~~

#### ~~deb http://http.kali.org/kali kali-rolling main non-free contrib~~

#### ~~#中科大的源~~

#### ~~deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib~~

#### ~~deb http://mirrors.ustc.edu.cn/kali kali-rolling main contrib non-free~~

#### ~~deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main contrib non-free~~

#### ~~deb http://mirrors.ustc.edu.cn/kali-security kali-current/updates main contrib non-free~~

#### ~~deb-src http://mirrors.ustc.edu.cn/kali-security kali-current/updates main contrib non-free~~

#### ~~#阿里云源~~

#### ~~deb http://mirrors.aliyun.com/kali sana main non-free contrib~~

#### ~~deb http://mirrors.aliyun.com/kali-security/ sana/updates main contrib non-free~~

#### ~~deb-src http://mirrors.aliyun.com/kali-security/ sana/updates main contrib non-free~~



deb http://http.kali.org/kali kali-rolling main non-free contrib

> deb-src http://http.kali.org/kali kali-rolling main non-free contrib

deb http://http.kali.org/kali kali main contrib non-free

deb http://security.kali.org/kali-security kali/updates main contrib non-free

\#官方源:

deb http://http.kali.org/kali sana main non-free contrib

> deb-src http://http.kali.org/kali sana main non-free contrib

deb http://security.kali.org/kali-security sana/updates main contrib non-free

> deb-src http://security.kali.org/kali-security sana/updates main contrib non-free

写入之后需更新

碰到如下问题

> 正在读取软件包列表... 完成
>
> 正在分析软件包的依赖关系树
>
> 正在读取状态信息... 完成
>
> E: 无法定位软件包 linux-headers-4.3.0-kali1-amd64
>
> E: 无法按照 glob ‘linux-headers-4.3.0-kali1-amd64’ 找到任何软件包
>
> E: 无法按照正则表达式 linux-headers-4.3.0-kali1-amd64 找到任何软件包

或者遇到各种依赖关系没有安装，或 apt-get -f install 无法起作用，需要执行如下命令：

（安装新的软件包）

apt-get dist-upgrade(安装新的内核文件)

或者setting----->Details------->Check For updates，检查更新，更新所有

PS：这个时间比较长，自己用了1个多小时，中间还需要自己点回车



1人点赞



[Kali2.0 Rolling版本](https://www.jianshu.com/nb/8651825)

# [解决centos下安装显卡驱动出现的unable to find the kernel source tree等关于内核版本问题](https://www.cnblogs.com/liuke-note/p/13712202.html)

如果看过我之前的[文章](https://www.cnblogs.com/liuke-note/p/10149977.html)，应该对Ubuntu下的显卡驱动以及CUDA安装比较了解了，但是那篇文章有点过时了，最近安装CUDA时，英伟达已经做的很不错了，给出了安装前的配置界面，同时也留下了一些自定义参数，对于nouveau等开源驱动也默认自动去掉了，省了很多麻烦。

但是另一个问题也存在：旧版本的Linux内核与驱动匹配问题比较难解决，实际这个问题也不算是英伟达的锅····

问题现象：驱动安装失败，安装log文件提示说源码树未发现或者版本不匹配

解决办法：很大程度上我们安装的kernel-devel与kernel-headers与实际内核版本不匹配，这里指的是自动安装的情况。比如下图：

![img](https://img2020.cnblogs.com/blog/650153/202009/650153-20200922143124387-2003731440.png)

 

 这种情况很容易出现，尤其是你在一个低版本的Linux发行版上安装kernel-devel与kernel-headers时。我不建议按照上图那样直接yum uninstall 或者remove！其实我们大可手动下载安装匹配版本的kernel-devel与kernel-headers。

去这个网站：https://pkgs.org/download/kernel-headers搜索与你内核匹配的kernel-headers，可能搜索到第三方编译的二进制文件，不要紧，大胆用就行。

去这个网站：https://pkgs.org/download/kernel-devel搜索与你内核匹配的kernel-devel，同样可能搜索到第三方的二进制文件，不要紧，大胆用。

不出意外，你应该找到了跟你内核匹配的RPM包，我们直接安装就可以：

rpm -Uvh 你下载的包

安装后，你的电脑上应该会有两套kernel-devel，一个是yum install自动从软件源里安装的不与实际内核匹配的，另一个是手动安装的。

我们的目的是让英伟达的安装程序正确调用kernel-devel，这就要在安装前指定源码树位置，还记得我刚刚提到的配置界面吗？我没有截图，但细心的你应该知道在哪个界面~~~

至于安装位置，https://pkgs.org/download/kernel-devel已经给出，一般是在/usr/src/kernels/目录下，如果你细心看，这个目录下应该会有两个版本，就是对应上述两个kernel-devel

FAQ：

Q：为什么不把之前的自动安装的版本卸载掉？

A：据说重启时会出现内核恐慌，还是留着吧，反正只在安装驱动等需要加载到内核的模块过程中才会调用，不过，有一个缺点，就是害怕其他驱动编译时不能自己指定目录，这样一来还是可能出错···

解决的办法可以创建软连接，不过我没有尝试。

分类: [技术分享](https://www.cnblogs.com/liuke-note/category/1352685.html)

标签: [centos](https://www.cnblogs.com/liuke-note/tag/centos/), [CUDA](https://www.cnblogs.com/liuke-note/tag/CUDA/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/650153/20140712142611.png)](https://home.cnblogs.com/u/liuke-note/)

[渔情禅心](https://home.cnblogs.com/u/liuke-note/)
[关注 - 0](https://home.cnblogs.com/u/liuke-note/followees/)
[粉丝 - 4](https://home.cnblogs.com/u/liuke-note/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/liuke-note/p/13583117.html)上一篇： [Linux下手动添加显示器分辨率](https://www.cnblogs.com/liuke-note/p/13583117.html)
[» ](https://www.cnblogs.com/liuke-note/p/13712960.html)下一篇： [在Linux下制作Linux以及windows启动盘](https://www.cnblogs.com/liuke-note/p/13712960.html)

# Linux安装NVIDIA显卡驱动的正确姿势

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

置顶 [FlyWine](https://flywine.blog.csdn.net/) 2018-08-20 21:05:58 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 201562 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 470

分类专栏： [ubuntu-配置](https://blog.csdn.net/wf19930209/category_6971007.html) 文章标签： [ubuntu安装英伟达显卡](https://so.csdn.net/so/search/s.do?q=ubuntu安装英伟达显卡&t=blog&o=vip&s=&l=&f=&viparticle=) [linux安装nvidia显卡](https://www.csdn.net/tags/MtzaIgwsOTYzNDYtYmxvZwO0O0OO0O0O.html) [nvidia驱动安装](https://www.csdn.net/tags/MtTaEg1sMDY4NDQtYmxvZwO0O0OO0O0O.html) [英伟达驱动安装](https://so.csdn.net/so/search/s.do?q=英伟达驱动安装&t=blog&o=vip&s=&l=&f=&viparticle=) [ubuntu安装显卡驱动](https://www.csdn.net/tags/MtTaEg5sODQyNDUtYmxvZwO0O0OO0O0O.html)

版权

[![img](https://img-blog.csdnimg.cn/20200218231002275.png?x-oss-process=image/resize,m_fixed,h_64,w_64)Angular入门到精通指南涵盖Angular所有相关知识及教程，适合入门、深入开发的你，文档以实用为主，精简为辅，愿祝你一臂之力！![img](https://profile.csdnimg.cn/0/F/E/3_wf19930209)FlyWine](https://blog.csdn.net/wf19930209/category_7461565.html)

¥19.90

订阅博主



### 文章目录

- [Linux安装NVIDIA显卡驱动的正确姿势](https://blog.csdn.net/wf19930209/article/details/81877822#LinuxNVIDIA_1)
- - [什么是nouveau驱动？](https://blog.csdn.net/wf19930209/article/details/81877822#nouveau_11)
  - [检测NVIDIA驱动是否成功安装](https://blog.csdn.net/wf19930209/article/details/81877822#NVIDIA_25)
  - [集显与独显的切换](https://blog.csdn.net/wf19930209/article/details/81877822#_80)
  - [使用标准仓库进行自动化安装](https://blog.csdn.net/wf19930209/article/details/81877822#_103)
  - [使用**PPA**仓库进行自动化安装](https://blog.csdn.net/wf19930209/article/details/81877822#PPA_149)
  - [使用官方的NVIDIA驱动进行手动安装](https://blog.csdn.net/wf19930209/article/details/81877822#NVIDIA_173)
  - [常见问题解决](https://blog.csdn.net/wf19930209/article/details/81877822#_271)



# Linux安装NVIDIA显卡驱动的正确姿势

可能想玩**Linux**系统的童鞋，往往死在安装**NVIDIA**显卡驱动上，所以这篇文章帮助大家以正常的方式安装**NVIDIA**驱动。

本文将介绍四种NVIDIA驱动安装方式。具体选择需要根据你的情况而定。

- 使用标准**Ubuntu**仓库进行自动化安装
- 使用**PPA**仓库进行自动化安装
- 使用官方的**NVIDIA**驱动进行手动安装

## 什么是nouveau驱动？

**nouveau**，是一个自由及开放源代码显卡驱动程序，是为**Nvidia**的显示卡所编写，也可用于属于系统芯片的**NVIDIA Tegra**系列，此驱动程序是由一群独立的软件工程师所编写，**Nvidia**的员工也提供了少许帮助。

该项目的目标为利用逆向工程**Nvidia**的专有Linux驱动程序来创造一个开放源代码的驱动程序。

所以**nouveau**开源驱动基本上是不能正常使用的，性能极低，所以网上有很多人都在骂：干死**黄仁勋**！！

![这里写图片描述](https://img-blog.csdn.net/20180821084915908?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

想了解历史的可以去看看这篇知乎，[腾讯和AMD是linux的罪人吗？](https://www.zhihu.com/question/59926840/answer/172323398)。

好了不扯了，正式开始讲安装把！

## 检测NVIDIA驱动是否成功安装

1. 使用**nvidia-settings**命令

```
nvidia-settings
1
```

终端执行这个命令会调出**NVIDIA**的驱动管理程序，如下：

![这里写图片描述](https://img-blog.csdn.net/20180821084947258?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

如果出现这个界面可以看到 **NVIDIA Driver Version：390.48**，这就代表**nvidia-setting**安装正常。

1. 使用**nvidia-smi**命令测试

英伟达系统管理接口（NVIDIA System Management Interface, 简称 **nvidia-smi**）是基于NVIDIA Management Library (NVML) 的命令行管理组件,旨在(intened to )帮助管理和监控**NVIDIA GPU**设备。

```
nvidia-smi
1
```

执行这条命令将会打印出当前系统安装的**NVIDIA**驱动信息，如下:

![这里写图片描述](https://img-blog.csdn.net/20180821085019220?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

我们可以看到我们显卡的型号，我的是**GTX 960M**，包括**显存**大小都可以看见。

1. 系统信息查看

这一步不重要，因为有时候系统信息里面显示的可能会有误，只显示**集显**不显示**独显**的情况。

比如我的就没有显示出**独显**，如下：

![这里写图片描述](https://img-blog.csdn.net/20180821085115764?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

这里面不显示没有关系，可以略过。

1. 命令行搜索集显和独显

打开终端执行以下命令：

```
lspci | grep VGA     # 查看集成显卡
lspci | grep NVIDIA  # 查看NVIDIA显卡
12
```

![这里写图片描述](https://img-blog.csdn.net/20180821085148526?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

如果都能搜索到说明正常。

> 查看nouveau是否启动运行可以执行下面命令:

```
lsmod | grep nouveau
1
```

> 没有返回代表没有运行。

## 集显与独显的切换

当我们需要切换独显与集显的时候，一般就是外出的时候，想节省电量，增长待机时间。下面讲解两种切换方式。

1. 使用nvidia-setting切换

终端执行**nvidia-setting**,在弹的界面中选择独显与集显:

![这里写图片描述](https://img-blog.csdn.net/2018082108521740?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1. 命令行切换

NVIDIA提供了一个切换显卡的命令：

```
sudo prime-select nvidia # 切换nvidia显卡
sudo prime-select intel  # 切换intel显卡
sudo prime-select query  # 查看当前使用的显卡
123
```

![这里写图片描述](https://img-blog.csdn.net/20180821085247529?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**注意：** *每一次切换显卡都需要重新启动电脑才能生效*。

## 使用标准仓库进行自动化安装

在安装的发行版中，如 **ubuntu**, **Linux Mint**等，找到**附加驱动管理软件**，下面是**Linux Mint**界面:

![这里写图片描述](https://img-blog.csdn.net/20180821085321183?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

选择推荐的驱动安装，点击应用更改，等待下载然后**重启**即可。

这种安装方式有如下**缺点**：

1. 如果你的显卡比较新可能会出现安装低版本的NVIDIA驱动而造成即可安装完成，但是并没有真正安装成功，可能会出现循环登录，关机死机等等原因。
2. 当你更换驱动的时候可能原有的NVIDIA驱动删除不干净。

当然这种方式也是有优点的:

1. 不需要手动禁止**nouveau**
2. 操作方便

可能有的童鞋还使用过命令行的方式安装：

```
sudo apt-get install nvidia*
1
```

如图：

![这里写图片描述](https://img-blog.csdn.net/20180821085354772?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

这种方式安装同样也是使用**ubuntu官方源**的形式安装的，你可以选择**不同的驱动版**本来安装，但是本质上和标准仓库进行自动化安装是一样的。

其实**ubuntu**自带命令行版本安装工具**ubuntu-drivers**,终端输入:

```
ubuntu-drivers devices   # 查询所有ubuntu推荐的驱动
1
```

![这里写图片描述](https://img-blog.csdn.net/20180821085428556?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

这路我是有一个推荐安装的驱动，那就是**nvidia-driver-390**，明显我已经安装完成了。

然后就可以使用下面一条命令安装所有推荐的驱动程序：

```
sudo ubuntu-drivers autoinstall
1
```

安装完成后**重启**就可以了，这里要注意，这种安装方式和**驱动管理器软件**安装的效果是一样的，就是一个是UI版本，一个是命令行版本。

## 使用**PPA**仓库进行自动化安装

使用图形驱动程序**PPA**存储库允许我们安装**NVIDIA beta**驱动程序，这有可能会出现**兼容性**的问题，但是有些时候必须使用这种方式，比如**显卡比较新**，使用上面所讲的方式**检测驱动**的安装情况，如果不正常那么只能使用这种方式安装最新的**NVIDIA**驱动。

1. 添加PPA到我们的系统：

```
sudo add-apt-repository ppa:graphics-drivers/ppa
1
```

更新系统源：

```
sudo apt update
1
```

此时我们就可以下载最新的NVIDIA驱动了:

安装的方式有以下三种，其实前面已经讲过，这里总结一下:

- 附加驱动管理软件
- sudo apt-get install nvidia-xxx
- ubuntu-drivers方式

这三种都可以，选择一个版本安装，然后重启即可。

## 使用官方的NVIDIA驱动进行手动安装

这种安装方式我认为是比较**野蛮**的，也是最**正规**，最**原始**的的方式，当然**难度**是**最高**的。你可以来挑战一下！！！！

**1. 查看当前电脑的显卡型号**

```
lshw -numeric -C display
1
```

执行完毕后我的显卡型号为 **GTX 960M**,如下图：

![这里写图片描述](https://img-blog.csdn.net/20180821085501411?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dmMTk5MzAyMDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**2. 下载NVIDIA官方驱动**

到NVIDIA的官方[驱动网站](https://www.geforce.cn/drivers)下载对应显卡的驱动程序，下载后的文件格式为**run**。

下载好之后放到用户目录下，等下后面会用到。

**3. 删除原有的NVIDIA驱动程序**

如果你没有安装过，或者已经卸载，可以忽略:

```
sudo apt-get remove –purge nvidia*
1
```

**4. bios禁用禁用secure boot，也就是设置为disable**

如果没有禁用**secure boot**,会导致**NVIDIA**驱动安装失败，或者不正常。

**5. 禁用nouveau**

打开编辑配置文件：

```
sudo gedit /etc/modprobe.d/blacklist.conf
1
```

在最后一行添加：

```
blacklist nouveau
1
```

这一条的含义是禁用**nouveau**第三方驱动，之后也不需要改回来。

由于nouveau是构建在内核中的，所以要执行下面命令生效:

```
sudo update-initramfs -u
1
```

**6. 重启**

```
reboot
1
```

重启之后，可以查看nouveau有没有运行:

```
lsmod | grep nouveau  # 没输出代表禁用生效
1
```

**7. 停止可视化桌面：**

为了安装新的**Nvidia**驱动程序，我们需要停止当前的显示服务器。最简单的方法是使用**telinit**命令更改为运行级别**3**。执行以下**linux**命令后，显示服务器将停止，因此请确保在继续之前保存所有当前工作（如果有）：

```
sudo telinit 3
1
```

之后会进入一个新的命令行会话，使用当前的用户名密码登录

**8. 安装驱动**

给驱动文件增加可执行权限：

```
sudo chmod a+x NVIDIA-Linux-x86_64-390.48.run
1
```

然后执行安装：

```
sudo sh ./NVIDIA-Linux-x86_64-390.48.run --no-opengl-files
1
```

安装完成后重启即可，记得验证是否安装成功，参考前面所讲。

> –no-opengl-files 参数必须加否则会循环登录，也就是loop login

参数介绍：

- –no-opengl-files 只安装驱动文件，不安装OpenGL文件。这个参数最重要
- –no-x-check 安装驱动时不检查X服务
- –no-nouveau-check 安装驱动时不检查nouveau
  后面两个参数可不加。

关于使用此方式可以参照[Ubuntu 18.04安装NVIDIA（英伟达） RTX2080Ti显卡](https://blog.csdn.net/wf19930209/article/details/95237824) 这篇文章。

**注意：**

> - 安装CUDA时一定使用runfile文件，这样可以进行选择。不再选择安装驱动，以及在弹出xorg.conf时选择NO

## 常见问题解决

1. 安装完驱动后，HDMI扩展屏幕不能使用，现象表现为能识别扩展屏幕但是黑屏。
   这种情况需要确定以下内容是否已经设置：

   - bios内是否已经禁止安全启动、快速启动。
   - linux系统是否设置了禁止nouveau

   如果上面的都已经做了，但还是有问题，可以尝试下面的配置：

   ```shell
   sudo nano /usr/share/X11/xorg.conf.d/10-amdgpu.conf
   1
   ```

   > 有可能不是这个文件，但是类似。

   修改为下面这样

   ```
   Section "OutputClass"
      Identifier "AMDgpu"
      MatchDriver "amdgpu"
      Driver "amdgpu"
      Option "PrimaryGPU" "no"
   EndSection
   123456
   ```

   下面修改nvidia的配置

   ```shell
   sudo nano /usr/share/X11/xorg.conf.d/10-nvidia.conf
   1
   ```

   修改为下面这样：

   ```
   Section "OutputClass"
      Identifier "nvidia"
      MatchDriver "nvidia-drm"
      Driver "nvidia"
      Option "AllowEmptyInitialConfiguration"
      Option "PrimaryGPU" "yes"
      ModulePath "/usr/lib/x86_64-linux-gnu/nvidia/xorg"
   EndSection
   12345678
   ```

   然后重新启动。

到此NVIDIA的安装方式讲解完了。。。。

**END**

# kali linux 升级内核 安装内核头文件 安装nvidia驱动

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[mixboot](https://mixboot.blog.csdn.net/) 2018-06-17 00:55:31 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 5303 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 3

分类专栏： [Kali Linux](https://blog.csdn.net/u010953692/category_6687313.html) 文章标签： [kali linux](https://www.csdn.net/tags/MtjaUgysMTg0Ny1ibG9n.html)

版权

#### 1.linux升级内核

```
apt-get update
apt-get upgrade
apt-get dist-upgrade
reboot1234
```

#### 2.方法二

```
apt update && apt full-upgrade1
```

#### 3.安装内核头文件

```
apt-get install linux-headers- `uname -r`1
```

#### 4.检车内核头文件是否安装

```
# dpkg-query -s linux-headers-$(uname -r)1
```

#### 5.安装nvidia驱动

执行命令后重启会进入不了图形界面，需要进入命令行界面Ctrl+Alt+f3

```
apt install -y ocl-icd-libopencl1 nvidia-driver nvidia-cuda-toolkit1
```

![这里写图片描述](https://img-blog.csdn.net/20180617171922150?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA5NTM2OTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

#### 6.验证nvidia驱动

```
# nvidia-smi1
```

![这里写图片描述](https://img-blog.csdn.net/2018061717193993?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA5NTM2OTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

#### 7.安装hashcat

```
# aptitude search hashcat
# aptitude install hashcat
# hashcat --help123
```

参考：
0.[2017年Kali Linux更新源](https://blog.csdn.net/wy_bk/article/details/78636342)
1.[更新系统](https://blog.csdn.net/qq_21774161/article/details/68070594)
2.[准备内核头文件](https://wizardforcel.gitbooks.io/daxueba-kali-linux-tutorial/content/8.html)
3.[Linux有问必答：如何在Linux上安装内核头文件](https://linux.cn/article-4625-1.html)
4.[在Kali Linux上安装NVIDIA GPU驱动程序](https://docs.kali.org/general-use/install-nvidia-drivers-on-kali-linux)