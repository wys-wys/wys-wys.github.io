# 怎么在Linux搭建一个可以装mod的Minecraft服务器（我的世界）

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[守望时空33](https://blog.csdn.net/yanhanhui1) 2020-02-03 15:43:56 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 8650 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 33

分类专栏： [笔记](https://blog.csdn.net/yanhanhui1/category_9567735.html) [Java](https://blog.csdn.net/yanhanhui1/category_7687685.html) [Linux](https://blog.csdn.net/yanhanhui1/category_9087635.html) 文章标签： [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [服务器](https://www.csdn.net/tags/MtTaEg0sNDcxOTgtYmxvZwO0O0OO0O0O.html) [我的世界](https://so.csdn.net/so/search/s.do?q=我的世界&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

  我的世界多人联机、协作是最有意思的玩法。那么怎么搭建一个可以装mod的我的世界服务器呢？

需要的软件及工具：

1，xshell和xftp（远程服务器连接与文件传输）：[官网下载](https://www.netsarang.com/zh/xshell-download/)

​                          或者FinalShell：[官网下载](http://www.hostbuf.com/)

2，我的世界服务端核心：[https://s3.amazonaws.com/Minecraft.Download/versions/版本号/minecraft_server.版本号.jar](https://s3.amazonaws.com/Minecraft.Download/versions/1.12.2/1.12.2.jar)

（例如我要下载1.7.10的，就把链接改为：https://s3.amazonaws.com/Minecraft.Download/versions/1.7.10/minecraft_server.1.7.10.jar） [备用地址](https://www.lanzous.com/b0bq75owb)

3，forge：[官网下载](http://files.minecraftforge.net/) [备用地址](https://www.lanzous.com/b0bq75oxc)

4，java运行环境Linux版：[官网下载](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8u211-later-5573849.html)

### 一、租一台服务器

  目前[阿里云](https://www.aliyun.com/)，[腾讯云](https://cloud.tencent.com/)，[百度云](https://cloud.baidu.com/)等等国内服务器提供商，以及[vultr](https://www.vultr.com/)等等国外服务器提供商都很好，大家可以自行选择。一般选择产品里面的云服务器即可。

### 二、安装xshell和xftp

在前面的官网下载地址下载xshell与xftp。需要填写你的邮箱，下载链接会发到你的邮箱。

### 三、远程连接服务器

租好服务器后，你可以从服务器供应商的控制台里面找到你的服务器并查看其ip，登录账号（一般是root），密码等等。

使用xshell连接：

![img](https://img-blog.csdnimg.cn/20200203130134739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20200203130319308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

 再连接，会让你输入用户名，填root：

![img](https://img-blog.csdnimg.cn/20200203131451837.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

后面要你输密码，填服务器供应商给的密码。然后连接完成！

### 四、下载java运行环境并上传至服务器并配置

先在上面给的java官网下载链接里面，找到linux的jdk，下载：

先注册登录oracle账号：

![img](https://img-blog.csdnimg.cn/20200203131826184.png)

 在找到下面Java SE Development Kit 8u...一栏，点击Accept License Agreement同意协议，并下载linux对应的64位jdk：

![img](https://img-blog.csdnimg.cn/20200203132002111.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

然后点击xshell上面的xftp图标，用xftp连接至服务器：

 ![img](https://img-blog.csdnimg.cn/20200203132107621.png)

 

![img](https://img-blog.csdnimg.cn/20200203132133505.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)连接完成

 把下载的jdk压缩包拖进去（右边一栏为服务器的文件）上传：

然后刷新，便可以在xftp里面看到文件了。

再回到xshell，输入以下命令解压jdk：

```bash
tar zxvf "文件路径"
```

可以在xftp里面右键-复制路径以获取文件路径。

![img](https://img-blog.csdnimg.cn/20200203132720564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

例如我的：

![img](https://img-blog.csdnimg.cn/20200203132759352.png)

解压完成，在xftp里面刷新即可看到解压出来的文件夹。

再在xftp里面进入/etc目录，找到profile文件，右键用记事本编辑：

![img](https://img-blog.csdnimg.cn/20200203133158317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

在最后加上以下内容以配置我们的java环境变量：

 

```bash
export JAVA_HOME=你的jdk根目录



export JRE_HOME=你的jdk根目录/jre



export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib



export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```

例如我的：

![img](https://img-blog.csdnimg.cn/20200203133624370.png)

 保存。

在找到/root目录下面的.bashrc文件(如果看不到就在xftp工具-选项里面勾选显示隐藏的文件），右键用记事本编辑，最底下加上：

```bash
source /etc/profile
```

保存。

返回xshell，也输入：

```bash
source /etc/profile
```

再输入java看看会不会输出相关内容。如果有则说明配置成功！

![img](https://img-blog.csdnimg.cn/20200203134149174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

###  五、上传我的世界服务器核心，forge

建议在xftp里面专门建立一个文件夹存放我的世界服务器核心及forge，然后cd进去，例如我的:

![img](https://img-blog.csdnimg.cn/20200203134410761.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

 ![img](https://img-blog.csdnimg.cn/20200203134437459.png)

下载我的世界服务器核心和forge的universal版，上面有地址（都是jar文件）：

 

![img](https://img-blog.csdnimg.cn/20200203134914105.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)forge下载

然后把两者全部上传至我们刚刚建的服务器核心文件夹。

![img](https://img-blog.csdnimg.cn/20200203140956648.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

# 注意：服务端核心的文件名千万不能改！否则后面无法运行forge加载mod！

然后，我们还要把一些运行库也上传到服务器核心文件夹里面，找到你们玩的我的世界电脑端里面.minecraft文件夹里面的libraries文件夹，整个文件夹上传至服务器核心文件夹：

![img](https://img-blog.csdnimg.cn/20200203140019981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20200203141008293.png)

然后，先在xshell运行一次服务器核心：

```bash
java -Xms256M -Xmx512M -jar "服务器核心文件路径" nogui



//-Xms后面接的是最小分配内存，-Xmx最大分配内存，根据你们服务器的内存大小自行决定
```

 如我的：

![img](https://img-blog.csdnimg.cn/20200203141220367.png)

再在xftp里面刷新，发现多了个 eula.txt，用记事本编辑，把里面的eula=false改为eula=true

再次运行上面命令，运行服务端核心。

此时程序会一直执行不会退出，可以后面看到加载地图的百分比，显示done便是加载完毕，再输入stop回车，退出。

![img](https://img-blog.csdnimg.cn/20200203141601158.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

再在xftp里面刷新，发现服务端核心文件夹里面生成许多文件。找到server.properties，右键记事本编辑，修改服务器参数：

我们一般要把online-mode后面改成false，否则非正版玩家无法进入。其它参数按需修改：

![img](https://img-blog.csdnimg.cn/20200203142137615.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

 现在，就要运行forge以配置了。现在第一次运行一下forge让其生成配置文件。

先输入以下指令：

```bash
java -Xms256M -Xmx512M -jar "forge路径" nogui
```

同样的，显示done后输入stop退出。

![img](https://img-blog.csdnimg.cn/20200203142727169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

xftp里面刷新，发现多了个mods文件夹，把需要的mod上传上去。注意，小地图，g键合成表，生物雷达，TMI内置修改器这种辅助插件型mod不要上传，否则服务器可能无法开启。

![img](https://img-blog.csdnimg.cn/20200203143022165.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmhhbmh1aTE=,size_16,color_FFFFFF,t_70)

再用上面命令执行一次forge，即可运行服务器了！

 这个时候，打开游戏，多人游戏，添加服务器，地址填：你的服务器外网地址:服务器端口

例如：47.12.33.142:25565

然后就行了！

但是我们关了xshell窗口会导致服务器也关掉，怎么使其后台运行呢？这里我用screen软件。

screen是linux上的一款软件，用于管理会话。

先stop关闭服务端，然后安装screen。

Debian安装：

```bash
apt-get install screen
```

CentOS安装：

```bash
yum install screen
```

`screen -ls`显示当前所有screen创建的窗口，此时我们还没有创建。
再`screen -S <窗口名>`创建一个名为‘窗口名’的窗口。

例如screen -S mc

输入screen -r mc挂载上创建的screen。

再输入：

```bash
java -Xms256M -Xmx512M -jar "forge路径" nogui
```

执行forge启动服务器。 

用xshell再创建一个窗口，还是连上你的服务器，再输入：

```bash
screen -d mc
```

使我们的窗口与主进程分离，这样就后台运行了！

以后再进入是：

```bash
screen -r mc
```

用完了记得再screen -d分离一下才行。 

注意，以后如果stop了服务器，再次开启是执行forge程序而不是服务端核心！

如果想重新生成世界，把服务端关闭，然后删除服务端文件夹里面的world文件夹，再运行forge开启，便会自动生成地图