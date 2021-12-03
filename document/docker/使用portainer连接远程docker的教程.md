更新时间：2020年03月05日 14:58:02  作者：BeiShangBuZaiLai  

Portainer是一个轻量级的docker环境管理UI，可以用来管理docker宿主机和docker swarm集群，这篇文章主要介绍了使用portainer连接远程docker的方法,需要的朋友可以参考下

Portainer是一个轻量级的docker环境管理UI，可以用来管理docker宿主机和docker swarm集群。他的轻量级，轻量到只要个不到100M的docker镜像容器就可以完整的提供服务

Portainer的Hub地址是：https://hub.docker.com/r/portainer/portainer/

运行命令是：

```
docker run -it --restart=always -d --name portainer-docker -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

**安装 portainer**

\> docker pull portainer/portainer

**启动 protainer**

\>docker run -d --name portainerUI -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer

**访问 protainer**

http://你安装protainer地址:9000

创建用户

![在这里插入图片描述](https://img.jbzj.com/file_images/article/202003/20200305150006103.png)

进入页面

![在这里插入图片描述](https://img.jbzj.com/file_images/article/202003/20200305150007104.png)

配置远程docker

选择左侧菜单栏Endpoints

![在这里插入图片描述](https://img.jbzj.com/file_images/article/202003/20200305150007105.jpg)

- Name你给docker起个名称
- Endpoint URL 远程docker地址 端口默认是2375
- 这个时候如果你的远程docker没有开启2375端口是链接不上的下面是配置docker端口方法

```
1. 编辑docker.service``vim /usr/lib/systemd/system/docker.service``找到 ExecStart字段修改如下``ExecStart=/usr/bin/dockerd-current -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock ` `2. 重启docker重新读取配置文件，重新启动docker服务``systemctl daemon-reload``systemctl restart docker` `3. 开放防火墙端口``firewall-cmd --zone=public --add-port=6379/tcp --permanent` `4.刷新防火墙``firewall-cmd --reload` `5.再次配置远程docker就可以了
```

**查看docker列表**

![在这里插入图片描述](https://img.jbzj.com/file_images/article/202003/20200305150008106.jpg) 

**总结**

到此这篇关于使用portainer连接远程docker的教程的文章就介绍到这了,更多相关portainer连接docker内容请搜索脚本之家以前的文章或继续浏览下面的相关文章希望大家以后多多支持脚本之家！

**您可能感兴趣的文章:**

- [docker可视化工具Portainer部署并汉化的操作](https://www.jb51.net/article/208245.htm)
- [kali安装docker和portainer的配置方法](https://www.jb51.net/article/215593.htm)
- [使用Portainer部署Docker容器的项目实践](https://www.jb51.net/article/209365.htm)
- [Docker使用Portainer搭建可视化界面的方法](https://www.jb51.net/article/199453.htm)
- [docker可视化图形工具portainer详解](https://www.jb51.net/article/226938.htm)



- [portainer](http://common.jb51.net/tag/portainer/1.htm)
- [docker](http://common.jb51.net/tag/docker/1.htm)

## 相关文章

- 

- [![解决Docker x509 insecure registry的问题](https://img.jbzj.com/images/xgimg/bcimg0.png)](https://www.jb51.net/article/208505.htm)

  [解决Docker x509 insecure registry的问题](https://www.jb51.net/article/208505.htm)

  这篇文章主要介绍了解决Docker x509 insecure registry的问题，具有很好的参考价值，希望对大家有所帮助。一起跟随小编过来看看吧

  2021-03-03

- [![docker安装kong网关的方法示例](https://img.jbzj.com/images/xgimg/bcimg1.png)](https://www.jb51.net/article/161408.htm)

  [docker安装kong网关的方法示例](https://www.jb51.net/article/161408.htm)

  这篇文章主要介绍了docker安装kong网关的方法示例，小编觉得挺不错的，现在分享给大家，也给大家做个参考。一起跟随小编过来看看吧

  2019-05-05

- [![docker 使用CMD或者ENTRYPOINT命令同时启动多个服务](https://img.jbzj.com/images/xgimg/bcimg2.png)](https://www.jb51.net/article/200252.htm)

  [docker 使用CMD或者ENTRYPOINT命令同时启动多个服务](https://www.jb51.net/article/200252.htm)

  这篇文章主要介绍了docker 使用CMD或者ENTRYPOINT命令同时启动多个服务，具有很好的参考价值，希望对大家有所帮助。一起跟随小编过来看看吧

  2020-11-11

- [![基于docker的caffe环境搭建方法](https://img.jbzj.com/images/xgimg/bcimg3.png)](https://www.jb51.net/article/141370.htm)

  [基于docker的caffe环境搭建方法](https://www.jb51.net/article/141370.htm)

  这篇文章主要介绍了基于docker的caffe环境搭建方法，小编觉得挺不错的，现在分享给大家，也给大家做个参考。一起跟随小编过来看看吧

  2018-06-06

- [![如何给Docker配置官方国内加速镜像](https://img.jbzj.com/images/xgimg/bcimg4.png)](https://www.jb51.net/article/116873.htm)

  [如何给Docker配置官方国内加速镜像](https://www.jb51.net/article/116873.htm)

  在国内访问 Docker 官方的镜像，一直以来速度都慢如蜗牛。为了快速访问 Docker 官方镜像都会配置三方加速器

  2017-06-06

- [![Docker私有仓库Registry部署的实现](https://img.jbzj.com/images/xgimg/bcimg5.png)](https://www.jb51.net/article/187864.htm)

  [Docker私有仓库Registry部署的实现](https://www.jb51.net/article/187864.htm)

  这篇文章主要介绍了Docker私有仓库Registry部署的实现，私有仓库最常用的就是Registry、Harbor两种，本文详细介绍如何搭建registry私有仓库，感兴趣的可以了解一下

  2020-06-06

- [![docker 如何添加证书](https://img.jbzj.com/images/xgimg/bcimg6.png)](https://www.jb51.net/article/208495.htm)

  [docker 如何添加证书](https://www.jb51.net/article/208495.htm)

  这篇文章主要介绍了docker 如何添加证书的操作方式，具有很好的参考价值，希望对大家有所帮助。一起跟随小编过来看看吧

  2021-03-03

- [![docker 详解设置容器防火墙](https://img.jbzj.com/images/xgimg/bcimg7.png)](https://www.jb51.net/article/103517.htm)

  [docker 详解设置容器防火墙](https://www.jb51.net/article/103517.htm)

  这篇文章主要介绍了docker 详解设置容器防火墙的相关资料,需要的朋友可以参考下

  2017-01-01

- [![Docker 教程之数据管理详细介绍](https://img.jbzj.com/images/xgimg/bcimg8.png)](https://www.jb51.net/article/104049.htm)

  [Docker 教程之数据管理详细介绍](https://www.jb51.net/article/104049.htm)

  这篇文章主要介绍了Docker 教程之数据管理详细介绍的相关资料,需要的朋友可以参考下

  2017-01-01

- [![Docker安装ClickHouse并初始化数据测试](https://img.jbzj.com/images/xgimg/bcimg9.png)](https://www.jb51.net/article/216008.htm)

  [Docker安装ClickHouse并初始化数据测试](https://www.jb51.net/article/216008.htm)

  clickhouse作为现在流行的数据分析数据库，非常热门，docker如何安装ClickHouse，很多朋友并不是很明白，今天小编抽空给大家分享一篇教程关于Docker安装ClickHouse并初始化数据测试的问题，一起看看吧

  2021-06-06



## 最新评论



# 其他主机开启远程连接docker端口

需要设置一下2375端口的监听。通过修改docker配置文件方式进行监听。
修改配置文件修改监听端口
使用Centos7安装的docker，所以下面的配置是适用于Centos7的。打开配置文件`/usr/lib/systemd/system/docker.service`
或者通过`systemctl status docker.service`命令查看docker.service文件所在路径
![img](https://img2020.cnblogs.com/blog/794174/202006/794174-20200623163859529-494724057.png)

修改配置项ExecStart中的值，若ExecStart中没有值，则直接添加`-H tcp://0.0.0.0:2375`，否则在已有参数后面添加，比如下面这样：

