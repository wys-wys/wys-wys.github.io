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

 

 