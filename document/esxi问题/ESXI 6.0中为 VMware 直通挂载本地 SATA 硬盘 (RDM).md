**正文**字体大小：[大](javascript:;) **中** [小](javascript:;)

[![此博文通过手机撰写(手机访问sina.cn)](http://simg.sinajs.cn/blog7style/images/common/sg_trans.gif)](http://news.sina.com.cn/437/2008/0703/24.html) 

## ESXI 6.0中为 VMware 直通挂载本地 SATA 硬盘 (RDM)

 ![此博文包含图片](http://simg.sinajs.cn/blog7style/images/common/sg_trans.gif) (2015-10-20 13:33:19)

[![img](http://simg.sinajs.cn/blog7style/images/common/sg_trans.gif)转载*▼*](javascript:;)

| 标签： it | 分类： [ESXI](http://blog.sina.com.cn/s/articlelist_2687364453_3_1.html) |
| --------- | ------------------------------------------------------------ |
|           |                                                              |

   作为虚拟化领域的领导厂商，VMware 当然也考虑到了这个问题，ESXi 支持设备的直通，包括各种 PCIe 设备（需要 ESXi 基础硬件的某些虚拟化特性，如 VT-D/IOMMU 等支持）。对于存储，官方的 RDM 一般只有通过认证的 RAID/SCSI 卡或 iscsi/SAN 存储设备才可以 RDM。不过无论如何，直接访问主板上连接的硬盘驱动器都不被官方支持。

那么，怎样才能让 ESXi 中的虚拟机直接访问主板挂载的 SATA 硬盘呢？这就需要我们另辟蹊径了。

   裸设备映射(RDM)可以理解为硬盘的直通。不同于虚拟磁盘是存在于VMFS存储卷中的一个文件，RDM是直接访问物理设备，不会改变物理设备的状态。在VMware 5.x中，RDM是为SAN（存储域网络）设计的，要使其用于SATA硬盘，需要借助”SecureCRT”这样的SSH Shell软件，并在ESXi主机上开启SSH Shell。

首先你得熟悉命令行操作，知道如何使用终端管理工具，使用 SSH 或 ESXi 控制台进入 ESXi 的 Shell 界面。

第一步、得找到需要映射的 RAW 驱动器名称：

![image-20210524082640179](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20210524082640179.png)

或者一下方式获得，

启动SecureCRT，新建一个SSH2 连接，提示输入帐号和密码。

ls /dev/disks

 

在 ESXi datastore 中建立硬盘标识文件，该文件也是以 vmdk 为后缀，不过它只以文本方式保存了硬盘 RAW 信息。

第二步、获得存储RDM映射文件的路径

![image-20210524082837074](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20210524082837074.png)

第三步、输入下面的命令执行。

| 1    | vmkfstools  -z /vmfs/devices/disks/<前面找到的RAW名称>[空格]/<存储RDM映射文件的路径>/映射文件名>.vmdk |
| ---- | ------------------------------------------------------------ |
|      |                                                              |



 下图为实列      ![image-20210524082854587](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20210524082854587.png) 成功后无任何信息提示，在 ESXi datastore 中建立硬盘标识文件，该文件也是以 vmdk 为后缀，不过它只以文本方式保存了硬盘 RAW 信息。

   接下来，在 vSphere Client 中编辑虚拟机配置，以添加现有虚拟磁盘的方式，选择刚刚创建的 RDM 映射文件就 OK 了。

分享：