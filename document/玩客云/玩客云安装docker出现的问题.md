玩客云 armbian EMMC直刷版本docker无法启动解决方案

w670165403 2020-11-10 19:11:05  1764  收藏 3
分类专栏： Linux
版权
先安装docker，提示dpkg: error processing package docker-ce (--configure):
使用systemctl status docker.services可以看到启动失败
运行下列命令：

 sudo mv /var/lib/dpkg/info/ /var/lib/dpkg/info_old/
 sudo mkdir /var/lib/dpkg/info/
 sudo apt-get update
 sudo apt-get -f install
 sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_old/
 sudo rm -rf /var/lib/dpkg/info
 sudo mv /var/lib/dpkg/info_old/ /var/lib/dpkg/info
 sudo mv /var/lib/dpkg/info/ /var/lib/dpkg/info_old/
 sudo mkdir /var/lib/dpkg/info/
 sudo apt-get update
 sudo apt-get -f install
 sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_old/
 sudo rm -rf /var/lib/dpkg/info
 sudo mv /var/lib/dpkg/info_old/ /var/lib/dpkg/info
重新安装docker即可

# https://blog.csdn.net/stickmangod/article/details/85316142

E: Sub-process /usr/bin/dpkg returned an error code (1)解决办法

Mr.Stick 2018-12-28 00:08:55  86347  收藏 158
分类专栏： ubuntu日常 文章标签： ubuntu
版权
E: Sub-process /usr/bin/dpkg returned an error code (1)解决办法
安装libapache2-svn出现了这个错误，是由于apt－get安装软件时出现了类似于：

dpkg: error processing package libapache2-mod-svn (--configure):
 subprocess installed post-installation script returned error exit status 1
No apport report written because the error message indicates its a followup error from a previous failure.
                                                                                                          dpkg: dependency problems prevent configuration of libapache2-svn:
 libapache2-svn depends on libapache2-mod-svn; however:
  Package libapache2-mod-svn is not configured yet.

