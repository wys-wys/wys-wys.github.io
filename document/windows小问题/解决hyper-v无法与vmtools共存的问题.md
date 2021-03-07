# 喜大普奔！Hyper-V 和 VMWare 终于可以无缝共存、同时运行了！

[![img](https://upload.jianshu.io/users/upload_avatars/38158/0c9d661bc816?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/39136033a03c)

[Kukmoon谷月](https://www.jianshu.com/u/39136033a03c)关注

0.1982020.07.19 01:33:53字数 1,089阅读 3,942



早期，Hyper-V 和 VMWare Workstation/Player 不能共存。如果在启用了 Hyper-V 的 Windows 中强行运行 VMWare Workstation/Player，它会提示“VMWare Workstation/Player and Hyper-V 不兼容，请在运行 VMWare Workstation/Player 之前移除 Hyper-V 角色。”(VMWare Workstation/Player and Hyper-V are not compatible. Remove the Hyper-V role from the system before running VMWare Workstation/Player）

![img](https://upload-images.jianshu.io/upload_images/38158-d17a57f7f59b86b4?imageMogr2/auto-orient/strip|imageView2/2/w/322/format/webp)

VMWare Workstation 弹出的不兼容提示

（图片来源：VMWare 官网[1]）

# 1. 原因分析

Hyper-V 是一个type 1 hypervisor[2]，当在 Windows 中启用 Hyper-V 时，Windows 系统在硬件底层与 Windows 应用层之间插入了一层 Hyper-V，而原来的 Windows 应用层则变成了一个运行在 Hyper-V 上的虚拟机。

而 VMWare Workstation/Player 使用一种被称为虚拟机监视器（Virtual Machine Monitor，VMM）[3]的机制，直接访问 CPU 内建的虚拟化功能，因此，它们本身不能在虚拟机环境中运行，换句话说，不支持嵌套虚拟化（nested virtualization）。

当 Windows 启用 Hyper-V 时，原来的 Windows 变成了虚拟机环境，偏偏 VMWare Workstation/Player 不能在虚拟机环境中运行，因此，运行VMWare Workstation/Player 时会报错。

# 2. 传统的解决方法

传统的解决方法是在选择多系统的启动菜单中新增一个选项，让 Windows 在启动时不加载 Hyper-V [4]。

主要步骤如下：

> **解决办法：**
>
> 以管理员身份打开命令提示符，运行如下两条命令：
>
> 
>
> ```jsx
> bcdedit /copy {default} /d "name"bcdedit /set {ID-Number} HyperVisorLaunchType OFF
> ```
>
> **命令详解：**
>
> 第一条命令中 name 参数支持自定义。
>
> 如果第一条命令成功的话，就会有一串很长的 ID 出现，复制它，第二条命令中需要用到，即 ID-Number 参数，要把它复制到“{}”这个符号中间。
>
> 比如我执行的命令：
>
> 
>
> ```jsx
> bcdedit /copy {default} /d "Windows Server 2012 Without Hyper-V"bcdedit /set {ce54aea7-ad33-11e9-9022-f8edf66e1542} HyperVisorLaunchType OFF
> ```
>
> 执行成功后可以用 msconfig 验证是否成功创建启动项，并将引导菜单超时时间修改大一些。
>
> 然后重启系统，在选择启动项界面选择"Windows Server 2012 Without Hyper-V"就能运行 VMWare 了。
>
> 这样比装双系统方便些，而且这两个引导进去的系统是一样的，只是，有一>个只能运行 VMWare，另一个只能运行 Hyper-V。

# 3. 遇到了新困难

Windows 引入的一些新功能，例如 WSL 2、 基于虚拟化的安全功能（Virtualization Based Security, VBS，包括Windows Sandbox、Credential Guard、 Application Guard 等）依赖 Hyper-V 环境[5]，如果 Windows 系统不加载 Hyper-V， 这些功能也无法使用。

古人有诗云，世间安得双全法，不负如来不负卿。有没有什么双全法可以兼得鱼与熊掌，让 VMWare Workstation/Player 与 Hyper-V 真正共存呢？

# 4. VMWare 和微软合作

从 VMWare Workstation/Player 15.5.5 版本开始，VMWare 公司重构了 VMM机制，将 VMM 机制调整为在用户级别运行[6]，不再直接访问硬件，而是通过利用微软的 Windows Hypervisor Platform (WHP) 的 API 来运行。从而彻底解决了 VMWare Workstation/Player 与 Hyper-V 的冲突问题。

# 5. 如何让 VMWare 和 Hyper-V 共存？

1. 将 Windows 版本升级到 Windows 10 20H1 或更高版本。
2. 将 VMWare Workstation/Player 升级到 15.5.5 或更高版本，本文以 VMWare Player 为例。**注意**，在安装时，需要在如图所示的这一步勾选“自动安装 Windows Hypervisor Platform (WHP)”。![img](https://upload-images.jianshu.io/upload_images/38158-927ac6bb9df67baa)
3. 运行 VMWare Workstation/Player，新建或导入虚拟机。
4. 打开虚拟机的设置选项，找到“处理器”，**去掉如图所示的三个选项前面的钩**，点击“确定”。![img](https://upload-images.jianshu.io/upload_images/38158-f4d6a61af74c46da)否则，在运行虚拟机时，VMWare Workstation/Player 会提示“开机时出错：VMWarePlayer 在此主机上不支持嵌套虚拟化。模块 MonitorMode 启动失败。未能启动虚拟机。”（VMware Workstation does not support nested virtualization on this host. Module ‘MonitorMode’ power on failed. Failed to start the virtual machine.）![img](https://upload-images.jianshu.io/upload_images/38158-e25abf0d14d617e1)

**至此，大功告成。
**

![img](https://upload-images.jianshu.io/upload_images/38158-65f7aeca6fa1f3c5)

**Hyper-V（左）和VMWare Player（右）同时运行**

**
**

![img](https://upload-images.jianshu.io/upload_images/38158-0e147d534d93191d)



### 参考资料

[1]VMware Workstation Zealot: *https://blogs.vmware.com/workstation/2019/08/workstation-hyper-v-harmony.html*[2]hyper-v 和 vmware 不兼容，是技术的原因？还是商业原因？: *https://www.zhihu.com/question/21260608*[3]VMware Workstation 15.5 Now Supports Host Hyper-V Mode: *https://blogs.vmware.com/workstation/2020/05/vmware-workstation-now-supports-hyper-v-mode.html*[4]windows下vmware和Hyper-v共存方法: *https://www.cnblogs.com/zqifa/p/11327539.html*[5]VMware Workstation and Hyper-V: *https://techcommunity.microsoft.com/t5/virtualization/vmware-workstation-and-hyper-v/ba-p/1419928*[6]VMware Workstation 15.5 Now Supports Host Hyper-V Mode: *https://blogs.vmware.com/workstation/2020/05/vmware-workstation-now-supports-hyper-v-mode.html*