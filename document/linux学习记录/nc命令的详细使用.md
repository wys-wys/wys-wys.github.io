[![程序员节Logo](https://common.cnblogs.com/images/festival/1024-2020-logo.png?id=102322)](https://www.cnblogs.com/)[首页](https://www.cnblogs.com/)[新闻](https://news.cnblogs.com/)[博问](https://q.cnblogs.com/)[专区](https://brands.cnblogs.com/)[闪存](https://ing.cnblogs.com/)[班级](https://edu.cnblogs.com/)![搜索](https://www.cnblogs.com/images/aggsite/search.svg)[注册](https://account.cnblogs.com/signup/)[登录](https://account.cnblogs.com/signin/?returnUrl=https://www.cnblogs.com/)

# [nmap](https://www.cnblogs.com/nmap/)

随笔 - 160, 文章 - 138, 评论 - 48, 引用 - 0

## [nc命令用法举例](https://www.cnblogs.com/nmap/p/6148306.html)

# 什么是nc

nc是netcat的简写，有着网络界的瑞士军刀美誉。因为它短小精悍、功能实用，被设计为一个简单、可靠的网络工具

# nc的作用

（1）实现任意TCP/UDP端口的侦听，nc可以作为server以TCP或UDP方式侦听指定端口

（2）端口的扫描，nc可以作为client发起TCP或UDP连接

（3）机器之间传输文件

（4）机器之间网络测速                                                                                                             

# nc的控制参数不少，常用的几个参数如下所列：

1) -l

用于指定nc将处于侦听模式。指定该参数，则意味着nc被当作server，侦听并接受连接，而非向其它地址发起连接。

2) -p <port>

暂未用到（老版本的nc可能需要在端口号前加-p参数，下面测试环境是centos6.6，nc版本是nc-1.84，未用到-p参数）

3) -s 

指定发送数据的源IP地址，适用于多网卡机 

4) -u

 指定nc使用UDP协议，默认为TCP

5) -v

输出交互或出错信息，新手调试时尤为有用

6）-w

超时秒数，后面跟数字 

7）-z

表示zero，表示扫描时不发送任何数据

 

 

 

# 前期准备

准备两台机器，用于测试nc命令的用法

主机A：ip地址 10.0.1.161

主机B：ip地址 10.0.1.162

 

两台机器先安装nc和nmap的包

yum install nc -y

yum install nmap -y

如果提示如下-bash： nc： command not found 表示没安装nc的包

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095517663-1040120011.png)

 

# **nc用法1，网络连通性测试和端口扫描**

 

 

**nc可以作为server端启动一个tcp的监听（注意，此处重点是起tcp，下面还会讲udp）**

先关闭A的防火墙，或者放行下面端口，然后测试B机器是否可以访问A机器启动的端口

在A机器上启动一个端口监听，比如 9999端口（注意：下面的-l 是小写的L，不是数字1）

默认情况下下面监听的是一个tcp的端口

nc -l 9999

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095543554-1037638344.png)

 

**客户端测试，****测试方法1**

在B机器上telnet A机器此端口，如下显示表示B机器可以访问A机器此端口

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095601413-784407778.png)

 

 

***\*客户端测试，\**测试方法2**

B机器上也可以使用nmap扫描A机器的此端口

nmap 10.0.1.161 -p9999

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095617601-914929817.png)

 

 

***\*客户端测试，\**测试方法3**

使用nc命令作为客户端工具进行端口探测

nc -vz -w 2 10.0.1.161 9999

（-v可视化，-z扫描时不发送数据，-w超时几秒，后面跟数字）

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095634851-958356921.png)

上面命令也可以写成

nc -vzw 2 10.0.1.161 9999

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095651569-1755893958.png)

 

 

***\*客户端测试，\**测试方法4（和方法3相似，但用处更大）**

nc可以可以扫描连续端口，这个作用非常重要。常常可以用来扫描服务器端口，然后给服务器安全加固

在A机器上监听2个端口，一个9999，一个9998，使用&符号丢入后台

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095712866-936204965.png)

 

