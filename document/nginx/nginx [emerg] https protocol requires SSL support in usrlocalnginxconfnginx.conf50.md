# [nginx: [emerg\] https protocol requires SSL support in /usr/local/nginx/conf/nginx.conf:50](https://www.cnblogs.com/dengxiaoning/p/12168865.html)

最近在nginx中配置一个443端口

### 一、安装nginx

首先得先安装个nginx

###### 1、安装依赖包

```shell
	# 一键安装上面四个依赖
	[root@dex ~]#  yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
```

###### 2、下载并解压nginx安装包

```shell
	# 创建一个文件夹
	[root@dex ~]#  cd /usr/local
	
	[root@dex local]#  mkdir nginx
	
	[root@dex local]#  cd nginx
	
	# 下载tar包
	[root@dex nginx]#  wget http://nginx.org/download/nginx-1.13.7.tar.gz
	
	# 解压 nginx 包
	[root@dex nginx]# tar -xvf nginx-1.13.7.tar.gz
```

[手动下载nginx http://nginx.org/en/download.html](http://nginx.org/en/download.html)

###### 3、执行安装nginx

```shell
	#进入nginx目录
	[root@dex nginx]# cd nginx-1.13.7
	
	#执行编译命令
	[root@dex nginx-1.13.7]# ./configure
	
	#执行make命令
	[root@dex nginx-1.13.7]#  make
	
	#执行make install命令
	[root@dex nginx-1.13.7]# make install
```

###### 4、配置nginx

```shell
	# 打开配置文件
	[root@dex ~]# vi /usr/local/nginx/conf/nginx.conf
```

###### 5、启动nginx

```shell
	[root@dex ~]#/usr/local/nginx/sbin/nginx
```

###### 6、查看nginx进程

```shell
	[root@dex nginx-1.13.7]# ps -ef|grep nginx
	root     22988     1  0 Dec20 ?        00:00:00 nginx: master process /usr/local/nginx/sbin/nginx
	nobody   22989 22988  0 Dec20 ?        00:00:00 nginx: worker process
	root     23638 23598  0 09:06 pts/0    00:00:00 grep --color=auto nginx
	[root@dex nginx-1.13.7]# 
```

### 二、下载ssl证书

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220222201687.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0ODE3NDQw,size_16,color_FFFFFF,t_70)
然后解压下载的 证书zip
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019122022224628.png)
会得到三个文件，我们打开nginx 的文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220222334112.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0ODE3NDQw,size_16,color_FFFFFF,t_70)

### 三、配置ssl

然后将这个两个文件上传到linux（我是上传到 /opt/sslCertificate/）目录下

```shell
	[root@dex ~]# ll /opt/sslCertificate/
	total 8
	-rw-r--r-- 1 root root 3733 Dec 20 21:25 1_www.benpaodehenji.com_bundle.crt
	-rw-r--r-- 1 root root 1704 Dec 20 21:25 2_www.benpaodehenji.com.key
```

ssl配置如下

```shell
    server {
        listen       443 ssl;
        server_name  www.benpaodehenji.com;

        ssl_certificate     /opt/sslCertificate/1_www.benpaodehenji.com_bundle.crt;
        ssl_certificate_key  /opt/sslCertificate/2_www.benpaodehenji.com.key;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        #ssl_ciphers  HIGH:!aNULL:!MD5;
        #ssl_prefer_server_ciphers  on;

        location / {
            root  /opt/html;
            index  index.html index.htm;
      }
        location /vueapp/ {
	    proxy_pass http://127.0.0.1:8191/;
       }
 
   }
```

然后监听80强制反向代理到https

```shell
    server {
        listen       80;
        server_name www.benpaodehenji.com ;
        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        
	    rewrite ^(.*)$ https://${server_name}$1 permanent;
		location  / {
			proxy_pass https://benpaodehenji.com;
		}
}
```

配置完成后运行`/usr/local/nginx/sbin/nginx -t` 时提示 如下错误

```shell
	[root@dex sbin]# ./nginx -t
	nginx: [emerg] https protocol requires SSL support in /usr/local/nginx/conf/nginx.conf:50
	nginx: configuration file /usr/local/nginx/conf/nginx.conf test failed
```

