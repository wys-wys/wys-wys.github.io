# 神器Termux

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[紫霄宫中布道者](https://blog.csdn.net/yaokingson) 2019-08-23 09:35:08 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 4699 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 87

分类专栏： [Termux](https://blog.csdn.net/yaokingson/category_9259859.html) 文章标签： [Termux](https://www.csdn.net/gather_2a/MtTaEg0sMDY1MzctYmxvZwO0O0OO0O0O.html)

版权

文章来源：企鹅号 - 一件风衣

# （一）——如何用安卓手机优雅地写Python

一款很牛逼的神器——Termux。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvZmxyZnMxNjNhZi5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

**一、关于Termux**

**（一）特性**

1.类型

这是一款大小只有几百K的apk，安装后可以在Android手机上搭建一个完整的Linux环境。

2.工作方式

命令行，乍看之下很不友好，实则提供了很多隐藏的功能，实际上手之后非常好用。

3.关于软件源

Termux有官方的软件源，网速挺快，与Linux软件源保持同步。

4.关于root

无需root！无需root！无需root！不需要root权限Termux就可以正常运行，不过需求多的用户能root自然是最好了，很多需要root权限的命令就可以执行了，包括文件管理上也会很方便。

5.可拓展性

很强，挖个坑，以后介绍。

**（二）安装与配置**

我的设备：OnePlus6，系统Android 8.1.0

**1.安装**

推荐在官方途径下载，这里放上官网：

https://termux.com

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvczB2ZGkweHd5dC5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

你也可以直接百度搜索Termux，请自行辨别备选链接。

官网提供了两种下载方式，Google Play不会翻墙或者手机Google框架不完整的话还是不要使用了，强烈建议选择在F-Droid（也是一个软件商店，不过很干净）搜索下载，选择“Termux Terminal emulator with packages”，当前版本是0.60，更新于四个月前（2018年年初），更新得很新了。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvM2toOGsxYjM0eC5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

下载完成后直接安装即可。

**2.配置Python运行环境**

打开之后就是很高（zhuang）端（bi）的命令行界面了，接下来我们按照下面的步骤进行环境配置（摸索了很久总结出的血泪教训。。T_T）。

**（1）更新包**

Linux用户应该很熟悉了：

apt update

apt upgrade

**（2）安装Python**

这里我们把Python2和Python3都装上（听我的不会错）：

apt install python python-dev python2 python2-dev

不加版本号的python是指Python3。

到这里，Python就可以正常使用了，可以分别输入

python —version

python2 —version

来验证是否安装成功（注意version前是两根短横线）。

接下来我们就可以写第一个python程序啦！

输入python，回车，开始写代码：

EZ

分割线头疼预警！！！

**（3）安装其他**（进阶用户使用）

•clang和g++——这两个不是Python模块，是编译器，下面的安装有些需要用到。（g++需要的时间挺久，下载包就有200M+）

apt install clang

apt install g++

•lxml——比标准库里xml模块性能更强大的xml处理模块

这个模块依赖的包很多，需要先安装：

apt install libcrypt libcrypt-dev

apt install libxml2 libxml2-dev libxslt libxslt-dev python-libxml2 python-libxslt

还需要安装pip（不然执行不了pip命令）：

apt install pip

接下来就可以安装了：

pip install lxml

•scrapy——专业爬虫库，依赖于lxml

先安装依赖项：

apt install openssl openssl-tool openssl-dev libffi libffi-dev

再安装：

pip install scrapy

•BeautifulSoup4——专业爬虫库

pip install BeautifulSoup4

pip install requests

•numpy——数学计算库

LDFLAGS=“-lm -lcompiler_rt” pip install numpy

•matplotlib——绘图模块

LDFLAGS=“-lm -lcompiler_rt” pip install matplotlib

•pandas——数据分析模块

LDFLAGS=“-lm -lcompiler_rt” pip install pandas

•Jupyter Notebook——超级好用的交互式记事本，下一篇会重点谈，和iPython公用内核，建议用这个

LDFLAGS=“-lm -lcompiler_rt” pip install jupyter

•demjson——json处理库

pip install demjson

常用的模块也就是这些了，其他的模块可以在需要的时候再进行安装。

之后就是自由发挥的时候了。

 

 

# （二）——如何用安卓手机舒服地写Python

用惯了windows和图形化界面的大家，或多或少对命令行有些抵触，有没有好的解决方案呢？先看看在Termux上写Python是种怎样的体验吧。

一、Python shell交互模式体验

在命令行中输入python按回车即可进入python原生的交互模式。

交互模式以 >>> 开头，用户可以直接输入代码，回车后程序执行代码，如：

退出交互模式可输入

exit()

或

quit()

交互模式可以一行行执行代码，也可以直接粘贴代码块，不过需要注意缩进。

体验了一段时间之后，发现确实不适合长时间写代码，总结缺点如下：

1.黑底白字很刺眼，长时间看容易眼疲劳，伤眼（颜色可以修改，以后会介绍）；

2.操作不易：

我们可以通过右滑屏幕左边呼出Termux的功能菜单，里面只有KEYBOARD和NEW SESSION两个功能和会话列表，长按KEYBOARD可以呼出隐藏的功能键盘，包含手机软键盘没有的功能键，比如tab、ctrl、shift、tab等，还有三种常用的线，如下图：

如此这般操作起来就很难受了，比如你输入了很长一串语句，突然发现前面的部分需要修改，你就得按住ctrl和b键，修改完之后，又得ctrl加f往后移动光标，大概修改了几次之后耐心就会被消磨的差不多了。

好在Termux提供了一个输入框，功能键盘向左滑动就可以看到，在这里面就可以通过点击来定位光标，不过输入框为单行，依然很不方便。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvazI3eGxsMG1odi5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

3.代码管理不方便，文件操作复杂，这两点就不说了，用过自然知道。

二、Jupyter的使用方法

那么有没有什么好的方案呢？当然是有的，下面给大家隆重介绍上一篇中提过的一个模块——Jupyter，先看看效果怎么样。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MveWZpYW55dWpjNy5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

看见没！甚至可以画图！

如果依照上篇中的步骤操作的话，执行完

LDFLAGS=“-lm -lcompiler_rt” pip install jupyter

这条语句之后，你就已经成功安装Jupyter了，下面介绍使用方法。

执行语句：

jupyter notebook -ip 0.0.0.0

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvcG55M284dmJkNC5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

看到上面的输出就代表已经成功搭建好基于网页的开发环境，第一次运行时，网址后会有一串token，用于验证身份，我们不用管，直接将整个网址复制进浏览器中，如果还要求输入token，可以按照提示把token手动复制进网页，接下来你可以设置密码，以后再次进入就不需要再验证了。

以上是理想情况，我在手机上登录该网页时就碰到了这种情况。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvMHd6ZHlpamU4Yy5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

原因还未知，暂且认为本机在解析这个地址时出现问题了吧，那问题怎么解决呢？

接着我想到了一个解决方案，不仅能解决这个问题，还可以把我们用于编程的设备变得更顺手！

思路就是把安装了Jupyter的手机和其他设备（比如平板电脑）置于同一局域网中，然后通过该设备访问该页面。

置于同一局域网可以通过连接同一路由器，或者用手机开启无线网络热点，其他设备接入该网络。我以手机开热点为例。

完成后，在命令行输入ifconfig查看手机IP地址，不过输出挺多看着挺烦，简单点就是在平板上的设置里查看Wi-Fi的信息：

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvZmpjc3E0dGMwbS5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

其中的路由器地址就是手机在局域网中的IP地址，如果是连接的同一个路由器的情况，则可以通过在手机端查看Wi-Fi设置，找到本机IP地址。

接下来在平板的浏览器中输入：

http://手机的IP地址:8888/

比如

http://192.168.43.1:8888/

接下来就成功进入网页了，为加上token的话需要按照要求填入，然后设置密码，接下来就可以舒服地写代码了！

Jupyter分为三个部分，一个是文件管理（可以上传文件），一个是正在运行，包括正在运行的终端和记事本，还有一个用于启用和设置运算集群的引擎数，我们暂时用不到（其实我也不会用QAQ）。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvbGZ4dXhnb2N1di5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

接下来我们新建一个Python3，可以看到如下界面，接下来我们就可以像在各种现代化的（雾）IDE里面一样编程啦，可以正常换行，每个输入框可以放置若干行代码，一般一个整体放在一起，看个人喜好了，点击run可以运行该部分代码，还可以终止或者重启内核，大家可以自行摸索，总之用起来舒服多啦！

举个例子：

为什么又是Hello world！难道作者你只会这个吗？？？

你不懂，我试试新的开发环境就是喜欢Hello world！

这个系列只负责介绍，高级一点的可以以后再交流嘛，只要你有想法和思路，以后有意思的事可多了，比如这个：

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvNzk0MnVmN245bS5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

你怕不怕？

# （三）——如何用安卓手机Hacking世界

2014年，Offensive Security团队发布了第一个版本的Kali Linux，这是一个基于Linux，面向专业渗透测试和安全审计（可以理解为黑客专用）的系统，预装了大量用于渗透的软件，从信息收集到提权一应俱全，经过本人的亲身体验，功能确实十分强大。

（图片来自Kali官网）

那么试想一下，如果这么强大的系统可以移植到手机上，岂不是很牛逼？

这一点当然早就被人想到了，还是Offensive Security团队，发布了Kali Nethunter，基于原生Android系统，可以安装到手机和平板上，移植了PC版本的绝大多数功能，把Pocket Hacking变为现实。本人在闲置的Nexus系列平板上尝试过，接上外接无线网卡可以轻易渗透无线网络，使用公共无线网的小伙伴们可得注意了。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvaTB0OHNyY2Nhei5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

（图片来自Nethunter官网）

但是如果要刷Kali的话，移动设备基本就只好专门用来做渗透测试了，倒也可以在Linux Deploy上安装Kali，不过对于爱好者来说可能不太友好，对知识体系的要求高了很多，那基于Termux呢？

既然是个Linux，只要在手机上适当配置，也可以实现Pocket Hacking的目标吧！

答案是肯定的，甚至Termux的官网上也给出了专门的Termux Hacking页面，指引在Termux下配置渗透工具。

下面讲讲几个非常经典、功能强大的安全软件在Termux下的安装，至于其他软件和这些软件的使用方法，在此就不做讨论了。

**一、Hydra**

一个经典的密码爆破软件，安装命令很简单：

pkg install hydra

安装完成后，配合密码本或者密码生成的命令就可以使用了。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvcWJrem5lZ2gzMy5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

**二、Metasploit Framework**

一款十分经典的开源安全漏洞检测工具，可以用来发现漏洞、利用漏洞，有强大的漏洞库，可以生成想要的payload，配合nmap可以囊括从开始扫描直到提权的所有要求。

官网提供了两种安装方法，手动方式我翻了一下，果断翻回自动方式，毕竟方便多了：

cd $HOME

pkg install wget

wgethttps://Auxilus.github.io/metasploit.sh

bash metasploit.sh

第一行用于切换到安装目录，可以根据需求自己选择，第二行安装wget，是个命令行下的下载工具，第三行下载用于自动安装Metasploit的批处理文件，第四行bash执行批处理脚本，接下来等待就行了。（按照官网的说法，只要没有红色的报警提示，就是安装成功了，Good luck～）

安装完成后，使用命令

./msfconsole

就可以运行Metasploit了。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvZ2p4Y3QzZDQ0aS5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

（这个载入图居然还有黑客帝国的梗～）

**三、Nmap**

一款非常经典的端口扫描工具，安装命令也非常简单：

pkg install nmap

使用也不介绍了，不过提醒一下，有些功能比如操作系统指纹识别需要root权限。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvM3ExanZ4NTF4ei5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

**四、sqlmap**

一款特别经典的sql注入工具，这个需要python2才能运行，安装命令如下：

git clonehttps://github.com/sqlmapproject/sqlmap.git

通过cd进入sqlmap路径之后，使用如下命令进入sqlmap：

python2 sqlmap.py

这样还是比较麻烦的，我们可以直接定义一个名为sqlmap的命令，以后使用的时候直接输入sqlmap后接参数就行了。

通过vim编辑profile文件添加命令，这个文件在termux中不一样，路径如下：

/usr/etc/profile

使用vim编辑该文件

vim profile

如果没有安装vim，通过命令

apt install vim

来安装vim。

在文件最后添加以下内容：

alias sqlmap=“python2 /sql的绝对路径/sqlmap.py”

就可以在任意路径使用sqlmap直接代替那一串啦！

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvN3NpZWZkM3BxOC5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

**五、RouterSploit**

这是一个还算经典的路由器漏洞利用工具，需要python3，安装命令如下：

git clonehttps://github.com/reverse-shell/routersploit

使用和Sqlmap类似，进入routersploit路径后执行：

python rsf.py

注意，此处不是python2。也可以通过相同的方法定义命令，前面的Metasploit也是如此。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvZ2p4Y3QzZDQ0aS5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

**六、关于root权限的使用**

如果想要更好的配合root权限使用Termux，可以使用termux-sudo，为命令提供root权限，安装命令如下：

git clonehttps://gitlab.com/st42/termux-sudo.git

然后进入路径，执行以下命令将其复制到bin目录：

cat sudo > /data/data/com.termux/files/usr/bin/sudo

chmod 700 /data/data/com.termux/files/usr/bin/sudo

之后就可以通过

sudo

来执行需要root权限的命令。

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MvaW9hcnh1OHJoYS5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

又到了自由发挥的时候啦，Termux系列到此结束啦（可拓展性由于缺乏硬件就不谈了）～

最后请各位注意

在探索发现的过程中

千万不要在违法的边缘试探哦～

 

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc2sucWNsb3VkaW1nLmNvbS9odHRwLXNhdmUvZGV2ZWxvcGVyLW5ld3MveTlpdGtiMThjei5qcGVnP2ltYWdlVmlldzIvMi93LzE2MjA?x-oss-process=image/format,png)

妮可妮可妮～

- 发表于: 2018-06-13
- 原文链接：https://kuaibao.qq.com/s/20180613G02IL800?refer=cp_1026
- 腾讯「云+社区」是腾讯内容开放平台帐号（企鹅号）传播渠道之一，根据[《腾讯内容开放平台服务协议》](https://om.qq.com/notice/a/20160429/047194.htm)转载发布内容。