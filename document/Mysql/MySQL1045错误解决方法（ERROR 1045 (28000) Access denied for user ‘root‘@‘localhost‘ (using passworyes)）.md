# [MySQL1045错误解决方法（ERROR 1045 (28000): Access denied for user ‘root‘@‘localhost‘ (using passwor:yes)）](https://my.oschina.net/u/4393165/blog/4613449)

[osc_9ntog5yq](https://my.oschina.net/u/4393165)

2020/09/20 13:36

阅读数 3.4W

登录数据库时，发现数据库连接不上，报错如下：

![img](https://img-blog.csdnimg.cn/20200917194504718.png)

ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using passwor:yes)

为了以后方便排查，这里记录一下。

首先，停止MySQL服务

```bash
service mysqld stop
```

既然是密码错误，那么就先跳过密码验证的步骤

```bash
#vim /etc/my.cnf
```

然后，搜索mysqld，找到[mysqld]（port=3306上面那个）：

/mysqld(在vim编辑状态下直接输入该命令可搜索文本内容)。

注：windows下修改的是my.ini。

在 [mysqld] 底下添加语句：

```bash
skip-grant-tables
```

（注：skip-grant-tables：不启动grant-tables授权表，作为启动参数的作用：MYSQL服务器不加载权限判断，任何用户都能访问数据库）

这是用来跳过密码验证的，添加之后保存退出。

重新启动MySQL服务

进入MySQL

```bash
mysql -u root -p
```

出现密码输入时，不用输入直接按回车，就可以不用密码就能登录

修改密码

```bash
mysql> update user set password=password(“新密码”) where user=”用户名”;
```

如果报错：

ERROR 1054(42S22) Unknown column 'password' in 'field list'

原因： 5.7版本下的mysql数据库下已经没有password这个字段了，password字段改成了authentication_string

```bash
mysql> update user set authentication_string=password(“新密码”) where user=”用户名”;

#刷新MySQL权限相关的表
mysql> flush privileges;
mysql> exit;
```

密码修改完毕

编辑my.cnf（Windows下my.ini），将上面添加的内容去掉（skip-grant-tables）。

重启MySQL

使用新密码登录即可