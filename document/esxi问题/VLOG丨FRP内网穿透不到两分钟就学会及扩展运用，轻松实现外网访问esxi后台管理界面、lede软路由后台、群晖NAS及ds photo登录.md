[VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录](https://www.vediotalk.com/archives/505)

2018.04.17 [VLOG](https://www.vediotalk.com/archives/category/feature) [内网穿透](https://www.vediotalk.com/archives/category/vt笔记/内网穿透) 74  [273 ](https://www.vediotalk.com/archives/505#comments) 112248 

目录



[视频介绍](https://www.vediotalk.com/archives/505#视频介绍)[注意：用国内服务器搭建，需要域名备案才能使用](https://www.vediotalk.com/archives/505#注意：用国内服务器搭建，需要域名备案才能使用)[一、frp的作用](https://www.vediotalk.com/archives/505#一、frp的作用)[二、配置说明](https://www.vediotalk.com/archives/505#二、配置说明)[1、实现功能](https://www.vediotalk.com/archives/505#1、实现功能)[2、配置前准备](https://www.vediotalk.com/archives/505#2、配置前准备)[三、安装frp](https://www.vediotalk.com/archives/505#三、安装frp)[1、公网服务器与内网服务器都需要下载frp进行安装](https://www.vediotalk.com/archives/505#1、公网服务器与内网服务器都需要下载frp进行安装)[2、下载地址是https://github.com/fatedier/frp/releases](https://www.vediotalk.com/archives/505#2、下载地址是https_//github_com/fatedier/frp/releases)[3.在WINDOWS下用winscp软件登录，上传frp_0.16.1_linux_amd64.tar.gz至root目录](https://www.vediotalk.com/archives/505#3_在WINDOWS下用winscp软件登录，上传frp0_16_1linuxamd64_tar_gz至root目录)[4.解压文件：](https://www.vediotalk.com/archives/505#4_解压文件：)[5.进入解压目录：](https://www.vediotalk.com/archives/505#5_进入解压目录：)[6.配置服务端：](https://www.vediotalk.com/archives/505#6_配置服务端：)[四、启动服务端](https://www.vediotalk.com/archives/505#四、启动服务端)[临时启动](https://www.vediotalk.com/archives/505#临时启动)[后台保持启动](https://www.vediotalk.com/archives/505#后台保持启动)[五、配置客户端](https://www.vediotalk.com/archives/505#五、配置客户端)[六、启动客户端](https://www.vediotalk.com/archives/505#六、启动客户端)[临时启动](https://www.vediotalk.com/archives/505#临时启动-2)[后台保持启动](https://www.vediotalk.com/archives/505#后台保持启动-2)[七、穿透公司代理内网](https://www.vediotalk.com/archives/505#七、穿透公司代理内网)[1.修改服务端配置文件](https://www.vediotalk.com/archives/505#1_修改服务端配置文件)[2.修改客户端配置文件](https://www.vediotalk.com/archives/505#2_修改客户端配置文件)[服务端与客户端启动方式不变，参照四、六。](https://www.vediotalk.com/archives/505#服务端与客户端启动方式不变，参照四、六。)[八、群晖NAS使用frp穿透服务](https://www.vediotalk.com/archives/505#八、群晖NAS使用frp穿透服务)[①.设置ROOT密码，获取群晖的ROOT权限](https://www.vediotalk.com/archives/505#①_设置ROOT密码，获取群晖的ROOT权限)[1.打开控制面板,开启SSH功能](https://www.vediotalk.com/archives/505#1_打开控制面板,开启SSH功能)[2.终端输入命令ssh admin@192.168.1.201登录，密码为群辉NAS的用户密码（地址修改为自己的NAS地址，win用户用Putty这个软件登录）](https://www.vediotalk.com/archives/505#2_终端输入命令ssh_admin@192_168_1_201登录，密码为群辉NAS的用户密码（地址修改为自己的NAS地址，win用户用Putty这个软件登录）)[3.输入命令](https://www.vediotalk.com/archives/505#3_输入命令)[4.设置root密码](https://www.vediotalk.com/archives/505#4_设置root密码)[②.客户端调试](https://www.vediotalk.com/archives/505#②_客户端调试)[1.使用root用户登录群晖6.1](https://www.vediotalk.com/archives/505#1_使用root用户登录群晖6_1)[2.群晖NAS登陆后台配置文件](https://www.vediotalk.com/archives/505#2_群晖NAS登陆后台配置文件)[2.使用群晖NAS手机APP的DS photo软件在外网访问配置文件](https://www.vediotalk.com/archives/505#2_使用群晖NAS手机APP的DS_photo软件在外网访问配置文件)[九、外网访问esxi后台管理、群晖NAS、群晖NAS客户端DS Photo、LEDE软路由后台](https://www.vediotalk.com/archives/505#九、外网访问esxi后台管理、群晖NAS、群晖NAS客户端DS_Photo、LEDE软路由后台)[十、用谷歌云和vultr服务器搭建frp无法使用 需要开放7000端口](https://www.vediotalk.com/archives/505#十、用谷歌云和vultr服务器搭建frp无法使用_需要开放7000端口)[十一、如何让Frp在群晖中自动开机运行](https://www.vediotalk.com/archives/505#十一、如何让Frp在群晖中自动开机运行)[1.进入群晖控制面板》任务计划》新增》触发任务》用户定义的脚本](https://www.vediotalk.com/archives/505#1_进入群晖控制面板》任务计划》新增》触发任务》用户定义的脚本)[2.添加脚本](https://www.vediotalk.com/archives/505#2_添加脚本)[3.按照下图的序号号顺序操作，重启群晖NAS即可](https://www.vediotalk.com/archives/505#3_按照下图的序号号顺序操作，重启群晖NAS即可)

收藏 6

# [![VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/04/frp.jpg)](https://www.vediotalk.com/wp-content/uploads/2018/04/frp.jpg)



[国内播放节点](https://www.bilibili.com/video/av22246557)

------

#### 视频介绍

frp内网穿透比ngrok要简单的多，无需多复杂的配置就可以达到比较好的穿透效果，扩展性也很强。

------

# 注意：用国内服务器搭建，需要域名备案才能使用

# 一、frp的作用

利用处于内网或防火墙后的机器，对外网环境提供 http 或 https 服务。
对于 http, https 服务支持基于域名的虚拟主机，支持自定义域名绑定，使多个域名可以共用一个80端口。
利用处于内网或防火墙后的机器，对外网环境提供 tcp 和 udp 服务，例如在家里通过 ssh 访问处于公司内网环境内的主机

# 二、配置说明

### 1、实现功能

（1）外网通过ssh访问内网机器
（2）自定义绑定域名访问内网web服务

### 2、配置前准备

（1）公网服务器1台
（2）内网服务器1台
（3）公网服务器绑定域名1个
（4）内网服务器部署一个web服务

# 三、安装frp

### 1、公网服务器与内网服务器都需要下载frp进行安装

### 2、下载地址是https://github.com/fatedier/frp/releases

也可以通过命令下载：

```
wget https://github.com/fatedier/frp/releases/download/v0.16.1/frp_0.16.1_linux_amd64.tar.gz
```

### 3.在WINDOWS下用winscp软件登录，上传frp_0.16.1_linux_amd64.tar.gz至root目录

### 4.解压文件：

```
tar -zxvf frp_0.16.1_linux_amd64.tar.gz
```

### 5.进入解压目录：

```
cd frp_0.16.1_linux_amd64
```

frps、frps.ini这个两个是服务端文件，frpc、frpc.ini这两个是客户端文件

### 6.配置服务端：

```
vi ./frps.ini
[common]
bind_port = 7000        #与客户端绑定的进行通信的端口
vhost_http_port = 80    #访问客户端web服务自定义的端口号
vhost_https_port = 443
token = 12345678        #秘钥可以自己修改
```

按”i”键进行编辑，按“esc”退出编辑状态，输入“:wq”退出

# 四、启动服务端

### 临时启动

```
./frps -c ./frps.ini
```

### 后台保持启动

```
nohup ./frps -c ./frps.ini &
```

# 五、配置客户端

```
vi ./frpc.ini
[common]  
server_addr = 120.56.37.48      #公网服务器ip  
server_port = 7000              #与服务端bind_port一致
token = 12345678               #与服务端秘钥一致
  
#公网通过ssh访问内部服务器  
[ssh]  
type = tcp                      #连接协议  
local_ip = 127.0.0.1            #内网服务器ip  
local_port = 22                 #ssh默认端口号  
remote_port = 6000              #自定义的访问内部ssh端口号  
  
#公网访问内部web服务器以http方式  
[web]  
type = http                     #访问协议
local_ip = 127.0.0.1            #内网服务器ip 
local_port = 80                 #内网web服务的端口号  
custom_domains = www.veelove.cn,veelove.cn   
#所绑定的公网服务器域名，一级、二级域名都可以，绑定多个域名时用英文“,”分开
```

# 六、启动客户端

### 临时启动

```
./frpc -c ./frpc.ini
```

### 后台保持启动

```
nohup ./frpc -c ./frpc.ini &
```

# 七、穿透公司代理内网

### 1.修改服务端配置文件

```
vi ./frps.ini
[common]
bind_port = 443        #端口号修改为443
vhost_http_port = 80    #访问客户端web服务自定义的端口号
token = 12345678       #与服务端秘钥一致
```

### 2.修改客户端配置文件

```
vi ./frpc.ini
[common]
server_addr = 118.24.127.138
server_port = 443                            #端口号修改为443
http_proxy = http://10.168.57.241:8088       #加入公司代理地址

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[web]
type = http
local_ip = 127.0.0.1
local_port = 80
custom_domains = www.veelove.cn
```

### 服务端与客户端启动方式不变，参照四、六。

# 八、群晖NAS使用frp穿透服务

## ①.设置ROOT密码，获取群晖的ROOT权限

## 1.打开控制面板,开启SSH功能

[![VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/FE841EBA-76C5-48E7-B063-351ECE53453F.jpg)](https://www.vediotalk.com/wp-content/uploads/2018/03/FE841EBA-76C5-48E7-B063-351ECE53453F.jpg)

## 2.终端输入命令ssh admin@192.168.1.201登录，密码为群辉NAS的用户密码（地址修改为自己的NAS地址，win用户用Putty这个软件登录）

[![VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-03-28-%E4%B8%8B%E5%8D%883.30.17.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/屏幕快照-2018-03-28-下午3.30.17.png)

## 3.输入命令

```
sudo -i
```

## 4.设置root密码

```
synouser --setpw root XXX
```

【XXX便是你要修改的密码】

## ②.客户端调试

### 1.使用root用户登录群晖6.1

```
ssh root@192.168.1.201
```

(地址修改为自己的群晖NAS地址)

### 2.群晖NAS登陆后台配置文件

```
[common]
server_addr = 118.24.127.138
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[nasweb]  
type = http                   
local_ip = 127.0.0.1           
local_port = 5000                     #群晖NAS登陆地址端口是5000
custom_domains = nas.veelove.cn
```

### 2.使用群晖NAS手机APP的DS photo软件在外网访问配置文件

```
[common]
server_addr = 118.24.127.138
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[nasweb]  
type = http                   
local_ip = 127.0.0.1           
local_port = 5000                     #群晖NAS登陆地址端口是5000
custom_domains = nas.veelove.cn

[nasphoto]  
type = tcp                             #协议为TCP协议
local_ip = 127.0.0.1           
local_port = 80
remote_port = 8000                    #需要做一个端口转发才可以实现APP登陆，端口自定义
custom_domains = photo.veelove.cn
```

# 九、外网访问esxi后台管理、群晖NAS、群晖NAS客户端DS Photo、LEDE软路由后台

```
[common]
server_addr = 118.24.127.138             #更换为自己服务器IP地址
server_port = 7000

[lede]
type = http                              #协议为http
local_ip = 192.168.1.1                   #保持不变，如果您更换过lede后台地址，请自行修改
local_port = 80
custom_domains = lede.veelove.cn         #更换为自己的域名

[esxi]
type = https                             #协议为https
local_ip = 192.168.1.101                 #更换为自己esxi后台管理地址
local_port = 443
custom_domains = esxi.veelove.cn         #更换为自己的域名

[dsphoto]
type = tcp                               #协议为tcp
local_ip = 127.0.0.1
local_port = 80
remote_port = 8000                       #转发端口可以自己设定
custom_domains = photo.veelove.cn        #更换为自己的域名

[dsm]
type = http                              #协议为http
local_ip = 127.0.0.1
local_port = 5000
custom_domains = nas.veelove.cn          #更换为自己的域名
```

# 十、用谷歌云和vultr服务器搭建frp无法使用 需要开放7000端口

[解决方法直通车](https://www.vediotalk.com/?p=520)

# 十一、如何让Frp在群晖中自动开机运行

### 1.进入群晖控制面板》任务计划》新增》触发任务》用户定义的脚本

[![VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/04/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-04-23-%E4%B8%8A%E5%8D%887.58.15.png)](https://www.vediotalk.com/wp-content/uploads/2018/04/屏幕快照-2018-04-23-上午7.58.15.png)

### 2.添加脚本

```
/root/frp/frpc -c /root/frp/frpc.ini
```

上面的frp修改为你frp目录的文件名称，我在视频里面建议是修改为frp方便记忆

[![VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/04/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-04-23-%E4%B8%8A%E5%8D%888.11.45.png)](https://www.vediotalk.com/wp-content/uploads/2018/04/屏幕快照-2018-04-23-上午8.11.45.png)

### 3.按照下图的序号号顺序操作，重启群晖NAS即可

[![VLOG丨FRP内网穿透不到两分钟就学会及扩展运用，轻松实现外网访问esxi后台管理界面、lede软路由后台、群晖NAS及ds photo登录 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/04/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-04-23-%E4%B8%8A%E5%8D%887.59.51.png)](https://www.vediotalk.com/wp-content/uploads/2018/04/屏幕快照-2018-04-23-上午7.59.51.png)

转载原创文章请注明，转载自: [Vedio Talk ](https://www.vediotalk.com/)- [VLOG丨](https://www.vediotalk.com/archives/505)