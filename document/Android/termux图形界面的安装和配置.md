# 为Termux安装图形化界面

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[@a'ゞ⃢戎⃢ 欢迎欢迎！](https://blog.csdn.net/overfile) 2019-10-31 21:47:25 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 16153 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 103

分类专栏： [Termux](https://blog.csdn.net/overfile/category_9475472.html) 文章标签： [Termux](https://www.csdn.net/gather_2a/MtTaEg0sMDY1MzctYmxvZwO0O0OO0O0O.html)

版权

\#**在学校闲着没事就逛逛论坛、博客、以及贴吧。突然发现一个好玩的东西，它就是**——**“Termux”**。#
也是咕哝了好久，在贴吧看到**Termux**可以装xfce桌面,于是便有此篇文章留作纪念，也同时感谢大佬们的默默努力，在此致敬！
一.首先安装Termux
二.更新源，字体，界面什么的网上都有很详细很详细的教程了，可以去搜一搜，有好多的，因为赶时间就没法说太多了。
三.”**正题**“——为termux安装桌面

***1.安装各种\*包**

```
pkg install x11-repo
pkg install xfce              /* 安装桌面，注意这里是xfce，而不是xfce4 */
pkg install python
pkg install openbox      /*安装窗口管理器*/
pkg install pypanel       /*安装轻量级面板*/
pkg install xorg-xsetroot  /*安装将根窗口背景设置为给定模式或颜色的经典X实用程序，*/
pip3 install PyXDG
pkg install aterm &          /*安装终端*/
12345678
```

**Openbox**（窗口管理器）
Openbox 是运行于搭载X11的GNU/Linux上的轻巧窗口管理器，Openbox 以GPL协议方式开放源代码，是免费自由软件。Openbox基于Blackbox，后者被认为原始窗口管理器之一（即代码自有）。【来源于百度百科】

**PyPanel**是用Python和C为X11窗口管理器编写的一个轻量级面板/任务栏。它可以很容易地定制，以匹配任何桌面主题或口味。PyPanel与EWMH兼容的WMS(Openbox、PekWM、FVWM等)一起工作。并且是在GNU通用公共许可证v2下分发的。

**xorg-xsetroot** 描述：将根窗口背景设置为给定模式或颜色的经典X实用程序

**PyXDG**是一个用于访问freedesktop.org标准的python库
**4 个独特的 Linux 终端模拟器**——http://www.sohu.com/a/295226634_100034897

***2.安装tigervnc***（你也可以安装别的远程桌面，这里以tigervnc为例）实现远程桌面控制

```bash
pkg install tigervnc
1
用vi启动编辑文件
vi startvnc
12
```

编写配置文件

```bash
#!/bin/bash -e
export DISPLAY=:10  #在10号屏幕打开程序
Xvnc --SecurityTypes=None $DISPLAY & 
sleep 1s
openbox-session &  #打开敞口管理器
xsetroot -solid gray #把背景弄成灰色
pypanel &
aterm & #启动终端
startxfce4 #开启xfce桌面12345678
```

注：我也不知道为啥安装xfce桌面,要startxfce4，要写这个4，[笑哭][笑哭]。
![演示](https://img-blog.csdnimg.cn/20191031213431905.png)

```
chmod +x startvnc 

./startvnc         /*启动*/
123
```

就可以无聊的连接远程桌面啦！！！！
撒花撒花撒花~~~~~~~~~~~~
点击安卓vnc
**输入localhost:5910**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191031213540170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L292ZXJmaWxl,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191031213644332.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L292ZXJmaWxl,size_16,color_FFFFFF,t_70)
**看吧效果图**
亲测有效。虽然随着时间变化教程可能会有一些改变，但大家要努力搞起来啊！！哈哈。

以及
1.配置Termux官方X11图形界面 https://www.jianshu.com/p/195fdb7adc41的简书文章
2.维基官方图形界面教程 https://wiki.termux.com/wiki/Graphical_Environment?cuid=3AD2F48F9C8812497E165BD84AC29BF1|0&cuid_galaxy2=3AD2F48F9C8812497E165BD84AC29BF1|0&cuid_gid=&timestamp=1572527747613&_client_version=10.3.8.12

******还可以在termux中安装linux发行版本，果需要教程，可以给我留言，（网上有好多例子的！！！）

**还有一些未解决的问题**

-  在termux中安装Linux后怎么使用远程桌面连接Linux。

欢迎大佬教学留言，希望我们共同成长！！！
安装完Termux，我们就可以搞很多事情啦哈哈哈哈！

最后致敬大佬们！！！！！！