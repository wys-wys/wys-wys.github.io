# your password has expired.To log in you must change it using a client that support expired passwords

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[cyhui03](https://blog.csdn.net/weixin_42281671) 2019-06-24 14:26:28 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 591 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [mysql安装](https://blog.csdn.net/weixin_42281671/category_9055502.html)

版权

Mysql打开时出现以上问题的解决办法。
上面意思为：密码过期，需要重新设置密码，最后设为永不过期。
步骤为：
1.以管理员身份运行进入Mysql安装目录的bin目录下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190624140238717.png)
2.登录，输入mysql -uroot -p，之后提示输入密码，输入你原本设置的密码。本人为root。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190624140429637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjI4MTY3MQ==,size_16,color_FFFFFF,t_70)
3.重新设置密码。输入 set password = password(‘root’); 仍将秘密设置为root。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019062414071817.png)
4.输入use mysql;
5.输入 select user,host from user;
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190624141100543.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjI4MTY3MQ==,size_16,color_FFFFFF,t_70)

步骤4、5的主要目的在于确定步骤6设置永不过期中数据库名称的内容。
6.设置密码永不过期。
步骤5中root对应的host名为localhost。输入： alter user’root’@‘localhost’ password expire never;
若步骤5中root对应的host名为%。输入alter user’root’@’%’ password expire never;
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190624141909783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjI4MTY3MQ==,size_16,color_FFFFFF,t_70)
7.更新设置。输入 flush privileges;
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190624142015270.png)
8.输入quit;退出。重新打开Navicat链接数据库。

