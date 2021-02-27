 [手记](https://www.imooc.com/article) /[后端开发](https://www.imooc.com/article/be)

# **阿里云服务器上安装MySQL**

2019.02.09 14:17 3162浏览

关闭防火墙和selinux
CentOS7以下：

```
service iptables stop 
setenforce 0
```

CentOS7.x

```
systemctl stop firewalld 
systemctl disable firewalld 
systemctl status firewalld 
vi /etc/selinux/config 
把SELINUX=enforcing 改成 SELINUX=disabled
```

一、安装依赖库
`yum -y install make gcc-c++ cmake bison-devel ncurses-devel`

二、创建mysql用户（但是不能使用mysql账号登陆系统）
`useradd mysql -s /sbin/nologin`       
创建用户mysql，不允许直接登录系统
`mkdir -p /var/mysql/data`        
创建MySQL数据库存放目录
`chown -R mysql:mysql /var/mysql/data` 
设置MySQL数据库目录权限

三、下载和安装MySQL
下载
`wget -c https://dev.mysql.com/get/Downloads/MySQL-5.6/mysql-5.6.41.tar.gz`

解压
`tar -zxvf mysql-5.6.41.tar.gz`
进入解压目录
`cd mysql-5.6.41`
配置(一条语句，复制执行即可)
`cmake -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \ -DMYSQL_UNIX_ADDR=/usr/local/mysql/mysql.sock \ -DDEFAULT_CHARSET=utf8 \ -DDEFAULT_COLLATION=utf8_general_ci \ -DWITH_MYISAM_STORAGE_ENGINE=1 \ -DWITH_INNOBASE_STORAGE_ENGINE=1 \ -DWITH_MEMORY_STORAGE_ENGINE=1 \ -DWITH_READLINE=1 -DENABLED_LOCAL_INFILE=1 \ -DMYSQL_DATADIR=/var/mysql/data \ -DMYSQL_USER=mysql -DMYSQL_TCP_PORT=3306`
编译并安装
`make && make install`
四、配置MySQL

`cd /usr/local/mysql`
进入安装目录
`cp ./support-files/my-huge.cnf /etc/my.cnf`
拷贝配置文件

`vi /etc/my.cnf`        
编辑配置文件，在 [mysqld] 部分增加
`datadir = /var/mysql/data`   
添加MySQL数据库路径

`./scripts/mysql_install_db --user=mysql`
生成mysql系统数据库
`cp ./support-files/mysql.server /etc/rc.d/init.d/mysqld`
把Mysql加入系统启动
`vi /etc/rc.d/init.d/mysqld`
编辑

`basedir=/usr/local/mysql`
MySQL程序安装路径
`datadir=/var/mysql/data`
MySQl数据库存放目录

`chmod 755 /etc/init.d/mysqld`
增加执行权限
`chkconfig mysqld on`
加入开机启动

`chown -R mysql /usr/local/mysql` 
修改/usr/local/mysql所属用户为mysql
`service mysqld start`
启动mysqld

```
vi /etc/profile`        
把mysql服务加入系统环境变量：在最后添加
`export PATH=$PATH:/usr/local/mysql/bin
```

`source /etc/profile`
使配置立即生效

`mkdir /var/lib/mysql`
创建目录
`ln -s /tmp/mysql.sock /var/lib/mysql/mysql.sock`
添加软链接
`mysql_secure_installation`
设置Mysql密码，根据提示按Y 回车输入2次密码
功能同上：mysql -u root -p password "123456" #或者直接修改密码

![webp](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAANSURBVBhXYzh8+PB/AAffA0nNPuCLAAAAAElFTkSuQmCC)

验证安装是否成功

若要设置root用户可以远程访问，执行
`mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;`

使授权立即生效
`FLUSH PRIVILEGES;`



作者：GHope
链接：https://www.jianshu.com/p/98a7a3577171

# 服务器上安装mysql

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[Pam Shao](https://blog.csdn.net/shaoyedeboke) 2019-05-22 19:19:29 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7686 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 12

分类专栏： [数据库](https://blog.csdn.net/shaoyedeboke/category_6958409.html) 文章标签： [服务器](https://www.csdn.net/tags/MtTaEg0sNDcxOTgtYmxvZwO0O0OO0O0O.html)

转载：https://blog.csdn.net/bianchengxiaoma/article/details/80800622 ，保存以便方便查找

CentOS 7 版本将MySQL数据库软件从默认的程序列表中移除，用MariaDB代替了，MariaDB数据库管理系统是MySQL的一个分支，主要由开源社区在维护，采用GPL授权许可。开发这个分支的原因之一是：甲骨文公司收购了MySQL后，有将MySQL闭源的潜在风险，因此社区采用分支的方式来避开这个风险。MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。

 

方法一：通过yum来进行mysql的安装

由于我安装的CentOS7.4默认安装了MariaDB，所以我只需要启动mariadb数据库就可以正常使用mysql了

(安装mariadb：yum install mariadb-server mariadb)

systemctl start mariadb

mariadb数据库的相关命令是：
systemctl start mariadb #启动MariaDB
systemctl stop mariadb #停止MariaDB
systemctl restart mariadb #重启MariaDB
systemctl enable mariadb #设置开机启动

安装mariadb后显示的也是 MariaDB [(none)]> ，可能看起来有点不习惯

接下来我们重新安装MySQL

1、卸载mariadb

yum list installed | grep mariadb  #检查mariadb是否已安装

yum -y remove mariadb*  #全部卸载

2、下载并安装mysql的YUM源

下载mysql的YUM源：wget -P /home/lisonglin http://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm(wget命令：http://man.linuxde.net/wget)

由于我们是下载到/home/lisonglin目录下，所以先切换到该目录下：cd /home/lisonglin

安装mysql的YUM源：rpm -ivh mysql57-community-release-el7-11.noarch.rpm

检查mysql的YUM源是否安装成功：yum repolist enabled | grep "mysql.*-community.*" 

看到上图所示表示安装成功

选择要启用的mysql版本

查看mysql版本,执行：yum repolist all | grep mysql

可以看到 5.5， 5.6，8.0 版本是默认禁用的

可以通过类似下面的语句来启动或禁用某些版本

yum-config-manager --enable mysql57-community

yum-config-manager --disable mysql56-community

或者通过修改vim /etc/yum.repos.d/mysql-community.repo文件，改变默认安装的mysql版本。比如要安装5.6版本，将5.7源的enabled=1改成enabled=0，然后再将5.6源的enabled=0改成enabled=1即可。

注意： 任何时候，只能启用一个版本。

查看当前的启用的 MySQL 版本：yum repolist enabled | grep mysql

3、安装MySQL

yum install mysql-community-server

安装过程中一直输入"y"就可以了，当出现下面的结果时，就代表mysql数据库安装成功了

4、测试

启动mysql服务：systemctl start mysqld

登录进Mysql（我的刚安装完时没有密码）：mysql -uroot或mysql

如果出现错误：ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)

则说明mysql安装完后给root用户生成了一个默认密码，所以你需要使用密码登录。

mysql -uroot -p 回车 然后输入默认密码即可登录myql。

关于如何查看默认密码，可以参考：CentOS7.4中安装了Mysql5.7之后如何查看默认密码

可能用到的命令：

systemctl start mysqld  #启动mysqld

systemctl stop mysqld  #停止mysqld

systemctl restart mysqld  #重启mysqld

systemctl enable mysqld  #设置开机启动

systemctl status mysqld  #查看 MySQL Server 状态

5、mysql相关配置

设置密码

mysqladmin -u root password 'new-password'

或set password for 'root'@'localhost' = password('123456');

设置完密码之后就可以使用mysql -u root -p 命令来登录我们的mysql数据库了

 

防火墙设置

远程访问 MySQL， 需开放默认端口号 3306.

firewall-cmd --permanent --zone=public --add-port=3306/tcp
firewall-cmd --permanent --zone=public --add-port=3306/udp

执行firewall-cmd --reload使最新的防火墙设置规则生效

 

远程访问设置

创建一个普通用户 sa ，密码是123456
CREATE USER 'sa'@'%' IDENTIFIED BY '123456'; 
给这个用户授予 SELECT,INSERT,UPDATE,DELETE 的远程访问的权限，这个账号一般用于提供给实施的系统访问 
GRANT SELECT,INSERT,UPDATE,DELETE ON *.* TO 'sa'@'%'; 
创建一个管理员用户 admin 账号 ，密码是 123456 
CREATE USER 'admin'@'%' IDENTIFIED BY '123456'; 
给这个用户授予所有的远程访问的权限。这个用户主要用于管理整个数据库、备份、还原等操作。 
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%'; 

设置用户 root 可以在任意 IP 下被访问：
grant all privileges on *.* to root@"%" identified by "新密码";
设置用户 root 可以在本地被访问：
grant all privileges on *.* to root@"localhost" identified by "新密码";

使授权立刻生效 
flush privileges;

 

设置字符集

一般的，为了支持中文，我们应该将字符集设为 UTF-8， 执行SHOW VARIABLES LIKE 'character%';

查看当前 MySQL 字符集

可以看到默认服务器的字符器是 latin1 ，对中文不友好。修改 /etc/my.cnf 文件，添加字符集的设置

 

[mysql]

default-character-set = utf8

[mysqld]

character_set_server = utf8

重启 MySQL ,可以看到字符集已经修改了

其他常用配置：

[plain] view plain copy

[mysqld] 
basedir   = path     # 使用给定目录作为根目录(安装目录)。 
datadir   = path     # 从给定目录读取数据库文件。 
pid-file   = filename   # 为mysqld程序指定一个存放进程ID的文件(仅适用于UNIX/Linux系统); 
 
 
socket = /tmp/mysql.sock   # 为MySQL客户程序与服务器之间的本地通信指定一个套接字文件(Linux下默认是/var/lib/mysql/mysql.sock文件) 
port       = 3306   # 指定MsSQL侦听的端口 
key_buffer    = 384M   # key_buffer是用于索引块的缓冲区大小，增加它可得到更好处理的索引(对所有读和多重写)。 
                索引块是缓冲的并且被所有的线程共享，key_buffer的大小视内存大小而定。 
table_cache   = 512    # 为所有线程打开表的数量。增加该值能增加mysqld要求的文件描述符的数量。可以避免频繁的打开数据表产生的开销 
sort_buffer_size = 2M    # 每个需要进行排序的线程分配该大小的一个缓冲区。增加这值加速ORDER BY或GROUP BY操作。 
                注意：该参数对应的分配内存是每连接独占！如果有100个连接，那么实际分配的总共排序缓冲区大小为100×6=600MB 
read_buffer_size = 2M    # 读查询操作所能使用的缓冲区大小。和sort_buffer_size一样，该参数对应的分配内存也是每连接独享。 
query_cache_size = 32M    # 指定MySQL查询结果缓冲区的大小 
read_rnd_buffer_size  = 8M # 改参数在使用行指针排序之后，随机读用的。 
myisam_sort_buffer_size =64M # MyISAM表发生变化时重新排序所需的缓冲 
thread_concurrency   = 8 # 最大并发线程数，取值为服务器逻辑CPU数量×2，如果CPU支持H.T超线程，再×2 
thread_cache      = 8 # #缓存可重用的线程数 
skip-locking         # 避免MySQL的外部锁定，减少出错几率增强稳定性。 
[mysqldump] 
max_allowed_packet   =16M # 服务器和客户端之间最大能发送的可能信息包 
 
[myisamchk] 
key_buffer  = 256M 
sort_buffer = 256M 
read_buffer = 2M 
write_buffer = 2M 
 

其他可选参数：
back_log = 384
指定MySQL可能的连接数量。 当MySQL主线程在很短时间内接收到非常多的连接请求，该参数生效，主线程花费很短时间检查连接并且启动一个新线程。 back_log参数的值指出在MySQL暂时停止响应新请求之前的短时间内多少个请求可以被存在堆栈中。 如果系统在一个短时间内有很多连接，则需要增大该参数的值，该参数值指定到来的TCP/IP连接的侦听队列的大小。 试图设定back_log高于你的操作系统的限制将是无效的。默认值为50。对于Linux系统推荐设置为小于512的整数。

max_connections = n
MySQL服务器同时处理的数据库连接的最大数量(默认设置是100)。超过限制后会报 Too many connections 错误

key_buffer_size = n
用来存放索引区块的RMA值(默认设置是8M)，增加它可得到更好处理的索引(对所有读和多重写)

record_buffer：
这里写代码片 每个进行一个顺序扫描的线程为其扫描的每张表分配这个大小的一个缓冲区。 如果你做很多顺序扫描，你可能想要增加该值。默认数值是131072(128K)

wait_timeout：
服务器在关闭它之前在一个连接上等待行动的秒数。

interactive_timeout：
服务器在关闭它前在一个交互连接上等待行动的秒数。 一个交互的客户被定义为对 mysql_real_connect()使用 CLIENT_INTERACTIVE 选项的客户。 默认数值是28800，可以把它改为3600。

skip-name-resolve
禁止MySQL对外部连接进行DNS解析，使用这一选项可以消除MySQL进行DNS解析的时间。 但需要注意，如果开启该选项，则所有远程主机连接授权都要使用IP地址方式，否则MySQL将无法正常处理连接请求！

log-slow-queries = slow.log
记录慢查询,然后对慢查询一一优化

skip-innodb
skip-bdb
关闭不需要的表类型,如果你需要,就不要加上这个

备份、还原
方法1:命令行 
备份 
mysqldump --socket=/var/lib/mysql/mysql.sock --single-transaction=TRUE -u root -p mysql> Solin.sql 
还原 
mysql --socket=/var/lib/mysql/mysql.sock -u root -p mysql< Solin.sql

 

 

 

参考：

https://www.cnblogs.com/xiaoluo501395377/archive/2013/04/07/3003278.html

https://www.cnblogs.com/TeiSi/p/6560282.html

http://blog.csdn.net/whatlookingfor/article/details/52382472

http://www.linuxidc.com/Linux/2016-06/132676.htm

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/simple1025/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/simplesally)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/loveisintheair/images/xml.gif)](https://www.cnblogs.com/simple1025/rss/)

随笔- 14 文章- 0 评论- 9 阅读- 37085 

# [linux服务器上安装mysql](https://www.cnblogs.com/simple1025/p/11133538.html)

mysql版本：mysql-5.6.44-linux-glibc2.12-x86_64.tar

linux操作系统和版本信息：

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704151415026-1508446560.png)