dpkg: error processing package libapache2-svn (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 libapache2-mod-svn
 libapache2-svn
E: Sub-process /usr/bin/dpkg returned an error code (1)
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
解决方法：
现将info文件夹更名

sudo mv /var/lib/dpkg/info /var/lib/dpkg/info.bk
1
新建一个新的info文件夹

sudo mkdir /var/lib/dpkg/info
1
安装修复

sudo apt-get update
$sudoapt-get install -f 
1
2
执行完上一步操作后，在info文件夹下生成一些文件，现将这些文件全部移到info.bk文件夹下

sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info.bk
1
把自己新建的info文件夹删掉

sudo rm -rf /var/lib/dpkg/info
1
恢复原有info文件夹，修改名字

sudo mv /var/lib/dpkg/info.bk /var/lib/dpkg/info
1
到这里已经成功安装了，但我还遇到了相关文件的缺失，例如

/etc/apache2/mods-available/dav_svn.conf

但是现在至少能够正常安装了，直接索性卸载重装

sudo apt-get --purge remove libapache2-mod-svn 
sudo apt-get --purge remove libapache2-svn 
sudo apt-get autoremove
1
2
3
再install一边，恢复正常


点赞
76

评论
26

分享

收藏
158

打赏

举报
关注
一键三连

https://blog.csdn.net/love1026999045/article/details/100072286

# 斐讯N1在armbian上安装docker,运行docker容器

# N1刷机避坑指南 篇十一：armbian系统如何安装docker

2020-08-02 15:50:16 31点赞 176收藏 17评论

> 如何才能快速换一种生活方式？参加[**#牛年Flag#**](https://www.smzdm.com/tag/tr0lp4e/post/)征稿活动，征集你2021年的购物学习生活计划！>>[**点击查看活动详情**](https://post.smzdm.com/p/a9gdrq6p/)<<本次征稿活动欢迎你的敢出敢买Flag、学习Flag以及各种生活Flag，优秀的投稿文章能获得优厚的大奖，让我们一起努力实现目标吧！

本文比较简单，主要是提供一下armbian安装docker的步骤。目前本人的N1一个刷了小钢炮，小钢炮内置docker，直接拉取portainer可视化界面即可，当然，docker在没有本地库的情况下，拉取镜像还是非常吃网络环境的，电信的网络最佳。

小钢炮系统唯一不方便一点就是不带无线，所以我只利用了docker安装了[next](https://pinpai.smzdm.com/20143/)cloud，存储了家里两个[手机](https://www.smzdm.com/fenlei/zhinengshouji/)的70G照片，[硬盘](https://www.smzdm.com/fenlei/yingpan/)通过[硬盘盒](https://www.smzdm.com/fenlei/yidongyingpanhe/)挂载在小钢炮上。另一个N1刷了[游戏](https://www.smzdm.com/fenlei/youxi/)系统后就没怎么玩了，哎。还有一个N1刷了armbian系统，然后安装了docker，homeassistant和mjpg-streamer运行在上面。平时孩子在床上睡觉的时候可以局域网内观察到她的状态。

首先，你需要一个N1的[Armbian系统](https://pan.baidu.com/s/1QS7ifApMfwWq55CF0W-bjg)（提取码：hhvu），可以安装20版本的。刷机步骤看我之前的文章，大同小异。

然后进入系统，创建账户等一系列做完。

### 第一步，更换源。

nano /etc/apt/sources.list

> deb https://mirrors.ustc.edu.cn/debian buster main contrib non-free
>
> deb https://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
>
> deb https://mirrors.ustc.edu.cn/debian buster-backports main contrib non-free
>
> deb https://mirrors.ustc.edu.cn/debian-security/ buster/updates main contribnon-free

[![把之前的注释掉，粘贴上国内ustc的源](https://qnam.smzdm.com/202008/01/5f251effaca4f7085.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_2/)把之前的注释掉，粘贴上国内ustc的源

Ctrl+O保存，Ctrl+X退出。

### 第二步，更新

apt-get update

虽然源改成了国内的，大部分软件更新会比较快，但是部分还是需要从armbian处获得，所以需要一点时间。

[![更新](https://qnam.smzdm.com/202008/01/5f25204787a3e2394.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_3/)更新

### 第三步，使用docker安装脚本

> curl -fsSL https://get.docker.com -o get-docker.sh
>
> sh get-docker.sh --mirror Aliyun

[![通过脚本自动安装](https://qnam.smzdm.com/202008/01/5f2520a1b0ac94775.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_4/)通过脚本自动安装

### 第四步，修改docker源

找到daemon.json文件，更改源地址。

文件在/etc/docker/。

> "registry-mirrors": ["https://registry.docker-cn.com","http://hub-mirror.c.163.com"]

[![更改docker源地址](https://qnam.smzdm.com/202008/01/5f2521b14f907693.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_5/)更改docker源地址

### 第五步，安装可视化portainer

这个不安装也可以，有些人不喜欢用可视化界面，其实就是创建了portainer.io容器和镜像。

> docker volume create portainer_data
>
> docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer:linux-arm64

[![docker会自动拉取镜像创建容器](https://qnam.smzdm.com/202008/01/5f2523e3774007069.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_6/)docker会自动拉取镜像创建容器

### 第六步，设置自启动 

第一次进入可视化界面要创建用户。

[![创建用户](https://qnam.smzdm.com/202008/02/5f265f5c961413309.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_7/)创建用户

选择local。

[![选择本地](https://qnam.smzdm.com/202008/02/5f265f77082c09640.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_8/)选择本地

找到刚创建的镜像，点击名称进入设置。

[![armbian系统如何安装docker](https://qnam.smzdm.com/202008/02/5f265f8ddf692160.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_9/)

重启策略改为always。

[![armbian系统如何安装docker](https://qnam.smzdm.com/202008/02/5f265fa0e75a47727.jpg_e680.jpg)](https://post.smzdm.com/p/a259v7wq/pic_10/)

这一步其实在创建容器的时候就可以附带上去，但是我试了下不好使，就图形化界面说明一下。

### 写在最后

家中女宝在一天天长大，每天都得陪着，所以没什么时间写文章，最近折腾的心和时间也不足。等孩子长大一点再折腾，哈哈哈哈。

我是Memol。

# https://blog.csdn.net/catoop/article/details/103463007  

Error response from daemon: error while removing network

catoop 2019-12-09 18:37:55  1741  收藏 1
分类专栏： Docker
版权

# docker 网络出问题了，然后使用命令进行删除，结果报错，如下：  原因是有容器正在使用当前设置的虚拟网卡停止容器后删除

[root@harbor harbor]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
93f0ec306ab5        bridge              bridge              local
821031255cda        harbor_harbor       bridge              local
[root@harbor harbor]# docker network rm 821031255cda
Error response from daemon: error while removing network: network harbor_harbor id 821031255cdaf4909913c8a1c9451db461e898a877661564f59cd13f4d0d68b5 has active endpoints
1
2
3
4
5
6
解决方法如下：

[root@harbor harbor]# docker network inspect harbor_harbor
[
    {
        "Name": "harbor_harbor",   #参数一
        "Id": "821031255cdaf4909913c8a1c9451db461e898a877661564f59cd13f4d0d68b5",
        "Created": "2019-11-08T17:16:11.031524353+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": true,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "98cbc25660b315f0a639d3340aad084b2819d43fc966969316597d42f5b1b84c": {
                "Name": "harbor-core",   # 参数二
                "EndpointID": "254f0dae9697b07294670b596f74e9d95056739d85f75c6722e70c539e50aa86",
                "MacAddress": "02:42:ac:12:00:08",
                "IPv4Address": "172.18.0.8/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {
            "com.docker.compose.network": "harbor",
            "com.docker.compose.project": "harbor",
            "com.docker.compose.version": "1.24.1"
        }
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
记下上面输出的“参数一”和“参数二”，然后执行如下命令：

[root@harbor harbor]# docker network disconnect -f harbor_harbor harbor-core
1
然后问题就解决了。

（END）

玩客云折腾记2--docker和openwrt安装

mocklan 2021-02-20 09:39:24  391  收藏 2
文章标签： 其他
版权
用的img是Armbian_20.12_Aml-s812_buster_current_5.9.0-rc7.img
用balenaetcher刷写到U盘
U盘插入usb2（靠近网口）
插电启动
运行/boot里面的install.sh
顺利装入emmc，拔掉upan重启进入系统，该img不支持hdmi显示，需要路由器查看ip后putty连接ssh
该img支持docker，但未安装，需要apt install docker.io
已经换源

装宝塔
docker pull portainer/portainer
docker run -d -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name portainer-test docker.io/portainer/portainer
访问方式：http://IP:9000
初次进入需要设置大于8位的密码
选择local连接，connnect
拉openwrt：（https://hub.docker.com/r/virking/openwrt）密码是snail
docker pull virking/openwrt:18.06

配置：
开启网卡混杂
ip link set eth0 promisc on
或
ifconfig eth0 promisc
加入永久，不用重启失效
vim /etc/rc.local
ip link set eth0 promisc on
重启网卡生效
/etc/init.d/networking restart
最佳：/etc/init.d/networking stop; /etc/init.d/networking start

重启

检查
ifconfig
docker搭建macvlan网络
docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 macnet

docker network ls ## 可查看已创建网络

配置 OpenWrt 容器网络

docker run --restart always -d --network macnet --privileged virking/openwrt:18.06 /sbin/init
查看容器：
docker ps -a
找到容器名字name
进入容器
docker exec -it flamboyant_banzai bash
编辑 OpenWrt 的网络配置文件：
ipaddr是openwrt的网址
vim /etc/config/network

config interface ‘lan’
option type ‘bridge’
option ifname ‘eth0’
option proto ‘static’
option ipaddr ‘192.168.1.254’
option netmask ‘255.255.255.0’
option ip6assign ‘60’
option gateway ‘192.168.1.1’
option broadcast ‘192.168.1.255’
option dns ‘192.168.1.1’

重启网络
/etc/init.d/network restart
推出docker
exit
重启网卡生效
/etc/init.d/networking restart

修复宿主主机网络

cp /etc/network/interfaces /etc/network/interfaces.bak # 备份文件
vim /etc/network/interfaces # 使用 vim 编辑文件
auto eth0
iface eth0 inet manual

auto macvlan
iface macvlan inet static
address 192.168.2.200
netmask 255.255.255.0
gateway 192.168.2.1
dns-nameservers 192.168.2.1
pre-up ip link add macvlan link eth0 type macvlan mode bridge
post-down ip link del macvlan link eth0 type macvlan mode bridge

重启
重启 OpenWrt/网络，就可以 192.168.2.254 登录 Docker 里的 OpenWrt 软路由了。密码是snail