- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/benpao1314/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/奔跑中的兔子)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/benpao1314/rss/)

随笔- 181 文章- 3 评论- 7 阅读- 38万 

# [mysql报错：You must reset your password using ALTER USER statement before executing this statement.](https://www.cnblogs.com/benpao1314/p/11534696.html)

新安装mysql后，登录后，执行任何命令都会报错：

You must reset your password using ALTER USER statement before executing this statement.

![img](https://img2018.cnblogs.com/blog/1040820/201909/1040820-20190917160956046-368939061.png)

 

 

 【解决办法】

MySQL版本5.7.6版本以前用户可以使用如下命令：

mysql> SET PASSWORD = PASSWORD('root2019');
MySQL版本5.7.6版本开始的用户可以使用如下命令：

mysql> ALTER USER USER() IDENTIFIED BY 'root2019';



出现这种情况的原因：

MySQL版本5.6.6版本起，添加了password_expired功能，它允许设置用户的过期时间。这个特性已经添加到mysql.user数据表，但是它的默认值是”N”，可以使用ALTER USER语句来修改这个值。

输入以下命令，将账号密码强制到期：

mysql> ALTER USER 'yonghuming'@'localhost' PASSWORD EXPIRE;
此时，用户可以登录到MYSQL服务器，但是在用户没有设置新密码之前，不能运行任何命令，就会得到上图的报错，修改密码即可正常运行账户权限内的所有命令。由于此版本密码过期天数无法通过命令来实现，所以DBA可以通过cron定时器任务来设置MySQL用户的密码过期时间。

MySQL 5.7.4版开始，用户的密码过期时间这个特性得以改进，可以通过一个全局变量default_password_lifetime来设置密码过期的策略，此全局变量可以设置一个全局的自动密码过期策略。可以在MySQL的my.ini配置文件中设置一个默认值，这会使得所有MySQL用户的密码过期时间都为120天，MySQL会从启动时开始计算时间。my.ini配置如下：

[mysqld]
default_password_lifetime=120
如果要设置密码永不过期，my.cnf配置如下：

[mysqld]
default_password_lifetime=0
如果要为每个具体的用户账户设置单独的特定值，可以使用以下命令完成（注意：此命令会覆盖全局策略），单位是“天”，命令如下：

ALTER USER ‘yonghuming’@‘localhost' PASSWORD EXPIRE INTERVAL 250 DAY;
如果让用户恢复默认策略，命令如下：

ALTER USER 'yonghuming'@'localhost' PASSWORD EXPIRE DEFAULT;
个别使用者为了后期麻烦，会将密码过期功能禁用，命令如下：

ALTER USER 'yonghuming'@'localhost' PASSWORD EXPIRE NEVER;

分类: [Mysql](https://www.cnblogs.com/benpao1314/category/1069934.html)

# You must reset your password using ALTER USER statement before executing thi

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[你就像甜甜的益达](https://yidajava.blog.csdn.net/) 2019-09-11 15:10:11 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 38811 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 13

分类专栏： [mysql](https://blog.csdn.net/qq_38366063/category_8377563.html)

版权

新电脑安装mysql5.7通过client连接mysql想要修改密码:
一开始执行的是

```sql
update mysql.user set authentication_string=password('root') where user='root' and Host ='localhost';

12
```

然后报错:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911150829241.png)
原来一开始是没有密码的,在初始化的时候有个密码,只是相当于临时密码:
直接执行设置密码即可:

```
alter user user() identified by "root";
```