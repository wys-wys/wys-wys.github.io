## 一.Docker图形化工具

​    docker 图形页面管理工具常用的有三种，DockerUI ，Portainer ，Shipyard 。DockerUI 是 Portainer 的前身，这三个工具通过docker api来获取管理的资源信息。平时我们常常对着shell对着这些命令行客户端，审美会很疲劳，如果有漂亮的图形化界面可以直观查看docker资源信息，也是非常方便的。今天我们就搭建单机版的三种常用图形页面管理工具。这三种图形化管理工具以Portainer最为受欢迎。

## 二.DockerUI

轻量级图形页面管理之DockerUI

1.查看dockerui镜像

```
[root@localhost ~]# docker search dockerui
```

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921161812839-1161447728.png)

2.选择喜欢的dockerui风格镜像，下载

```
[root@localhost ~]# docker pull abh1nav/dockerui
```

3.启动dockerui容器，这里需要注意带上privileged参数，提升权限

```
[root@localhost ~]# docker run -d --privileged --name dockerui -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock abh1nav/dockerui
```

前往网页查看之前，你需要打开服务器的9000端口：   firewall-cmd --permanent --zone=public --add-port=9000/tcpfirewall-cmd --reload

4.浏览器查看dockerui：[http://192.168.2.119:9000](http://192.168.2.119:9000/)   或者 curl http://192.168.2.119:9000

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921160841743-448633112.png)

## 三.Shipyard

轻量级图形页面管理之Shipyard

## ![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921163444930-1449197767.png)

## 四.Portainer

轻量级图形页面管理之Portainer

1.查看portainer镜像

```
[root@localhost ~]# docker search portainer
```

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921161723460-1361137261.png)

2.选择喜欢的portainer风格镜像，下载

```
[root@localhost ~]# docker pull portainer/portainer 
```

3.启动dockerui容器

```
[root@localhost ~]# docker run -d --name portainerUI -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

4.浏览器访问 [http://192.168.2.119:9000](http://192.168.2.119:9000/) , 设置一个密码即可，点击创建用户

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921162528714-901461854.png)

![img](https://f12.baidu.com/it/u=1997667158,3125340408&fm=173&app=25&f=JPEG?w=597&h=377&s=48AE3C72037F402B1875C4DA000050B2&access=215967316)

我们搭建的是单机版，直接选择Local ，点击连接

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921162717769-145855775.png)

![img](https://f11.baidu.com/it/u=1266655624,1442914627&fm=173&app=25&f=JPEG?w=597&h=431&s=2172C432072E470DD04160D60300C0B0&access=215967316)

现在就可以使用了，点击Local进入仪表盘主页面。

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921165040584-1231389831.png)

容器页面

![img](https://img2018.cnblogs.com/blog/1385722/201809/1385722-20180921164941854-544053238.png)

 

![img](https://f12.baidu.com/it/u=1156235942,926832626&fm=173&app=25&f=JPEG?w=640&h=233&s=09B1EC101726652240DD98CB020080B4&access=215967316)

![img](https://f12.baidu.com/it/u=3237575840,3806081523&fm=173&app=25&f=JPEG?w=640&h=221&s=1112EC320E0AC5285C7DB4DA000010B2&access=215967316)

分类: [系统运维](https://www.cnblogs.com/frankdeng/category/1206141.html)

标签: [Docker](https://www.cnblogs.com/frankdeng/tag/Docker/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1385722/20180509232100.png)](https://home.cnblogs.com/u/frankdeng/)

[Frankdeng](https://home.cnblogs.com/u/frankdeng/)
[关注 - 42](https://home.cnblogs.com/u/frankdeng/followees/)
[粉丝 - 422](https://home.cnblogs.com/u/frankdeng/followers/)

[+加关注](javascript:void(0);)

1

0

[« ](https://www.cnblogs.com/frankdeng/p/9275092.html)上一篇： [Docker 简介与shell操作使用](https://www.cnblogs.com/frankdeng/p/9275092.html)
[» ](https://www.cnblogs.com/frankdeng/p/9572017.html)下一篇： [Storm（三）Storm的原理机制](https://www.cnblogs.com/frankdeng/p/9572017.html)

posted @ 2018-09-21 16:52 [Frankdeng](https://www.cnblogs.com/frankdeng/) 阅读(40130) 评论(1) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=9686735) [收藏](javascript:void(0)) [举报](javascript:void(0))