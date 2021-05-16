a

Docker搭建Minecraft服务器

willblog 2018-12-10 19:42:17  9441  收藏 15
分类专栏： games 文章标签： games docker
版权
minecraft
本篇文章介绍使用docker容器方式在linux操作系统上搭建最新版本minecraft服务器，并使用bungeecord配置为群组服务器模式。
常规方式搭建minecraft服务器参考这篇文章：
https://blog.csdn.net/networken/article/details/84477537

YINWU正版公益服务器地址:server.yinwurealm.org
YINWU服务器官网:https://www.yinwurealm.org/Docker搭建Minecraft服务器

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[willblog](https://blog.csdn.net/networken) 2018-12-10 19:42:17 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10035 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 15

分类专栏： [games](https://blog.csdn.net/networken/category_8938458.html) 文章标签： [games](https://www.csdn.net/tags/MtjaQgysOTQ5ODctYmxvZwO0O0OO0O0O.html) [docker](https://www.csdn.net/tags/Ntjakg4sNzAwMC1ibG9n.html)

版权

# minecraft

本篇文章介绍使用docker容器方式在linux操作系统上搭建最新版本minecraft服务器，并使用bungeecord配置为群组服务器模式。
常规方式搭建minecraft服务器参考这篇文章：
https://blog.csdn.net/networken/article/details/84477537

------

```java
YINWU正版公益服务器地址:server.yinwurealm.org
YINWU服务器官网:https://www.yinwurealm.org/
YINWU QQ交流群：568753879
123
```

------



## 搭建环境介绍

操作系统版本:CentOS7 minimal最小安装版
下载地址：https://www.centos.org/download/
本次搭建在阿里云购买一台4G内存的centos服务器进行测试。
访问minecraft服务端时，默认连接25565端口（可自定义），注意配置阿里云服务器安全规则，放通25565端口。

关闭linux防火墙

```java
systemctl stop firewalld && systemctl disable firewalld
sed -i ‘s/^SELINUX=enforcing$/SELINUX=disabled/’ /etc/selinux/config
setenforce 0
123
```

**本次搭建服务端整体结构：**

BC代理端和所有子服全部运行在一台服务器上，逻辑结构如下图：
![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAxOS9wbmcvMjQ3MzkwLzE1NjU0MzIzNzI4MzItZTA1M2Q5NWQtMjIzMS00OGYyLWIyMDMtOGE5Zjk5Njg1NWIwLnBuZw#align=left&display=inline&height=592&originHeight=592&originWidth=1139&size=0&status=done&width=1139)

**安装docker**

```java
#下载安装脚本并执行
curl -fsSL https://get.docker.com -o get-docker.sh 
sh get-docker.sh --mirror Aliyun

#配置镜像加速
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF

#启动docker服务
systemctl enable --now docker
1234567891011121314
```

**安装docker-compose工具**
docker-compose负责实现对 Docker 容器集群的快速编排,它允许用户通过一个单独的 docker-compose.yml 模板文件来定义一组相关联的应用容器为一个项目.

```java
#安装epel源
# yum install -y epel-release 
#安装docker-compose
# yum install -y docker-compose
1234
```

## 安装MC服务端

这里仅做测试，基于容器方式运行以下三个容器：

- mcworld1
- mcworld2
- mcbungeecord

**说明：**

- mcworld1和mcworld2是minecraft的两个服务端，也即两个子服，mcbungeecord为服务端代理软件。
- 使用的容器镜像为dockerhub镜像：
  https://hub.docker.com/r/itzg/minecraft-server/
  https://hub.docker.com/r/itzg/bungeecord/
- 安装的服务端版本为PaperSpigot 1.13.2。

**1.运行mcworld1服务端容器：**

```java
docker run -d -e EULA=TRUE \
    -v /mcworld1_data:/data \
    -e TYPE=PAPER \
    -e VERSION=1.13.2 \
    -e OPS=willminec \
    -e ONLINE_MODE=FALSE \
    -p 25566:25565 \
    --restart always \
    --name mcworld1 \
    itzg/minecraft-server --noconsole
12345678910
```

**2.运行mcworld2服务端容器：**

```java
docker run -d -e EULA=TRUE \
    -v /mcworld2_data:/data \
    -e TYPE=PAPER \
    -e VERSION=1.13.2 \
    -e OPS=willminec \
    -e ONLINE_MODE=FALSE \
    -p 25567:25565 \
    --restart always \
    --name mcworld2 \
    itzg/minecraft-server --noconsole
12345678910
```

**3.运行mcbungeecord容器：**

```java
docker run -d -v /mcbg_data:/server \
    -p 25565:25577 \
    --name mcbungeecord \
    --restart always \
    itzg/bungeecord
12345
```

**4.使用docker-compose运行容器（可选）**

我们也可以使用docker-compose来一次运行多个容器，这里已经提前安装了docker-compose，下面我们将运行3个容器的命令写入yml文件并使用docker-compose执行。

在/root目录下创建docker-compose.yml文件，配置如下内容：

```yaml
[root@willcentos ~]# vim docker-compose.yml
version: '2'
services:

  mcworld1:
    image: itzg/minecraft-server
    ports:
      - 25566:25565
    volumes:
      - /mcworld1_data:/data
    environment:
      - EULA=true
      - TYPE=PAPER
      - VERSION=1.13.2
      - OPS=willminec
      - ONLINE_MODE=FALSE
    container_name: mcworld1
    tty: true
    stdin_open: true
    restart: always

  mcworld2:
    image: itzg/minecraft-server
    ports:
      - 25567:25565
    volumes:
      - /mcworld2_data:/data
    environment:
      - EULA=true
      - TYPE=PAPER
      - VERSION=1.13.2
      - OPS=willminec
      - ONLINE_MODE=FALSE
    container_name: mcworld2
    tty: true
    stdin_open: true
    restart: always

  mcbg:
    image: itzg/bungeecord 
    ports:
      - 25565:25577
    volumes:
      - /mcbg_data:/server
    links:
      - mcworld1
      - mcworld2
    container_name: mcbungeecord
    restart: always
12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849
```

执行docker-compose文件,运行容器：

```java
[root@willcentos ~]# docker-compose up -d
1
```

执行效果与前三步运行3个容器一样。

**5.查看下载的容器镜像：**

```java
[root@willcentos ~]# docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
itzg/minecraft-server   latest              c6a0d0b8e7e5        4 weeks ago         309MB
itzg/bungeecord         latest              e9aff248403a        6 months ago        86.5MB
1234
```

**6.查看容器运行状态：**

STATUS列全部为UP（healthy）说明容器已经正常运行

```java
[root@willcentos ~]# docker ps -a
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS                   PORTS                                 NAMES
b73c30462d8d        itzg/bungeecord         "/usr/bin/run-bungee…"   7 minutes ago       Up 7 minutes             0.0.0.0:25565->25577/tcp              mcbungeecord
bea699ee3242        itzg/minecraft-server   "/start"                 7 minutes ago       Up 7 minutes (healthy)   25575/tcp, 0.0.0.0:25567->25565/tcp   mcworld2
7c3cd9e03326        itzg/minecraft-server   "/start"                 7 minutes ago       Up 7 minutes (healthy)   0.0.0.0:25566->25565/tcp, 25575/tcp   mcworld1

123456
```

**7.查看三个容器配置文件和数据在主机上的存放目录：**

服务端的配置文件全部存放在主机本地根目录下，删除容器数据不会被删除。

```java
[root@willcentos ~]# ll /
total 16
...
drwxr-xr-x    4 1000 1000  158 Nov 25 12:10 mcbg_data
drwxrwxr-x    6 1000 1000  125 Nov 25 11:57 mcworld1_data
drwxrwxr-x    6 1000 1000  125 Nov 25 12:01 mcworld2_data
...
1234567
```

## 第四章 修改配置文件

**修改bungeecord配置文件**

1.查看bungeecord目录下有哪些配置文件：

```shell
[root@willcentos ~]# ll /mcbg_data/
total 10084
-rw-r--r-- 1 1000 1000 10297582 Nov 25 15:57 BungeeCord.jar
-rw-r--r-- 1 1000 1000      989 Nov 25 15:57 config.yml
-rw-r--r-- 1 1000 1000        3 Nov 25 15:57 locations.yml
drwxr-xr-x 2 1000 1000     4096 Nov 25 15:57 modules
-rw-r--r-- 1 1000 1000      155 Nov 25 15:57 modules.yml
drwxr-xr-x 2 1000 1000     4096 Nov 25 15:57 plugins
-rw-r--r-- 1 1000 1000     3911 Nov 25 15:59 proxy.log.0
-rw-r--r-- 1 1000 1000        0 Nov 25 15:57 proxy.log.0.lck
12345678910
```

2.首先获取云服务器网卡IP地址,我这里是172.31.112.2

```shell
[root@willcentos ~]# ip a
......
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:0a:26:84 brd ff:ff:ff:ff:ff:ff
    inet 172.31.112.2/20 brd 172.31.127.255 scope global dynamic eth0
       valid_lft 315270699sec preferred_lft 315270699sec
123456
```

3.需要修改的配置文件为config.yml,，修改如下内容：

```yml
[root@localhost ~]# vim /mcbg_data/config.yml 
online_mode: true   #默认ture
......
ip_forward: true    #默认为false，改为true
......
#复制lobby内容，增加一个子服务器create，注意修改IP和端口
servers:            
  lobby:
    motd: 'Welcome the lobby world!'
    address: 172.31.112.2:25566
    restricted: false
  create:
    motd: 'Welcome the create world!'
    address: 172.31.112.2:25567
    restricted: false
......
12345678910111213141516
```

**修改mcworld服务端配置文件**

需要修改mcworld1和mcworld2配置文件，这里以mcworld1为例：

1.查看mcworld1服务端目录下有哪些配置文件

```java
[root@willcentos ~]# ll /mcworld1_data/
total 42508
-rw-rw-r-- 1 1000 1000        2 Nov 25 15:57 banned-ips.json
-rw-rw-r-- 1 1000 1000        2 Nov 25 15:57 banned-players.json
-rw-rw-r-- 1 1000 1000     1053 Nov 25 15:57 bukkit.yml
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 cache
-rw-rw-r-- 1 1000 1000      598 Nov 25 15:57 commands.yml
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 config
-rw-rw-r-- 1 1000 1000       65 Nov 25 15:57 eula.txt
-rw-rw-r-- 1 1000 1000     2576 Nov 25 15:57 help.yml
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 logs
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 mods
-rw-rw-r-- 1 1000 1000      137 Nov 25 15:57 ops.json
-rw-rw-r-- 1 1000 1000       11 Nov 25 15:57 ops.txt.converted
-rw-rw-r-- 1 1000 1000 43431489 Nov 25 15:57 paper_server.jar
-rw-rw-r-- 1 1000 1000     5473 Nov 25 15:58 paper.yml
-rw-rw-r-- 1 1000 1000        0 Nov 25 15:57 permissions.yml
drwxrwxr-x 3 1000 1000     4096 Nov 25 15:57 plugins
-rw-r--r-- 1 1000 1000      912 Nov 25 15:58 server.properties
-rw-rw-r-- 1 1000 1000     3358 Nov 25 15:58 spigot.yml
-rw-rw-r-- 1 1000 1000      108 Nov 25 15:57 usercache.json
-rw-rw-r-- 1 1000 1000       47 Nov 25 15:57 version_history.json
-rw-rw-r-- 1 1000 1000        2 Nov 25 15:57 whitelist.json
drwxrwxr-x 8 1000 1000     4096 Nov 25 16:13 world
drwxrwxr-x 4 1000 1000     4096 Nov 25 16:13 world_nether
drwxrwxr-x 4 1000 1000     4096 Nov 25 16:13 world_the_end
[root@willcentos ~]# 
123456789101112131415161718192021222324252627
```

2.需要修改的配置文件为server.properties和spigot.yml：

```java
[root@willcentos ~]# vim /mcworld1_data/server.properties 
......
online-mode=false   #此项如果为true需要改为false
123
```

修改spigot.yml配置文件：

```java
[root@willcentos ~]# vim /mcworld1_data/spigot.yml 
......
config-version: 11
settings:
......
  bungeecord: true    #将false改为true
......
1234567
```

3.mcworld2配置需要做同样修改，这里省略

4.修改配置文件后需要重启3个docker容器，使配置生效

```java
[root@willcentos ~]# docker restart mcbungeecord mcworld1 mcworld2
1
```

**基本原理：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181211160926603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)

## 登录MC服务端

**1.下载安装官方客户端：**

官方客户端下载地址：https://minecraft.net/zh-hans/download/

下载与服务端版本相同的客户端版本（即最新的1.13.2）：

官网注册账号，购买游戏，下载minecraft客户端并安装到个人电脑，启动客户端并登录，登录后界面如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125164115594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)

**2.配置服务端IP地址并连接**

选择开始游戏，然后选择多人游戏
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125165243806.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
输入服务器名称，可以默认，输入服务端IP地址，即阿里云服务器的公网地址，点击完成：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181126211346138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
点击加入服务器，即可登录游戏：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125165815904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
登录游戏后默认为生存模式，输入/server提示当前登录的服务端为lobby，即mcworld1服务端，并且提示可登录的服务器为lobby和create两个服务端。
输入/server create切换到create服务端，即mcworld2服务端：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125170945283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
再次输入/server可以看到当前所在服务端为create服务器端：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181125171223157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
到这里群组服务器已经完成，可以正常游戏了。

**3.服务端配置修改**
目前两个服务端都是生存模式，我们可以通过修改配置文件，更改游戏模式，调整op权限等各种操作。
这里先配置OP权限，运行容器是已经添加willminec用户为op管理员，但在ops.json的配置文件中默认uuid不对，需要进行更改：
查看当前的ops.json配置信息：

```json
[root@willcentos ~]# vim /mcworld1_data/ops.json 
[
  {
    "uuid": "9f8064f3-8797-312e-af07-ac091656b63d",
    "name": "willminec",
    "level": 4,
    "bypassesPlayerLimit": false
  }
12345678
```

查询willminec用户的uuid
访问查询网站：[https://mcuuid.net](https://mcuuid.net/)，输入用户名进行查询：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181126212027291.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
我们查询到该用户的uuid后进行替换：

```json
[root@willcentos ~]# vim /mcworld1_data/ops.json 
[
  {
    "uuid": "44702a33-29dc-4b8f-a545-f8aa499517ef",
    "name": "willminec",
    "level": 4,
    "bypassesPlayerLimit": false
  }
]
123456789
```

然后保存配置重启该容器：

```java
[root@willcentos ~]# docker restart mcworld1
1
```

重新登录游戏，即可拥有op权限，可以进行大部分命令的操作：

例如使用/deop （玩家名）删除op时提示当前可删除的op为willminec.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181126212548404.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)
可使用/op <玩家名> 为其他用户设置op权限。

使用/gamemode xxx切换游戏模式：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181126212855947.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)

