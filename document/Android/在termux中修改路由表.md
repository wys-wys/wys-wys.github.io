# 操作Android手机路由表

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[gongzhxu](https://blog.csdn.net/Yshe_xun) 2013-06-25 16:32:43 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 11859 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

版权

公司为了安全wifi网络需要手工设置路由表才能上网，查了好久的资料终于找到。

用电脑操作android手机工具[adb](http://download.csdn.net/download/yshe_xun/5647769)方便输入命令（也可用手机终端模拟器），这是通过usb线来调试管理手机的工具，使用非常简单在控制台下输入adb.exe文件的路径再空格后输入shell，即可管理手机。



1，显示路由命令

\#ip route show

2，添加路由命令

\#route add -net 146.0.0.0 netmask 255.0.0.0 gw 192.168.0.2

或者

\#ip route add 146.0.0.0/8 dev wlan0

3，删除路由命令

\#ip route del 146.0.0.0/8

# android系统（107）---Android路由表设置（route &amp; DNS）

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[zhangbijun1230](https://blog.csdn.net/zhangbijun1230) 2018-06-19 08:30:14 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 5611 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [android 系统](https://blog.csdn.net/zhangbijun1230/category_6500595.html)

# Android路由表设置（route & DNS）

# 

# route设置

android4.4只使用了一份路由表，使用busybox route就可以完成路由表的设置，从android5.0之后，考虑要对多网络的支持，采用了多路由表，下面的设置方法只适用于android4.4之前的版本，android5.0之后的版本路由表如何设置留到以后再说明。

1、查看路由表 busybox route -n 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 0 0 0 eth0 
0.0.0.0 192.168.7.1 0.0.0.0 UG 202 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0 
192.168.7.1 0.0.0.0 255.255.255.255 UH 0 0 0 eth0

2、删除默认路由 busybox route del default 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 202 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0 
192.168.7.1 0.0.0.0 255.255.255.255 UH 0 0 0 eth0

3、添加一条默认路由 busybox route add -net 0.0.0.0 gw 192.168.7.1 netmask 0.0.0.0 dev eth0 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0 
192.168.7.1 0.0.0.0 255.255.255.255 UH 0 0 0 eth0

4、删除一条主机路由 busybox route del -host 192.168.7.1 dev eth0 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0

5、添加一条主机路由 busybox route add -host 192.168.7.1 dev eth0 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0 
192.168.7.1 0.0.0.0 255.255.255.255 UH 0 0 0 eth0

6、删除一条网络路由 busybox route del -net 192.168.0.0 netmask 255.255.248.0 dev eth 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0

7、添加一条网络路由 busybox route add -net 192.168.0.0 netmask 255.255.248.0 dev eth 
Kernel IP routing table 
Destination Gateway Genmask Flags Metric Ref Use Iface 
0.0.0.0 192.168.7.1 0.0.0.0 UG 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 0 0 0 eth0 
192.168.0.0 0.0.0.0 255.255.248.0 U 202 0 0 eth0

# DNS Server设置

同样以android4.4为例来进行说明，[Android](http://lib.csdn.net/base/android)系统中，不管是dns server的设置，还是域名解析，都是由netd进程来执行的，netd与dns的相关操作是调用了一个netbsd的库，netd中dns server设置对应于文件ResolverController.cpp，域名解析对应于文件DnsProxyListener.cpp。

原生的android系统只提供了设置系统dns server的接口，而没有提供查看系统dns server的接口，需要自己添加代码来实现。

通过ndc配合netd可以对android dns进行设置和查看。 
1、设置dns interface & server 
ndc resolver setdefaultif eth0 
ndc resolver setifdns eth0 “” 192.168.7.2

2、查看dns interface 
ndc resolver getdefaultif 
226 0 DNS default interface is eth0

3、查看dns server 
ndc resolver getdefaultServer 1 
226 0 DNS default server[1] is 192.168.7.2

