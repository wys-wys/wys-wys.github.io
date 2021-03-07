# bi查看本地服务器MYSQL的端口号

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[鹿鸣天涯](https://blog.csdn.net/jayjaydream) 2019-08-02 04:05:39 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3748 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 3

版权

[![img](https://img-blog.csdnimg.cn/20190528210135341.jpeg?x-oss-process=image/resize,m_fixed,h_64,w_64)软考网络规划设计师备考专栏软考网络规划设计师备考笔记![img](https://profile.csdnimg.cn/5/7/F/3_jayjaydream)鹿鸣天涯](https://blog.csdn.net/jayjaydream/category_9286598.html)

¥79.90

订阅博主

进入mysql后，输入命令：show global variables like 'port'; 

具体如下:

~$ mysql
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 5.7.20-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.


mysql> show global variables like 'port';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port     | 3306 |
+---------------+-------+
1 row in set (0.02 sec)

\--------------------- 
 

关于如何查看mysql版本：

方法一：

进入mysql cmd，

status;
将显示当前mysql的version的各种信息。 


方法二：

还是在mysql的cmd下，输入：

select version();

查看MySQL端口号：

show global variables like 'port';
\------

### 如何查看mysql 默认端口号和修改端口号

\1. 登录mysql  

[root@test /]# mysql -u root -p  
Enter password:  

\2. 使用命令show global variables like 'port';查看端口号  

mysql> show global variables like 'port';  
+---------------+-------+  
| Variable_name | Value |  
+---------------+-------+  
| port | 3306 |  
+---------------+-------+  
1 row in set (0.00 sec)  

\3. 修改端口，编辑/etc/my.cnf文件。  

[root@test etc]# vi my.cnf  
[mysqld]  
port=3506  
datadir=/var/lib/mysql  
socket=/var/lib/mysql/mysql.sock  
user=mysql  
\# Disabling symbolic-links is recommended to prevent assorted security risks  
symbolic-links=0  

[mysqld_safe]  
log-error=/var/log/mysqld.log  
pid-file=/var/run/mysqld/mysqld.pid  

"my.cnf" 11L, 261C written  
[root@test etc]#  

\4. 重新启动mysql  

[root@test ~]# /etc/init.d/mysqld restart  或 service mysql restart
Stopping mysqld: [ OK ]  
Starting mysqld: [ OK ]  

5.再次登录后检查端口已修改为’3506’.  

[root@test etc]# mysql -u root -p  
Enter password:  

mysql> show global variables like 'port';  
+---------------+-------+  
| Variable_name | Value |  
+---------------+-------+  
| port | 3506 |  
+---------------+-------+  
1 row in set (0.00 sec)  

\--------------------- 查看本地服务器MYSQL的端口号

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[鹿鸣天涯](https://blog.csdn.net/jayjaydream) 2019-08-02 04:05:39 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3748 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 3

版权

[![img](https://img-blog.csdnimg.cn/20190528210135341.jpeg?x-oss-process=image/resize,m_fixed,h_64,w_64)软考网络规划设计师备考专栏软考网络规划设计师备考笔记![img](https://profile.csdnimg.cn/5/7/F/3_jayjaydream)鹿鸣天涯](https://blog.csdn.net/jayjaydream/category_9286598.html)

¥79.90

订阅博主

进入mysql后，输入命令：show global variables like 'port'; 

具体如下:

~$ mysql
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 5.7.20-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.


mysql> show global variables like 'port';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port     | 3306 |
+---------------+-------+
1 row in set (0.02 sec)

\--------------------- 
 

关于如何查看mysql版本：

方法一：

进入mysql cmd，

status;
将显示当前mysql的version的各种信息。 


方法二：

还是在mysql的cmd下，输入：

select version();

查看MySQL端口号：

show global variables like 'port';
\------

### 如何查看mysql 默认端口号和修改端口号

\1. 登录mysql  

[root@test /]# mysql -u root -p  
Enter password:  

\2. 使用命令show global variables like 'port';查看端口号  

mysql> show global variables like 'port';  
+---------------+-------+  
| Variable_name | Value |  
+---------------+-------+  
| port | 3306 |  
+---------------+-------+  
1 row in set (0.00 sec)  

\3. 修改端口，编辑/etc/my.cnf文件。  

[root@test etc]# vi my.cnf  
[mysqld]  
port=3506  
datadir=/var/lib/mysql  
socket=/var/lib/mysql/mysql.sock  
user=mysql  
\# Disabling symbolic-links is recommended to prevent assorted security risks  
symbolic-links=0  

[mysqld_safe]  
log-error=/var/log/mysqld.log  
pid-file=/var/run/mysqld/mysqld.pid  

"my.cnf" 11L, 261C written  
[root@test etc]#  

\4. 重新启动mysql  

[root@test ~]# /etc/init.d/mysqld restart  或 service mysql restart
Stopping mysqld: [ OK ]  
Starting mysqld: [ OK ]  

5.再次登录后检查端口已修改为’3506’.  

[root@test etc]# mysql -u root -p  
Enter password:  

mysql> show global variables like 'port';  
+---------------+-------+  
| Variable_name | Value |  
+---------------+-------+  
| port | 3506 |  
+---------------+-------+  
1 row in set (0.00 sec)  

\--------------------- 