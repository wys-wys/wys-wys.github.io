# CentOS7.4中安装了Mysql5.7之后如何查看默认密码

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[日出东方VS唯我不败](https://blog.csdn.net/qq_32786873) 2018-06-12 14:06:24 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 12849 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 7

分类专栏： [◆Linux](https://blog.csdn.net/qq_32786873/category_7329008.html)

版权

之前在虚拟机中安装了CentOS7.4，然后在CentOS7.4中安装了Mysql5.7，安装完成后，Mysql没有生成默认密码，所以可以直接使用命令mysql -uroot或mysql登录mysql。今天我在腾讯云服务器(操作系统：CentOS7.4)上安装完Mysql5.7之后，依然使用命令mysql -uroot或mysql登录mysql，结果报如下错误：

ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)

说明mysql安装完后给root用户生成了一个默认密码，所以需要使用密码登录。

那么问题来了，我们怎么查看mysql生成的默认密码呢？

为了加强安全性，MySQL5.7为root用户随机生成了一个密码，如果安装的是RPM包，则默认是在/var/log/mysqld.log中。

查看默认密码：grep 'temporary password' /var/log/mysqld.log

![img](https://img-blog.csdn.net/20180612140331987)

其中.,Ntun/n/5lf 就是默认密码