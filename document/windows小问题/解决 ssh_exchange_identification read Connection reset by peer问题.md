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