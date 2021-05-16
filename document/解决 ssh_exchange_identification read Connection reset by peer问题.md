# 解决 ssh_exchange_identification: read: Connection reset by peer问题

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[奋斗吧，青年！](https://blog.csdn.net/lilygg) 2019-01-09 23:09:54 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 138958 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 36

版权

**ssh连接主机时，出现如下报错如何解决？**

在客户端连接服务端：

```
[root@foundation66 ~]# ssh root@172.25.254.166
ssh_exchange_identification: read: Connection reset by peer
12
## -v表示查看连接详细信息
[root@foundation66 ~]# ssh -v root@172.25.254.166
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190109225908178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlnZw==,size_16,color_FFFFFF,t_70)
解决方案：在服务端更改配置文件

```
[root@localhost Desktop]# vi /etc/hosts.allow
#########################
sshd: ALL    ##允许所有ip主机均能连接本机
123
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190109230004830.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpbHlnZw==,size_16,color_FFFFFF,t_70)

```
[root@localhost Desktop]# systemctl restart sshd
1
```

测试：

```
[root@foundation66 ~]# ssh root@172.25.254.166
Last login: Wed Jan  9 22:51:17 2019 from 172.25.254.66
12
```



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞9
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论8](https://blog.csdn.net/lilygg/article/details/86187028#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏36](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReward.png)打赏
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[suse ssh连接拒绝，报错 *ssh_exchange_identification*: *read*: *Connection* *reset* by *peer*](https://blog.csdn.net/liuleinevermore/article/details/83617868)

[liuleinevermore的博客](https://blog.csdn.net/liuleinevermore)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 1万+

[  操作报错现象，ssh远程服务器，提示*ssh_exchange_identification*: *read*: *Connection* *reset* by *peer* ，但是能够ping的通  执行ssh -v user@ip 查看细节详情。（盗网上一张图）  网上有种*解决*思路，说是频繁连接远程服务器，导致服务器将自己的ip加入到 /etc/hosts.deny中，可以进入服务器的控制中...](https://blog.csdn.net/liuleinevermore/article/details/83617868)





[![img](https://profile.csdnimg.cn/0/5/1/3_weixin_45710390)](https://blog.csdn.net/weixin_45710390)

![表情包](https://csdnimg.cn/release/blogv2/dist/pc/img/emoticon.png)



- [![u010571211](https://profile.csdnimg.cn/C/0/0/3_u010571211)](https://blog.csdn.net/u010571211)

  [朴瑞祥](https://blog.csdn.net/u010571211)**:**怎么登录到服务端呢？1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)3

- - [![lishenluo](https://profile.csdnimg.cn/5/3/C/3_lishenluo)](https://blog.csdn.net/lishenluo)

    [Sen-Lee](https://blog.csdn.net/lishenluo)回复**:**阿里云的话可以通过web阿里云控制台1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

  - [![Hanoi_ahoj](https://profile.csdnimg.cn/8/5/D/3_hanoi_ahoj)](https://blog.csdn.net/Hanoi_ahoj)

    [ahojcn](https://blog.csdn.net/Hanoi_ahoj)回复**:**这是一个好问题1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)1

- [![weixin_40647946](https://profile.csdnimg.cn/9/C/F/3_weixin_40647946)](https://blog.csdn.net/weixin_40647946)

  [饭饭饭饭饭～](https://blog.csdn.net/weixin_40647946)**:**我的机子账户全部报这个消息；已经登录不上了；内部服务器，无阿里云类似的控制台；请问大佬有招吗？4 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)1

- [![weixin_44023015](https://profile.csdnimg.cn/E/F/5/3_weixin_44023015)](https://blog.csdn.net/weixin_44023015)

  [码哥![码哥](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[weixin_44023015](https://blog.csdn.net/weixin_44023015)**:**改完重启一下 service sshd restart 就好了昨天回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![yujiannxl](https://profile.csdnimg.cn/8/6/4/3_yujiannxl)](https://blog.csdn.net/yujiannxl)

  [yujiannxl](https://blog.csdn.net/yujiannxl)**:**我改了还是老样子3 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![lizhenlzlz](https://profile.csdnimg.cn/7/7/6/3_lizhenlzlz)](https://blog.csdn.net/lizhenlzlz)

  [码皇![码皇](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[lizhenlzlz](https://blog.csdn.net/lizhenlzlz)**:**对我有用3 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![weixin_43557605](https://profile.csdnimg.cn/B/B/4/3_weixin_43557605)](https://blog.csdn.net/weixin_43557605)

  [码农![码农](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[Sunlit_g](https://blog.csdn.net/weixin_43557605)**:**谢谢 解决了我的问题4 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

# [ssh连接失败，排错经验](https://www.cnblogs.com/starof/p/4709805.html)

# 一、场景描述

ssh连接服务器，发现连接失败，但是对应服务器的ip能够ping通。

场景：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@yl-web ~]# ssh root@10.1.101.35
ssh_exchange_identification: read: Connection reset by peer
[root@yl-web ~]# ping 10.1.101.35
PING 10.1.101.35 (10.1.101.35) 56(84) bytes of data.
64 bytes from 10.1.101.35: icmp_seq=1 ttl=64 time=0.587 ms
64 bytes from 10.1.101.35: icmp_seq=2 ttl=64 time=0.722 ms
64 bytes from 10.1.101.35: icmp_seq=3 ttl=64 time=0.475 ms
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

ping是一个网络层的协议，只是表面网络在3层是通的；

ssh是应用层协议，具体还是从主机上找原因。

# 二、排错

## 1、ssh -v

用ssh -v去连有问题的服务器，会有比较详细的调试信息在屏幕上输出，可以帮助判断是哪一步出了问题。

主要是看是客户端还是服务器的问题。如果是客户端的问题，应该log中有写。如果是没有什么有用信息，就可能是服务器端出问题了。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@yl-web ~]# ssh -v root@10.1.101.35
OpenSSH_6.6.1, OpenSSL 1.0.1e-fips 11 Feb 2013
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 56: Applying options for *
debug1: Connecting to 10.1.101.35 [10.1.101.35] port 22.
debug1: Connection established.
debug1: permanently_set_uid: 0/0
debug1: identity file /root/.ssh/id_rsa type -1
debug1: identity file /root/.ssh/id_rsa-cert type -1
debug1: identity file /root/.ssh/id_dsa type -1
debug1: identity file /root/.ssh/id_dsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa type -1
debug1: identity file /root/.ssh/id_ecdsa-cert type -1
debug1: identity file /root/.ssh/id_ed25519 type -1
debug1: identity file /root/.ssh/id_ed25519-cert type -1
debug1: Enabling compatibility mode for protocol 2.0
debug1: Local version string SSH-2.0-OpenSSH_6.6.1
ssh_exchange_identification: read: Connection reset by peer
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 2、连接服务器

现在看起来是服务器出问题了，虽然不能ssh到服务器，但一般来说主机会提供一些方法比去让你连接，比如通过物理终端连进去，具体情况具体对待了，总之就是要连接到服务器上。

## 3、写一个排错弯路，但也是有用的

如果有`debug1: Connection refused by tcp wrapper`之类的log可参考这一步。

就是说你的客户端ip可能被服务器给禁掉了，fail2ban或者其他的程序可能把你的客户端ip扔到/etc/hosts.deny中了。

通过vi /etc/hosts.allow查看

![img](https://images0.cnblogs.com/blog2015/315302/201508/070934386278524.png)

加上一行sshd: ALL。

然后重启ssh。

```
#service sshd restart
```

如果问题真的出在ip被禁，这样重启之后应该就ok了。

客户端重新ssh试一下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@yl-web ~]# ssh -v root@10.1.101.35
OpenSSH_6.6.1, OpenSSL 1.0.1e-fips 11 Feb 2013
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 56: Applying options for *
debug1: Connecting to 10.1.101.35 [10.1.101.35] port 22.
debug1: connect to address 10.1.101.35 port 22: Connection refused
ssh: connect to host 10.1.101.35 port 22: Connection refused
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

说明我的问题不在这里。

## 4、两条有用的命令

在服务器上执行下面命令可以显示ssh的所有 log。

centos系统如下：

```
#service sshd stop
#/usr/sbin/sshd -d
```

如果是ubuntu可能命令是：`sudo service ssh stop` ，`sudo /usr/sbin/sshd -d`。

![img](https://images0.cnblogs.com/blog2015/315302/201508/070946167055091.png)

问题出现了： /var/empty/sshd must be owned by root and not group or world-writable。

是权限的问题了，查看一下。

![img](https://images0.cnblogs.com/blog2015/315302/201508/071026305496982.png)

我的权限变成777了，而sshd这个目录

正常情况该目录的权限应该是：

```
[root@yl-web ~]# ll /var/empty/
total 0
drwx--x--x. 2 root root 6 May 13 03:41 sshd
```

 修改权限：

![img](https://images0.cnblogs.com/blog2015/315302/201508/071037092057535.png)

改好权限后重启sshd服务【service sshd restart】。客户端再ssh就ok，大功告成了。

## 5、命令简介

至此问题已解决，但是/usr/sbin/sshd -d又是什么意思呢？

\# man sshd看一下这两个参数。

```
     -D      When this option is specified, sshd will not detach and does not become a daemon.  This allows easy monitoring of sshd.

     -d      Debug mode.  The server sends verbose debug output to standard error, and does not put itself in the background.  The server also will not fork and will only process one connection.  This
             option is only intended for debugging for the server.  Multiple -d options increase the debugging level.  Maximum is 3.
```

 -d是debug模式，服务器会向屏幕输出详细的debug信息，服务器只能有一个ssh链接。

## 三、题外话

虽然问题解决了，回想一下为什么会出这个问题？因为我昨天在解决一个日志权限的问题时，暴力的将每层目录权限都设置成777，想试探一下是否是目录读写权限的问题，然后再缩小权限，结果影响到了ssh登录。

想想解决一个问题若不能知道原理，很容易放大问题，甚至出现新bug。写代码需谨慎，排错需谨慎，知其然不知其所以然很重要。

参考：

[Connection Reset By Peer](http://jonkuperman.com/connection-reset-by-peer/)

 

本文作者[starof](http://www.cnblogs.com/starof/),因知识本身在变化，作者也在不断学习成长，文章内容也不定时更新，为避免误导读者，方便追根溯源，请诸位转载注明出处：http://www.cnblogs.com/starof/p/4709805.html有问题欢迎与我讨论，共同进步。

**如果觉得本文对您有帮助~可以微信支持一下：**