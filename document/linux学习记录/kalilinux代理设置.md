- 
- apt 代理

/etc/apt/apt.conf
Acquire::ftp::proxy “ftp://127.0.0.1:8087/”
Acquire::http::proxy “http://127.0.0.1:8087/”
Acquire::https::proxy “https://127.0.0.1:8087/”
Acquire::socks::proxy “https://127.0.0.1:8087/”

- bash shell 代理

/etc/bash.bashrc
export ftp_proxy=“ftp://user:password@proxyIP:port”
export http_proxy=“http://user:password@proxyIP:port”
export https_proxy=“https://user:password@proxyIP:port”
export socks_proxy=“https://user:password@proxyIP:port”

- proxy chain 代理

代理链主要设置
\#dynamic_chain 动态代理链
中间如有掉线节点，自动跳过掉线的节点

# strict_chain 静态代理链

中间如有掉线节点，代理链将无法使用、

\#random_chain 随机代理链
\#chain_len = 2 随机代理链长度

\#proxy_dns 是否做dns代理

# 代理链

[ProxyList]

# add proxy here …

# meanwile

# defaults set to “tor”

socks4 127.0.0.1 9050
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
0x2 应用层代理

- tor匿名浏览器

去官网下载tor for linux 解压进入解压文件夹，在Browser文件夹同级有可执行程序，运行

可能出现如下错误：

tor默认进制root账号运行，可以修改Browser文件夹中的start-tor-browser
搜索root：

将这个0改成其他数字，如1，即可。

如果出现下述错误：

可以使用下面的命令：

目前在国内使用也需要进行初始化的配置，选择一个网桥。

0x3 其他浏览器或软件

如firefox、chrom等可以通过tor开启的代理服务从本地端口经由tor进行代理。

tor本地服务端口是9150

# linux给终端设置代理

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[weixin_30768661](https://me.csdn.net/weixin_30768661) 2013-09-04 22:58:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 70 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

版权

 由于众所周知的原因，用linux终端链接某些网站的时候会链接不上，

采用下面方式可以使用代理，

export http_proxy="代理地址:端口"

http代理：

http_proxy=http://IP地址:端口
ftp代理：
ftp_proxy=ftp://IP地址:端口

转载于:https://www.cnblogs.com/wwb0111/p/3302294.html