在客户端B机器上扫描连续的两个端口，如下

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095732429-1764157681.png)

 

 

 

**nc作为server端启动一个udp的监听（注意，此处重点是起udp，上面主要讲了tcp）**

启动一个udp的端口监听

nc  -ul  9998

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095753835-1671845784.png)

复制当前窗口输入 netstat -antup |grep 9998 可以看到是启动了udp的监听

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209095812632-1749454663.png)

 

 

**客户端测试，测试方法1**

nc -vuz 10.0.1.161 9998

由于udp的端口无法在客户端使用telnet去测试，我们可以使用nc命令去扫描（前面提到nc还可以用来扫描端口）

（telnet是运行于tcp协议的）

（u表示udp端口，v表示可视化输出，z表示扫描时不发送数据）

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100707882-1433264712.png)

上面在B机器扫描此端口的时候，看到A机器下面出现一串XXXXX字符串

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100725866-2147390474.png)

 

 

 

**客户端测试，测试方法2**

nmap -sU 10.0.1.161 -p 9998 -Pn

（它暂无法测试nc启动的udp端口，每次探测nc作为server端启动的udp端口时，会导致对方退出侦听，有这个bug，对于一些程序启动的udp端口在使用nc扫描时不会有此bug）

下面，A机器启动一个udp的端口监听，端口为9998

在复制的窗口上可以确认已经在监听了

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100746272-590584994.png)

B机器使用nmap命令去扫描此udp端口，在扫描过程中，导致A机器的nc退出监听。所以显示端口关闭了（我推测是扫描时发数据导致的）

nmap -sU 10.0.1.161 -p 9998 -Pn

-sU ：表示udp端口的扫描

-Pn ：如果服务器禁PING或者放在防火墙下面的，不加-Pn 参数的它就会认为这个扫描的主机不存活就不会进行扫描了，如果不加-Pn就会像下面的结果一样，它也会进行提示你添加上-Pn参数尝试的

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100804726-1083735542.png)

注意：如果A机器开启了防火墙，扫描结果可能会是下面状态。（不能确定对方是否有监听9998端口）

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100817866-337685966.png)

既然上面测试无法使用nmap扫描nc作为服务端启动的端口，我们可以使用nmap扫描其余的端口

（额，有点跑题了，讲nmap的用法了，没关系，主要为了说明nmap是也可以用来扫描udp端口的，只是扫描nc启动的端口会导致对方退出端口监听）

下面，A机器上rpcbind服务，监听在udp的111端口

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100833757-599551176.png)

在B机器上使用nmap扫描此端口，是正常的检测到处于open状态

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100847319-1809046272.png)

 

**客户端测试，测试方法3**

**nc扫描大量udp端口**

扫描过程比较慢，可能是1秒扫描一个端口，下面表示扫描A机器的1到1000端口（暂未发现可以在一行命令中扫描分散的几个端口的方法）

nc -vuz 10.0.1.161 1-1000

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100901819-1505522198.png)

 

 

 

 

 

 

 

 

 

 

 

 

 

 

# **nc用法2，使用nc传输文件和目录**

 

**方法1，传输文件演示（先启动接收命令）**

使用nc传输文件还是比较方便的，因为不用scp和rsync那种输入密码的操作了

把A机器上的一个rpm文件发送到B机器上

需注意操作次序，receiver先侦听端口，sender向receiver所在机器的该端口发送数据。  

 

**步骤1，先在B机器上启动一个接收文件的监听，格式如下**

意思是把赖在9995端口接收到的数据都写到file文件里（这里文件名随意取）

nc -l port >file

nc -l 9995 >zabbix.rpm

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100917507-1008395936.png)

 

***\*步骤2，\**在A机器上往B机器的9995端口发送数据，把下面rpm包发送过去**

nc 10.0.1.162 9995 < zabbix-release-2.4-1.el6.noarch.rpm

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100931116-1268991306.png)

B机器接收完毕，它会自动退出监听，文件大小和A机器一样，md5值也一样

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209100944897-733297904.png)

 

 

**方法2，传输文件演示（先启动发送命令）**

