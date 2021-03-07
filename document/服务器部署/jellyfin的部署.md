# 让NAS成为你的私人影视中心，Jellyfin+kodi如何部署

2020-03-26 21:31:56 237点赞 2913收藏 135评论

**创作立场声明：**Hello，大家好！我是Liuspy。这期将为喜爱电影的你讲一讲私人影视中心的种种玩法，海报墙、影视管理、在线流媒体播放一次全部集成。

# 一、前言

已经部署了NAS的小伙伴除了方便存储文件外，很大一部分都是电影爱好者，购买NAS的初衷就是存储和观看大量的高清影视作品。而群辉、[威联通](https://pinpai.smzdm.com/3063/)自带的影视管理器又不是太完美，总是存在各种各样的小问题。所以就有了本文为大家介绍的【Jellyfin】，利用第三方的影视类软件可以更加方便的管理我们珍藏的电影，提供完美的刮削器、海报墙、硬件解码等功能。下面我们就一起来看看【Jellyfin】能给我们带来什么样的体验，及如何部署吧。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fbf04d374514.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_2/)

# 二、搭建影视中心准备工作

在搭建家庭影视中心前我们需要做一些准备工作，目前主流的第三方影视类软件Emby、Plex和Jellyfin应该如何选择？另外使用以上的第三方影视类软件必须有一个载体平台（Windows、群晖、威联通）。由于在NAS中群晖的受众最广，本文将以群晖为基础平台讲解如何安装影视中心软件。

## 1、为什么以Jellyfin作为第三方影视中心

目前在NAS系统上搭建的第三方影视类套件必然跑不出Emby、Plex和Jellyfin这三座大山。这三款软件所能实现的功能大体都是相同的，只是在细节优化上略有不同。Emby和Plex是两款成熟的软件，在功能、美观和体验上都趋于完美，适配的各个平台的插件/app也完善一些。不过正是因为如此Emby和Plex的一些功能是收费的，只有高级会员才可以享受。这也是本次经验分享选择Jellyfin的根本原因，目前为止还可以免费使用。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fbe74d7a2179.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_3/)

Jellyfin功能上是和Emby差不多的，由于Emby3.6开始闭源后，一些核心人员出走开发了Jellyfin。并将其打造成为一款自由免费的软件媒体系统，可让您实现媒体的管理和流媒体播放。

## 2、硬件平台的选择

硬件平台我选择了群晖的DS918+，4盘位加上不错的硬件配置，可以保证绝大多数场景的使用。



京东[![img](https://y.zdmimg.com/201712/19/5a38308b5c3b02824.jpg_a200.jpg)](https://go.smzdm.com/d24c74e4c079e34a/ca_bb_yc_163_akmg5wgr_10289_2315_173_0)[**Synology 群晖 DS918+ 四盘位NAS网络存储服务器 黑色**](https://go.smzdm.com/d24c74e4c079e34a/ca_bb_yc_163_akmg5wgr_10289_2315_173_0)4680元起实时价格15小时前已更新[去购买](https://go.smzdm.com/d24c74e4c079e34a/ca_bb_yc_163_akmg5wgr_10289_2315_173_0)



▼群晖DS918+是一款定位4盘位高性能机型，采用Intel Celeron J3455处理器(睿频可高达2.3GHz)。支持4K视频硬件转码流媒体播放、虚拟机部署及Docker，性能强劲。可以满足你对NAS的所有需求。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fbec042c4286.jpg_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_4/)

▼一般而言如果预算足够的话，我还是推荐选购4盘位的机型。无论是在存储空间或是数据沉余备份的选择上都更加的灵活。4盘位机型在raid组建上支持安全性更高的Raid6模式，也可以使用raid1+2块basic磁盘模式，存储不同安全级别的文件。我目前的方案是3块4T硬盘组建raid5存储照片等重要资料+一块basic 8T存储影视文件。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fbfebe9b3869.jpg_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_5/)

▼在接口扩展方面，DS918+配置了2个千兆网口及一个esata的阵列柜扩展接口。另外在背部还有一个USB3.0接口，可以挂载[移动硬盘](https://www.smzdm.com/fenlei/yidongyingpan/)进行热备份，或连接UPS作为通信端口来使用。在机器的底部还设计有两个M2的SSD接口，可以安装SSD用了缓存加速或构建高速储存池。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fc11089f5994.jpg_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_6/)

▼DS918+采用了方方正正棱角分明的设计，简约又不失质感。不错的颜值可以随意部署而不影响美观，例如我将其放置于桌面大小也刚好合适，整个桌面非常的和谐。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc1a91745219.jpg_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_7/)

