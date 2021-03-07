centos7 刚安装，需要做一些配置才能正常上网！

**1.虚拟网络编辑器配置**

1）通过VMware菜单栏，依次点击***\*编辑\****和**虚拟网络编辑器**

![img](https://img-blog.csdn.net/20180807210632604?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZWF0eGlhb3Rpbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

2）选中VMnet8，**取消勾选****使用本地DHCP服务将IP地址分配给虚拟机****，**查看**DHCP**确保**未启用**，点击**NAT设置**

![img](https://img-blog.csdn.net/20180807210736542?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZWF0eGlhb3Rpbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

3）查看网关IP，并记住**192.168.255.2**，用于网络配置文件设置

![img](https://img-blog.csdn.net/20180807210808775?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZWF0eGlhb3Rpbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**2.修改mac地址**

如果本虚拟机为克隆机，则需要重新生成mac地址；如果是非克隆机，可跳过此步骤！

通过VMware菜单栏，依次点击**虚拟机**和**设置**，然后选中**网络适配器**，点击**高级**和**生成**mac地址。

![img](https://img-blog.csdn.net/20180811003429634?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZWF0eGlhb3Rpbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 

**3.网络配置文件设置**

1）进入网络配置文件目录

cd /etc/sysconfig/network-scripts

**ifcfg-eno16777736就是需要设置的网络配置文件**

**![img](https://img-blog.csdn.net/20180807231035548?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZWF0eGlhb3Rpbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)**

2）编辑网络配置文件

**sudo** **vim** **ifcfg-eno16777736**

网络配置文件内容编辑如下（红色标识为变动的部分）：

TYPE="Ethernet"

BOOTPROTO="**static**"

DEFROUTE="yes"

PEERDNS="yes"

PEERROUTES="yes"

IPV4_FAILURE_FATAL="no"

IPV6INIT="yes"

IPV6_AUTOCONF="yes"

IPV6_DEFROUTE="yes"

IPV6_PEERDNS="yes"

IPV6_PEERROUTES="yes"

IPV6_FAILURE_FATAL="no"

NAME="eno16777736"

UUID="0e6ca219-0d2e-4000-8f17-bf7424e46595"

DEVICE="eno16777736"

ONBOOT="**yes**"

**IPADDR=192.168.255.101**

**GATEWAY=192.168.255.2**

**NETMASK=255.255.255.0**

**DNS=192.168.255.1**

3）保存修改网络配置文件，重启网卡服务

service network restart

**4.验证网络配置结果**

**ping www.baidu.com**

出现如下结果，表示虚拟机网络配置成功！

![img](https://img-blog.csdn.net/20180807232234227?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZWF0eGlhb3Rpbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

# [centos7 下修改网络配置](https://www.cnblogs.com/jpfss/p/10912052.html)

# 修改ip地址

1. 编辑 /etc/sysconfig/network-scripts/ifcfg-eth0

   TYPE=Ethernet
   BOOTPROTO=static **静态ip**
   DEFROUTE=yes
   IPV4_FAILURE_FATAL=no
   IPV6INIT=yes
   IPV6_AUTOCONF=yes
   IPV6_DEFROUTE=yes
   IPV6_FAILURE_FATAL=no
   NAME=eno16777736
   UUID=34bbe4fa-f0b9-4ced-828a-f7f7e1094e4a
   DEVICE=eno16777736
   ONBOOT=yes
   PEERDNS=yes
   PEERROUTES=yes
   IPV6_PEERDNS=yes
   IPV6_PEERROUTES=yes
   IPADDR=192.168.179.3 **ip地址**
   NETMASK=255.255.255.0 **子网掩码**
   GATEWAY=192.168.179.2 **网关**

2. 运行 service network restart

# 修改dns地址

编辑/etc/resolv.conf
修改文件内容 nameserver 114.114.114.114

# 常用dns地址

114.114.114.114
114.114.115.115
223.5.5.5 阿里
223.6.6.6 阿里
180.76.76.76 百度

# VMware虚拟机中Centos7网络配置及ping不通思路

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/bestlope)

[bestlope](https://blog.51cto.com/bestlope)关注0人评论[70286人阅读](javascript:;)[2017-10-28 19:05:57](javascript:;)

在安装好VMware虚拟机并且安装好Centos7系统后，我们就需要进行网络配置了。

因为实验环境中，需要固定IP，方便各种环境的使用。

我们可以用VMware的NET模式进行网络配置。

下面，我们进入配置流程：



一、配置VMware的NET网络模式

1、关闭目前需要更改配置的虚拟机。

2、点击 编辑虚拟机设置——网络适配器——NAT模式（N）：用于共享侏罗纪的IP地址，确定。

[![ad445bbf2b48f883895df60fdb60a742.png-wh_](https://s5.51cto.com/oss/201710/28/ad445bbf2b48f883895df60fdb60a742.png-wh_500x0-wm_3-wmp_4-s_4022650243.png)](https://s5.51cto.com/oss/201710/28/ad445bbf2b48f883895df60fdb60a742.png-wh_500x0-wm_3-wmp_4-s_4022650243.png)

3、在VMware虚拟机任务栏——编辑（E）——虚拟网络编辑器——VMnet8——取消勾选的 使用本地DHCP服务将IP地址分配给虚拟机 #因为我们需要固定IP，所以，不能直接让虚拟机分配IP——把 子网IP 改为： 192.168.137.0 #因为此网段为window分配给VMnet8的网段——确定

[![f1bd8d7724e8bb08fcd3ab442437c531.png-wh_](https://s2.51cto.com/oss/201710/28/f1bd8d7724e8bb08fcd3ab442437c531.png-wh_500x0-wm_3-wmp_4-s_144411794.png)](https://s2.51cto.com/oss/201710/28/f1bd8d7724e8bb08fcd3ab442437c531.png-wh_500x0-wm_3-wmp_4-s_144411794.png)



二、配置window的internet连接共享

1、我的电脑——空白处右键属性——控制面板主页——网络和internet——网络和共享中心——更改适配器设置——以太网（或叫本地网络）右键属性——共享——选择家庭网络连接（H）：VMware Network Adapter VMnet8——勾选：允许其他网络用户通过此计算机的internet连接来连接——确定

[![1e57b5f7066c0accf566b0bbbb4d5d04.png-wh_](https://s2.51cto.com/oss/201710/28/1e57b5f7066c0accf566b0bbbb4d5d04.png-wh_500x0-wm_3-wmp_4-s_768567238.png)](https://s2.51cto.com/oss/201710/28/1e57b5f7066c0accf566b0bbbb4d5d04.png-wh_500x0-wm_3-wmp_4-s_768567238.png)





三、手动配置Centos7系统里的网络配置

```
cd /etc/sysconfig/network-scripts
ls #找到当前网络配置文件为ifcfg-ens32
sudo vim ifcfg-ens32
#修改如下网络配置
BOOTPROTO=static #以静态方式获取IP
IPADDR=192.168.137.7 #IP地址为192.168.137.7（192.168.137.0网段内）
NETMASK=255.255.255.0
GATEWAY=192.168.137.1 #网关需要与IP在一个网段内
DNS1=192.168.137.1
ONBOOT=yes #开机启动网卡
：wq #保存退出
```

[![b93bc0a0446a87c0857848467a900468.png-wh_](https://s3.51cto.com/oss/201710/28/b93bc0a0446a87c0857848467a900468.png-wh_500x0-wm_3-wmp_4-s_841934748.png)](https://s3.51cto.com/oss/201710/28/b93bc0a0446a87c0857848467a900468.png-wh_500x0-wm_3-wmp_4-s_841934748.png)

```
sudo systemctl restart network #重启网卡
sudo systemctl enable network #开机启动网卡
```



四、测试

```
ifconfig #查看网卡信息
ping www.baidu.com #能PING通就是联网成功
```

[![a05712486f23dc5b5781dbc29136864a.png-wh_](https://s2.51cto.com/oss/201710/28/a05712486f23dc5b5781dbc29136864a.png-wh_500x0-wm_3-wmp_4-s_950996265.png)](https://s2.51cto.com/oss/201710/28/a05712486f23dc5b5781dbc29136864a.png-wh_500x0-wm_3-wmp_4-s_950996265.png)



五、常见问题

1、偶尔window主机后，进入Centos7不能联网

bestlope：可以尝试把 网络共享——允许其他网络用户通过此计算机的internet连接来连接取消打勾后确认，再打勾一次确认，基本上Centos7就能联网了。

具体是为什么，目前我就不知道了。

[![1e57b5f7066c0accf566b0bbbb4d5d04.png-wh_](https://s2.51cto.com/oss/201710/28/1e57b5f7066c0accf566b0bbbb4d5d04.png-wh_500x0-wm_3-wmp_4-s_768567238.png)](https://s2.51cto.com/oss/201710/28/1e57b5f7066c0accf566b0bbbb4d5d04.png-wh_500x0-wm_3-wmp_4-s_768567238.png)

©著作权归作者所有：来自51CTO博客作者bestlope的原创作品，如需转载，请注明出处，否则将追究法律责任