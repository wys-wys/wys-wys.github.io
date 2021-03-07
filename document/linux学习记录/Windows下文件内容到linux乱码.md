- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/kevingrace/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/散尽浮华)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/kevingrace/rss/)

随笔- 569 文章- 39 评论- 922 阅读- 835万 

# [windows平台下编辑的内容传到linux平台出现中文乱码的解决办法](https://www.cnblogs.com/kevingrace/p/7720150.html)

 

现象说明：**在windows下编辑的内容，上传到linux平台下出现中文乱码**。如下：

**在windows平台编写haha.txt文件，内容如下：**

![img](https://images2017.cnblogs.com/blog/907596/201710/907596-20171024005441910-449852672.png)

**上传到linux平台，出现中文乱码，如下：**

 ![img](https://images2017.cnblogs.com/blog/907596/201710/907596-20171024005612676-941587556.png)

**基本上面出现的问题，有如下两种解决办法：**

**1）使用windows平台的"记事本"软件编辑haha.txt文件，将字符集改为"UTF-8"**
按Win键+run出现"运行"，在里面输入"notepad"即可打开记事本。然后"文件"->"打开" haha.txt文件，将下面一栏的编码改为"UTF-8"，然后将之前编辑的内容覆盖到新的UTF-8编码的haha.txt文件

![img](https://images2017.cnblogs.com/blog/907596/201710/907596-20171024010043973-113401442.png)

再次上传到linux平台下，查看就不会出现中文乱码了！

![img](https://images2017.cnblogs.com/blog/907596/201710/907596-20171024010842410-1723691276.png)

**2）在linux平台上用iconv命令纠正中文乱码**

```
[root@``test``-vm01 ~]``# cat haha.txt``°???????????asdfsadf``°?????????????????``[root@``test``-vm01 ~]``# iconv -f gbk -t utf8 haha.txt > haha.txt.utf8``[root@``test``-vm01 ~]``# cat haha.txt.utf8 > haha.txt``[root@``test``-vm01 ~]``# cat haha.txt``阿斯蒂芬撒打发似的fasdfsadf``阿斯蒂芬考虑实际负担：我去
```

 

**----------------------------------------------------XShell连接CentOS后，终端显示中文乱码问题的解决方法------------------------------------------**

使用U盘往Windows主机、Linux主机传文件是经常的事，但有时文件名有中文，传到Linux机器会有乱码，选择起来也很麻烦，下面简单说下应对方法：

**解决办法：**
一般这种问题是文件的编码字符集、Shell编码字符集、XShell编码字符集不匹配，设置匹配基本就OK了。

**临时办法**
**1)简体中文的Windows一般使用GB字符集，这里将XShell设置为GBK**

**![img](https://images2017.cnblogs.com/blog/907596/201710/907596-20171031184259183-273559156.png)**

**2) Linux主机**

```
[root@AppServer1 ~]``# export LANG=zh_CN.gbk``或者``[root@AppServer1 ~]``# vim /etc/sysconfig/i18n``LANG=zh_CN.gbk``[root@AppServer1 ~]``# source /etc/sysconfig/i18n
```

 

再试，就可以正常显示中文了。不过以上设置只对当前shell连接生效，新开的shell还是用的原来的设置。

### **永久生效**

**1) XShell属性设置**

![img](https://images2017.cnblogs.com/blog/907596/201710/907596-20171031185304683-2080592951.png)

**2) Linux环境变量设置**

```
[root@AppServer1 ~]``# vim /etc/profile``export` `LANG=zh_CN.gbk    ``//``在末尾追加
```

*************** 当你发现自己的才华撑不起野心时，就请安静下来学习吧！***************

分类: [常规运维](https://www.cnblogs.com/kevingrace/category/796260.html)

# WINDOWS上传中文文件名文件到LINUX显示乱码

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[安_shuai](https://blog.csdn.net/xyajia) 2017-09-30 17:14:53 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3254 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [Linux](https://blog.csdn.net/xyajia/category_6943397.html)

版权

现象：WINDOWS上传中文文件名文件到LINUX后，中文文件名乱码，中文内容乱码

解决：首先考虑到的应该是字符编码不一致导致，其次再看是否没安装中文包

1、**检查是否安装convmv工具**

[oracle@result tmp]$ rpm -qa |grep convmv
convmv-1.15-2.el6.noarch

说明已经安装，如没安装则 yum -y install convmv

2、**转换文件名格式为utf-8，正确显示**

convmv -f gbk -t utf8 -r --notest /photo/dataexchange/pic/zjdy/*.jpg

# 从windows中文名文件上传到linux服务器上以后文件名会成乱码

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[趋势大仙](https://blog.csdn.net/wyyother1) 2020-04-04 17:35:24 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 516 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [linux ubuntu14.04](https://blog.csdn.net/wyyother1/category_6705867.html) 文章标签： [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [服务器](https://www.csdn.net/tags/MtTaEg0sNDcxOTgtYmxvZwO0O0OO0O0O.html)

版权

1、中文名文件上传后保存在linux服务器上文件名会乱码，但是我们通过SSH直接对服务器上的一个文件进行重命名是可以使用中文的，而且显示出来是正确的，这说明服务器是可以支持中文的。

2、而为什么上传的中文名文件保存起来以后文件名会乱码呢？这是因为Windows的默认编码为GBK，Linux的默认编码为UTF-8。在Windows下编辑的中文，上传到Linux下就会显示为乱码。为了解决此问题，修改Linux的默认编码为GBK，就能够成功的解决乱码问题。


首先运行locale查看本地编码方式：

方式一：

[root@localhost hins]# locale

LANG=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=

方式二：

[root@localhost hins]# echo $LANG
zh_CN.GBK

这是服务器默认的编码，根据后面的方法修改后应该为：
（我修改为GBK以后的linux服务器的编码）


方法如下：

方法1：(试了一下，编码方式没有改变，可能是要重启服务器才能生效)
vi /etc/sysconfig/i18n
默认为:
LANG="en_US.UTF-8"
SYSFONT="latarcyrheb-sun16"


修改为:
LANG="zh_CN.GBK"
SUPPORTED="zh_CN.UTF-8:zh_CN:zh"
SYSFONT="latarcyrheb-sun16"


方法2：(推荐这种方法，不用重启服务器)
vi /etc/profile

export LC_ALL="zh_CN.GBK"
export LANG="zh_CN.GBK"

生效：source /etc/profile


[root@localhost hins]# locale
LANG=zh_CN.GBK
LC_CTYPE="zh_CN.GBK"
LC_NUMERIC="zh_CN.GBK"
LC_TIME="zh_CN.GBK"
LC_COLLATE="zh_CN.GBK"
LC_MONETARY="zh_CN.GBK"
LC_MESSAGES="zh_CN.GBK"
LC_PAPER="zh_CN.GBK"
LC_NAME="zh_CN.GBK"
LC_ADDRESS="zh_CN.GBK"
LC_TELEPHONE="zh_CN.GBK"
LC_MEASUREMENT="zh_CN.GBK"
LC_IDENTIFICATION="zh_CN.GBK"
LC_ALL=zh_CN.GBK


运行locale指令得到当前系统编码设置的详细资料。

一、locale的五脏六腑


1、 语言符号及其分类(LC_CTYPE)
2、 数字(LC_NUMERIC)
3、 比较和排序习惯(LC_COLLATE)
4、 时间显示格式(LC_TIME)
5、 货币单位(LC_MONETARY)
6、 信息主要是提示信息,错误信息, 状态信息, 标题, 标签, 按钮和菜单等(LC_MESSAGES)
7、 姓名书写方式(LC_NAME)
8、 地址书写方式(LC_ADDRESS)
9、 电话号码书写方式(LC_TELEPHONE)
10、度量衡表达方式(LC_MEASUREMENT)
11、默认纸张尺寸大小(LC_PAPER)
12、对locale自身包含信息的概述(LC_IDENTIFICATION)。


二、理解locale的设置


设定locale就是设定12大类的locale分类属性，即 12个LC_*。除了这12个变量可以设定以外，为了简便起见，还有两个变量：LC_ALL和LANG。


它们之间有一个优先级的关系：LC_ALL > LC_* > LANG


可以这么说，LC_ALL是最上级设定或者强制设定，而LANG是默认设定值。


三 具体设定locale的方法（zh_CN.UTF-8、zh_CN.GBK）


freebsd的设置：


1.GDM登录改为终端登录后startx启动图形桌面


2.在~/.cshrc中增加如下语句,（根据自己使用的shell进行相应设置）


setenv LANG zh_CN.GBK
setenv LC_ALL zh_CN.GBK
setenv LC_CTYPE zh_CN.GBK


3.修改/etc/fstab的默认值：


linux 设置：


1.修改/etc/sysconfig/i18n文件，LANG="zh_CN.UTF-8"或LANG="zh_CN.GBK"


普通用户修改~/.profile


...
export LANG zh_CN.GBK
...


2.修改/etc/fstab的默认值

