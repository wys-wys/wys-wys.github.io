# xshell出现WARNING!The remote SSH server rejected X11 forwarding request.

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[WuGenQiang](https://wugenqiang.blog.csdn.net/) 2019-01-19 18:05:33 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 37314 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 51

分类专栏： [centos](https://blog.csdn.net/wugenqiang/category_8616591.html) [Linux](https://blog.csdn.net/wugenqiang/category_7793034.html)

版权

使用xshell第一次连接时，可能会连接多次才能连上，出现：WARNING!The remote SSH server rejected X11 forwarding request.

![img](https://img-blog.csdnimg.cn/2019011917340029.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1Z2VucWlhbmc=,size_16,color_FFFFFF,t_70)

解决方法：

vi /etc/ssh/sshd_config  在X11这行改为X11Forwarding yes,
然后再将UseLogin参数为no，可能这一行最开始是被注释，去掉注释，保存之后重启sshd服务，重新连接即可

![img](https://img-blog.csdnimg.cn/20190119173808741.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1Z2VucWlhbmc=,size_16,color_FFFFFF,t_70)

重启ssh服务

```
[root@wugenqiang ~]# systemctl restart sshd
```

如果还不行检查 xorg-x11-xauth 的rpm包是否安装，未安装则进行下面操作

```
[root@wugenqiang ~]# yum install xorg-x11-xauth
```

![img](https://img-blog.csdnimg.cn/20190119180309267.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1Z2VucWlhbmc=,size_16,color_FFFFFF,t_70)

测试重新连接：

![img](https://img-blog.csdnimg.cn/20190119180432745.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1Z2VucWlhbmc=,size_16,color_FFFFFF,t_70)

successful！！



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞27
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论19](https://blog.csdn.net/wugenqiang/article/details/86554753#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏51](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReward.png)打赏
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[解决 *Xshell* 连接*出现* *The* *remote* *SSH* *server* *rejected* *X11* *forwarding* *request* 问题](https://blog.csdn.net/awadg10570/article/details/101630261)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 1669

[问题描述 使用 *Xshell* 5 首次连接虚拟机 CentOS 7*.*6 *出现*这样的提示： *WARNING**!* *The* *remote* *SSH* *server* *rejected* *X11* *forwarding* *request**.* 经搜索得知原来是*.**.**.* 此处省略一大段原理。 解决方法 yum install xorg -*x11* -xauth -y 安装完成后再次登录，问题解决。但是，却出*.**.**.*](https://blog.csdn.net/awadg10570/article/details/101630261)





[![img](https://profile.csdnimg.cn/0/5/1/3_weixin_45710390)](https://blog.csdn.net/weixin_45710390)

![表情包](https://csdnimg.cn/release/blogv2/dist/pc/img/emoticon.png)



- [![ljh101](https://profile.csdnimg.cn/D/6/A/3_ljh101)](https://blog.csdn.net/ljh101)

  [码农![码农](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[代码当酒喝](https://blog.csdn.net/ljh101)**:**腾讯云链接上后过一会儿就自动断开怎么解决啊？博主2 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![kshxbx](https://profile.csdnimg.cn/3/5/9/3_kshxbx)](https://blog.csdn.net/kshxbx)

  [kshxbx](https://blog.csdn.net/kshxbx)**:**搞定了，谢谢楼主大佬5 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![qq_47590278](https://profile.csdnimg.cn/6/7/A/3_qq_47590278)](https://blog.csdn.net/qq_47590278)

  [小白学加瓦](https://blog.csdn.net/qq_47590278)**:**原来X11 forwarding依赖xorg-x11-xauth软件包，所以必须先安装xorg-x11-xauth软件包。5 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![weixin_41220603](https://profile.csdnimg.cn/9/5/9/3_weixin_41220603)](https://blog.csdn.net/weixin_41220603)

  [weixin_41220603](https://blog.csdn.net/weixin_41220603)**:**太棒了，完美解决，谢谢楼主！7 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![JueChenYi](https://profile.csdnimg.cn/4/8/5/3_juechenyi)](https://blog.csdn.net/JueChenYi)

  [派大星爱摸鱼](https://blog.csdn.net/JueChenYi)**:**感谢，成功解决问题9 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![Jelly_oy](https://profile.csdnimg.cn/B/A/F/3_jelly_oy)](https://blog.csdn.net/Jelly_oy)

  [无尽光芒oy](https://blog.csdn.net/Jelly_oy)**:**厉害厉害，问题已解决，感谢感谢9 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![weixin_43600461](https://profile.csdnimg.cn/5/9/5/3_weixin_43600461)](https://blog.csdn.net/weixin_43600461)

  [你让我叫啥我就叫啥吧](https://blog.csdn.net/weixin_43600461)**:**问题已解决 谢谢 有用呀1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![qq_35174943](https://profile.csdnimg.cn/4/5/1/3_qq_35174943)](https://blog.csdn.net/qq_35174943)

  [橙子橙子你在哪里](https://blog.csdn.net/qq_35174943)**:**Lunix小白提问，按照说明命令行输入vi /etc/ssh/sshd_config，按i进入编辑模式，在X11这行改为X11Forwarding yes,然后再将UseLogin参数为no去掉注释，然后Esc返回一般模式，然后按:wq保存，一直保存不成功是什么原因呢？1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- - [![dandycheung](https://profile.csdnimg.cn/F/D/0/3_dandycheung)](https://blog.csdn.net/dandycheung)

    [dandycheung](https://blog.csdn.net/dandycheung)回复**:**应该是你没有权限，sudo 操作试试。1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![qq_41433833](https://profile.csdnimg.cn/B/6/A/3_qq_41433833)](https://blog.csdn.net/qq_41433833)

  [码哥![码哥](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[Kai Havterz](https://blog.csdn.net/qq_41433833)**:**能说一下原因吗1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- - [![wugenqiang](https://profile.csdnimg.cn/6/F/5/3_wugenqiang)](https://blog.csdn.net/wugenqiang)

    [WuGenQiang![img](https://csdnimg.cn/release/blogv2/dist/components/img/bloger@2x.png)](https://blog.csdn.net/wugenqiang)回复**:**应该是权限问题导致的吧，这个方法也是我好久之前在csdn看到的，大佬解决的1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![chenbeiping888](https://profile.csdnimg.cn/3/A/9/3_chenbeiping888)](https://blog.csdn.net/chenbeiping888)

  [jasonchen666](https://blog.csdn.net/chenbeiping888)**:**博主，每次装系统都出现此问题是什么原因呢2 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- - [![wugenqiang](https://profile.csdnimg.cn/6/F/5/3_wugenqiang)](https://blog.csdn.net/wugenqiang)

    [WuGenQiang![img](https://csdnimg.cn/release/blogv2/dist/components/img/bloger@2x.png)](https://blog.csdn.net/wugenqiang)回复**:**正常吧，几乎都会遇到，应该是权限问题导致的吧1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

![The remote SSH server rejected X11 forwarding警告](https://pic4.zhimg.com/v2-e63ad03f54b260311e53e81ad721f418_1440w.jpg?source=172ae18b)

# The remote SSH server rejected X11 forwarding警告

[![gaofengge](https://pic1.zhimg.com/v2-601e12d2fce15303a837bdc3a7a4f79c_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/gafengge)

[gaofengge](https://www.zhihu.com/people/gafengge)

高校计算机专业教师

4 人赞同了该文章

最近使用XShell连接Linux操作系统总出现：“WARNING! The remote SSH server rejected X11 forwarding request.”警告。

![img](https://pic1.zhimg.com/v2-e63ad03f54b260311e53e81ad721f418_r.jpg)

解决办法如下：

1.右击会话选择”属性“菜单。

![img](https://pic4.zhimg.com/v2-c2a58deb891389313f53b9368c298bdb_r.jpg)

2.点击“隧道”取消“转发X11连接”到（X)。

![img](https://pic2.zhimg.com/v2-5022efa44005dd0b8455172d652d77e9_r.jpg)

3.点击“确定”，双击会话重新连接。

![img](https://pic3.zhimg.com/v2-bed01332959f5676063f442a905c445a_r.jpg)



发布于 2020-03-12

[SSH Server](https://www.zhihu.com/topic/20050963)

[Windows Server](https://www.zhihu.com/topic/20011837)

[SSH(Secure Shell)](https://www.zhihu.com/topic/19557973)

赞同 4

6 条评论

分享

喜欢收藏申请转载



### 文章被以下专栏收录

- [![高老师聊IT](https://pic1.zhimg.com/4b70deef7_xs.jpg?source=172ae18b)](https://www.zhihu.com/column/gaofengge)

- ## [高老师聊IT](https://www.zhihu.com/column/gaofengge)

- 计算机技术实战

### 推荐阅读

- ![SSh连接失败，Socket error Event: 32 Error: 10053.](https://pic4.zhimg.com/v2-3ecb8e48e42da40d8fccb2b80e28b1e4_250x0.jpg?source=172ae18b)

- # SSh连接失败，Socket error Event: 32 Error: 10053.

- CPING

- # Telnet、SSH和VNC 三种协议的比较

- 前言：我们经常听见各种各样的协议，什么ssh,vnc,rdp,telnet等等，他们似乎都实现着类似的功能，有时候傻傻分不清楚，其实她们基本上都是近亲，本文着重讨论一下这三者之间的关系，可以参考…

- 沈鹏燕

- # 电脑通过SSH连接Termux

- 本文转载自 https://glow.li/technology/2015/11/06/run-an-ssh-server-on-your-android-with-termux/转载纯粹为了备份。 With the brilliant Termux terminal emulator app you can run an…

- 司徒旭明

- # Linux远程管理协议（RFB、RDP、Telnet和SSH）

- 提到远程管理，通常指的是远程管理服务器，而非个人计算机。个人计算机可以随时拿来用，服务器通常放置在机房中，用户无法直接接触到服务器硬件，只能采用远程管理的方式。 远程管理，实际…

- 不朽的传奇

## 6 条评论

切换为时间排序

写下你的评论...







发布

- [![cloud erow](https://pic1.zhimg.com/da8e974dc_s.jpg?source=06d4cd63)](https://www.zhihu.com/people/cloud-erow)[cloud erow](https://www.zhihu.com/people/cloud-erow)2020-09-02

  掩耳盗铃式解决问题

  7回复踩 举报

- [![暗香浮动月黄昏](https://pic2.zhimg.com/v2-5002cf396d8bd7a4806028d55243cb38_s.jpg?source=06d4cd63)](https://www.zhihu.com/people/an-xiang-fu-dong-yue-huang-hun-16-16)[暗香浮动月黄昏](https://www.zhihu.com/people/an-xiang-fu-dong-yue-huang-hun-16-16)回复[cloud erow](https://www.zhihu.com/people/cloud-erow)2020-09-22

  哈哈哈，说的太对了

  赞回复踩 举报

- ![知乎用户](https://pic1.zhimg.com/da8e974dc_s.jpg?source=06d4cd63)知乎用户回复[cloud erow](https://www.zhihu.com/people/cloud-erow)02-24

  可能是因为没有安装 xmanager 又启用了转发，才打印出失败的警告消息，所以不是服务器拒绝了，而它准备建立一个转发的隧道时不成功。

  赞回复踩 举报

- 展开其他 1 条回复

- [![陌路流年](https://pic1.zhimg.com/v2-151c923933f8b42b5b8687a8bd9b41a2_s.jpg?source=06d4cd63)](https://www.zhihu.com/people/mo-lu-liu-nian-4)[陌路流年](https://www.zhihu.com/people/mo-lu-liu-nian-4)02-19

  服了，我就是要用这个

  赞回复踩 举报

- [![学生奶粉罐](https://pic1.zhimg.com/v2-7d6453ddff6421b8cdb5eea11e8bf8d2_s.jpg?source=06d4cd63)](https://www.zhihu.com/people/xue-sheng-nai-fen-guan)[学生奶粉罐](https://www.zhihu.com/people/xue-sheng-nai-fen-guan)2020-12-18

  可以的，只少我看不到了