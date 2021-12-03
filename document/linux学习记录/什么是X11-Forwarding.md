# 什么是X11-Forwarding

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[正在Coding](https://blog.csdn.net/weixin_41668084) 2021-01-29 00:34:14 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 608 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 4

分类专栏： [Linux](https://blog.csdn.net/weixin_41668084/category_10707813.html) [虚拟机工具](https://blog.csdn.net/weixin_41668084/category_10656950.html) [CentOS](https://blog.csdn.net/weixin_41668084/category_10657025.html) 文章标签： [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [X11-forwarding](https://so.csdn.net/so/search/s.do?q=X11-forwarding&t=blog&o=vip&s=&l=&f=&viparticle=) [远程连接工具](https://www.csdn.net/tags/MtTaEg0sMDM4ODUtYmxvZwO0O0OO0O0O.html) [图形化显示](https://so.csdn.net/so/search/s.do?q=图形化显示&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

## 一、问题描述

当我们使用[MobaXterm](https://mobaxterm.mobatek.net/)连接远程服务器，连接成功页面显示几个列表，其中包括X11-Forwarding，并且显示服务器禁用。那么它到底是什么东西呢？
![img](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210128204900.png)

## 二、什么是X11（X协议原理简介）

> Linux 本身是没有图形化界面的，所谓的图形化界面系统只不过中 Linux 下的应用程序。这一点和 Windows 不一样。Windows 从 Windows 95 开始，图形界面就直接在系统内核中实现了，是操作系统不可或缺的一部分。Linux 的图形化界面，底层都是基于 X 协议。

### 2.1.X 协议由 X server 和 X client 组成：

1. X server 管理主机上与显示相关的硬件设置（如显卡、硬盘、鼠标等），它负责屏幕画面的绘制与显示，以及将输入设置（如键盘、鼠标）的动作告知 X client。
2. X client (即 X 应用程序) 则主要负责事件的处理（即程序的逻辑）。

### 2.2.案例说明

> 举个例子，如果用户点击了鼠标左键，因为鼠标归 X server 管理，于是 X server 就捕捉到了鼠标点击这个动作，然后它将这个动作告诉 X client，因为 X client 负责程序逻辑，于是 X client 就根据程序预先设定的逻辑（例如画一个圆），告诉 X server 说：“请在鼠标点击的位置，画一个圆”。最后，X server 就响应 X client 的请求，在鼠标点击的位置，绘制并显示出一个圆。

## 三、什么是X11 Forwarding

许多时候 X server 和 X client 在同一台主机上，这看起来没什么。但是， **X server 和 X client 完全可以运行在不同的机器上，只要彼此通过 X 协议通信即可。**

于是，我们就可以做一些“神奇”的事情，在本地显示 (X server)运行在服务器上的 GUI 程序 (X client)。这样的操作可以通过 SSH X11 Forwarding 来实现。X11 中的 X 指的就是 X 协议，**11 指的是采用 X 协议的第 11 个版本**。

![X11 Forwarding](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210129000651.jpeg)

### 3.1.X11 Forwarding

有了X11 Forwarding，通过SSH连接并运行Linux上有GUI的程序，就像是在Windows下运行GUI程序一样方便。很多时候，这样的机制可以方便有图形显示的程序的调试。但是要实现X11 Forwording，需要具备X Server的SSH客户端，推荐使用MobaXTerm软件，默认就带X Server程序，免费的非常好用。

X Client部分，要安装一下软件包，要打开SSH的配置文件，将X11Forwarding修改为Yes。

## 四、远程执行图形化程序

1.Linux服务器安装X11-Forwarding的支持，以及一个图形化小软件xclock。

```bash
yum install  xorg-x11-xauth xorg-x11-fonts-* xorg-x11-font-utils xorg-x11-fonts-Type1 xclock -y
1
```

![image-20210129001957732](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210129002001.png)2.打开mobaxterm，连接服务器。

![img](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210128204900.png)

> 虽然安装了支持，但是我们ssh还没有启用x11-forwarding的功能。

3.在/etc/ssh/sshd_config里，将X11Forwarding改为yes

![image-20210129001326754](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210129001329.png)

4.重启sshd服务

```bash
systemctl restart sshd
1
```

5.重连服务器

> X11-forwading开启成功

![image-20210128235535822](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210128235545.png)

6.远程开启图形化程序 xclock

```bash
xclock
1
```

![image-20210129002148751](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210129002151.png)

7.远程开启图形化程序 firefox-浏览器

```bash
firefox
1
```

![image-20210129002518859](https://gitee.com/gbc_sxy/imagebed/raw/master/img/20210129002521.png)

以上，请参考！

------

### 参考链接

1. [什么是X11 Forwarding？](https://www.maixj.net/ict/x11-forwarding-20298)
2. [X协议原理简介](https://www.maixj.net/ict/x-xieyi-20296)
3. [使用X11-Forwarding，远程执行图形化程序](https://www.kentonhu.com/?p=1837)