**其他命令例如：**

```java
/tp 1000 64 1000    #传送到x坐标为1000，y坐标为64，z坐标为1000的位置
/time set day       #将时间切换到白天
12
```

## 服务端安装插件

对于插件安装，直接下载后放在服务端对应plugins目录下，然后重启容器即可，这里以mcworld1为例：
访问bukkit官网下载对应版本的插件：https://dev.bukkit.org/bukkit-plugins
这里仅下载worldedit、worldguard、EssentialsX、PermissionsEx四个插件进行测试，下载后的插件全部为jar文件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181126213621277.png)
使用winspc或者FlashFXP从windows系统传送到linux系统的/mcworld1_data/plugins目录下即可：

```java
[root@willcentos ~]# ll /mcworld1_data/plugins/
total 5872
drwxrwxr-x 2 1000 1000    4096 Nov 26 20:08 bStats
-rw-r--r-- 1 root root 1211165 Nov 26 18:07 EssentialsX-2.15.0.1.jar
-rw-r--r-- 1 root root   14270 Nov 26 18:07 EssentialsXAntiBuild-2.15.0.1.jar
-rw-r--r-- 1 root root   12792 Nov 26 18:07 EssentialsXChat-2.15.0.1.jar
-rw-r--r-- 1 root root 1120585 Nov 26 18:07 EssentialsXGeoIP-2.15.0.1.jar
-rw-r--r-- 1 root root   19387 Nov 26 18:07 EssentialsXProtect-2.15.0.1.jar
-rw-r--r-- 1 root root   18251 Nov 26 18:07 EssentialsXSpawn-2.15.0.1.jar
-rw-r--r-- 1 root root  334630 Nov 26 18:07 EssentialsXXMPP-2.15.0.1.jar
-rw-r--r-- 1 root root  722895 Nov 26 18:40 PermissionsEx-1.23.4.jar
-rw-r--r-- 1 root root 1449119 Nov 16 13:35 worldedit-bukkit-7.0.0-beta-01.jar
-rw-r--r-- 1 root root 1088638 Nov 24 12:54 worldguard-bukkit-6.2.2.jar
[root@willcentos ~]#
1234567891011121314
```