# Your password has expired. To log in you must change it using a client that supports expired passwor

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[zw_hard](https://blog.csdn.net/zhengwei125) 2017-03-30 13:57:56 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7041 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [MySql](https://blog.csdn.net/zhengwei125/category_5576255.html) 文章标签： [mysql密码过期](https://www.csdn.net/tags/OtDaMgwsOTEzNC1ibG9n.html) [mysql忘记密码](https://www.csdn.net/tags/MtTaEg2sNTg2OC1ibG9n.html)

版权

﻿﻿

mysql 5.7.14安装完后登陆报错，意思是密码过期

[root@mysql]# mysql -u root -p
Enter password:
ERROR 1862 (HY000): Your password has expired. To log in you must change it using a client that supports expired passwords.


**解决办法：**



**1.在my.cnf mysqld 部分加入 skip-grant-tables 参数。**

[mysqld]
**skip-grant-tables**

**2.重启mysql数据库，然后登陆**

[root@llmj-mysql-40-115 tools]# mysql -u root -p
Enter password:  #这里直接回车，不需要密码即可登陆
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.14-log MySQL Community Server (GPL)
Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.=
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

**3.查看mysql的用户状态**

\>select host,user,password_expired,account_locked from mysql.user;
+-----------+-----------+------------------+----------------+
| host   | user   | **password_expired** | account_locked |
+-----------+-----------+------------------+----------------+
| localhost | root   | **Y**        | N       |
| localhost | mysql.sys | N        | Y       |
+-----------+-----------+------------------+----------------+
3 rows in set (0.00 sec)

**password_expired ：y说明密码已经过期，可以改成N,就是未过期**

\>update mysql.user set password_expired='N';
Query OK, 1 row affected (0.03 sec)
Rows matched: 2 Changed: 1 Warnings: 0



**4.然后注释掉skip-grant-tables参数**

重启mysql，用过期的密码就可以登陆了，登陆之后可以用下面的命令修改密码
\>alter user user() identified by '123456';
Query OK, 0 rows affected (0.03 sec)

\>flush privileges;
Query OK, 0 rows affected (0.03 sec)Your password has expired. To log in you must change it using a client that supports expired passwor

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[zw_hard](https://blog.csdn.net/zhengwei125) 2017-03-30 13:57:56 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7041 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [MySql](https://blog.csdn.net/zhengwei125/category_5576255.html) 文章标签： [mysql密码过期](https://www.csdn.net/tags/OtDaMgwsOTEzNC1ibG9n.html) [mysql忘记密码](https://www.csdn.net/tags/MtTaEg2sNTg2OC1ibG9n.html)

版权

﻿﻿

mysql 5.7.14安装完后登陆报错，意思是密码过期

[root@mysql]# mysql -u root -p
Enter password:
ERROR 1862 (HY000): Your password has expired. To log in you must change it using a client that supports expired passwords.


**解决办法：**



**1.在my.cnf mysqld 部分加入 skip-grant-tables 参数。**

[mysqld]
**skip-grant-tables**

**2.重启mysql数据库，然后登陆**

[root@llmj-mysql-40-115 tools]# mysql -u root -p
Enter password:  #这里直接回车，不需要密码即可登陆
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.14-log MySQL Community Server (GPL)
Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.=
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

**3.查看mysql的用户状态**

\>select host,user,password_expired,account_locked from mysql.user;
+-----------+-----------+------------------+----------------+
| host   | user   | **password_expired** | account_locked |
+-----------+-----------+------------------+----------------+
| localhost | root   | **Y**        | N       |
| localhost | mysql.sys | N        | Y       |
+-----------+-----------+------------------+----------------+
3 rows in set (0.00 sec)

**password_expired ：y说明密码已经过期，可以改成N,就是未过期**

\>update mysql.user set password_expired='N';
Query OK, 1 row affected (0.03 sec)
Rows matched: 2 Changed: 1 Warnings: 0



**4.然后注释掉skip-grant-tables参数**

重启mysql，用过期的密码就可以登陆了，登陆之后可以用下面的命令修改密码
\>alter user user() identified by '123456';
Query OK, 0 rows affected (0.03 sec)

\>flush privileges;
Query OK, 0 rows affected (0.03 sec)

# Your password has expired. To log in you must change it using a client that supports expired passwor

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[zw_hard](https://blog.csdn.net/zhengwei125) 2017-03-30 13:57:56 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7041 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [MySql](https://blog.csdn.net/zhengwei125/category_5576255.html) 文章标签： [mysql密码过期](https://www.csdn.net/tags/OtDaMgwsOTEzNC1ibG9n.html) [mysql忘记密码](https://www.csdn.net/tags/MtTaEg2sNTg2OC1ibG9n.html)

版权

﻿﻿

mysql 5.7.14安装完后登陆报错，意思是密码过期

[root@mysql]# mysql -u root -p
Enter password:
ERROR 1862 (HY000): Your password has expired. To log in you must change it using a client that supports expired passwords.


**解决办法：**



**1.在my.cnf mysqld 部分加入 skip-grant-tables 参数。**

[mysqld]
**skip-grant-tables**

**2.重启mysql数据库，然后登陆**

[root@llmj-mysql-40-115 tools]# mysql -u root -p
Enter password:  #这里直接回车，不需要密码即可登陆
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.14-log MySQL Community Server (GPL)
Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.=
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

**3.查看mysql的用户状态**

\>select host,user,password_expired,account_locked from mysql.user;
+-----------+-----------+------------------+----------------+
| host   | user   | **password_expired** | account_locked |
+-----------+-----------+------------------+----------------+
| localhost | root   | **Y**        | N       |
| localhost | mysql.sys | N        | Y       |
+-----------+-----------+------------------+----------------+
3 rows in set (0.00 sec)

**password_expired ：y说明密码已经过期，可以改成N,就是未过期**

\>update mysql.user set password_expired='N';
Query OK, 1 row affected (0.03 sec)
Rows matched: 2 Changed: 1 Warnings: 0



**4.然后注释掉skip-grant-tables参数**

重启mysql，用过期的密码就可以登陆了，登陆之后可以用下面的命令修改密码
\>alter user user() identified by '123456';
Query OK, 0 rows affected (0.03 sec)

\>flush privileges;
Query OK, 0 rows affected (0.03 sec)