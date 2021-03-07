# mysql远程连接：ERROR 1130 (HY000): Host '*.*.*.*' is not allowed to connect to this MySQL server解决办法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[ghostyusheng](https://blog.csdn.net/ghostyusheng) 2017-07-25 11:56:23 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 950 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [解决方案](https://blog.csdn.net/ghostyusheng/category_2947549.html) [mysql](https://blog.csdn.net/ghostyusheng/category_7051659.html) 文章标签： [mysql远程连接](https://www.csdn.net/tags/OtDaMgzsNTk4OS1ibG9n.html) [error](https://so.csdn.net/so/search/s.do?q=error&t=blog&o=vip&s=&l=&f=&viparticle=) [not allowed to conne](https://so.csdn.net/so/search/s.do?q=not allowed to conne&t=blog&o=vip&s=&l=&f=&viparticle=)

安装完[MySQL](http://lib.csdn.net/base/mysql)后，远程连接[数据库](http://lib.csdn.net/base/mysql)的时候，出现 ERROR 1130 (HY000): Host '192.168.0.1' is not allowed to connect to this [mysql](http://lib.csdn.net/base/mysql) server提示信息，不能远程连接数据库。考虑可能是因为系统数据库mysql中user表中的host是localhost的原因，于是，我尝试把这个值改为自己服务器的ip，果然就好用了，不过用 mysql -u root -p命令就连不上数据库了，需要用mysql -h 服务器ip -u root -p因为默认的连接mysql数据库user表中host的值，而这个命令的默认host是localhost，就连不上了。

具体操作方法：

用localhost连接上mysql后，
use mysql;
update user set host='123.456.789.254';（IP为你想要远程连接数据库的本地机器的IP）
\q;

退出mysql,然后重新启动mysql就可以了。

其他解决方案

\2. **改表法**。可能是你的帐号不允许从远程登陆，只能在localhost。这个时候只要在localhost的那台电脑，登入mysql后，更改 "mysql" 数据库里的 "user" 表里的 "host" 项，从"localhost"改称"%"
mysql -u root -pvmware
mysql>use mysql;
mysql>update user set host = '%' where user = 'root';
mysql>flush privileges;
mysql>select host, user from user;

\3. **授权法**。例如，你想myuser使用mypassword从任何主机连接到mysql服务器的话。
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
如果你想允许用户myuser从ip为192.168.1.3的主机连接到mysql服务器，并使用mypassword作为密码
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'192.168.0.1' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;


***********************************************************************
phpMyAdmin说是用户名密码的问题，这就奇怪了,root用户名密码肯定没有问题,而且通过命令行连接没有问题。又仔细查看配置文件，还是没有问题。于是去搜了一下，找到这个解决方法.

先用root登录MYSQL服务器，执行
mysql>set password for 你要用的用户名@"localhost"=old_password('这个用户的密码');

原因是因为你使用的mysql服务器版本中使用了新的密码验证机制，这需要客户端的版本要在4.0以上，原来的密码函数被改为old_password();，这样使用password()生成的密码在旧的版本上就可以解决这个问题了.

转自:http://blog.sina.com.cn/s/blog_4ee4286501000c45.html

# ERROR 1130 (HY000): Host XXX is not allowed to connect to this MySQL server

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[今天你敲代码了吗？](https://blog.csdn.net/qq_32748869) 2019-02-25 15:34:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 195 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

版权

　　***\*在my.ini的mysqld后边加上skip-grant-tables（\*\*跳过数据库权限验证）可以用任意账号和密码登录\*\**\***

**1。 改表法。**

　　可能是你的帐号不允许从远程登陆，只能在localhost。这个时候只要在localhost的那台电脑，登入mysql后，更改 "mysql" 数据库里的 "user" 表里的 "host" 项，从"localhost"改称"%"

　　mysql -u root -pvmwaremysql>use mysql;

　　mysql>update user set host = '%' where user = 'root' and host='localhost';

　　mysql>select host, user from user;

**2. 授权法。**

　　例如，你想myuser使用mypassword从任何主机连接到mysql服务器的话。

　　GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;

　　FLUSH  PRIVILEGES;

　　如果你想允许用户myuser从ip为192.168.1.6的主机连接到mysql服务器，并使用mypassword作为密码

　　GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'192.168.1.3' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;

　　FLUSH  PRIVILEGES;

　　如果你想允许用户myuser从ip为192.168.1.6的主机连接到mysql服务器的dk数据库，并使用mypassword作为密码

　　GRANT ALL PRIVILEGES ON dk.* TO 'myuser'@'192.168.1.3' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;

　　FLUSH  PRIVILEGES;

　　我用的第一个方法,刚开始发现不行,在网上查了一下,少执行一个语句 mysql>FLUSH RIVILEGES 使修改生效.就可以了

　　另外一种方法,不过我没有亲自试过的,在csdn.net上找的,可以看一下.

　　在安装mysql的机器上运行：

　　　　1、d:/mysql/bin/>mysql  -h  localhost  -u  root //这样应该可以进入MySQL服务器

　　　　2、mysql>GRANT  ALL  PRIVILEGES  ON  *.*  TO  'root'@'%'  WITH  GRANT  OPTION //赋予任何主机访问数据的权限

　　　　3、mysql>FLUSH  PRIVILEGES //修改生效

　　　　4、mysql>EXIT //退出MySQL服务器

这样就可以在其它任何的主机上以root身份登录啦！