然后重启mcworld1容器，插件即可生效，登录游戏进行验证：

```java
[root@willcentos ~]# docker restart mcworld
1
```

可以看到已经支持了world相关命令，我们用worldedit插件功能创建一个半径为5的空心玻璃圆形，执行命令：//hcyl glass 5 1
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181126215747229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25ldHdvcmtlbg==,size_16,color_FFFFFF,t_70)



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞3
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论3](https://blog.csdn.net/networken/article/details/84945172#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏15](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReward.png)打赏
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[3分钟用*Docker**搭建*一个*Minecraft**服务器*](https://download.csdn.net/download/weixin_38635996/12901837)

09-30

[主要介绍了3分钟用*Docker**搭建*一个*Minecraft**服务器**的*相关资料,非常不错具有参考借鉴价值，需要*的*朋友可以参考下](https://download.csdn.net/download/weixin_38635996/12901837)

[群晖*docker*_利用群晖*docker**搭建**Minecraft**服务器*：图形界面操作，傻瓜式教程（附官方*服务器*端地址）_NAS存储...](https://blog.csdn.net/weixin_39612726/article/details/111704134)

[weixin_39612726的博客](https://blog.csdn.net/weixin_39612726)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 196

[2020-12-19 18:01:5310点赞57收藏4评论你是AMD Yes党？还是intel和NVIDIA*的*忠实簇拥呢？最新一届#装机大师赛#开始啦！本次装机阵营赛分为3A红组、intel NVIDIA蓝绿组、混搭组还有ITX组，实体or虚拟装机都能参与，可使用值得买定制化DIY装机工具在文中展现配置单！每个小组均有精美礼品，优秀文章还可角逐装机大师终极大奖，点击参与<<<前...](https://blog.csdn.net/weixin_39612726/article/details/111704134)





[![img](https://profile.csdnimg.cn/0/5/1/3_weixin_45710390)](https://blog.csdn.net/weixin_45710390)

![表情包](https://csdnimg.cn/release/blogv2/dist/pc/img/emoticon.png)



- [![xaiweiok1111](https://profile.csdnimg.cn/4/6/E/3_xaiweiok1111)](https://blog.csdn.net/xaiweiok1111)

  [欲梦](https://blog.csdn.net/xaiweiok1111)**:**大佬请问一下，我jar包没有自动展开是为什么，目录里没有配置文件什么的8 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![qq_38621077](https://profile.csdnimg.cn/E/3/1/3_qq_38621077)](https://blog.csdn.net/qq_38621077)

  [calm dream](https://blog.csdn.net/qq_38621077)**:**大佬你好，我在执行docker-compose文件报错了，不知道原因。 [code=plain] [root@stars ~]# docker-compose up -d Creating mcworld1 ... error Creating mcworld1 ... Creating mcworld2 ... ERROR: for mcworld1 Cannot create container for service mcworld1: b'Conflict. The conta Creating mcworld2 ... errorf354a7f2e575af288740cb58b171cf". You have to remove (or rename) that container to be able to reuse that name.' ERROR: for mcworld2 Cannot create container for service mcworld2: b'Conflict. The container name "/mcworld2" is already in use by container "3432a21d24f2eb0d48715feeba04447b6367162cedd9fbf8923ee7bdafd7ca61". You have to remove (or rename) that container to be able to reuse that name.' ERROR: for mcworld1 Cannot create container for service mcworld1: b'Conflict. The container name "/mcworld1" is already in use by container "ff4aa7936f9d330437d5ab132307fb6f30f354a7f2e575af288740cb58b171cf". You have to remove (or rename) that container to be able to reuse that name.' ERROR: for mcworld2 Cannot create3 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- - [![networken](https://profile.csdnimg.cn/4/0/C/3_networken)](https://blog.csdn.net/networken)

    [willblog![img](https://csdnimg.cn/release/blogv2/dist/components/img/bloger@2x.png)](https://blog.csdn.net/networken)回复**:**这一步是可选的，三个docker已经跑起来了，它提示你容器名字重复了2 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

YINWU QQ交流群：568753879
1
2
3
搭建环境介绍
操作系统版本:CentOS7 minimal最小安装版
下载地址：https://www.centos.org/download/
本次搭建在阿里云购买一台4G内存的centos服务器进行测试。
访问minecraft服务端时，默认连接25565端口（可自定义），注意配置阿里云服务器安全规则，放通25565端口。

关闭linux防火墙

systemctl stop firewalld && systemctl disable firewalld
sed -i ‘s/^SELINUX=enforcing$/SELINUX=disabled/’ /etc/selinux/config
setenforce 0
1
2
3
本次搭建服务端整体结构：

BC代理端和所有子服全部运行在一台服务器上，逻辑结构如下图：


安装docker

#下载安装脚本并执行
curl -fsSL https://get.docker.com -o get-docker.sh 
sh get-docker.sh --mirror Aliyun

#配置镜像加速
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF

#启动docker服务
systemctl enable --now docker
1
2
3
4
5
6
7
8
9
10
11
12
13
14
安装docker-compose工具
docker-compose负责实现对 Docker 容器集群的快速编排,它允许用户通过一个单独的 docker-compose.yml 模板文件来定义一组相关联的应用容器为一个项目.

#安装epel源
# yum install -y epel-release 
#安装docker-compose
# yum install -y docker-compose
1
2
3
4
安装MC服务端
这里仅做测试，基于容器方式运行以下三个容器：

mcworld1
mcworld2
mcbungeecord
说明：

mcworld1和mcworld2是minecraft的两个服务端，也即两个子服，mcbungeecord为服务端代理软件。
使用的容器镜像为dockerhub镜像：
https://hub.docker.com/r/itzg/minecraft-server/
https://hub.docker.com/r/itzg/bungeecord/
安装的服务端版本为PaperSpigot 1.13.2。
1.运行mcworld1服务端容器：

docker run -d -e EULA=TRUE \
    -v /mcworld1_data:/data \
    -e TYPE=PAPER \
    -e VERSION=1.13.2 \
    -e OPS=willminec \
    -e ONLINE_MODE=FALSE \
    -p 25566:25565 \
    --restart always \
    --name mcworld1 \
    itzg/minecraft-server --noconsole
1
2
3
4
5
6
7
8
9
10
2.运行mcworld2服务端容器：

docker run -d -e EULA=TRUE \
    -v /mcworld2_data:/data \
    -e TYPE=PAPER \
    -e VERSION=1.13.2 \
    -e OPS=willminec \
    -e ONLINE_MODE=FALSE \
    -p 25567:25565 \
    --restart always \
    --name mcworld2 \
    itzg/minecraft-server --noconsole
1
2
3
4
5
6
7
8
9
10
3.运行mcbungeecord容器：

docker run -d -v /mcbg_data:/server \
    -p 25565:25577 \
    --name mcbungeecord \
    --restart always \
    itzg/bungeecord
1
2
3
4
5
4.使用docker-compose运行容器（可选）

我们也可以使用docker-compose来一次运行多个容器，这里已经提前安装了docker-compose，下面我们将运行3个容器的命令写入yml文件并使用docker-compose执行。

在/root目录下创建docker-compose.yml文件，配置如下内容：

[root@willcentos ~]# vim docker-compose.yml
version: '2'
services:

  mcworld1:
    image: itzg/minecraft-server
    ports:
      - 25566:25565
    volumes:
      - /mcworld1_data:/data
    environment:
      - EULA=true
      - TYPE=PAPER
      - VERSION=1.13.2
      - OPS=willminec
      - ONLINE_MODE=FALSE
    container_name: mcworld1
    tty: true
    stdin_open: true
    restart: always

  mcworld2:
    image: itzg/minecraft-server
    ports:
      - 25567:25565
    volumes:
      - /mcworld2_data:/data
    environment:
      - EULA=true
      - TYPE=PAPER
      - VERSION=1.13.2
      - OPS=willminec
      - ONLINE_MODE=FALSE
    container_name: mcworld2
    tty: true
    stdin_open: true
    restart: always

  mcbg:
    image: itzg/bungeecord 
    ports:
      - 25565:25577
    volumes:
      - /mcbg_data:/server
    links:
      - mcworld1
      - mcworld2
    container_name: mcbungeecord
    restart: always
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
执行docker-compose文件,运行容器：

[root@willcentos ~]# docker-compose up -d
1
执行效果与前三步运行3个容器一样。

5.查看下载的容器镜像：

[root@willcentos ~]# docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
itzg/minecraft-server   latest              c6a0d0b8e7e5        4 weeks ago         309MB
itzg/bungeecord         latest              e9aff248403a        6 months ago        86.5MB
1
2
3
4
6.查看容器运行状态：

STATUS列全部为UP（healthy）说明容器已经正常运行

[root@willcentos ~]# docker ps -a
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS                   PORTS                                 NAMES
b73c30462d8d        itzg/bungeecord         "/usr/bin/run-bungee…"   7 minutes ago       Up 7 minutes             0.0.0.0:25565->25577/tcp              mcbungeecord
bea699ee3242        itzg/minecraft-server   "/start"                 7 minutes ago       Up 7 minutes (healthy)   25575/tcp, 0.0.0.0:25567->25565/tcp   mcworld2
7c3cd9e03326        itzg/minecraft-server   "/start"                 7 minutes ago       Up 7 minutes (healthy)   0.0.0.0:25566->25565/tcp, 25575/tcp   mcworld1

1
2
3
4
5
6
7.查看三个容器配置文件和数据在主机上的存放目录：

服务端的配置文件全部存放在主机本地根目录下，删除容器数据不会被删除。

[root@willcentos ~]# ll /
total 16
...
drwxr-xr-x    4 1000 1000  158 Nov 25 12:10 mcbg_data
drwxrwxr-x    6 1000 1000  125 Nov 25 11:57 mcworld1_data
drwxrwxr-x    6 1000 1000  125 Nov 25 12:01 mcworld2_data
...
1
2
3
4
5
6
7
第四章 修改配置文件
修改bungeecord配置文件

1.查看bungeecord目录下有哪些配置文件：

[root@willcentos ~]# ll /mcbg_data/
total 10084
-rw-r--r-- 1 1000 1000 10297582 Nov 25 15:57 BungeeCord.jar
-rw-r--r-- 1 1000 1000      989 Nov 25 15:57 config.yml
-rw-r--r-- 1 1000 1000        3 Nov 25 15:57 locations.yml
drwxr-xr-x 2 1000 1000     4096 Nov 25 15:57 modules
-rw-r--r-- 1 1000 1000      155 Nov 25 15:57 modules.yml
drwxr-xr-x 2 1000 1000     4096 Nov 25 15:57 plugins
-rw-r--r-- 1 1000 1000     3911 Nov 25 15:59 proxy.log.0
-rw-r--r-- 1 1000 1000        0 Nov 25 15:57 proxy.log.0.lck
1
2
3
4
5
6
7
8
9
10
2.首先获取云服务器网卡IP地址,我这里是172.31.112.2

[root@willcentos ~]# ip a
......
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:0a:26:84 brd ff:ff:ff:ff:ff:ff
    inet 172.31.112.2/20 brd 172.31.127.255 scope global dynamic eth0
       valid_lft 315270699sec preferred_lft 315270699sec
1
2
3
4
5
6
3.需要修改的配置文件为config.yml,，修改如下内容：

[root@localhost ~]# vim /mcbg_data/config.yml 
online_mode: true   #默认ture
......
ip_forward: true    #默认为false，改为true
......
#复制lobby内容，增加一个子服务器create，注意修改IP和端口
servers:            
  lobby:
    motd: 'Welcome the lobby world!'
    address: 172.31.112.2:25566
    restricted: false
  create:
    motd: 'Welcome the create world!'
    address: 172.31.112.2:25567
    restricted: false
......
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
修改mcworld服务端配置文件

需要修改mcworld1和mcworld2配置文件，这里以mcworld1为例：

1.查看mcworld1服务端目录下有哪些配置文件

[root@willcentos ~]# ll /mcworld1_data/
total 42508
-rw-rw-r-- 1 1000 1000        2 Nov 25 15:57 banned-ips.json
-rw-rw-r-- 1 1000 1000        2 Nov 25 15:57 banned-players.json
-rw-rw-r-- 1 1000 1000     1053 Nov 25 15:57 bukkit.yml
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 cache
-rw-rw-r-- 1 1000 1000      598 Nov 25 15:57 commands.yml
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 config
-rw-rw-r-- 1 1000 1000       65 Nov 25 15:57 eula.txt
-rw-rw-r-- 1 1000 1000     2576 Nov 25 15:57 help.yml
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 logs
drwxrwxr-x 2 1000 1000     4096 Nov 25 15:57 mods
-rw-rw-r-- 1 1000 1000      137 Nov 25 15:57 ops.json
-rw-rw-r-- 1 1000 1000       11 Nov 25 15:57 ops.txt.converted
-rw-rw-r-- 1 1000 1000 43431489 Nov 25 15:57 paper_server.jar
-rw-rw-r-- 1 1000 1000     5473 Nov 25 15:58 paper.yml
-rw-rw-r-- 1 1000 1000        0 Nov 25 15:57 permissions.yml
drwxrwxr-x 3 1000 1000     4096 Nov 25 15:57 plugins
-rw-r--r-- 1 1000 1000      912 Nov 25 15:58 server.properties
-rw-rw-r-- 1 1000 1000     3358 Nov 25 15:58 spigot.yml
-rw-rw-r-- 1 1000 1000      108 Nov 25 15:57 usercache.json
-rw-rw-r-- 1 1000 1000       47 Nov 25 15:57 version_history.json
-rw-rw-r-- 1 1000 1000        2 Nov 25 15:57 whitelist.json
drwxrwxr-x 8 1000 1000     4096 Nov 25 16:13 world
drwxrwxr-x 4 1000 1000     4096 Nov 25 16:13 world_nether
drwxrwxr-x 4 1000 1000     4096 Nov 25 16:13 world_the_end
[root@willcentos ~]# 
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
2.需要修改的配置文件为server.properties和spigot.yml：

[root@willcentos ~]# vim /mcworld1_data/server.properties 
......
online-mode=false   #此项如果为true需要改为false
1
2
3
修改spigot.yml配置文件：

[root@willcentos ~]# vim /mcworld1_data/spigot.yml 
......
config-version: 11
settings:
......
  bungeecord: true    #将false改为true
......
1
2
3
4
5
6
7
3.mcworld2配置需要做同样修改，这里省略

4.修改配置文件后需要重启3个docker容器，使配置生效

[root@willcentos ~]# docker restart mcbungeecord mcworld1 mcworld2
1
基本原理：


登录MC服务端
1.下载安装官方客户端：

官方客户端下载地址：https://minecraft.net/zh-hans/download/

下载与服务端版本相同的客户端版本（即最新的1.13.2）：

官网注册账号，购买游戏，下载minecraft客户端并安装到个人电脑，启动客户端并登录，登录后界面如下：


2.配置服务端IP地址并连接

选择开始游戏，然后选择多人游戏

输入服务器名称，可以默认，输入服务端IP地址，即阿里云服务器的公网地址，点击完成：

点击加入服务器，即可登录游戏：

登录游戏后默认为生存模式，输入/server提示当前登录的服务端为lobby，即mcworld1服务端，并且提示可登录的服务器为lobby和create两个服务端。
输入/server create切换到create服务端，即mcworld2服务端：

再次输入/server可以看到当前所在服务端为create服务器端：

到这里群组服务器已经完成，可以正常游戏了。

3.服务端配置修改
目前两个服务端都是生存模式，我们可以通过修改配置文件，更改游戏模式，调整op权限等各种操作。
这里先配置OP权限，运行容器是已经添加willminec用户为op管理员，但在ops.json的配置文件中默认uuid不对，需要进行更改：
查看当前的ops.json配置信息：

[root@willcentos ~]# vim /mcworld1_data/ops.json 
[
  {
    "uuid": "9f8064f3-8797-312e-af07-ac091656b63d",
    "name": "willminec",
    "level": 4,
    "bypassesPlayerLimit": false
  }
1
2
3
4
5
6
7
8
查询willminec用户的uuid
访问查询网站：https://mcuuid.net，输入用户名进行查询：

我们查询到该用户的uuid后进行替换：

[root@willcentos ~]# vim /mcworld1_data/ops.json 
[
  {
    "uuid": "44702a33-29dc-4b8f-a545-f8aa499517ef",
    "name": "willminec",
    "level": 4,
    "bypassesPlayerLimit": false
  }
]
1
2
3
4
5
6
7
8
9
然后保存配置重启该容器：

[root@willcentos ~]# docker restart mcworld1
1
重新登录游戏，即可拥有op权限，可以进行大部分命令的操作：

例如使用/deop （玩家名）删除op时提示当前可删除的op为willminec.

可使用/op <玩家名> 为其他用户设置op权限。

使用/gamemode xxx切换游戏模式：


其他命令例如：

/tp 1000 64 1000    #传送到x坐标为1000，y坐标为64，z坐标为1000的位置
/time set day       #将时间切换到白天
1
2
服务端安装插件
对于插件安装，直接下载后放在服务端对应plugins目录下，然后重启容器即可，这里以mcworld1为例：
访问bukkit官网下载对应版本的插件：https://dev.bukkit.org/bukkit-plugins
这里仅下载worldedit、worldguard、EssentialsX、PermissionsEx四个插件进行测试，下载后的插件全部为jar文件：

使用winspc或者FlashFXP从windows系统传送到linux系统的/mcworld1_data/plugins目录下即可：

[root@willcentos ~]# ll /mcworld1_data/plugins/
total 5872
drwxrwxr-x 2 1000 1000    4096 Nov 26 20:08 bStats
-rw-r--r-- 1 root root 1211165 Nov 26 18:07 EssentialsX-2.15.0.1.jar
-rw-r--r-- 1 root root   14270 Nov 26 18:07 EssentialsXAntiBuild-2.15.0.1.jar
-rw-r--r-- 1 root root   12792 Nov 26 18:07 EssentialsXChat-2.15.0.1.jar
-rw-r--r-- 1 root root 1120585 Nov 26 18:07 EssentialsXGeoIP-2.15.0.1.jar
-rw-r--r-- 1 root root   19387 Nov 26 18:07 EssentialsXProtect-2.15.0.1.jar
-rw-r--r-- 1 root root   18251 Nov 26 18:07 EssentialsXSpawn-2.15.0.1.jar
-rw-r--r-- 1 root root  334630 Nov 26 18:07 EssentialsXXMPP-2.15.0.1.jar
-rw-r--r-- 1 root root  722895 Nov 26 18:40 PermissionsEx-1.23.4.jar
-rw-r--r-- 1 root root 1449119 Nov 16 13:35 worldedit-bukkit-7.0.0-beta-01.jar
-rw-r--r-- 1 root root 1088638 Nov 24 12:54 worldguard-bukkit-6.2.2.jar
[root@willcentos ~]#
1
2
3
4
5
6
7
8
9
10
11
12
13
14
然后重启mcworld1容器，插件即可生效，登录游戏进行验证：

[root@willcentos ~]# docker restart mcworld
1
可以看到已经支持了world相关命令，我们用worldedit插件功能创建一个半径为5的空心玻璃圆形，执行命令：//hcyl glass 5 1



点赞
3

评论
3

分享

收藏
15

打赏

举报
关注
一键三连

docker-minecraft-bedrock-server：Minecraft基岩服务器的Docker容器构建-源码
02-12
docker-minecraft-bedrock-server：Minecraft基岩服务器的Docker容器构建



欲梦:大佬请问一下，我jar包没有自动展开是为什么，目录里没有配置文件什么的6 月前回复


calm dream:大佬你好，我在执行docker-compose文件报错了，不知道原因。 [code=plain] [root@stars ~]# docker-compose up -d Creating mcworld1 ... error Creating mcworld1 ... Creating mcworld2 ... ERROR: for mcworld1 Cannot create container for service mcworld1: b'Conflict. The conta Creating mcworld2 ... errorf354a7f2e575af288740cb58b171cf". You have to remove (or rename) that container to be able to reuse that name.' ERROR: for mcworld2 Cannot create container for service mcworld2: b'Conflict. The container name "/mcworld2" is already in use by container "3432a21d24f2eb0d48715feeba04447b6367162cedd9fbf8923ee7bdafd7ca61". You have to remove (or rename) that container to be able to reuse that name.' ERROR: for mcworld1 Cannot create container for service mcworld1: b'Conflict. The container name "/mcworld1" is already in use by container "ff4aa7936f9d330437d5ab132307fb6f30f354a7f2e575af288740cb58b171cf". You have to remove (or rename) that container to be able to reuse that name.' ERROR: for mcworld2 Cannot create3 年前回复


码工willblog回复:这一步是可选的，三个docker已经跑起来了，它提示你容器名字重复了2 年前回复