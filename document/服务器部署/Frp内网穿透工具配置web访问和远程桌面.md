frp下载:
https://github.com/fatedier/frp/releases

`frpc` 是客户端 `frpc.ini` 是客户端配置
`frps` 是服务端 `frps.ini`是服务端配置

`_full.ini` 是对应配置文件的 所有参数的说明 里边有具体的注释

将服务端部署到有公网ip的那台主机
将客户端部署在内网机器

我需要内网穿透使用web服务和远程桌面
下面是我的配置(frp_0.29.0版本):

服务端配置:

```
[common]
bind_port = 7000 ;客户端和服务端之间通信的端口
vhost_http_port = 9000 ;对外网提供web访问的端口
token = 7777777;密钥 默认是12345678

dashboard_user = admin ;控制面板的用户名
dashboard_pwd = password ;控制面板的密码
dashboard_port = 7500 ;控制面板的端口
```

客户端配置:

```
[common]
server_addr = xx.xxx.xxx.xx;服务端ip
server_port = 7000;服务端通讯端口
token = 7777777;验证密钥


[web];第一个站点  通过www.xxx.com:9000访问
type = http;
local_port = 80 ;本地端口
custom_domains = www.xxx.com ;


[web2];第二个站点    通过dev.xxx.com:9000访问
type = http;
local_port = 8080;本地端口
custom_domains = dev.xxx.com ;


[RemoteDesktop]  通过tsc.xxx.com:9060 /进行远程桌面
type = tcp;
local_ip = 127.0.0.1;
local_port = 3389 ;
remote_port = 9060;
custom_domains = tsc.xxx.com ;

;[ssh]
;type = tcp
;local_ip = 127.0.0.1
;local_port = 22
;remote_port = 9002
```

启动程序

```
./frps -c ./frps.ini #服务端启动(linux)
frpc.exe -c frpc.ini #客户端启动(windows)
```

linux上如遇permission denied错误，表明frps可能没有运行权限，则先赋权然后再次启动：
`chmod 700 frps`

注意:
在阿里云腾讯云等服务商的控制面板将相关端口放行
安装了宝塔面板需要在面板 放行1-65535 端口

#### 开机自启

借助 winsw 工具可以将frpc注册为windows系统中的服务。实现开机自启。
(要注意以管理员方式运行)
参考文章:https://www.cnblogs.com/qianzf/p/6807167.html

我的winsw.xml:

```markup
<service>
     <id>frpc</id>
     <name>frpc</name>
     <description>内网穿透客户端</description>
     <executable>frpc</executable>
      <arguments>-c frpc.ini</arguments>
      <logmode>reset</logmode>
   </service>
```