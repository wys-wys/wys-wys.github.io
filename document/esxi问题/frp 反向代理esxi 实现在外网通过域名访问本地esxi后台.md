# frp 反向代理esxi 实现在外网通过域名访问本地esxi后台

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Yionr](https://blog.csdn.net/weixin_42318691) 2020-09-04 06:50:30 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 2331 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

文章标签： [运维](https://www.csdn.net/tags/MtTaEg0sMDQyNTMtYmxvZwO0O0OO0O0O.html)

版权

# 期望效果

通过个人解析的域名`esxi.yionr.cn`访问本地内网的esxi后台，并且能操控每个虚拟机。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwMzczNC5wbmc?x-oss-process=image/format,png)

# 前言

搭建的方式有很多种，但是我在网上暂时没看到有很完善的教程，遂着笔此文。

本篇文章适合**会自己简单配置使用nginx(SSL)、frp**的玩家阅读。

# 环境描述与搭建

以下描述与本题相关的我的局域网环境：

- esxi的ip为192.168.1.5 ，本地第一次通过浏览器访问会出现证书错误的页面(相信大家都是这样的。。。)。
- esxi中有一台虚拟机用来做反向代理（总不可能直接在esxi上安装frp吧？不过也没试过欸），ip为192.168.1.4，下文称此机器为`代理机`（这台机器其实是我的黑群晖）

云端环境：

- 阿里云ecs中安装frps和nginx。
- 一个申请了ssl证书的域名地址`esxi.yionr.cn`（本文默认你会ssl证书的申请、ngxin带证书部署开启ssl访问等操作，不过其实这都很简单了，耐心看下阿里云有关nginx证书部署的相关文档就会了）

*双端的nginx均为最新版，frp为snowdreamtech/frp(s/c):0.31.2（不过这个应该不重要，之所以frp用这个版本是因为以前配置不来frp，所以不敢乱升级）*

## 搭建

### 本地环境

代理机nginx配置本地**随便**一个**不被占用**的端口转发至192.168.1.5，比如我使用的是9651端口

```conf
server{
    listen  9651;
    server_name     127.0.0.1;
    
    location / {
            proxy_pass https://192.168.1.5;
            proxy_redirect off;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
            proxy_set_header X-NginX-Proxy true;

			proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
    }
}
1234567891011121314151617
```

其中

```conf
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
123
```

这三句**很重要**，至于为什么在下文讲。

上一步配置成功并启动nginx之后，就能通过`http://192.168.1.4:9651`访问到esxi的登录界面了,而且并不会像直接访问192.168.1.5一样**强制转换为https然后警告证书错误**，这一点很重要。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIxMTkxNy5wbmc?x-oss-process=image/format,png)

然后配置frpc，最普通不过的配置

```ini
[common]
server_addr = xxx
server_port = 7000
token = xxx

[yionr-esxi]
type = http
local_ip = 127.0.0.1
local_port = 8
custom_domains = esxi.yionr.cn
12345678910
```

### 云端环境

frps也是用的最普通的配置，要和代理机中frpc配置的匹配上

```ini
[common]
bind_port = 7000
token = xxx
vhost_http_port = 520
1234
```

然后配置nginx，先配置**强制https**转发（如果不配置使用https访问，而直接用http访问的话，之后会出现问题，具体见下文问题解析：esxi登录页面提示“请刷新你的浏览器”）

```conf
server{
        listen  80;
        rewrite ^(.*)$  https://$host$1 permanent;
}
1234
```

然后配置esxi.yionr.cn 域名对应的配置文件。当ngxin收到`https://esxi.yionr.cn`的请求时，将请求转发到本地520端口处理。520端口就是我的frps中配置的http接收端口`vhost_http_port = 520`。

```conf
server{
        listen  443     ssl;
        server_name     esxi.absd.top;

        ssl_certificate /www/server/nginx/cert/absd.top.pem;
        ssl_certificate_key     /www/server/nginx/cert/absd.top.key;
        ssl_session_timeout     5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;

        location / {
                proxy_pass http://127.0.0.1:520;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $host;
                proxy_set_header X-Forward-Proto https;
                
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
        }
}
12345678910111213141516171819202122
```

这里需要注意的也是location中最后这三句。和代理机中的一样，这个的功能是开启nginx对于websocket的支持，esxi后台虚拟机控制台的图形化窗口就是通过websocket通信的，如果nginx不支持websocket，会导致无法使用esxi的控制台功能。（具体见下文问题解析：esxi控制台显示“无法连接”）

至此，启动双端的frp和云主机的nginx，就可以通过`https://esxi.yionr.cn`访问esxi了。以上就是我的成功案例，根据以上内容将ip地址、证书、域名和端口等内容换成自己的也没道理成功不了，加油！

# 各种可能出现的问题解析

以下会有部分问题我不知道出现的原因。但是我会通过将上面的正解修改个别配置从而复现问题。阅读我的配置方式，至少应该能让你知道问题出现在哪个环节。

## nginx502

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwNDc1Ny5wbmc?x-oss-process=image/format,png)

导致502的原因是本地没使用nginx将https代理为http，而直接使用https作为frp传输类型

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwNDkxMC5wbmc?x-oss-process=image/format,png)

然后在服务器nginx中也将请求转发至frps中配置的vhost_https_port端口

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwNTUwMS5wbmc?x-oss-process=image/format,png)

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwNTAyNS5wbmc?x-oss-process=image/format,png)

然后其实也能在nginx的日志中找到报错

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwNTcxMy5wbmc?x-oss-process=image/format,png)

*猜测是本地esxi证书错误导致的，所以我的解决方案在本地起了一个nginx将https转换为http，frp传输http流量*

# esxi控制台显示“无法连接”

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwMzkyNy5wbmc?x-oss-process=image/format,png)

根据别的博客，这有可能是浏览器的问题，可以换个浏览器试试。如果不行的话，那就是websocket传输受阻了，可以打开浏览器console看看是否有提示

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwNDEwNi5wbmc?x-oss-process=image/format,png)

如何解决？首先，frp是不需要额外配置websocket通信的，所以问题都会出现在nginx中，我的方案中有两个地方使用到了nginx，所以本地和云主机nginx的配置文件对应地方都要加上以下三句才能让websocket通信通顺。

```conf
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
123
```

具体配置见正文。

## esxi登录页面提示“请刷新你的浏览器”

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwMzIzMi5wbmc?x-oss-process=image/format,png)

（此时服务器端的配置）

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly95aW9uci5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltYWdlcy8yMDIwMDkwMzIwMzMwMS5wbmc?x-oss-process=image/format,png)

以上教程中，如果在服务器端nginx不配置ssl，直接通过http80端口接收esxi.yionr.cn的话，就会出现这个问题