1、检查linux服务器上是否已安全mysql

[root@localhost ~]# rpm -qa|grep -i mysql

未安装则无任何信息返回，若已安装则会返回已安装的版本信息，可通过--nodeps关键字卸载mysql

[root@localhost local]#rpm -e *返回的mysql版本信息* --nodeps

2、添加分组和用户

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704152820252-1056006990.png)

[root@localhost ~]# cd /usr/local
[root@localhost local]# groupadd mysql
[root@localhost local]# useradd -r -g mysql mysql
[root@localhost local]# groups mysql

3、将下载的安装包上传到/usr/local目录上，解压安装包

[root@localhost local]# tar zxvf mysql-5.6.44-linux-glibc2.12-x86_64.tar.gz 

解压后重命名解压后的文件夹：

[root@localhost local]# mv mysql-5.6.44-linux-glibc2.12-x86_64 mysql

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704153453104-660928217.png)

4、进入mysql目录，对用户和分组进行授权

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704153655825-681196394.png)

5、进入/mysql/scripts/目录执行mysql_install_db脚本

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704154646151-1740313342.png)

安装报错，可直接在线安装perl和autoconf

[root@localhost scripts]# yum install perl

[root@localhost scripts]# yum -y install autoconf

再次执行[root@localhost scripts]# ./mysql_install_db --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data --pid-file=/usr/local/mysql/data/mysql.pid --tmpdir=/tmp

