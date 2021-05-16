573_玩客云安装qbittorrent

grey_csdn 2021-03-21 11:38:14  31  收藏 1
分类专栏： Linux 树莓派
版权
全部学习汇总：https://github.com/GreyZhang/little_bits_of_linux

工具安装比较简单，但是网络上看到很多说法说这个得安装docker。关于工具的安装，直接执行如下命令：

apt-get install qbittorrent-nox

安装成功之后，运行

qbittorrent-nox -d

之后，可以通过8080端口在浏览器中访问。访问的方式可以使用Ip，也可以使用主机名。访问的效果如下：

# 573_玩客云安装qbittorrent

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[grey_csdn](https://greyzhang.blog.csdn.net/) 2021-03-21 11:38:14 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 31 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [Linux](https://blog.csdn.net/grey_csdn/category_6639467.html) [树莓派](https://blog.csdn.net/grey_csdn/category_7277647.html)

版权

全部学习汇总：https://github.com/GreyZhang/little_bits_of_linux

工具安装比较简单，但是网络上看到很多说法说这个得安装docker。关于工具的安装，直接执行如下命令：

apt-get install qbittorrent-nox

安装成功之后，运行

qbittorrent-nox -d

之后，可以通过8080端口在浏览器中访问。访问的方式可以使用Ip，也可以使用主机名。访问的效果如下：

![img](https://img-blog.csdnimg.cn/2021032111373859.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZXlfY3Nkbg==,size_16,color_FFFFFF,t_70)

输入账号密码即可使用，账号admin，密码adminadmin。登录之后的效果：

![img](https://img-blog.csdnimg.cn/20210321113738128.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZXlfY3Nkbg==,size_16,color_FFFFFF,t_70)



可以添加链接或者BT种子来下载资源。

![img](https://img-blog.csdnimg.cn/20210321113738132.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZXlfY3Nkbg==,size_16,color_FFFFFF,t_70)

这个比较好的一个功能其实在空白方框下面写了，每行一个链接，这个也就意味着其实是可以多个链接一次写入搞定的。我试了一下，的确是可以的。

![img](https://img-blog.csdnimg.cn/20210321113738129.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dyZXlfY3Nkbg==,size_16,color_FFFFFF,t_70)



只是可能我测试的链接质量一般，一直没有下载的速度。不过，默认情况下有3个下载任务，我们倒是可以选中全部之后来一个强制恢复让所有的开启下载。经过了这么一轮操作，我现在尝试的资源已经有了几个文件至少是有速度了。

看了别人的经验，很多人的资源都是能够跑满带宽的。说实话，这样的资源我试了一阵子是没找到的，唯一还可以的能够大概1/4带宽跑满。类似的工具安装，在树莓派上也是一致的。

输入账号密码即可使用，账号admin，密码adminadmin。登录之后的效果：




可以添加链接或者BT种子来下载资源。



这个比较好的一个功能其实在空白方框下面写了，每行一个链接，这个也就意味着其实是可以多个链接一次写入搞定的。我试了一下，的确是可以的。




只是可能我测试的链接质量一般，一直没有下载的速度。不过，默认情况下有3个下载任务，我们倒是可以选中全部之后来一个强制恢复让所有的开启下载。经过了这么一轮操作，我现在尝试的资源已经有了几个文件至少是有速度了。

看了别人的经验，很多人的资源都是能够跑满带宽的。说实话，这样的资源我试了一阵子是没找到的，唯一还可以的能够大概1/4带宽跑满。类似的工具安装，在树莓派上也是一致的。