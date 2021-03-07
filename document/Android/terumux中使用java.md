![把安卓手机性能发挥到极致之-Termux运行Java及性能测试](https://pic1.zhimg.com/v2-5dc9141b4946abc0e8e62d71c28b4e91_1440w.jpg?source=172ae18b)

# 把安卓手机性能发挥到极致之-Termux运行Java及性能测试

[![myastrotong](https://pic1.zhimg.com/v2-630280f8f6d2060f01810f0a1fc2ea18_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/tang-kong-wen)

[myastrotong](https://www.zhihu.com/people/tang-kong-wen)

空!=无

关注他

5 人赞同了该文章

(一)常规思路

由于Termux团队的设计理念，默认情况下JDK是不能安装进Termux的（当然有替代的安装方案，太麻烦，我就不用了），所以ecj成为代替品。由于安卓不认识.class文件，还需要安装dx。dx用于格式转换，将.class文件转换为.dex文件。

```text
pkg instal  ecj
pkg install dx
```

然后就可以在Termux上使用Java了！

比如把一个名为JavaTest.jar的包制作成dex文件:

```text
dx --dex --output=JavaTest.dex JavaTest.jar
```

然后使用dalvikvm运行JavaTest目录里的org.com.Test（假设有个Test文件，含有main函数）：

```text
dalvikvm -cp JavaTest.dex org.com.Test
```



（二）不走寻常路

Java号称是平台无关的，所以一种可行的思路是：我在电脑端制作成.class文件或者jar文件，然后使用dx和dalvikvm就可以直接用！！

可行方案如下：用NetBeans或者Eclipse或者任意你熟悉的IDE把需要的Java文件打包成jar。如JavaTest.jar

然后Termux下制作dex文件：

```text
dx --dex --output=JavaTest.dex JavaTest.jar
```

然后执行，任何含有main函数的文件，如Test、Test2：

```text
dalvikvm -cp JavaTest.dex org.com.Test
dalvikvm -cp JavaTest.dex org.com.Test2
```

本方法的bug是，dx性能很捉急，慢！而且在处理大型jar时报错（OutOfMemoryError）：

![img](https://pic4.zhimg.com/v2-423b0a42717a513e60bd5a24a88aaecb_r.jpg)

所以这个方法用来做做小项目还行，大型的事儿就省省吧！

（三）进一步不走寻常路

Android Studio是电脑端开发安卓的利器，他可以直接生成dex和apk文件。那么我上述操作就完全多余了！

我完全可以利用Android Studio把我常用的包生成dex文件或者apk文件。一般Android Studio生成的dex文件路径为（文件名为classes.dex，需要自己给他手动改名字！）：

```text
app\build\intermediates\dex\release\mergeDexRelease\out\classes.dex
```

或者直接用rar或者zip把生成的apk解压缩，里面的文件如下：

![img](https://pic4.zhimg.com/v2-8c3d3c99322240e094b205be94da112f_r.jpg)

把里面的classes.dex文件解压出来就可以直接使用。

比如假定我把classes.dex重命名为JavaTest.dex，把文件拷进去Termux以后，在该目录下运行：

```text
dalvikvm -cp JavaTest.dex org.com.Test
```

（四）性能测试

Termux运行Java的能力如何呢？跑个测试呗：

我运行了一个自有程序，分别在电脑（3700X）、Termux和安卓apk（没错，我把程序简单做了个简单的app，手机为小米Mix2S），运行时间分别是：

1、3700X 1.575s

2、安卓App 5.575s

3、Termux 39.811s

![img](https://pic2.zhimg.com/v2-ff81aaa033e55c3535eab205a02cd045_r.jpg)Termux在Mix2S上的计算时间

![img](https://pic2.zhimg.com/80/v2-c46c2e3324fe36da836f55ab000d0b45_720w.png)Netbeans本地电脑3700X计算时间

归一化成绩为：

1、3700X 1

2、安卓App 3.54

3、Termux 25.28

没想到Termux运行Java的性能慢了如此之多！！！各位看官有没有解决之道呢？难道我得上ArchLinux或者Ubantu？

我的解决之道是：

1）换Aid Learning。具体可见：

[myastrotong：把安卓手机性能发挥到极致之-Aid Learning运行Java及性能测试zhuanlan.zhihu.com![图标](https://pic2.zhimg.com/v2-398862aab05605124e5ee51d5df92301_120x160.jpg)](https://zhuanlan.zhihu.com/p/92489740)

2）Termux安装完整版Linux，方法如下：

[myastrotong：极致安卓之—Termux安装完整版Linuxzhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/95865982)

新手机就推荐安装Aid Linux，这个app是个神器，谁用谁知道。

老手机，比如三星Note3这类渣渣，你可以安装老版本的Termux，然后按我说的方法来安装Linux。

![把安卓手机性能发挥到极致之-Aid Learning运行Java及性能测试](https://pic1.zhimg.com/v2-398862aab05605124e5ee51d5df92301_1440w.jpg?source=172ae18b)

# 把安卓手机性能发挥到极致之-Aid Learning运行Java及性能测试

[![myastrotong](https://pic1.zhimg.com/v2-630280f8f6d2060f01810f0a1fc2ea18_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/tang-kong-wen)

[myastrotong](https://www.zhihu.com/people/tang-kong-wen)

空!=无

关注他

13 人赞同了该文章

在此篇文章中，介绍了Termux上安装Java。发现Java性能非常捉急。

[myastrotong：把安卓手机性能发挥到极致之-Termux运行Javazhuanlan.zhihu.com![图标](https://pic2.zhimg.com/v2-5dc9141b4946abc0e8e62d71c28b4e91_120x160.jpg)](https://zhuanlan.zhihu.com/p/92471681)

考虑到Aid Learning是基于Debian的，那么有非常可靠的OpenJDK可以使用，赶紧找一下：

```text
apt search openjdk
```

找到如下相关内容：

![img](https://pic1.zhimg.com/v2-864eba7267f8bbe7b3d0a1bdd6360218_r.jpg)





果然有opnjdk-8，话不多说，安装！

```text
apt install openjdk-8-jdk
apt install openjdk-8-jre
```

安装完成后，输入

```text
java -version
```

然并卵，一堆错误！

jdk肯定是安上去了，可是执行不了，那肯定是环境变量Path找不到jdk在哪儿。

我也不知道jdk安到哪儿去了，一通查找，在一个犄角旮旯里面找到了，原来是藏在：

```text
/usr/lib/jvm
```

![img](https://pic1.zhimg.com/v2-48cf87b25c9872691178a16b312cbdfc_r.jpg)

可以看到里面有三个jdk，鬼知道怎么安上的这么多！

利用vim修改修改/etc/profile的配置文件，修改环境变量Path

![img](https://pic3.zhimg.com/v2-d74933feab10d1a91ae606d6fc7a3d4a_r.jpg)

加入如上图的4行话。保存退出。

输入：

```text
java -version
```

成功！

![img](https://pic4.zhimg.com/v2-f8b5a79ea95e982fb109c882bafa5467_r.jpg)

开始性能测试：

输入:

```text
java -cp xxx.jar xx.xx.XXX
```

![img](https://pic3.zhimg.com/v2-fbe84ad01bdf56eb3751da4617223a66_r.jpg)

计算时间为3.734s！！！！基于真正的Linux jdk性能比Termux提升很明显！！！

运行时间对比如下：

|运行时间 |归一化

1、3700X | 1.575s | 1

2、安卓App | 5.575s | 3.54

3、Termux | 39.811s | 25.28

4、AidLearning | 3.734 | 2.371

小米Mix2S只比3700X慢了1.371倍！！！！要知道3700X的TDP功耗可是65W，小米顶了天功耗4~5W！

手机也能成为生产力工具了！！！！这可真是喜大普奔！！！

从这篇文章我们看出，国货Aid Learning某些方面已经领先Termux了！因为他貌似是纯正的Debian啊！（我不懂Linux，说错了勿怪！我只关心性能！）

Aid Learning真香！

编辑于 02-05

「