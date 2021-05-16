# [配置nginx 支持php](https://www.cnblogs.com/liyuanhong/p/12017232.html)

一、确保php-fpm已经启动：

```
ps -A | grep php-fpm
```

如果没有启动，则启动php-fpm：

```
/usr/local/sbin/php-fpm
```

查看是否启动成功：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
root@iZ25fm7iewtZ:/usr/local/etc# ps -ef | grep php-fpm
root      3691     1  0 18:49 ?        00:00:00 php-fpm: master process (/usr/local/etc/php-fpm.conf)
www-data  3692  3691  0 18:49 ?        00:00:00 php-fpm: pool www      
www-data  3693  3691  0 18:49 ?        00:00:00 php-fpm: pool www      
root      4982 29553  0 18:59 pts/1    00:00:00 grep --color=auto php-fpm


root@iZ25fm7iewtZ:/usr/local/etc# netstat -tnl | grep 9000
tcp        0      0 127.0.0.1:9000          0.0.0.0:*               LISTEN  
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

修改nginx的配置文件，支持php文件的解析，找到location的添加位置，在后面添加下面这个location

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
location ~ \.php$ {
            root           /usr/local/nginx/html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            #fastcgi_param  SCRIPT_FILENAME  /usr/local/nginx/html/$fastcgi_script_name;
            #以下方式也可以
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

重启nginx

```
service nginx restart
```

进入web更目录，编辑index.php

```
<?php``  ``echo ``"hello php !"
```

浏览器中输入：localhost/index.php 即可

博客里大都是转载的内容，其目的主要用户知识的组织和管理。

分类: [php](https://www.cnblogs.com/liyuanhong/category/1610476.html), [运维](https://www.cnblogs.com/liyuanhong/category/1027435.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/sample_face.gif)](https://home.cnblogs.com/u/liyuanhong/)

[远洪](https://home.cnblogs.com/u/liyuanhong/)
[关注 - 0](https://home.cnblogs.com/u/liyuanhong/followees/)
[粉丝 - 38](https://home.cnblogs.com/u/liyuanhong/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/liyuanhong/p/12016767.html)上一篇： [centos7编译安装php 遇到的问题](https://www.cnblogs.com/liyuanhong/p/12016767.html)
[» ](https://www.cnblogs.com/liyuanhong/p/12017935.html)下一篇： [linux下安装编译为安装的php扩展](https://www.cnblogs.com/liyuanhong/p/12017935.html)