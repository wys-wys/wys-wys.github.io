# CentOS7编译安装nginx

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_10632839)

[IT大表哥](https://blog.51cto.com/u_10632839)关注0人评论[1170人阅读](javascript:;)[2021-02-19 12:07:34](javascript:;)

系统版本
![CentOS7编译安装nginx](https://s4.51cto.com/images/blog/202102/19/e00af4b712cd9704d5bd2d828a12433d.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

1、安装nginx服务器需要的相关依赖

登录后复制

```
yum -y install gcc gcc-c++ zlib zlib-devel openssl openssl-devel pcre-devel
gcc gcc-c++编译环境
```

gzip 模块需要 zlib 库

rewrite 模块需要 pcre 库

ssl 功能需要openssl库

2、下载nginx源码包。

```
wget http://nginx.org/download/nginx-1.19.2.tar.gz
```

3、解压nginx源码包

```
tar xvf nginx-1.19.2.tar.gz
```

4、进入安装目录

cd nginx-1.19.2

5、使用./configure，生成配置文件makefile，并配置nginx的安装路径

./configure --prefix=/usr/local/nginx
![CentOS7编译安装nginx](https://s4.51cto.com/images/blog/202102/19/e1b1cc7c098f4c4f8542e016412b02a5.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

6、编译安装nginx

make && make install

7、因为编译需要配置才能使用systemctl启动，所以我们先通过安装路径启动一下我们的nginx

登录后复制

```
/usr/local/nginx/sbin/nginx 启动服务

/usr/local/nginx/sbin/nginx -s top 停止服务

/usr/local/nginx/sbin/nginx -s reload 重启服务
```

8、通过netstat -tnlp 或者 ps aux|grep nginx查看服务是否启动。

![CentOS7编译安装nginx](https://s4.51cto.com/images/blog/202102/19/49c6e646f32b9ca35fa4d75a42273ba4.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

9、测试(注意如果你用的是VMWare虚拟机的话，需要关闭防火墙，才能在我们的物理机访问nginx)
![CentOS7编译安装nginx](https://s4.51cto.com/images/blog/202102/19/1831e74712489c77aaf33b0f0b878309.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

10、给nginx配置通过systemctl启动,打开vim /usr/lib/systemd/system/nginx.service文件，输入以下内容:

[Unit]

Description=nginx - high performance web server

Documentation=http://nginx.org/en/docs/

After=network.target remote-fs.target nss-lookup.target

[Service]

Type=forking

ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf

ExecReload=/bin/kill -s HUP $MAINPID

ExecStop=/bin/kill -s QUIT $MAINPID

PrivateTmp=true

[Install]

WantedBy=multi-user.target

这个时候会出现如下图所示的报错
![CentOS7编译安装nginx](https://s4.51cto.com/images/blog/202102/19/55fc75042d5336dc7e590341371b11aa.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

解决方法如下:

[root@localhost ~]# mkdir /etc/systemd/system/nginx.service.d

[root@localhost ~]# printf "[Service]\nExecStartPost=/bin/sleep 0.1\n" > /etc/systemd/system/nginx.service.d/override.conf

[root@localhost ~]# systemctl deamon-reload 加载新的unit 配置文件

11、如下图所示就是配置成功了,可以设置一下开机自启动systemctl enable nginx.service

![CentOS7编译安装nginx](https://s4.51cto.com/images/blog/202102/19/8055cf74ccc2d30427826724319a02b8.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

©著作权归作者所有：来自51CTO博客作者IT大表哥的原创作品，如需转载，请注明出处，否则将追究法律责任

[linux](https://blog.51cto.com/search/result?q=linux)[centos](https://blog.51cto.com/search/result?q=centos)[nginx](https://blog.51cto.com/search/result?q=nginx)

0

分享

收藏

[下一篇：CentOS7.8通过QQ邮箱实...](https://blog.51cto.com/u_10632839/2633095)

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_10632839)

[IT大表哥](https://blog.51cto.com/u_10632839)

### 3篇文章，3413人气，0粉丝

#### 欢迎关注大表哥的微信公众号

关注

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_10632839)

Ctrl+Enter 发布

发布

取消



**0**



分享

关注TA解锁更多精彩文章

关注

[IT大表哥](https://blog.51cto.com/u_10632839)

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_10632839)

- 相关文章

  [适用于新手站长的Linux面板推荐，最重要的是免费！](https://blog.51cto.com/u_10632839/2633844)

  [CentOS7.8通过QQ邮箱实现邮件报警](https://blog.51cto.com/u_10632839/2633095)

  [Nginx工作原理](https://blog.51cto.com/u_14449530/2450997)

  [在Centos中yum安装和卸载软件的使用方法](https://blog.51cto.com/gzmaster/72278)

  [centos7手把手教你搭建zabbix监控](https://blog.51cto.com/xiaogongju/2084464)

  [centos7的网卡重启方法](https://blog.51cto.com/andyboge/2073420)

  [CentOS 7 网络配置详解](https://blog.51cto.com/simonhu/1588971)

  [Nginx配置跨域请求 Access-Control-Allow-Origin *](https://blog.51cto.com/u_13523664/2060430)

  [Centos7和Centos6.5密码破解](https://blog.51cto.com/u_13670314/2157265)

  [关于Nginx的server_name。](https://blog.51cto.com/onlyzq/535279)

  [服务器排障 之 nginx 499 错误的解决](https://blog.51cto.com/yucanghai/1713803)

  [史上最详细版Centos6安装详细教程](https://blog.51cto.com/u_13670314/2160430)

  [消息队列rabbitmq](https://blog.51cto.com/u_13107138/2767557)

  [使用Rocky Linux 8.3 RC1部署Jenkins搭建NodeJS与Java编译环境](https://blog.51cto.com/lidongni/2767201)

  [linux磁盘扩容](https://blog.51cto.com/u_15167199/2765572)

  [centos7.4升级openssh7.4p1到openssh8.5p1](https://blog.51cto.com/cherryqi/2764235)

  [CA证书申请颁发以及ssh服务详解](https://blog.51cto.com/puppydong/2764096)

  [k8s上使用prometheus监控websocket服务](https://blog.51cto.com/wutengfei/2763728)

  [Linux主机bonding的配置--采用主备模式](https://blog.51cto.com/u_15182035/2763573)

  [jenkins修改JENKINS_HOME及自启动配置](https://blog.51cto.com/m51cto/2762091)

## 推荐专栏[更多](https://blog.51cto.com/cloumn/index?utm_source=p)

[![img](https://s1.51cto.com/images/blog/201804/27/dc6736c5fd50474b5df8b76b040e3d03.jpg)](https://blog.51cto.com/cloumn/detail/5)

[带你玩转高可用](https://blog.51cto.com/cloumn/detail/5)

### 前百度高级工程师的架构高可用实战

#### 共15章 | [曹林华](https://blog.51cto.com/u_13527416)

##### ￥51.00 524人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/5)

[![img](https://s1.51cto.com/images/blog/201811/28/629650e188ddde78b213e564c2e9ebff.jpg)](https://blog.51cto.com/cloumn/detail/6)

[负载均衡高手炼成记](https://blog.51cto.com/cloumn/detail/6)

### 高并发架构之路

#### 共15章 | [sery](https://blog.51cto.com/sery)

##### ￥51.00 607人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/6)

[![img](https://s1.51cto.com/images/blog/201808/03/a940c66317ecbe58436a2ad3831c2d7d.png)](https://blog.51cto.com/cloumn/detail/13)

[基于Python的DevOps实战](https://blog.51cto.com/cloumn/detail/13)

### 自动化运维开发新概念

#### 共20章 | [抚琴煮酒](https://blog.51cto.com/yuhongchun)

##### ￥51.00 575人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/13)

[![img](https://s1.51cto.com/images/blog/201808/20/45862f289339dc922ffda669fd74ad9b.jpg)](https://blog.51cto.com/cloumn/detail/18)

[网工2.0晋级攻略 ——零基础入门Python/Ansible](https://blog.51cto.com/cloumn/detail/18)

### 网络工程师2.0进阶指南

#### 共30章 | [姜汁啤酒](https://blog.51cto.com/gingerbeer)

##### ￥51.00 2077人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/18)

[![img](https://s1.51cto.com/images/blog/201811/06/5353379fc95da1d7d34fd243b9ace17f.jpg)](https://blog.51cto.com/cloumn/detail/30)

[全局视角看大型园区网](https://blog.51cto.com/cloumn/detail/30)

### 路由交换+安全+无线+优化+运维

#### 共40章 | [51CTOsummer](https://blog.51cto.com/weilan2222)

##### ￥51.00 2648人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/30)

## 好课推荐[更多](https://edu.51cto.com/center/course/index/search?q=linux&qd=bkwz)

- ![linux网络基础](https://s1.51ctocdn.cn/images/201905/25/2af89a4ad9e66285c0371acf04112cdf.jpg)

  [linux网络基础26580人学习免费试看](http://edu.51cto.com/course/18243.html?qd=bloghktj)

- ![ linux存储](https://s1.51ctocdn.cn/images/avater/202012/332642f73a2b32de7e27311ac93fe270eb15f8.jpg)

  [linux存储934人学习免费试看](http://edu.51cto.com/course/26007.html?qd=bloghktj)

- ![linux基础知识和项目实战部署课程](https://s1.51ctocdn.cn/images/avater/202104/865abd656b03f021e3a002611185074ad95f0f.jpg)

  [linux基础知识和项目实战部署课程11233人学习免费试看](http://edu.51cto.com/course/22284.html?qd=bloghktj)

- ![Linux内核编程必备基础](https://s1.51ctocdn.cn/images/201905/22/34697361862f456a1d227c5503bac96c.jpg)

  [Linux内核编程必备基础15076人学习免费试看](http://edu.51cto.com/topic/2385.html?qd=bloghktj)