# 三、Jellyfin影视中心安装

NAS准备好后我们就可以开始Jellyfin的安装了，整个安装过程相对还是比较简单的，通过Docker进行部署，只需要简单几步就可完成。

▼首先我们需要在群晖的套件中心安装好Docker，在安装前。我们要文件管理器内的docker[文件夹](https://www.smzdm.com/fenlei/wenjianjia/)下新建一个名字叫jellyfin的文件夹。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fc2661108147.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_8/)

▼另外我们需要将这个新创建的【jellyfin文件夹】设置下权限，方便我们以后的使用。对jellyfin文件夹右键——点属性——点权限——新增——设置为everyone，将权限赋予所有人使用。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fc230a2c4519.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_9/)

▼设置完文件夹权限后，我们就可以在Docker中搜索jellyfin，选择第一项。并下载最新版本的jellyfin，整个安装包在500M左右，我们需要稍微等一会完成下载。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc37495a5718.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_10/)

▼在Docker的映像选项下，能够看到我们下载好的安装映像。点击启动——高级设置——将jellyfin和存储电影的文件夹都添加上（按照下图设置装载路径/media /config ）

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc30c4f45528.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_11/)

▼最后我们只需要再设置一下端口（使用默认8096）、勾选【使用高权限执行容器】、添加环境变量【PGID、PUID 为 0】就完成了。根据软件提示一路下一步完成docker的部署就可以了。最后我们在容器中就可以看到已经运行的jellyfin。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc3e735c7862.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_12/)

▼我们通过网页访问NAS ip地址+8096端口就可以访问jellyfin。初次使用我们先进行初始化设定，选址语言和地区，全部选择中国。然后设定登录的账号及密码，另外媒体库可以先跳过不设置，我们进入系统后再详细设定就可以啦。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc41761e2314.gif_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_13/)

▼如果你第一下登录是英文界面，不要着急按照楼主的设定，先调节成为我们最熟悉的中文界面吧。左上角图标——Dashboard——General——language，选择chinses就可以啦！

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc5640d11948.gif_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_14/)

▼最后我们对媒体库进行关联就可以愉快的使用了。媒体库的设置位置如下图所示，根据个人的需求进行勾选一些参数。我几乎所有的选项都勾选上了。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc6ac4861440.gif_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_15/)

至此一个简单的影视中心就已经构建完成。

# 四、Jellyfin使用体验

经过以上的设置后就可以初步的使用Jellyfin的影视中心功能了。不仅能够刮削获取电影封面，并且可以像[爱奇艺](https://pinpai.smzdm.com/37404/)一样在线播放视频。

▼经过一段时间对媒体库的扫描后。可以正确的识别出电影的名称，并加载电影海报及简介信息。我们可以直接对这些电影进行管理，移动删除都会在磁盘端同步设置。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fc5aa07a7663.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_16/)

▼点击电影海报可以进入影片的详细界面，显示电影的简介等信息，可以方便的查看。而且还会关联与之相关的影片推荐。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fc899a78290.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_17/)

▼当然最吸引人的还是像使用爱奇艺一样，直接在网页上观看电影。甚至设置好端口转发后，在外网也可以顺利流媒体播放影片。真正做到了和爱奇艺一样的使用效果。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fc876db73178.gif_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_18/)

▼观看影片的时候还支持转换码率进行播放。这对于外网条件下使用还是比较重要的，可以相对的降低码率，使播放更加的流畅。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fca213ea8241.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_19/)

Jellyfin除了全平台的应用、方便快捷的影视管理体验外，还可以配合Kodi来使用，效果非常的不错。可以大大增加Kodi的使用体验。Jellyfin有适配Kodi的插件包，可直接安装使用。

▼打开Kodi，依次选择设置——插件——从zip文件安装。选择我们从官方地址下载的Kodi插件的压缩包，就可完成插件库的安装了。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fce175c62998.gif_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_20/)

▼接下来我们只需要在插件中找到刚才安装的插件库，安装对应的插件包就可以。这里我们选择安装最新版本的插件0.5.1版本。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://am.zdmimg.com/202003/26/5e7c8fcb1270a501.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_21/)

▼等待插件全部下载完毕后，会自动弹出设置画面。根据提示依次输入IP地址、账号和密码、选择ADD-On、选择ALL就可以设置完成了。等待系统扫描完成数据库，展现出和web页面相同的海报墙。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fcbb85e95126.gif_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_22/)

▼为了方便演示我使用的是PC版本的Kodi，电视和盒子版本的设置方法都是相同的。设置成功后就可以同步媒体中心的影视文件了，管理和使用更加的方便快捷。

