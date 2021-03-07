# 解决重装Vmware出现无法安装服务“Vmware Authorization Service”( VmAuthdService)。请确保您有足够的权限安装系统服务。

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[simplebooy](https://me.csdn.net/simplebooy) 2020-03-30 17:41:20 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3472 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

文章标签： [vmware](https://so.csdn.net/so/search/s.do?q=vmware&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

**仅供后面的兄弟们参考**
今天虚拟机出现了一系列问题，诸如：无法连接至虚拟机、无法安装服务等等，网上给出的方法大多是删除某些文件，禁用或重启某些服务等等。在我多次尝试，包括使用管理员权限也无法重启某些服务时，我选择用VMware自带的安装程序用来修复，然而还是无法解决，提示不够权限写入某dll文件。
多次在网上搜索解决方案后无果，心力憔悴，只能在控制面板将Vmware卸载后选择重装。

巧的是，重装过程中，也出现了提示没有足够权限安装系统服务
![没错又是这个](https://img-blog.csdnimg.cn/20200330170053995.png)
翻阅了一些文章之后，我找到了下面这篇：
https://www.fujieace.com/vmware/vmauthdservice.html

> 出现问题的原因： 1、权限不足（不是管理员权限）；
>
> 2、曾经此电脑安装过Vmware（以前安装的Vmware和现在安装的Vmware版本是一样的），但是并没有彻底卸载（注册表、服务…没有彻底清理）

不排除用管理员权限安装就能快速解决问题，但在重装软件之前排错的时候已经确定并非权限问题，所以我将原因锁定在第二个身上。
在多次筛选之后，我找到了另一篇文章：
https://blog.csdn.net/weixin_33873846/article/details/86391031
尝试以管理员身份启动cmd，输入以下代码：

```
net stop VMAuthdService
taskkill /F /IM mmc.exe
sc delete VMAuthdService
123
```

输入之后，cmd内会报错1060。这个时候再去重装VMware，就能安装成功了
因为VMware出错的时候问题五花八门，所以还是得提一句：**仅供参考**
**仅供后面的兄弟们参考**


随笔 - 4 文章 - 0 评论 - 4

# [VMware Workstation 16激活码](https://www.cnblogs.com/xianyux/p/13678149.html)

虚拟机 VMware Workstation 16
激活码：ZF3R0-FHED2-M80TY-8QYGC-NPKYF

赶紧安排上