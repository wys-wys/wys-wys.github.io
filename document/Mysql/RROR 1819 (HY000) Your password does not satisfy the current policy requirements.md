# ERROR 1819 (HY000): Your password does not satisfy the current policy requirements

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[枕书年华](https://blog.csdn.net/calistom) 2019-02-26 17:56:37 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 26627 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 36

分类专栏： [数据库](https://blog.csdn.net/calistom/category_8702082.html)

版权

**之前在CentOS安装完MySQL修改默认密码时出现了如下错误:**

```shell
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
1
```

**原因是因为密码设置的过于简单会报错,MySQL有密码设置的规范，具体是与validate_password_policy的值有关,下图表明该值规则**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226144810183.png)
**如果想要查看MySQL完整的初始密码规则,登陆后执行以下命令**

```shell
SHOW VARIABLES LIKE 'validate_password%';
1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226180639819.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NhbGlzdG9t,size_16,color_FFFFFF,t_70)
**密码的长度是由validate_password_length决定的,但是可以通过以下命令修改**

```shell
set global validate_password_length=4;
1
```

**validate_password_policy决定密码的验证策略,默认等级为MEDIUM(中等),可通过以下命令修改为LOW(低)**

```shell
set global validate_password_policy=0;
1
```

**修改完成后密码就可以设置的很简单，比如1234之类的。**
如果需要转载, 转载时请注明博文出处！