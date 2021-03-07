[云社区](https://bbs.huaweicloud.com/) [博客](https://bbs.huaweicloud.com/blogs) 博客详情

# linux系统手动搭建FTP站点教程

[![img](https://bbs-img.huaweicloud.com/user/img/head/1600331463981_6749_1769.jpg)](https://bbs.huaweicloud.com/community/usersnew/id_1497583906686032) *[a.l.e.x](https://bbs.huaweicloud.com/community/usersnew/id_1497583906686032)* 发表于 2020-05-31 21:30:03

 128 

 0 

 0

[Linux](https://developer.huaweicloud.com/tags/200597/blog_1)[FTP](https://developer.huaweicloud.com/tags/200600/blog_1)

【摘要】 步骤一：安装vsftpd安装vsftpdyum install -y vsftpd设置FTP服务开机自启动systemctl enable vsftpd.service启动FTP服务systemctl start vsftpd.service查看FTP服务监听的端口netstat -antup | grep ftp输出如下图所示，表示监听端口为21步骤二：配置vsftpd配置主...

步骤一：安装vsftpd

安装vsftpd

```javascript
yum install -y vsftpd
```

![1.png](https://s2.51cto.com/images/20200530/1590853634300758.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)


设置FTP服务开机自启动

```javascript
systemctl enable vsftpd.service
```

启动FTP服务

```javascript
systemctl start vsftpd.service
```

查看FTP服务监听的端口

```javascript
netstat -antup | grep ftp
```

输出如下图所示，表示监听端口为21

![2.png](https://s2.51cto.com/images/20200530/1590853640664249.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

步骤二：配置vsftpd
配置主动模式下匿名用户上传文件权限
首先，修改配置文件/etc/vsftpd/vsftpd.conf

```javascript
vim /etc/vsftpd/vsftpd.conf
```

将匿名上传权限的注释去掉，修改为anon_upload_enable=YES
如下图所示：

![3.png](https://s2.51cto.com/images/20200530/1590853663347801.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

更改/var/ftp/pub目录的权限，为FTP用户添加写权限

```javascript
chmod o+w /var/ftp/pub/
```

重新加载配置文件

```javascript
systemctl restart vsftpd.service
```

![4.png](https://s2.51cto.com/images/20200530/1590853669659498.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

步骤三：设置安全组
在实例安全组的入方向添加规则并放行下列FTP端口
FTP为主动模式时：端口21

![5.png](https://s2.51cto.com/images/20200530/1590853677229444.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

FTP为被动模式时：端口21，以及配置文件/etc/vsftpd/vsftpd.conf中参数pasv_min_port和pasv_max_port之间的所有端口。

![6.png](https://s2.51cto.com/images/20200530/1590853681664603.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

原文地址：https://leffz.com/1273.html

文章来源: blog.51cto.com，作者：soldi，版权归原作者所有，如需转载，请联系作者。

原文链接：https://blog.51cto.com/14094768/2499980

# Linux下搭建ftp服务

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[不进则退2020](https://blog.csdn.net/qq_32706349) 2018-11-05 10:40:46 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 16664 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 17

分类专栏： [linux](https://blog.csdn.net/qq_32706349/category_7713794.html)

# 原文https://www.cnblogs.com/freeweb/p/6518257.html

# [Linux下搭建ftp服务](https://www.cnblogs.com/freeweb/p/6518257.html)

 

过程中比较常用的命令：

```
#启动ftp



service vsftpd start
```

\------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

　　Linux下ftp服务可以通过搭建vsftpd服务来实现，以CentOS为例，首先查看系统中是否安装了vsftpd，可以通过执行命令 rpm -qa | grep vsftpd 来查看是否安装相应的包，如果没有安装那么可以执行 **yum -y install vsftpd** 来安装，安装之后首先**创建ftp用户**，比如ftp_test，命令如下：

```html
useradd -s /sbin/nologin -d /home/ftp_test ftp_test
```

　　**目录尽量不要选择根目录下，这里是/home/ftp_test，并且ftp_test这个目录不要手动创建，否则权限会有问题，执行命令的时候会自动创建，**

　　![img](https://images2015.cnblogs.com/blog/734555/201703/734555-20170308134324469-607202910.png)

　　可以看到权限现在是对于ftp_test用户是可读可写可执行的，其他用户和组下面的都没有任何权限，现在为ftp_test用户创建密码：输入passwd 用户名

```html
passwd ftp_test
```

　　执行之后输入2次密码确认就设置好了密码【实际测试中，需要设置较为复杂的密码】

　　然后编辑vsftpd配置文件，位置是:vim /etc/vsftpd/vsftpd.conf

　　找到anonymous_enable这个配置项，默认是YES，修改成NO，表示不允许匿名用户登录

　　![img](https://images2015.cnblogs.com/blog/734555/201703/734555-20170308134722203-574856946.png)

　　现在直接保存配置文件，执行 systemctl start vsftpd.service 启动vsftp服务，然后可以通过命令： systemctl status vsftpd.service 查看ftp服务的运行状态，现在就可以用ftp客户端进行连接了，这里用FileZilla测试，连接正常

　　![img](https://images2015.cnblogs.com/blog/734555/201703/734555-20170308135112609-482707460.png)![img](https://images2015.cnblogs.com/blog/734555/201703/734555-20170308135225906-611761313.png)

 

　　现在基本的ftp服务就部署完了，客户端可以正常上传，下载，修改文件；但是这样有个问题就是所有的目录都暴露给客户端了，虽然客户端不能随意修改删除其余的文件，但是因为目录可见，所以总会有一些风险，所以接下来还需要配置让ftp用户只在自己的家目录下面活动，而无法查看其它任何目录，同样是打开配置文件/etc/vsftpd/vsftpd.conf，找到chroot_local_user=YES这个配置，默认是注释的，这里去掉注释，表示只让用户在自己的目录里面活动，如果只是保存这一个配置的话，用ftp连接客户端会返回500 OOPS: vsftpd: refusing to run with writable root inside chroot()的错误，即禁止运行在可写的家目录中，因为刚才ftp_test这个目录有w权限，而现在我们使用的vsftpd版本是3.0.2 属于比较新的版本，为了安全性做了一些限制，如果你此时想通过 chmod a-w /home/ftp_test 来去掉目录的写权限，那么连接成功是没问题的，但是无法上传文件了，所以网上很多说修改权限的方法是不可取的，正确的做法是应该在下面添加一行配置allow_writeable_chroot=YES表示允许对家目录的写权限，具体配置如下：

　　![img](https://images2015.cnblogs.com/blog/734555/201703/734555-20170308140902531-1619049785.png)

　　配置完这两项以后保存退出，然后执行 systemctl restart vsftpd.service 重启vsftpd服务，现在重新使用ftp连接就成功了，并且任何操作也是没问题的

　　![img](https://images2015.cnblogs.com/blog/734555/201703/734555-20170308141222078-1358772630.png)

　　现在可以看到上面的路径是一个/，对于ftp用户来说也就是根目录了，只能在这个目录下操作，而无法跳出这个目录

　　以上就是vsftpd服务的基本搭建过程，实际使用时可以分配多个用户

**备注：**

https://blog.csdn.net/myphp2012/article/details/78295396 FTP服务器vsftpd配置详解

- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/89402670d5413a8c62e9f4bb1ffc508c9ace8175.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=1)1
- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/51cd85cec7f88a77963cd9f86e4a2f27e6eff875.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=2)2
- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/2947750192dd33406212c033881c99c0aefcf175.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=3)3
- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/9881b1fce186242f7393c5ab35e434daf15ee875.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=4)4
- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/bfa52adaf05e4a239890afa91dd818196020e275.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=5)5
- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/d4071b96b814f4d097e19966cdfe474ec383237a.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=6)6
- [![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/fb738d9c2cf7dfb2eefb9f98d01b1edef5dc137a.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html?picindex=7)7

[分步阅读](http://jingyan.baidu.com/album/380abd0a77ae041d90192cf4.html)

FTP 是File Transfer Protocol（文件传输协议）的英文简称，而中文简称为“文传协议”。用于Internet上的控制文件的双向传输。同时，它也是一个应用程序（Application）。基于不同的操作系统有不同的FTP应用程序，而所有这些应用程序都遵守同一种协议以传输文件。在FTP的使用当中，用户经常遇到两个概念："下载"（Download）和"上传"（Upload）。

一般在各种linux的发行版中，默认带有的ftp软件是vsftp，从各个linux发行版对vsftp的认可可以看出，vsftp应该是一款不错的ftp软件。

## 方法/步骤

- 1、检查安装vsftpd软件

  使用如下命令#rpm -qa |grep vsftpd可以检测出是否安装了vsftpd软件，

  如果没有安装，使用YUM命令进行安装。

  ![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/89402670d5413a8c62e9f4bb1ffc508c9ace8175.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

- 2、启动服务 

  使用vsftpd软件，主要包括如下几个命令：

  启动ftp命令#service vsftpd start

  停止ftp命令#service vsftpd stop

  重启ftp命令#service vsftpd restart

  ![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/51cd85cec7f88a77963cd9f86e4a2f27e6eff875.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

- 3、vsftpd的配置

  ftp的配置文件主要有三个，位于/etc/vsftpd/目录下，分别是：

  ftpusers  该文件用来指定那些用户不能访问ftp服务器。

  user_list  该文件用来指示的默认账户在默认情况下也不能访问ftp

  vsftpd.conf  vsftpd的主配置文件

- 4、以匿名用户为例，我们去掉配置文件vsftpd.conf 里面以下

  anon_upload_enable=YES

  anon_mkdir_write_enable=YES

  两项前面的#号，就可以完成匿名用户的配置，此时匿名用户既可以登录上传、下载文件。记得修改配置文件后需要重启服务。

  ![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/2947750192dd33406212c033881c99c0aefcf175.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  ![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/9881b1fce186242f7393c5ab35e434daf15ee875.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

- 5、非匿名账户的创建与使用

  vsftpd服务与系统用户是相互关联的，例如我们创建一个名为test 的系统用户，那么此用户在默认配置的情况下就可以实现登录，如图

  ![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/bfa52adaf05e4a239890afa91dd818196020e275.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  ![Linux平台下快速搭建FTP服务器](https://exp-picture.cdn.bcebos.com/d4071b96b814f4d097e19966cdfe474ec383237a.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

- 登录后在页面创建名为“aa”的文件夹，同样我们在服务器test用户 的home目录里也可以看到相同的文件。