# 



[![img](https://upload.jianshu.io/users/upload_avatars/832668/e9518d40b6fe?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/7753478e1554)

[乐百川](https://www.jianshu.com/u/7753478e1554)关注

22019.02.15 05:02:59字数 1,536阅读 20,925

![img](https://upload-images.jianshu.io/upload_images/832668-4a5c077115f04029.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

frp项目

如果你想把家里的电脑当做服务器用，做一个网站或者游戏服务器什么的，肯定会遇到一个问题：由于没有公网IP，而且有家里的路由器把关，导致其他地方的人完全无法连接到服务器。这时候就需要内网穿透和端口映射工具了，这样的工具有很多，我列举常用的几个：

- 花生壳
- nat123
- ngrok

不过这几个工具虽然都算是挺好用的，但是都是收费的，虽然都有免费版，但是免费版功能实在太少，基本上只能绑定一个应用，端口号还是随机的。临时玩玩倒是可以，真正要用的话还是不行。经过一番寻找，最后我锁定了frp这个工具，它的优点就是完全开源免费，自定义配置；缺点是不提供服务，也就是说我们需要自己买个服务器在上面搭建。

## 下载

frp也是托管在Github上的开源项目，直接到Release页面下载即可，链接如下：



```ruby
https://github.com/fatedier/frp/releases
```

![img](https://upload-images.jianshu.io/upload_images/832668-193224ea5fd6514f.png?imageMogr2/auto-orient/strip|imageView2/2/w/660/format/webp)

图片.png

下载解压之后是一个文件夹，里面包含了frpc、frps可执行程序，以及它们对应的示例配置文件，前者是客户端程序，后者是服务端程序。运行frp需要同时运行客户端和服务端程序才行。full和min分别是最大和最小配置文件，如果需要参考的话可以打开看看，最大配置文件中列出了frp支持的所有选项。

## 服务端配置

首先我们看看如何配置frp的服务端。服务端配置比较简单，如果不使用高级功能的话，只需要两三行就可以了。



```ini
# frps.ini
[common]
bind_port = 7000
token = 123456
```

bind_port是服务端与客户端之间通信使用的端口号，默认就可以。token用于验证连接，只有服务端和客户端token相同的时候才能正常访问。如果不使用token，那么所有人都可以直接连接上，所以我建议大家在使用的时候还是把token加上。

配置完毕后就可以启动服务端了，启动命令也很简单：



```css
frps -c frps.ini
```

一般情况下服务端这么配置就可以了，大部分配置都是在客户端的配置文件中处理。作者这样设计还是挺合理的，将来如果有改动的话，只需要修改客户端配置文件，服务端一般情况下不需要改动。

## 端口转发

下面来看看客户端配置，frp可以实现很多常用功能，都是在客户端配置文件中完成配置。首先来看看最基本的端口转发配置。



```ini
# frpc.ini
[common]
server_addr = x.x.x.x
server_port = 7000
token = 123456
[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
```

首先是common下的配置项，需要和服务端配置文件相同。然后是ssh下的配置，type是连接类型，大部分应用都是tcp协议的，所以这里就写tcp就好；local_ip是本地ip，默认127.0.0.1即可；local_port是要转发的端口号，官方实例中这里是远程转发SSH，所以端口号是22，如果你想做游戏服务器的话，改成对应的端口号即可；remote_port是端口转发之后暴露在外网的端口号。

客户端配置完毕之后，就可以启动了，启动命令类似：



```css
frpc -c frpc.ini
```

如果你想简单把本地部署的网站开放出去，也可以以这种方式直接将本地80端口转发出去。如果你购买了域名，希望别人通过域名访问本地网站，还可以使用接下来要介绍的，专门的web转发功能。

## 转发web服务

首先是服务端，需要添加vhost_http_port参数：



```ini
# frps.ini
[common]
bind_port = 7000
vhost_http_port = 80
```

然后是客户端，注意web下的参数，type是协议类型，http或者https，local_port是本地网站的端口号，custom_domains是购买的网站域名，需要注意这个网站域名需要事先在域名服务商那里设置好域名解析才能正常使用。



```ini
# frpc.ini
[common]
server_addr = x.x.x.x
server_port = 7000
[web]
type = http
local_port = 8080
custom_domains = www.yourdomain.com
```

配置完成后，访问服务器网址[http://x.x.x.x](http://x.x.x.x/)即可看到部署在本地[http://localhost:8080](http://localhost:8080/)上的网站。如果需要https的话，只要把vhost_http_port改成vhost_https_port，再把客户端web下type设置为https即可。

## 仪表盘

frp还支持仪表盘功能，可以从网页查看运行的流量等信息。开启仪表盘需要在服务端进行设置。



```ini
# frps.ini
[common]
dashboard_port = 7500
# dashboard 用户名密码，默认都为 admin
dashboard_user = admin
dashboard_pwd = admin
```

设置完毕后，在浏览器中访问服务端地址:端口号并输入用户名与密码即可查看仪表盘。

![img](https://upload-images.jianshu.io/upload_images/832668-c56ae4c8694dcb3c.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

仪表盘

以上就是frp的一些介绍，如果有需要的请查看官方中文文档，详细列出了frp支持的各项功能，还可以参考frpc_full.ini与frps_full.ini，查看完整配置文件支持的选项。文档地址：



```ruby
https://github.com/fatedier/frp/blob/master/README_zh.md
```

## 太阳神三国杀游戏服务器搭建

以前我也了解过frp，不过基本没用过。这几天和同学玩三国杀，我突然想到以前经常玩的太阳神三国杀，后来因为没有公网IP，再也没有和同学联机过。有了frp，我就可以让同学连接到我的游戏主机上。

服务端配置仍然是非常简单的那几行，就不说了。重点是客户端配置，其实也很简单，太阳神三国杀游戏使用的端口号是9527，所以直接把端口号改为9527即可。然后连接的时候输入服务器IP即可。



```ini
[common]
server_addr = xxxx
server_port = 7000
token = xxxxx

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 9527
remote_port = 9527
```

### 软件简介

frp 是一个高性能的反向代理应用，可以帮助您轻松地进行内网穿透，对外网提供服务，支持 tcp, http, https 等协议类型，并且 web 服务支持根据域名进行路由转发。

### frp 的作用

- 利用处于内网或防火墙后的机器，对外网环境提供 http 或 https 服务。
- 对于 http 服务支持基于域名的虚拟主机，支持自定义域名绑定，使多个域名可以共用一个80端口。
- 利用处于内网或防火墙后的机器，对外网环境提供 tcp 服务，例如在家里通过 ssh 访问处于公司内网环境内的主机。
- 可查看通过代理的所有 http 请求和响应的详细信息。（待开发）

### 开发状态

frp 目前正在前期开发阶段，master 分支用于发布稳定版本，dev 分支用于开发，您可以尝试下载最新的 release 版本进行测试。

目前的交互协议可能随时改变，不能保证向后兼容，升级新版本时需要注意公告说明。

### 架构

![img](http://static.oschina.net/uploads/space/2016/0801/113210_HnfV_2353773.png)

### 使用示例

  根据对应的操作系统及架构，从 [Release](https://github.com/fatedier/frp/releases) 页面下载最新版本的程序。

  将 frps 及 frps.ini 放到有公网 IP 的机器上。

  将 frpc 及 frpc.ini 放到处于内网环境的机器上。

### 通过 ssh 访问公司内网机器

1. 修改 frps.ini 文件，配置一个名为 ssh 的反向代理：`# frps.ini [common] bind_port = 7000 [ssh] listen_port = 6000 auth_token = 123`

2. 启动 frps：

   ```
   ./frps -c ./frps.ini
   ```

3. 修改 frpc.ini 文件，设置 frps 所在服务器的 IP 为 x.x.x.x：

   ```
   # frpc.ini
   [common]
   server_addr = x.x.x.x
   server_port = 7000
   auth_token = 123
   
   [ssh]
   local_port = 22
   ```

4. 启动 frpc：

   ```
   ./frpc -c ./frpc.ini
   ```

5. 通过 ssh 访问内网机器，假设用户名为 test：

   ```
   ssh -oPort=6000 test@x.x.x.x
   ```

### 通过指定域名访问部署于内网的 web 服务

有时想要让其他人通过域名访问或者测试我们在本地搭建的 web 服务，但是由于本地机器没有公网 IP，无法将域名解析到本地的机器，通过 frp 就可以实现这一功能，以下示例为 http 服务，https 服务配置方法相同， vhost_http_port 替换为 vhost_https_port， type 设置为 https 即可。

1. 修改 frps.ini 文件，配置一个名为 web 的 http 反向代理，设置 http 访问端口为 8080，绑定自定义域名 www.yourdomain.com:

   ```
   # frps.ini
   [common] bind_port = 7000
   vhost_http_port = 8080
   
   [web]
   type = http
   custom_domains = www.yourdomain.com
   auth_token = 123
   ```

   

2. 启动 frps；

   

   ```
   ./frps -c ./frps.ini
   ```

   

3. 修改 frpc.ini 文件，设置 frps 所在的服务器的 IP 为 x.x.x.x，local_port 为本地机器上 web 服务对应的端口：

   ```
   # frpc.ini
   [common]
   server_addr = x.x.x.x
   server_port = 7000
   auth_token = 123
   
   [web]
   type = http
   local_port = 80
   ```

   

4.  启动 frpc：

   

   ```
    ./frpc -c ./frpc.ini
   ```

   

5.  将 [www.yourdomain.com](http://www.yourdomain.com/) 的域名 A 记录解析到 x.x.x.x，如果服务器已经有对应的域名，也可以将 CNAME 记录解析到服务器原先的域名。

6. 通过浏览器访问 http://www.yourdomain.com:8080 即可访问到处于内网机器上的 web 服务。

### 开发计划

计划在后续版本中加入的功能与优化，排名不分先后，如果有其他功能建议欢迎在 [issues](https://github.com/fatedier/frp/issues) 中反馈。

- Dashboard 界面。
- 流量，连接数等代理信息统计与展示。
- udp 协议支持。
- 针对短连接的连接池优化。
- 特权模式支持端口白名单。
- 支持泛域名。
- 支持 url 路由转发。
- frpc 支持负载均衡到后端不同服务。
- frpc debug 模式，控制台显示代理状态，类似 ngrok 启动后的界面。
- frpc http 请求及响应信息展示。
- 支持 udp 打洞的方式，提供两边内网机器直接通信，流量不经过服务器转发。

