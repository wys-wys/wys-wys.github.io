# [ESXi 配置公网访问](https://chenjiehua.me/linux/esxi-public-access-config.html) 

目录 [[隐藏](https://chenjiehua.me/linux/esxi-public-access-config.html#)]

- [1 ESXi](https://chenjiehua.me/linux/esxi-public-access-config.html#ESXi)
- [2 满满都是坑](https://chenjiehua.me/linux/esxi-public-access-config.html#i)
- [3 Haproxy 二次转发](https://chenjiehua.me/linux/esxi-public-access-config.html#Haproxy)
- [4 Nginx配置Https](https://chenjiehua.me/linux/esxi-public-access-config.html#NginxHttps)
- [5 VMWare远程连接](https://chenjiehua.me/linux/esxi-public-access-config.html#VMWare)

最近花费大价钱购入了一台工控软路由，打算来做迷你服务器，安装了 VMWare ESXi 做虚拟化。由于家里光纤没有公网，便用frp来做内网穿透，中间折腾许久踩了不少坑，顺便就记录一下笔记。



# ESXi

安装采用 VMWare ESXi 6.7，默认自动生成了一个不受信任的证书，内网使用IP访问虽然浏览器有提示不过也不影响使用：

![img](https://chenjiehua.me/wp-content/uploads/2020/04/exsi.png)

# 满满都是坑

首先我们使用 frp 来做内网穿透，在 esxi 上开一个虚拟机来跑 frpc，简单配置如下：

```
[common]
server_addr = chenjiehua.me     # frps服务器的IP或域名
server_port = 7000              # frps监听的端口

[esxi]
type = tcp 
local_ip = 10.0.0.20            # 内网ESXi的IP
local_port = 443                # ESXi要求使用https
remote_port = 5001              # 映射到frps服务器的端口
```

由于服务器上使用的是Nginx做 Web Server，我们还需要配置一下 nginx 来对外访问：

```
server {
        listen 80;
        index index.html index.htm;
        server_name esxi.chenjiehua.me;

        access_log /home/ubuntu/log/nginx/esxi.log main;
        error_log /home/ubuntu/log/nginx/esxi-err.log;

        location /ticket {
                proxy_pass http://127.0.0.1:5001;
                include proxy_params;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
        }

        location / {
                proxy_pass http://127.0.0.1:5001;
                include proxy_params;
        }
}
```

尝试通过外网域名访问一下，提示 502 Bad Gateway……

![img](https://chenjiehua.me/wp-content/uploads/2020/04/502.png)

查看Nginx日志，发现报错：

```
2020/04/05 11:08:01 [error] 361#361: *400035 upstream prematurely closed connection while reading response header from upstream, client: 120.230.127.182, server: esxi.chenjiehua.me, request: "GET /ui/ HTTP/1.1", upstream: "http://127.0.0.1:5001/ui/", host: "esxi.chenjiehua.me"
```

*upstream prematurely closed connection，*也就是说我们内网的 ESXi 过早的关闭了这个连接。

一番排查之后，怀疑是因为 ESXi 要求使用 https 访问，但是证书却又不受信任导致的。

那有没有什么办法可以忽略 https 么？

# Haproxy 二次转发

看了 frp 的配置文档，似乎并没有提供什么解决方法，于是便想是否可以尝试 haproxy 来再做一次转发，并忽略 ssl 校验。

果然，haproxy 的文档中：

```
5.Bind and server options
5.2.Server and default-server options

ssl
This option enables SSL ciphering on outgoing connections to the server. It
is critical to verify server certificates using "verify" when using SSL to
connect to servers, otherwise the communication is prone to trivial man in
the-middle attacks rendering SSL useless. When this option is used, health
checks are automatically sent in SSL too unless there is a "port" or an
"addr" directive indicating the check should be sent to a different location.
See the "no-ssl" to disable "ssl" option and "check-ssl" option to force
SSL health checks.

verify [none|required]
This setting is only available when support for OpenSSL was built in. If set
to 'none', server certificate is not verified. In the other case, The
certificate provided by the server is verified using CAs from 'ca-file' and
optional CRLs from 'crl-file' after having checked that the names provided in
the certificate's subject and subjectAlternateNames attributes match either
the name passed using the "sni" directive, or if not provided, the static
host name passed using the "verifyhost" directive. When no name is found, the
certificate's names are ignored. For this reason, without SNI it's important
to use "verifyhost". On verification failure the handshake is aborted. It is
critically important to verify server certificates when using SSL to connect
to servers, otherwise the communication is prone to trivial man-in-the-middle
attacks rendering SSL totally useless. Unless "ssl_server_verify" appears in
the global section, "verify" is set to "required" by default.
```

于是，我们增加 haproxy 转发：

```
listen esxi
	bind 127.0.0.1:15000
	mode tcp
	server myserver 10.0.0.20:443 ssl verify none
```

并修改 frpc 配置：

```
[esxi]
type = tcp
local_ip = 127.0.0.1
local_port = 15000     # 转发到 haproxy 监听的端口
remote_port = 5001
```

如此一顿骚操作下来，发现果然可以在外网通过域名访问了，简直想要来个双击666

# Nginx配置Https

然鹅……登录的时候竟然发现又出问题了（黑人问号？？？）

![img](https://chenjiehua.me/wp-content/uploads/2020/04/esxi-login-300x180.png)

查看了 Chrom 的网络请求，发现登录的时候会自动跳转到 https：

> ![img](https://chenjiehua.me/wp-content/uploads/2020/04/exsi-https.png)

看来服务器上Nginx还是需要配置 https 访问，通过 letencrypt 申请免费的 https 证书，然后修改 nginx 配置：

```
# esxi
server {
        listen 80;
        server_name esxi.chenjiehua.me;
        return 301 https://$host$request_uri$is_args$args;
}

server {
        listen 443 ssl;

        index index.html index.htm;
        server_name esxi.chenjiehua.me;

        ssl on;
        ssl_certificate /etc/letsencrypt/live/esxi.chenjiehua.me/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/esxi.chenjiehua.me/privkey.pem;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers "ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4";
        ssl_prefer_server_ciphers on;
        ssl_session_cache shared:SSL:10m;
        ssl_session_timeout 10m;

        access_log /home/ubuntu/log/nginx/esxi.log main;
        error_log /home/ubuntu/log/nginx/esxi-err.log;

        location /ticket {
                proxy_pass http://127.0.0.1:5001;
                include proxy_params;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
        }

        location / {
                proxy_pass http://127.0.0.1:5001;
                include proxy_params;
        }
        location ~ /.well-known {
                root /var/www;
        }
}
```

这下子终于可以正常在外网通过域名访问我们内网的ESXi服务器了。

# VMWare远程连接

上面的所有配置最后使得我们能够正常通过浏览器访问，但我们知道除了Web访问，其实ESXi也支持通过 VMWare Fusion（macOS）或VMWare Workstations（Windows）直接连接访问：

![img](https://chenjiehua.me/wp-content/uploads/2020/04/vmware-esxi.png)

在内网的情况下，我们直接填写 ESXi 服务器的IP地址即可顺利连接并访问到虚拟机。不过如果是通过公网域名访问，却会发现正常打开虚拟机，提示：

```
无法连接 MKS: Failed to connect to server esxi.chenjiehua.me:902
```

看来除了前面web端口需要设置内网穿透，还是多配置902端口：

```
[esxi2]
type = tcp
local_ip = 10.0.0.20
local_port = 902
remote_port = 902
```

果然一切都正常了。



 码字很辛苦，转载请注明来自**[ChenJiehua](https://chenjiehua.me/)**的[《ESXi 配置公网访问》](https://chenjiehua.me/linux/esxi-public-access-config.html)