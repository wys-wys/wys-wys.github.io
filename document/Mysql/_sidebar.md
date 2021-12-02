# [nginx检查报错：nginx: [emerg\] "server" directive is not allowed here in](https://www.cnblogs.com/orzs/p/11563875.html)

想检查一个配置文件是否正确，-c 指定之后发现有报错，如下：

```
[root@op-2:~# nginx -t -c /etc/nginx/conf.d/default.conf
nginx: [emerg] "server" directive is not allowed here in /etc/nginx/conf.d/default.conf:1
nginx: configuration file /etc/nginx/conf.d/default.conf test failed
```

 

有时候文件是正确无误，但是也会报错。

实际问题是进行语法检测的对象有问题；

要检测现有的修改过的Nginx配置是否有错误，不是只检测 .conf文件，而是不管任何时候，始终都是去检测主文件/etc/nginx/nginx.conf，只有这样，才能顺利的在对应的模块加载.conf 文件。

这样保证了配置的前后语境的正确性，这样才是真正的检测。

所以正确的检测修改的Nginx的语法是否错误的命令应该是： `nginx -t -c /etc/nginx/nginx.conf` ，如果配置文件有异常，会直接报出，否则就是

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

[root@op-2:~# nginx -t -c /etc/nginx/nginx.conf
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful


[root@op-2:~# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)