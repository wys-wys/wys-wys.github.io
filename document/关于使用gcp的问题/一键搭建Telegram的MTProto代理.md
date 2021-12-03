# 一键搭建Tele[Telegram 代理](https://tizi.blog/telegram-代理)

# 一键搭建Telegram的MTProto代理

[梯子博客 ](https://tizi.blog/author/vpntool)• July 27, 2021 9:13 pm • [Telegram 代理](https://tizi.blog/telegram-代理)

### MTProto协议介绍

MTProto协议是 Telegram 为了对抗网络封锁开发的专用代理（MTProxy）协议，目前全平台的 TG 客户端中都支持MTProto协议和MTProxy代理。有了MTProxy代理，即使没有VPN或者其他代理的情况下，也能顺畅访问TG。

本文介绍一键搭建Telegram的MTProto代理。

### 一键搭建Telegram的MTProto代理

第一步，请准备一台境外的VPS，购买可参考 CN2 GIA VPS和商家推荐 或 做站VPS推荐，操作系统选 CentOS 7/8、Ubuntu 16/18/20，或者Debian 8/9/10；

第二步，SSH登录到服务器，windows可参考 Bitvise连接Linux服务器教程，mac用户请参考 Mac电脑连接Linux教程；

第三步，执行下面的命令一键搭建Telegram的MTProto代理：

\# CentOS/AliyunOS/AMI系统

```
yum install -y curl
bash <(curl -sL https://storage.googleapis.com/tiziblog/mt_setup.sh)
```

\# Ubuntu/Debian系统

```
apt install -y curl
bash <(curl -sL https://storage.googleapis.com/tiziblog/mt_setup.sh)
```

输入命令后，会出现如下菜单：

[![一键安装MTProto代理](https://tizi.blog/wp-content/uploads/2021/07/0210725211816.png)](https://tizi.blog/wp-content/uploads/2021/07/0210725211816.png)

首次使用输入 1，然后回车，按照提示输入一个端口号并回车（端口号随便设置，不和其他软件冲突即可）。

安装成功后，会输出如下信息：

[![MTPROTO代理信息](http://tizi.blog/wp-content/uploads/2021/07/6eccc-20210725211837.png)](http://tizi.blog/wp-content/uploads/2021/07/6eccc-20210725211837.png)

第三步，接下来打开TG客户端，参考 配置Telegram走SS/SSR/V2ray/trojan代理 的操作添加自定义代理，选择MTPROTO，将一键脚本输出的IP、端口和密钥填上去，点击保存：

[![配置Telegram走MTPROTO代理](http://tizi.blog/wp-content/uploads/2021/07/437c3-469838454-5fde3b5dda17f_fix732.png)](http://tizi.blog/wp-content/uploads/2021/07/437c3-469838454-5fde3b5dda17f_fix732.png)

[![配置Telegram走MTPROTO代理](http://tizi.blog/wp-content/uploads/2021/07/b7cf4-1041118037-5fde3b7fd83df_fix732.png)](http://tizi.blog/wp-content/uploads/2021/07/b7cf4-1041118037-5fde3b7fd83df_fix732.png)

[![配置Telegram走MTPROTO代理](http://tizi.blog/wp-content/uploads/2021/07/68309-2345975146-5fde3b9831d95_fix732.png)](http://tizi.blog/wp-content/uploads/2021/07/68309-2345975146-5fde3b9831d95_fix732.png)

接下来，就可以在不开启代理/VPN的情况下使用TG客户端了。

### 注意事项

目前MTProto已经发展到第三代，已经不建议使用V2ray内置的MTProto来搭建
本脚本使用了 9seconds 的docker镜像搭建；
因为docker访问外网需求，因此禁用了VPS的防火墙。如果你的VPS用于网站等重要业务，不建议使用本脚本搭建；
如果有国内VPS，建议使用 中转，防止被封；
MTProto很可能过一段时间就导致被封，稳妥的方法还是使用带伪装的V2ray或者trojan，然后参考 配置Telegram走SS/SSR/V2ray/trojan代理 的操作使用TG。

### 分享到：

- [Facebook](https://tizi.blog/33.html?share=facebook&nb=1)
- [更多](https://tizi.blog/33.html#)
- 

### 赞过：gram的MTProto代理