这个是nginx 不支持 https，接下来得进入如下配置，让其支持ssl

### 四、配置nginx 支持ssl

###### 1、首先`cd /usr/local/nginx/nginx-1.13.7` 然后执行如下命令

```shell
	[root@dex nginx-1.13.7]# ./configure --prefix=/usr/local/nginx --with-http_ssl_module
	checking for OS
	 + Linux 3.10.0-957.21.3.el7.x86_64 x86_64
	checking for C compiler ... found
	 + using GNU C compiler
	 + gcc version: 4.8.5 20150623 (Red Hat 4.8.5-39) (GCC) 
	.....省略
	  nginx http uwsgi temporary files: "uwsgi_temp"
	  nginx http scgi temporary files: "scgi_temp"
```

这里并可没有完，需要先停掉nginx 然后在执行make 进行重新编译
注意不要使用make install那样就是重新安装一次 nginx 了

```shell
	[root@dex nginx-1.13.7]# make
	make -f objs/Makefile
	make[1]: Entering directory `/usr/local/nginx/nginx-1.13.7'
	cc -c -pipe  -O -W -Wall -Wpointer-arith -Wno-unused-parameter -Werror -g  -I src/core -I src/event -I src/event/modules -I src/os/unix -I objs \
		-o objs/src/core/nginx.o \
	... 省略
	-ldl -lpthread -lcrypt -lpcre -lssl -lcrypto -ldl -lz \
	-Wl,-E
	sed -e "s|%%PREFIX%%|/usr/local/nginx|" \
		-e "s|%%PID_PATH%%|/usr/local/nginx/logs/nginx.pid|" \
		-e "s|%%CONF_PATH%%|/usr/local/nginx/conf/nginx.conf|" \
		-e "s|%%ERROR_LOG_PATH%%|/usr/local/nginx/logs/error.log|" \
		< man/nginx.8 > objs/nginx.8
	make[1]: Leaving directory `/usr/local/nginx/nginx-1.13.7'
```

###### 2、执行完成后，我们备份一下原来的nginx （这个以防万一，如果你的nginx中没有其他部署那倒是无所谓）

```shell
	[root@dex nginx-1.13.7]# cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx_bak
```

###### 3、 再把刚才编译的nginx 拷贝覆盖原来的nginx

```shell
	[root@dex nginx-1.13.7]# cp ./objs/nginx /usr/local/nginx/sbin/
```

###### 4、nginx 安装情况

```shel
	[root@dex nginx-1.13.7]# /usr/local/nginx/sbin/nginx -v
	nginx version: nginx/1.13.7
```

###### 5、 在执行一下nginx -t 检测一下

```shell
	[root@dex nginx-1.13.7]# /usr/local/nginx/sbin/nginx -t
	nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
	nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
```

###### 6、启动nginx

```shell
	[root@dex nginx-1.13.7]# /usr/local/nginx/sbin/nginx
	
	# 看看哈进程
	[root@dex nginx-1.13.7]# ps -ef|grep nginx
	root     22988     1  0 22:45 ?        00:00:00 nginx: master process /usr/local/nginx/sbin/nginx
	nobody   22989 22988  0 22:45 ?        00:00:00 nginx: worker process
	root     23014 20315  0 22:51 pts/0    00:00:00 grep --color=auto nginx
	[root@dex nginx-1.13.7]# 
```

记录下其他nginx相关命令

```shell
	./nginx 启动nginx
	./nginx -s quit:此方式停止步骤是待nginx进程处理任务完毕进行停止。
	./nginx -s stop:此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
	
	./nginx -s reload 重新加载配置
```

linux 进程查询、 关闭

```shell
	[root@dex sbin]# ps -ef|grep nginx
	nobody    6715 14665  0 Dec12 ?        00:00:00 nginx: worker process
	root     14665     1  0 Nov03 ?        00:00:00 nginx: master process /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
	root     22551 20315  0 22:06 pts/0    00:00:00 grep --color=auto nginx
	[root@dex sbin]# kill -9 14665
	[root@dex sbin]# kill -9 22551
	-bash: kill: (22551) - No such process
```