安装成功

6、完成后将mysql/目录下除了data/目录的所有文件，改回root用户所有，mysql用户只需作为mysql/data/目录下所有文件的所有者

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704155640164-365324237.png)

[root@localhost mysql]# chown -R root:root ./
[root@localhost mysql]# chown -R mysql:mysql data

7、设置启动脚本

[root@localhost mysql]# cp support-files/mysql.server /etc/init.d/mysqld

[root@localhost mysql]# chmod 755 /etc/init.d/mysqld

8、复制配置文件并修改配置文件

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704155816471-567716399.png)

[root@localhost mysql]# cp ./support-files/my-default.cnf /etc/my.cnf

修改配置文件，编辑etc/my.cnf文件，在[mysqld]下增加

[mysqld]
datadir = /usr/local/mysql/data
log-error = /usr/local/mysql/data/error.log
pid-file = /usr/local/mysql/data/mysql.pid
user = mysql
tmpdir = /tmp

9、启动服务

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704163156167-1821234032.png)

[root@localhost mysql]# service mysqld start

10、修改环境变量，编辑etc/profile文件，在文件的最后增加：

MYSQL_HOME=/usr/local/mysql

export PATH=$PATH:$MYSQL_HOME/bin

11、连接数据库，进入bin目录： ./mysql

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704163629738-2072509438.png)

12、修改root的用户密码和允许远程连接

mysql> use mysql;

mysql> update user set password=passworD("密码") where user='root';

mysql> flush privileges;

mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'trawe901' WITH GRANT OPTION;

mysql> flush privileges;

mysql>exit;

13、配置字符编码等

在/etc/my.cnf中的[mysqld]下方添加：

character_set_server = utf8

lower_case_table_names=1

log_bin_trust_function_creators=true

14、通过客户端工具连接mysql数据库成功

![img](https://img2018.cnblogs.com/blog/1728242/201907/1728242-20190704164538497-1608788188.png)

 

作者：simplesally 出处：https://www.cnblogs.com/simple1025/ 说明：本文版权归作者和博客园共有，欢迎转载和提出建议，但未经作者同意必须保留此段声明，且在文章页面明显位置给出原文连接，否则保留追究法律责任的权利。