**步骤1，先在B机器上，启动发送文件命令**

下面命令表示通过本地的9992端口发送test.mv文件

nc -l 9992 <test.mv

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101002038-290824858.png)

 

**步骤2，A机器上连接B机器，取接收文件**

下面命令表示通过连接B机器的9992端口接收文件，并把文件存到本目录下，文件名为test2.mv

nc 10.0.1.162 9992 >test2.mv

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101017632-493505389.png)

 

 

 

**方法3，传输目录演示（方法发送文件类似）**

 

**步骤1，B机器先启动监听，如下**

A机器给B机器发送多个文件

传输目录需要结合其它的命令，比如tar

经过我的测试管道后面最后必须是 - ，不能是其余自定义的文件名

nc -l 9995 | tar xfvz -

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101035476-313895763.png)

 

**步骤2，A机器打包文件并连接B机器的端口**

管道前面表示把当前目录的所有文件打包为 - ，然后使用nc发送给B机器

tar cfz - * | nc 10.0.1.162 9995

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101051101-1053431813.png)

B机器这边已经自动接收和解压

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101107241-716031832.png)

 

 

 

 

 

 

 

 

 

 

 

 

 

# **nc用法3，测试网速**

测试网速其实利用了传输文件的原理，就是把来自一台机器的/dev/zero 发送给另一台机器的/dev/null

就是把一台机器的无限个0，传输给另一个机器的空设备上，然后新开一个窗口使用dstat命令监测网速

在这之前需要保证机器先安装dstat工具

yum install -y dstat

 

**方法1，测试网速演示（先启动接收命令方式）**

步骤1，A机器先启动接收数据的命令，监听自己的9991端口，把来自这个端口的数据都输出给空设备（这样不写磁盘，测试网速更准确）

nc -l 9991 >/dev/null

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101124179-1971991069.png)

 

步骤2，B机器发送数据，把无限个0发送给A机器的9991端口

nc 10.0.1.161 9991 </dev/zero

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101150304-1813015616.png)

 

在复制的窗口上使用dstat命令查看当前网速，dstat命令比较直观，它可以查看当前cpu，磁盘，网络，内存页和系统的一些当前状态指标。

我们只需要看下面我选中的这2列即可，recv是receive的缩写，表示接收的意思，send是发送数据，另外注意数字后面的单位B，KB，MB

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101211132-150010168.png)

 

可以看到A机器接收数据，平均每秒400MB左右

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101227069-1285313680.png)

B机器新打开的窗口上执行dstat，看到每秒发送400MB左右的数据

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101252491-2064947286.png)

 

 

 

**方法2，测试网速演示（先启动发送命令方式）**

步骤1，先启动发送的数据，谁连接这个端口时就会接收来自zero设备的数据（二进制的无限个0）

nc -l 9990 </dev/zero

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101318991-1622147288.png)

步骤2，下面B机器连接A机器的9990端口，把接收的数据输出到空设备上

nc 10.0.1.161 9990 >/dev/null

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101335976-869694121.png)

同样可以使用dstat观察数据发送时的网速