```
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H fd:// --containerd=/run/containerd/containerd.sock
```

修改完之后保存文件，然后重启docker服务

```
systemctl daemon-reload
systemctl restart docker
```

> 注意：需要对所有的docker节点都进行上面的修改配置文件的操作。

# 在Portainer上添加其他主机上的docker

![img](https://img2020.cnblogs.com/blog/794174/202006/794174-20200623164558531-454223980.png)
![img](https://img2020.cnblogs.com/blog/794174/202006/794174-20200623164700667-410329597.png)

分类: [Docker](https://www.cnblogs.com/sanduzxcvbnm/category/1531519.html), [Portainer](https://www.cnblogs.com/sanduzxcvbnm/category/1792335.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/794174/20161001123043.png)](https://home.cnblogs.com/u/sanduzxcvbnm/)

[三度](https://home.cnblogs.com/u/sanduzxcvbnm/)
[关注 - 0](https://home.cnblogs.com/u/sanduzxcvbnm/followees/)
[粉丝 - 35](https://home.cnblogs.com/u/sanduzxcvbnm/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/sanduzxcvbnm/p/13182007.html)上一篇： [Portainer实用教程](https://www.cnblogs.com/sanduzxcvbnm/p/13182007.html)
[» ](https://www.cnblogs.com/sanduzxcvbnm/p/13186014.html)下一篇： [Docker Compose](https://www.cnblogs.com/sanduzxcvbnm/p/13186014.html)

posted @ 2020-06-23 16:47 [三度](https://www.cnblogs.com/sanduzxcvbnm/) 阅读(1031) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=13182948) [收藏](javascript:void(0)) [举报](javascript:void(0))





[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/sanduzxcvbnm/p/13182948.html#)[返回顶部](https://www.cnblogs.com/sanduzxcvbnm/p/13182948.html#top)

登录后才能查看或发表评论，立即 [登录](javascript:void(0);) 或者 [逛逛](https://www.cnblogs.com/) 博客园首页

**编辑推荐：**
· [Three.js 实现脸书元宇宙 3D 动态 Logo](https://www.cnblogs.com/dragonir/p/15574412.html)
· [关于研发规范化的一些实践和思考](https://www.cnblogs.com/wangjiming/p/15572643.html)
· [2次心态变化和27个问题：机制落地的部分全貌与节奏控制](https://www.cnblogs.com/yexiaochai/p/15564407.html)
· [CPU 被挖矿，Redis 竟是内鬼！](https://www.cnblogs.com/xuanyuan/p/15564302.html)
· [巧用滤镜实现高级感拉满的文字快闪切换效果](https://www.cnblogs.com/coco1s/p/15559744.html)

**最新新闻**：

# Portainer添加Endpoints节点，管理远程Docker主机

[![img](https://upload.jianshu.io/users/upload_avatars/22249315/bdb15df7-d033-419a-aafa-c7e4d9687cf7?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/a3aa9e546732)

[沉思的雨季](https://www.jianshu.com/u/a3aa9e546732)关注

2020.06.08 16:58:22字数 302阅读 1,457

# 一、配置Docker主机防火墙，允许远程访问

1、查看防火墙状态，若关闭则跳过配置，否则继续防火墙设置
firewall-cmd--state
2、查看防火墙已开放端口，若有2375则跳过配置，否则继续防火墙设置
firewall-cmd --permanent --zone=public --list-ports
3、添加2375端口到防火墙允许开放端口
firewall-cmd--zone=public--add-port=2375/tcp--permanent
4、重新加载防火墙配置
firewall-cmd--reload
5、查看2375端口是否添加成功
firewall-cmd --permanent --zone=public --list-ports

# 二、配置Docker主机，允许远程连接

1、修改Docker主机daemon.json文件
*代码如下：*



```csharp
[root@localhost ~]# vi /etc/docker/daemon.json 
{
   "insecure-registries":["11.1.14.145:8080"],
   "hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"]
}
```

**注："insecure-registries":["11.1.14.145:8080"]为私用仓库配置，若无私有仓库删掉该行。**
2、重启docker引擎，使配置生效



```csharp
[root@localhost ~]# systemctl daemon-reload         
[root@localhost ~]# systemctl restart docker.service
```

# 三、登录Portainer页面，添加Endpoints节点

1、访问[http://IP:9000](https://links.jianshu.com/go?to=http%3A%2F%2FIP%3A9000)页面，点击右侧树Endpoints，打开Endpoints管理页面。

![img](https://upload-images.jianshu.io/upload_images/22249315-35702da5726e1f7f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)


2、点击页面“Add endpoint”按钮，打开Endpoints节点编辑页面。

![img](https://upload-images.jianshu.io/upload_images/22249315-f01e168d83b67096.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)


3、保存成功后，可进行新增节点docker的管理。





0人点赞



[devops专题](https://www.jianshu.com/nb/44191585)



更多精彩内容，就在简书APP