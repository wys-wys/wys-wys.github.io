# [centos8安装搭建php环境](https://www.cnblogs.com/hjh666/p/12622567.html)

window/centos双系统安装完成之后，接下来在centos上搭建php的环境。

网上也有很多安装的教程，其实都一个样，以下我直接使用yum安装。默认都是安装最新版本。

安装apache:

```
yum install httpd
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//配置ServerName
//将#ServerName www.example.com:80修改为ServerName localhost:80

vi /etc/httpd/conf/httpd.conf
//启动apache：
systemctl start httpd

///查看安装版本： （我的是apache/2.4.37）
httpd -v

//设置开机启动：
systemctl enable httpd
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

安装mysql:

```
yum install mysql mysql-server
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//启动mysql
systemctl start mysqld.service
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//设置root密码为123456
mysqladmin -u root password 123456
//后续如果需要修改root密码
alter user 'root'@'%' identified with mysql_native_password by '新密码’；

//登录mysql
mysql -u root -p  //需要输入密码

//设置远程可访问
grant all privileges on *.* to 'root'@'%'with grant option;
flush privileges;//如果远程还是无法访问，有可能是防火墙的原因，关闭防火墙

//这里可以查看root用户的host ‘localhost' 已经变成了 ’%‘
use mysql 
select host,user from user;
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

安装php:

```
yum install php php-devel
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//查看php版本 (我的是php 7.2.11)
php -v//安装php扩展
yum install php-mysql php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc

//我这里在安装php-mysql的时候会提示错误：没有匹配的参数：php-mysql
//解决如下：
yum search php-mysql
//找到两个匹配版本：php-mysqlnd.x86_64 ;执行安装
yum install php-mysqlnd.x86_64
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//启动php
systemctl start php-fpm
//设置开机启动
systemctl enable php-fpm
```

最后重启apache: systemctl restart httpd. 到这里已经全部安装完环境。

 

apache默认解析目录是在 /var/www/html 目录下，更改成 /var/www 目录

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
vim /etc/httpd/conf/httpd.conf 

从 DocumentRoot “var/www/html/" 开始 改成 ”var/www/" 重启apache ：
systemctl restart httpd
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
可测试：在/var/www/目录下新建文件 index.php  浏览器直接访问：localhost 会显示index.php的内容

设置多站点： /etc/httpd/conf.d/目录下  新建.conf 文件；对应 /var/www/目录下新建网站目录
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
cd /etc/httpd/conf.d/ 
touch test.conf

//test.conf 插入代码
<VirtualHost *:80> 
 DocumentRoot /var/www/test
 ServerName www.test.com

 <Directory "/var/www/test"> 
  Require all granted
  Options FollowSymLinks
  AllowOverride all
  #Require all denied
 </Directory> 
</VirtualHost>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
客户端 hosts 指定ip地址和 域名，就可以正常访问网站了。（如 192.168.2.144  www.test.com）
```