![img](https://images2015.cnblogs.com/blog/1076878/201612/1076878-20161209101801304-671989613.png)

 

 

 

分类: [Linux实用命令](https://www.cnblogs.com/nmap/category/921315.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1076878/20161209142058.png)](https://home.cnblogs.com/u/nmap/)

[nmap](https://home.cnblogs.com/u/nmap/)
[关注 - 5](https://home.cnblogs.com/u/nmap/followees/)
[粉丝 - 78](https://home.cnblogs.com/u/nmap/followers/)

[+加关注](javascript:void(0);)

15

0


[» ](https://www.cnblogs.com/nmap/p/6198561.html)下一篇： [记录一次CentOS环境升级Python2.6到Python2.7并安装最新版pip](https://www.cnblogs.com/nmap/p/6198561.html)

posted on 2016-12-09 14:08 [nmap](https://www.cnblogs.com/nmap/) 阅读(173313) 评论(5) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=6148306) [收藏](javascript:void(0))





### 评论

## [#1楼](https://www.cnblogs.com/nmap/p/6148306.html#3766317)  

好文章！

[支持(0) ](javascript:void(0);)[反对(0)](javascript:void(0);)

2017-08-25 14:04 | [立志做一个好的程序员](https://www.cnblogs.com/oxspirt/)

## [#2楼](https://www.cnblogs.com/nmap/p/6148306.html#4201542)  

mark

[支持(0) ](javascript:void(0);)[反对(0)](javascript:void(0);)

2019-03-13 17:57 | [FancyBrain](https://home.cnblogs.com/u/1053693/)

## [#3楼](https://www.cnblogs.com/nmap/p/6148306.html#4210861)  

m

[支持(0) ](javascript:void(0);)[反对(0)](javascript:void(0);)

2019-03-22 23:20 | [飞鸿影](https://www.cnblogs.com/52fhy/)

## [#4楼](https://www.cnblogs.com/nmap/p/6148306.html#4612954)  

好文章

[支持(0) ](javascript:void(0);)[反对(0)](javascript:void(0);)

2020-06-21 17:33 | [zwd108867](https://www.cnblogs.com/zhang2019104/)

## [#5楼](https://www.cnblogs.com/nmap/p/6148306.html#4672195)  

博主，想问下，为什么我在本机测试无法通过 /dev/zero 发送数据进来网速测试呢?具体表现是 reveiver 没有接收到任何数据。

[支持(0) ](javascript:void(0);)[反对(0)](javascript:void(0);)

2020-09-01 00:33 | [吕吕_Louis](https://home.cnblogs.com/u/475384/)



[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/nmap/p/6148306.html#)[返回顶部](https://www.cnblogs.com/nmap/p/6148306.html#top)

登录后才能发表评论，立即 [登录](javascript:void(0);) 或 [注册](javascript:void(0);)， [访问](https://www.cnblogs.com/) 网站首页。

- [首页](https://www.cnblogs.com/)
-  

- [新闻](https://news.cnblogs.com/)
-  

- [博问](https://q.cnblogs.com/)
-  

- [专区](https://brands.cnblogs.com/)
-  

- [闪存](https://ing.cnblogs.com/)
-  

- [班级](https://edu.cnblogs.com/)

### 导航

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/nmap/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/nmap)
- 
- [管理](https://i.cnblogs.com/)

| [<](javascript:void(0);)2020年10月[>](javascript:void(0);) |      |      |      |      |      |      |
| ---------------------------------------------------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 日                                                         | 一   | 二   | 三   | 四   | 五   | 六   |
| 27                                                         | 28   | 29   | 30   | 1    | 2    | 3    |
| 4                                                          | 5    | 6    | 7    | 8    | 9    | 10   |
| 11                                                         | 12   | 13   | 14   | 15   | 16   | 17   |
| 18                                                         | 19   | 20   | 21   | 22   | 23   | 24   |
| 25                                                         | 26   | 27   | 28   | 29   | 30   | 31   |
| 1                                                          | 2    | 3    | 4    | 5    | 6    | 7    |

### 公告

昵称： [nmap](https://home.cnblogs.com/u/nmap/)
园龄： [3年10个月](https://home.cnblogs.com/u/nmap/)
粉丝： [78](https://home.cnblogs.com/u/nmap/followers/)
关注： [5](https://home.cnblogs.com/u/nmap/followees/)

[+加关注](javascript:void(0))

### 搜索

 

 

### 常用链接

- [我的随笔](https://www.cnblogs.com/nmap/p/)
- [我的评论](https://www.cnblogs.com/nmap/MyComments.html)
- [我的参与](https://www.cnblogs.com/nmap/OtherPosts.html)
- [最新评论](https://www.cnblogs.com/nmap/RecentComments.html)
- [我的标签](https://www.cnblogs.com/nmap/tag/)

### 我的标签

- [openssh8.0p1(1)](https://www.cnblogs.com/nmap/tag/openssh8.0p1/)
- [openssh升级(1)](https://www.cnblogs.com/nmap/tag/openssh升级/)
- [ssh升级(1)](https://www.cnblogs.com/nmap/tag/ssh升级/)

### 随笔分类

- [2008R2(1)](https://www.cnblogs.com/nmap/category/955116.html)
- [apache(2)](https://www.cnblogs.com/nmap/category/957595.html)
- [cloudstack(4)](https://www.cnblogs.com/nmap/category/944095.html)
- [DNS(2)](https://www.cnblogs.com/nmap/category/1409255.html)
- [ESXI虚拟化(4)](https://www.cnblogs.com/nmap/category/921318.html)
- [GlusterFS(1)](https://www.cnblogs.com/nmap/category/946394.html)
- [KVM(4)](https://www.cnblogs.com/nmap/category/944094.html)
- [Linux实用命令(8)](https://www.cnblogs.com/nmap/category/921315.html)
- [Linux网络和路由(4)](https://www.cnblogs.com/nmap/category/927121.html)
- [Linux问题解决(9)](https://www.cnblogs.com/nmap/category/925697.html)
- [Mysql(21)](https://www.cnblogs.com/nmap/category/938388.html)
- [openstack(12)](https://www.cnblogs.com/nmap/category/944096.html)
- [Oracle(9)](https://www.cnblogs.com/nmap/category/921316.html)
- [Python(7)](https://www.cnblogs.com/nmap/category/1022483.html)
- [Python处理运营和开发的一些需求(10)](https://www.cnblogs.com/nmap/category/1245081.html)
- [SaltStack(13)](https://www.cnblogs.com/nmap/category/928393.html)
- [Tomcat(3)](https://www.cnblogs.com/nmap/category/953901.html)
- [USG华为防火墙(2)](https://www.cnblogs.com/nmap/category/921317.html)
- [Windows-2008R2(3)](https://www.cnblogs.com/nmap/category/921320.html)
- [Wireshark(1)](https://www.cnblogs.com/nmap/category/938380.html)

### 随笔档案

- [2019年7月(2)](https://www.cnblogs.com/nmap/archive/2019/07.html)
- [2019年4月(2)](https://www.cnblogs.com/nmap/archive/2019/04.html)
- [2019年3月(74)](https://www.cnblogs.com/nmap/archive/2019/03.html)
- [2019年2月(14)](https://www.cnblogs.com/nmap/archive/2019/02.html)
- [2017年6月(2)](https://www.cnblogs.com/nmap/archive/2017/06.html)
- [2017年5月(16)](https://www.cnblogs.com/nmap/archive/2017/05.html)
- [2017年4月(14)](https://www.cnblogs.com/nmap/archive/2017/04.html)
- [2017年2月(18)](https://www.cnblogs.com/nmap/archive/2017/02.html)
- [2017年1月(14)](https://www.cnblogs.com/nmap/archive/2017/01.html)
- [2016年12月(4)](https://www.cnblogs.com/nmap/archive/2016/12.html)

### 最新评论

- [1. Re:centos7 升级openssh到openssh-8.0p1版本](https://www.cnblogs.com/nmap/p/10779658.html)
- 为了解决 OpenSSH 命令注入漏洞(CVE-2020-15778) 的漏洞，我安装的是openssh-8.4p1.tar.gz和openssl-1.1.1h.tar.gz，当前的最新版本。其中默认...
- --深海浮冰
- [2. Re:（转）mysql创建表时反引号的作用](https://www.cnblogs.com/nmap/p/6714031.html)
- 知道了，mark
- --youthere
- [3. Re:Docker网络解决方案-Flannel（转）](https://www.cnblogs.com/nmap/p/9377811.html)
- 学习
- --NewSea
- [4. Re:python调用mediainfo工具批量提取视频信息](https://www.cnblogs.com/nmap/p/9336707.html)
- 执行exe报:"提取此文件信息失败"issue，能告诉一下怎么解决吗
- --唐唐的的的的
- [5. Re:nc命令用法举例](https://www.cnblogs.com/nmap/p/6148306.html)
- 博主，想问下，为什么我在本机测试无法通过 /dev/zero 发送数据进来网速测试呢?具体表现是 reveiver 没有接收到任何数据。
- --吕吕_Louis
- [6. Re:centos7 升级openssh到openssh-8.0p1版本](https://www.cnblogs.com/nmap/p/10779658.html)
- 我的环境： [root@1188181.cn /data/tools/openssl-1.1.1g]# cat /etc/redhat-release CentOS Linux release 7.7...
- --绿色心灵
- [7. Re:centos7 升级openssh到openssh-8.0p1版本](https://www.cnblogs.com/nmap/p/10779658.html)
- 楼主你太牛叉了，这个教程真的超精致，很棒！感谢，已打赏！
   能不能加个微信好友哈，我的微信搜索 84213955 可以添加。
   2020年7月24日07:02:43
- --绿色心灵
- [8. Re:nc命令用法举例](https://www.cnblogs.com/nmap/p/6148306.html)
- 好文章
- --zwd108867
- [9. Re:centos7 升级openssh到openssh-8.0p1版本](https://www.cnblogs.com/nmap/p/10779658.html)
- 感谢楼主分享，问题已解决！
- --辛辣天蝎
- [10. Re:centos7 升级openssh到openssh-8.0p1版本](https://www.cnblogs.com/nmap/p/10779658.html)
- @nmap 不使用系统原来使用的sshd.service，而改用/etc/init.d/sshd，是不是因为前者会无限重启的原因？...
- --euzen

### 阅读排行榜

- [1. nc命令用法举例(173312)](https://www.cnblogs.com/nmap/p/6148306.html)
- [2. Wireshark常用过滤使用方法(143967)](https://www.cnblogs.com/nmap/p/6291683.html)
- [3. nmap命令-----基础用法(123712)](https://www.cnblogs.com/nmap/p/6232207.html)
- [4. centos7 升级openssh到openssh-8.0p1版本(61568)](https://www.cnblogs.com/nmap/p/10779658.html)
- [5. nmap命令-----高级用法(60665)](https://www.cnblogs.com/nmap/p/6232969.html)

### 评论排行榜

- [1. centos7 升级openssh到openssh-8.0p1版本(26)](https://www.cnblogs.com/nmap/p/10779658.html)
- [2. nc命令用法举例(5)](https://www.cnblogs.com/nmap/p/6148306.html)
- [3. openstack--1--基础环境搭建(3)](https://www.cnblogs.com/nmap/p/6416017.html)
- [4. nmap命令-----基础用法(3)](https://www.cnblogs.com/nmap/p/6232207.html)
- [5. （转）mysql创建表时反引号的作用(2)](https://www.cnblogs.com/nmap/p/6714031.html)

### 推荐排行榜

- [1. nc命令用法举例(15)](https://www.cnblogs.com/nmap/p/6148306.html)
- [2. nmap命令-----基础用法(12)](https://www.cnblogs.com/nmap/p/6232207.html)
- [3. nmap命令-----高级用法(5)](https://www.cnblogs.com/nmap/p/6232969.html)
- [4. centos7 升级openssh到openssh-8.0p1版本(3)](https://www.cnblogs.com/nmap/p/10779658.html)
- [5. （转）mysql创建表时反引号的作用(3)](https://www.cnblogs.com/nmap/p/6714031.html)

Powered by:
[博客园](https://www.cnblogs.com/)
Copyright © 2020 nmap
Powered by .NET 5.0.0-rc.2.20475.5 on Kubernetes

<iframe id="blockbyte-bs-sidebar" class="notranslate" aria-hidden="true" __idm_frm__="138" data-pos="right" style="opacity: 0; pointer-events: none; position: fixed; top: 0px; left: auto; width: 350px; max-width: none; height: 0px; z-index: 2147483646; speak: none; border: none; transform: translate3d(350px, 0px, 0px); transition: width 0s ease 0.3s, height 0s ease 0.3s, opacity 0.3s ease 0s, transform 0.3s ease 0s; background-color: rgba(255, 255, 255, 0.8) !important; display: block !important; right: 0px; color: rgb(0, 0, 0); font-family: &quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-size: 14px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"></iframe>