[![让NAS成为你的私人影视中心，Jellyfin+kodi如何部署](https://qnam.smzdm.com/202003/26/5e7c8fcce52c5124.png_e680.jpg)](https://post.smzdm.com/p/akmg5wgr/pic_23/)

# 五、尾声

以上就是本文的全部内容啦，通过NAS的部署可以方便电影爱好者下载、收藏、整理以及观看各种各样的大片。另外流媒体播放功能更加的强大，非常适合作为家庭影视中心来使用。

如果你对各种新奇有趣的[数码产品](https://www.smzdm.com/fenlei/diannaoshuma/)感兴趣，快关注楼主吧。未来楼主还会不断更新家庭娱乐中心的升级进化过程，带给你更多有趣的玩法！

# 一款开源免费且类似Emby的个人媒体服务器：Jellyfin

[![img](https://upload.jianshu.io/users/upload_avatars/2457033/8dbeb49b-f8a2-482b-a506-bd9385c160e4.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/7b093aebe76a)

[WMSmile](https://www.jianshu.com/u/7b093aebe76a)关注

0.3712019.03.22 15:31:18字数 990阅读 7,308

说明：目前比较火的个人媒体服务器差不多是Plex和Emby，2款都挺强大的，现在再说个最近才出来的一个媒体服务器Jellyfin，功能上是和Emby差不多的。按照官方的说法是，由于Emby 3.6开始闭源后，引起了一些核心开发人员的不满，所以最近在Emby的基础上单独开发了Jellyfin媒体服务器，致力于让所有用户都能访问最好的媒体系统。并且可以将Emby版本3.5.2及之前的数据无缝迁移过来。前景是很不错的，这里就发下搭建教程。

简介
Jellyfin是一个自由软件媒体系统，可让您控制媒体的管理和流媒体。它是专有的Emby和Plex的替代品，可通过多个应用程序从专用服务器向终端用户设备提供媒体。Jellyfin是Emby 3.5.2版本的后代，移植到.NET Core框架以支持完整的跨平台支持。没有任何附加条件，只是一个团队想要更好地构建更好的东西并共同努力实现它，致力于让所有用户都能访问最好的媒体系统。

[官方教程](https://links.jianshu.com/go?to=https%3A%2F%2Fjellyfin.org%2Fdocs%2Fgeneral%2Fadministration%2Finstalling.html)

截图



![img](https://upload-images.jianshu.io/upload_images/2457033-695ba4cfabd65cb4?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

在这里插入图片描述



![img](https://upload-images.jianshu.io/upload_images/2457033-5bce0750ab4d2e2d?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

在这里插入图片描述



![img](https://upload-images.jianshu.io/upload_images/2457033-0a2773012673b619?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

在这里插入图片描述



![img](https://upload-images.jianshu.io/upload_images/2457033-2eaef46819758ca9?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

在这里插入图片描述

更新
【2019.2.19】
官方新增多系统软件包，更新安装方法
安装
Github地址：[https://github.com/jellyfin/jellyfin](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fjellyfin%2Fjellyfin)

Jellyfin客户端：[https://jellyfin.readthedocs.io/en/latest/user-docs/apps/](https://links.jianshu.com/go?to=https%3A%2F%2Fjellyfin.readthedocs.io%2Fen%2Flatest%2Fuser-docs%2Fapps%2F)

这里主要说Linux系统的安装方法；Windows系统直接下载文件就行了，下载地址→传送门。

Linux系统的安装方法有3种，使用软件库、软件包、Docker安装。

1、使用软件库安装
该方法适用于Debian 8+和Ubuntu 14.04+。

导入GPG签名密钥：



```csharp
#安装依赖
sudo apt install apt-transport-https

#Debian系统
wget -O - https://repo.jellyfin.org/debian/jellyfin_team.gpg.key | apt-key add -

#Ubuntu系统
sudo add-apt-repository universe
wget -O - https://repo.jellyfin.org/ubuntu/jellyfin_team.gpg.key | sudo apt-key add -
```

配置存储库：



```bash
#先看下面的说明，然后修改为相应的版本号，再运行下面的命令
#Debian系统
echo "deb [arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/debian $( lsb_release -c -s ) main" | sudo tee /etc/apt/sources.list.d/jellyfin.list
#Ubuntu系统
echo "deb [arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/ubuntu $( lsb_release -c -s ) main" | sudo tee /etc/apt/sources.list.d/jellyfin.list
#这里的<release>为系统版本号，相对应的如下：
Debian 8为jessie
Debian 9为stretch
Debian 10为buster
Ubuntu 14为trusty
Ubuntu 16为xenial
Ubuntu 18.04为bionic
Ubuntu 18.10为cosmic
```

最后安装Jellyfin:



```bash
#更新存储库
apt update
#安装依赖
apt install apt-transport-https -y
#安装jellyfin
apt install jellyfin -y
#启动jellyfin
service jellyfin start
```

然后就可以通过ip:8096访问该媒体库了。端口可以在面板里自行修改。



```bash
#相关使用命令
重启程序：service jellyfin restart
查看状态：service jellyfin status
开机自启：systemctl enable jellyfin
```

2、使用软件包安装
首先下载软件包，下载地址→传送门，目前支持系统有Win、Mac、Arch等Linux，然后根据自己的系统进行选择，下面以最新版10.2.2为例，如果软件包地址404，可以向博主反馈更新。

CentOS系统：



```csharp
#安装依赖
yum install libicu fontconfig -y
#安装软件包
rpm -Uvh --nodeps https://repo.jellyfin.org/releases/server/centos/stable/server/jellyfin-10.6.4-1.el7.x86_64.rpm
#启动jellyfin
service jellyfin start
#查看状态
service jellyfin status

#CentOS 6开机自启
chkconfig jellyfin on
#CentOS 7开机自启
systemctl enable jellyfin
Debian 8+和Ubuntu 14.04+系统：

#Debian下载软件包
wget https://repo.jellyfin.org/releases/server/debian/stable/server/jellyfin-server_10.6.4-1_amd64.deb
#Ubuntu下载软件包
wget https://repo.jellyfin.org/releases/server/ubuntu/stable/server/jellyfin-server_10.6.4-1_amd64.deb

#更新系统
apt update
#安装依赖
apt install at libsqlite3-0 libfontconfig1 libfreetype6 libssl1 -y
#安装软件包
dpkg -i jellyfin_*.deb
#如果报错，再自动修复并安装下依赖和软件
apt -f install -y
#查看状态
service jellyfin status
#开机自启
systemctl enable jellyfin
```

> 注：不用版本的wget 包的地址 可以参考 [https://repo.jellyfin.org/releases/server/](https://links.jianshu.com/go?to=https%3A%2F%2Frepo.jellyfin.org%2Freleases%2Fserver%2F) 查看替换

然后就可以通过ip:8096访问该媒体库了。程序管理命令参考上面的就行了。

一般CentOS和Ubuntu是没安装ffmpeg的，先使用命令ffmpeg -version检查下ffmpeg是否存在，不存在的使用命令：

[linux安装请看这里](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.csdn.net%2Fwm9028%2Farticle%2Fdetails%2F108448676)

Ubuntu



```csharp
sudo apt-get install -y software-properties-common
add apt-repository ppa:mc3man/trusty-media

apt-get update
apt-get dist-upgrade


apt-get install ffmpeg


ffmpeg -version
```

[linux安装请看这里](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.csdn.net%2Fwm9028%2Farticle%2Fdetails%2F108448676)

3、使用Docker安装
安装Docker：



```csharp
#CentOS 6
rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
yum update -y
yum -y install docker-io
service docker start
chkconfig docker on


#CentOS 7、Debian、Ubuntu
curl -sSL https://get.docker.com/ | sh
systemctl start docker
systemctl enable docker.service
```

再拉取镜像：



```jsx
docker run -d -p 8096:8096 -v /jellyfin/config:/config -v /jellyfin/media:/media jellyfin/jellyfin
```

以上命令默认的程序访问地址为ip:8096，配置文件夹为/jellyfin/config，媒体库文件夹为/jellyfin/media。

如果你想修改上面的端口和路径的话，直接修改-p和-v所指的前面的参数即可，照葫芦画瓢就行了。

如果你是CentOS系统，打不开媒体界面的话，还需要开启防火墙端口，使用命令：



```csharp
#CentOS 6
iptables -I INPUT -p tcp --dport 8096 -j ACCEPT
service iptables save
service iptables restart

#CentOS 7
firewall-cmd --zone=public --add-port=8096/tcp --permanent
firewall-cmd --reload
```

如果你开了端口还不能打开，可能还需要去服务商后台开启对应的端口。

最后安装好了，就自行去后台设置，转码那里还需要你填上ffmpeg路径，一般为/usr/bin，可使用which ffmpeg查看路径。关于从Emby 3.5.2及之前的版本无缝迁移到Jellyfin的教程可以查看→传送门，然后其它的就自行折腾下。
[官方教程](https://links.jianshu.com/go?to=https%3A%2F%2Fjellyfin.org%2Fdocs%2Fgeneral%2Fadministration%2Finstalling.html)