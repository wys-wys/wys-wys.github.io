# Docker 搭建我的世界私服

[![img](https://upload.jianshu.io/users/upload_avatars/1059552/db0dbe6584e7?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/129da6b27afa)

[Mr_LiTong](https://www.jianshu.com/u/129da6b27afa)关注

0.0742018.09.18 16:26:31字数 73阅读 4,826

#### 启动器

[HMCL启动器(GitHub)](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fhuanghongxun%2FHMCL)

[HMCL启动器[官网\]](https://links.jianshu.com/go?to=https%3A%2F%2Fhmcl.huangyuhui.net%2F)

#### Java JDK

[Java JDK下载](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.oracle.com%2Ftechnetwork%2Fjava%2Fjavase%2Fdownloads%2Findex.html)

#### Mod仓库

[MC百科](https://links.jianshu.com/go?to=http%3A%2F%2Fmcmod.cn)

#### Docker搭建我的世界私服



```ruby
//同意协议 -e EULA=TRUE
//指定端口 -p 25565:25565
//指定挂载位置 -v /Users/litong/Desktop/Docker/Minecraft:/data
//指定版本 -e VERSION=1.12.2
docker run -d -p 25565:25565 \
-v /Users/litong/Desktop/Docker/Minecraft:/data \
-e EULA=TRUE \
-e VERSION=1.12.2 \
--name=mc \
itzg/minecraft-server
```

#### Docker搭建我的世界私服并开启Forge插件



```ruby
//通过-e TYPE=FORGE在命令行中添加来启用Forge服务器模式
//默认情况下，容器将运行Forge服务器的RECOMMENDED版本， 但您也可以选择使用运行特定版本。-e FORGEVERSION=10.13.4.1448
docker run -d -p 25565:25565 \
-v /Users/litong/Desktop/Docker/Minecraft:/data \
-e EULA=TRUE \
-e VERSION=1.12.2 \
-e TYPE=FORGE \
--name=mc \
itzg/minecraft-server

//要从自定义位置（例如您自己的文件存储库）下载Forge安装程序
docker run -d -p 25565:25565  -v /root/桌面/Minecraft:/data -e EULA=TRUE -e VERSION=1.12.2 -e TYPE=FORGE -e FORGE_INSTALLER_URL=http://HOST/forge-1.11.2-13.20.0.2228-installer.jar --name=mc itzg/minecraft-server

//使用预下载的Forge安装程序，将其放置在附件/data目录中，并使用来指定安装程序文件的名称FORGE_INSTALLER
docker run -d -p 25565:25565  -v /root/桌面/Minecraft:/data -e EULA=TRUE -e VERSION=1.12.2 -e TYPE=FORGE -e FORGE_INSTALLER=forge-1.12.2-14.23.5.2768-installer.jar --name=mc itzg/minecraft-server
```

#### 配置服务器

[server.properties配置说明](https://links.jianshu.com/go?to=https%3A%2F%2Fminecraft-zh.gamepedia.com%2FServer.properties)



```cpp
//打开server.properties文件

//定义世界名称及其文件夹名称。
//你也可以把你已生成的世界存档复制过来，
//然后让这个值与那个文件夹的名字保持一致，
//服务器就可以载入该存档。
level-name=我的世界

//为你的世界定义一个种子
level-seed=34525

//是否开启在线验证
online-mode=false

//是否允许PvP
pvp=true
```

#### 开启和关闭服务



```ruby
//打印日志
docker logs -f mc ( Ctrl-C to exit logs action )
//关闭服务
docker stop mc
//开启服务
docker start mc
```

#### 设置管理员



```bash
# 打开ops.json文件，添加管理员
[
  {
    "uuid": "用户1的uuid",
    "name": "用户1名称",
    "level": 4,
    "bypassesPlayerLimit": false
  },
  {
    "uuid": "用户2的uuid",
    "name": "用户2名称",
    "level": 4,
    "bypassesPlayerLimit": false
  }
]
```



1人点赞



[服务器](https://www.jianshu.com/nb/29352117)



更多精彩内容下载简书APP

"小礼物走一走，来简书关注我"

赞赏支持还没有人赞赏，支持一下

[![  ](https://upload.jianshu.io/users/upload_avatars/1059552/db0dbe6584e7?imageMogr2/auto-orient/strip|imageView2/1/w/100/h/100/format/webp)](https://www.jianshu.com/u/129da6b27afa)

[Mr_LiTong](https://www.jianshu.com/u/129da6b27afa)

总资产1 (约0.11元)共写了1.0W字获得18个赞共10个粉丝

关注

### 全部评论0只看作者按时间倒序按时间正序

### 推荐阅读[更多精彩内容](https://www.jianshu.com/)

- [使用docker搭建游戏私服之win7下部署docker环境](https://www.jianshu.com/p/06009c2fa7f2)

  最近在忙着搭建游戏私服的事情，因此前面的关于游戏业务篇师徒系统的内容会迟一点写，这个坑怎么说都还是要填的，不要错过...

  [![img](https://upload.jianshu.io/users/upload_avatars/3981501/5254b174d90e.png?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)codjust](https://www.jianshu.com/u/8806a8abfdf5)阅读 5,334评论 0赞 14

  ![img](https://upload-images.jianshu.io/upload_images/3981501-a2df9bf080600c04.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)

- [Linux下搭建带mod的Minecraft服务器](https://www.jianshu.com/p/89f14756d16c)

  前言   Minecraft，中文翻译为我的世界，是一款老少皆宜的游戏，高中时期室友用手机玩，我也入了这个坑，后来...

  [![img](https://upload.jianshu.io/users/upload_avatars/7875603/08ae0111-1e2e-4ac9-8cc8-bf0b6ecd9def.png?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)crossous](https://www.jianshu.com/u/50094e11ed08)阅读 15,238评论 0赞 4

  ![img](https://upload-images.jianshu.io/upload_images/7875603-e9fac697f9cbf278.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)

- [深入理解docker虚拟化](https://www.jianshu.com/p/afff1630fde9)

  1.Docker简介 1.1 什么是虚拟化 在计算机中，虚拟化（英语：Virtualization）是一种资源管理...

  [![img](https://upload.jianshu.io/users/upload_avatars/16258760/1d7f3bc3-2f12-4591-ab44-ea6b920cc1cf?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)EdwinGates](https://www.jianshu.com/u/d4ee8f0acc1c)阅读 1,224评论 0赞 0

  ![img](https://upload-images.jianshu.io/upload_images/16258760-ec8b730ebf2fd2d3.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)

- [使用Docker搭建Hadoop集群](https://www.jianshu.com/p/dd8a13ffc08a)

  前言 我是按照docker环境下搭建hadoop集群(ubuntu16.04 LTS系统）这篇博客来搭建的，然后遇...

  [![img](https://upload.jianshu.io/users/upload_avatars/6168671/0440c699-e6b8-43c1-8eb1-5e8f213d8977.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)Azur_wxj](https://www.jianshu.com/u/7ae4bcde0f80)阅读 317评论 0赞 0

  ![img](https://upload-images.jianshu.io/upload_images/6168671-9edf70fcf9a92bfa.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)

- [喜报| 热烈庆祝我餐厅荣获“西安市文明餐桌行动”示范单位称号，服务员陈英荣获“服务之星”称号](https://www.jianshu.com/p/9dc7d7517995)

  接西安市教委授权，经市文明办、市商务局、市工商局、市旅游局、市食品药监局五家职能部门联合评比，我餐厅在陕西省...

  [![img](https://cdn2.jianshu.io/assets/default_avatar/2-9636b13945b9ccf345bc98d0d81074eb.jpg)胡萝卜炖了个小白兔](https://www.jianshu.com/u/ef15ba1f515e)阅读 103评论 0赞 2

  ![img](https://upload-images.jianshu.io/upload_images/3076266-8935c6f17cd6b932.JPG?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)

[![img](https://upload.jianshu.io/users/upload_avatars/1059552/db0dbe6584e7?imageMogr2/auto-orient/strip|imageView2/1/w/90/h/90/format/webp)](https://www.jianshu.com/u/129da6b27afa)

[Mr_LiTong](https://www.jianshu.com/u/129da6b27afa)

关注

总资产1 (约0.11元)

[App Store 隐私政策网址(URL)](https://www.jianshu.com/p/430534146224)

阅读 84

[技术支持网址(URL)](https://www.jianshu.com/p/773aa74168a2)

阅读 512

群辉Docker搭建Minecraft服务器

百度看我干嘛你要GG了 2018-10-08 21:08:08  9200  收藏 4
分类专栏： Docker
版权
    早就想拥有自己的mc服务器了,无奈囊中羞涩没钱买.就萌生了用自己的黑裙搭建mc服务器的想法,而Docker的出现让这一切变得可行.废话不多说直接上教程:

安装Docker

这个不用多说



Docker中安装mc服务器镜像,并配置

镜像安装这个版本的（其他的还在研究）



其他的基本就是常规创建容器操作，个人根据自己的nas情况选择配置。下面是我的配置



并且开启服务查看对应的日志





下面我们测试连接服务器



这时会报错



这是由于默认开启了正版验证才失败的下面我们需要关闭正版检验

修改配置文件,关闭正版验证(重点)

首先进到自己的mc服务器的控制台，点击新建



使用ls命令获取文件目录，会有一个server.properties的文件



Linux一般使用vi或者vim命令修改文档，我们使用vi命令测试一下



同样的vim也是不支持的，这时我们需要自己安装vim。在控制台中执行以下代码apt-get install vim，提示是否继续时执行Y



等待一会儿就安装好了



下面开始修改server.properties文件，执行vi server.properties命令，键入i进入insert模式开始修改文件。找到online-mode=true将true改成false，



修改完成按ESC退出编辑模式，使用“：”命令进入底线命令模式执行w保存文件，再使用“：”命令进入底线命令执行q退出然后重启容器。再连接试试，注意重启后端口会变注意修改



到这就就可以愉快的玩耍了，有其他镜像玩法的小伙伴也可以联系我，欢迎交流。

 

 

当前位置： 

[社区首页 ](https://post.smzdm.com/)

 

[电脑数码 ](https://post.smzdm.com/fenlei/diannaoshuma/)

 

[存储设备 ](https://post.smzdm.com/fenlei/cunchushebei/)

 

[网络存储 ](https://post.smzdm.com/fenlei/wangluocunchu/)

 

[NAS存储 ](https://post.smzdm.com/fenlei/nascunchufuwuqi/)

 

文章详情

![img](https://qna.smzdm.com/202012/19/5fdd9fbf2df175598.jpg_fo742.jpg)

# 利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）

2020-12-19 18:01:53 22点赞 148收藏 36评论

## 前言

[群晖](https://pinpai.smzdm.com/2315/)docker中安装mc[服务器](https://www.smzdm.com/fenlei/fuwuqi/)的方法有好几种，但是总归来说要么是直接使用docker中mc服务器镜像，要么是使用linux虚拟机，在虚拟机中搭建服务器，本文选择第二种方法，这种方法操作起来比前者稍微复杂一丢丢，但是可自定义程度高且技术通用，理解后基本可以直接在常规服务器上搭建，脱离群晖docker的初级方法。![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/43.png)

## 前提准备：

1、装好docker套件的群晖NAS一台（未安装则在套件中心中搜索安装）

2、Minecratf服务器端文件（可在各个论坛及网络下载各种类型服务器，文中附官方java版下载地址）

3、可设置端口转发的[路由器](https://www.smzdm.com/fenlei/luyouqi/)一台（不用多说了）![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/45.png)

## 安装教程： 

### 一、安装Centos虚拟机 

我们打开群晖docker套件，点击“**注册表**”，不出意外第二行就是centos，没找到也可以搜索。双击或右键下载此映像。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd774aa4a5d2606.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_2/)

等待下载完成后点击左侧“**映像**”，选择centos，点击启动看到如下界面。容器名称可以随意设置，我就保持默认了，“**使用高权限执行容器**”以及“**启用资源限制**”都是开不开无所谓的选项，我这里不勾选。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd78bcaca9a1256.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_3/)

点击“**高级设置**”，看到如下界面，我们主要关注“**卷**”和“**端口设置**”这两个项目。

“**启动自动重新启动**”可选可不选，我不需要mc的服务器一直待机，只是我想和朋友一起玩的时候手动开启，因此这个我是不选的。

“**创建桌面快捷方式**”同样可选可不选。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd7a33e8f247144.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_4/)

接下来点击“**卷**”，点击“**添加[文件夹](https://www.smzdm.com/fenlei/wenjianjia/)**”可以看到如下界面，我们在docker中新建一个“**Minecraft**”文件夹，点击“**选择**”。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://am.zdmimg.com/202012/19/5fdd7b52721808246.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_5/)

linux目录结构中用户目录分为“**/root”**系统管理员目录以及“**/home**”存放用户个人数据的目录，因此我们的“**装载目录**”填写“**/home/mc**”即可，当然选择其他目录也是完全没有问题的。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd890613bb27980.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_6/)

之后我们点击“**端口设置**”，服务器的默认端口是25565，后面也可以进行修改，但是这一步我们先按照默认的来，点击“**+**”新增如图所示端口设置。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd89e1734b06535.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_7/)

之后点击“**应用**”→“**下一步**”，检查一下设置没有问题的话就可以应用了，我这里已经有一个了，所以端口冲突，我个人稍微修改一下端口以及文件夹![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/79.png) 。点击“**容器**”，看到已经运行的centos就说明顺利完成了虚拟机的安装和配置了，接下来就要安装服务器了。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd8c13d03735999.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_8/)

### 二、安装及配置Minecraft服务器

首先选中这个已运行的centos1，点击“**详情**”，再点击“**终端机**”即可进入控制台。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd8c23a50c47216.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_9/)

看了下这个centos版本为centos8，我们首先进行换源，要不然后面的操作太慢了。提示一下，我们可以先按“**Ctrl + A**”进入前缀模式，再使用“**Ctrl + C**”以及“**Ctrl + V**”进行复制粘贴。![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/77.png)

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd8e1d4b2387816.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_10/)

> 1、cd /etc/yum.repos.d/

> 2、rm -f CentOS-Base.repo CentOS-AppStream.repo CentOS-PowerTools.repo CentOS-centosplus.repo CentOS-Extras.repo

> 3、curl -o CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-8.repo

> 4、yum makecache

这里换的是阿里源，按照顺序分别输入命令，最终换源成功。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd8ece0a2679370.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_11/)

之后我们对yum进行更新操作，途中遇到[y/N]就输入“**y”**并按回车，由于换过源，这里下载应该非常快，之后等待更新完成即可。（如果下载过程非常慢可以尝试重新更换源或者更换其他源）

> yum update

[![输入“y”并回车](https://qnam.smzdm.com/202012/19/5fdd901af30484726.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_12/)输入“y”并回车

当屏幕上出现“**Complete！**”字样时就可以进行下一步了。

安装java1.8.0，当然选择其他版本也可以，我个人电脑也是1.8.0为了保持一致性选择1.8.0。另外如果你觉得当前屏幕显示东西太多太乱可以按“**Ctrl + L**”清屏。输入以下命令同时也是一路“**yes**”即可，等待安装完成。

> yum -y install java-1.8.0-openjdk*

同样，当屏幕上出现“**Complete！**”字样时就可以进行下一步了。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9331f3c3a4653.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_13/)

此时其实就可以上传服务器文件并且运行了，但这并不是个明智的选择，因为根据官方文件我们每次都需要输入很长的命令，因此我们这样做，首先在文件目录即“**/docker/Minecraft**”里创建一个新建文本文档并输入以下命令。（我这里演示的是流程所以之前改过文件夹“**/docker/MC**”）

> java -Xmx2048M -Xms1024M -jar minecraft_server.1.16.4.jar nogui

这里“**-Xmx2048M**”代表给服务器分配最大内存为2G，“**-Xms1024M**”代表分配最小内存为1G，“**minecraft_server.1.16.4.jar**”是服务器端包的名称，你也可以替换成自己从网上下来的各种其他服务器包，后面就不再强调这一点了。保存后我们将“**新建文本文档.txt**”改为“**run.sh**”。

接着我们去官网下载一份服务器端包，并将其放入“**/docker/Minecraft**”。DSM里上传也好，局域网拖进去也好，不管用什么方法，总之放到目录里即可。![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/22.png)

https://www.minecraft.net/zh-hans/download/server

之后把下载下来的“**serve.jar**”改为“**minecraft_server.1.16.4.jar**”，也就是run.sh中的服务器包名称，当然你改run.sh也是没问题的。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9639616cd7059.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_14/)

我们输入以下命令进入“/docker/Minecraft”并查看文件，如图所示。（我的目录是“**/docker/mc**”后面不再提了）

> cd /home/Minecraft

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd97982f0f59312.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_15/)

接着我们输入如下命令，会提示失败，不用担心，第一次是释放文件必定失败的。![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/36.png)

> ./run.sh

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd98930448a7356.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_16/)

提示我们去同意EULA，我们用电脑进入“/docker/Minecraft”目录打开“**eula.txt**”,将“**eula=false**”改为“**eula=true**”并保存。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd99799ced52624.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_17/)

接着不要急，**这一步是重点！！！**使用[记事本](https://www.smzdm.com/fenlei/bijiben/)或其他软件打开“**server.properties**”文件，这里可以对服务器端进行诸如“游戏难度”、“是否生成村名”、“服务器最大人数”等等设置，我们找到“**online-mode=true**”这一行并改为“**online-mode=false**”，以关闭正版验证，这样你还可以和使用启动器的朋友一起玩耍。![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/32.png)

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9b0f33a249389.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_18/)

到这里服务器端的安装和配置就完成了，接下来在路由器设置端口转发，毕竟不太可能大家都在局域网里玩吧。![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/57.png)

这里的教程站内外都有很多我就不详述了。

### 三、启动并连接服务器

在上述的设置完成后我们再返回“**终端机**”中，再次输入“**./run.sh**”就会看到服务器正在进行地图的创建等操作，第一次启动会比较慢，耐心等待即可，当我们看到“**Done**”字样的时候就运行完毕了。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9d1722d138090.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_19/)

我们打开游戏并点击“**多人游戏**”，“**服务器名称**”随便设置一个即可，“**服务器地址**”输入“你的群晖ip或域名:25565（端口号）”即可，我这里端口是25564，点击“**完成**”。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9e105d7c61816.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_20/)

可以看到以及连接成功，如果没成功可以等待一会或者重新启动游戏。

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9e107db0c2004.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_21/)

最后将你的服务器地址告诉你的小伙伴们并且一起快乐游戏吧！祝大家玩得愉快！![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/35.png)

[![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://qnam.smzdm.com/202012/19/5fdd9e101e8f36480.jpg_e680.jpg)](https://post.smzdm.com/p/a25dlvqn/pic_22/)

感谢看到这里的各位，欢迎各位点赞收藏转发评论支持一下，有疑问的话欢迎大家下方留言讨论！![利用群晖docker搭建Minecraft服务器：图形界面操作，傻瓜式教程（附官方服务器端地址）](https://res.smzdm.com/images/emotions/38.png)