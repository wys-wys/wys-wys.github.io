

[Xray](https://www.v2rayssr.com/xray)

# X-ui，支持多协议多用户的 Xray 面板！V2-ui全面停止更新，后续逐渐用 X-ui 面板取代 V2-ui 面板！

- 3月前
- 0
- 52.1k



![img](https://www.v2rayssr.com/wp-content/uploads/thumb/2020/04/fill_w120_h120_g0_mark_1f58e4666a0e6f_1_avatar.png)

**V2raySSR综合网**V2raySSR综合网

关注 私信

文章导读目录



[前言](https://www.v2rayssr.com/x-ui.html#前言)[视频观看](https://www.v2rayssr.com/x-ui.html#视频观看)[功能介绍](https://www.v2rayssr.com/x-ui.html#功能介绍)[准备工作](https://www.v2rayssr.com/x-ui.html#准备工作)[安装 X-ui 面板](https://www.v2rayssr.com/x-ui.html#安装_X-ui_面板)[申请 SSL 证书](https://www.v2rayssr.com/x-ui.html#申请_SSL_证书)[更新及安装组件](https://www.v2rayssr.com/x-ui.html#更新及安装组件)[安装 Acme 脚本](https://www.v2rayssr.com/x-ui.html#安装_Acme_脚本)[80 端口空闲的证书申请方式](https://www.v2rayssr.com/x-ui.html#80_端口空闲的证书申请方式)[安装证书到指定文件夹](https://www.v2rayssr.com/x-ui.html#安装证书到指定文件夹)[安装 & 升级 X-ui 面板](https://www.v2rayssr.com/x-ui.html#安装_升级_X-ui_面板)[安装及升级的一键代码](https://www.v2rayssr.com/x-ui.html#安装及升级的一键代码)[节点配置及功能讲解](https://www.v2rayssr.com/x-ui.html#节点配置及功能讲解)[V2-ui - X-ui数据迁移](https://www.v2rayssr.com/x-ui.html#V2-ui_-_X-ui数据迁移)

## 前言

sprov 这位大神开发的这套面板程序，很是方便，可以可视化的搭建SS、V2ray、Xray、Trojan等热门的协议，并且可以实时看到 VPS 的性能状态以及流量的使用情况。

那在经过将近两年的不断更新之后，V2-ui面板，迎来了一个比较大的转折——停止更新了。

sprov 大神又用 GO 语言重新开发了一套面板 X-UI。那这套面板相比原来的 V2-ui，兼容性更强，也便于维护， GO 语言的性能更好，而且内存占用也会相对的低一些。

## 视频观看

[![img](https://www.v2rayssr.com/wp-content/uploads/2021/07/123123123123123123.png)](https://www.v2rayssr.com/go?url=https://youtu.be/6ztPETEiY8M)

## 功能介绍

- 系统状态监控
- 支持多用户多协议，网页可视化操作
- 支持的协议：vmess、vless、trojan、shadowsocks、dokodemo-door、socks、http
- 支持配置更多传输配置
- 流量统计，**限制流量**，**限制到期时间**
- 可自定义 xray 配置模板
- 支持 https 访问面板（自备域名 + ssl 证书）
- 更多高级配置项，详见该项目的 GitHub：[点击访问](https://www.v2rayssr.com/go?url=https://github.com/sprov065/x-ui)

![img](https://www.v2rayssr.com/wp-content/uploads/2021/07/1.png)

## 准备工作

1、VPS 一台重置好主流的操作系统 （CentOS 7+、Ubuntu 16+、Debian 8+），作者使用：[搬瓦工 VPS](https://www.v2rayssr.com/bwg.html)

2、域名一个，做好相关的解析，若是需要套用 CDN，请托管域名到 cloudflare ，[不会请点击](https://www.v2rayssr.com/yumingreg.html)

## 安装 X-ui 面板

### 申请 SSL 证书

下面环境的安装方式，大家根据自己的系统选择命令安装就好了。

#### 更新及安装组件

```
apt update -y          # Debian/Ubuntu 命令apt install -y curl    #Debian/Ubuntu 命令apt install -y socat    #Debian/Ubuntu 命令
yum update -y          #CentOS 命令yum install -y curl    #CentOS 命令yum install -y socat    #CentOS 命令
```

#### 安装 Acme 脚本

```
curl https://get.acme.sh | sh
```

#### 80 端口空闲的证书申请方式

自行更换代码中的域名、邮箱为你解析的域名及邮箱

```
~/.acme.sh/acme.sh --register-account -m xxxx@xxxx.com~/.acme.sh/acme.sh  --issue -d hk1.gcop.xyz   --standalone
```

#### 安装证书到指定文件夹

自行更换代码中的域名为你解析的域名

```
~/.acme.sh/acme.sh --installcert -d hk1.gcop.xyz --key-file /root/private.key --fullchain-file /root/cert.crt
```

### 安装 & 升级 X-ui 面板

#### 安装及升级的一键代码jj

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

#### 节点配置及功能讲解

![img](https://www.v2rayssr.com/wp-content/uploads/2021/07/2.png)

节点配置及龙能方面，请看 [视频教程](https://www.v2rayssr.com/go?url=https://youtu.be/6ztPETEiY8M)

#### V2-ui - X-ui数据迁移

安装完 X-ui 以后，输入以下代码，即可完成用户数据的迁移（不包含管理员账号及密码，仅针对已部署的节点部分）

```
x-ui v2-ui
```

迁移成功后请关闭 v2-ui 并且重启 x-ui，否则 v2-ui 的 inbound 会与 x-ui 的 inbound 会产生端口冲突，若是有问题，请看 [视频教程](https://www.v2rayssr.com/go?url=https://youtu.be/6ztPETEiY8M)

 

点点赞赏，手留余香

赞赏

还没有人赞赏，快来当第一个赞赏的人吧！



海报分享收藏

00

[SSL证书申请](https://www.v2rayssr.com/tag/ssl证书申请)[v2-ui停更](https://www.v2rayssr.com/tag/v2-ui停更)[v2-ui停止更新](https://www.v2rayssr.com/tag/v2-ui停止更新)[v2-ui无法使用](https://www.v2rayssr.com/tag/v2-ui无法使用)[X-ui](https://www.v2rayssr.com/tag/x-ui)[X-ui介绍](https://www.v2rayssr.com/tag/x-ui介绍)[X-ui教程](https://www.v2rayssr.com/tag/x-ui教程)[X-ui面板](https://www.v2rayssr.com/tag/x-ui面板)[Xray+面板](https://www.v2rayssr.com/tag/xray面板)[Xray可视化](https://www.v2rayssr.com/tag/xray可视化)[Xray搭建](https://www.v2rayssr.com/tag/xray搭建)[单台VPS多协议](https://www.v2rayssr.com/tag/单台vps多协议)[多协议搭建](https://www.v2rayssr.com/tag/多协议搭建)[多用户管理](https://www.v2rayssr.com/tag/多用户管理)[最新SSL证书申请](https://www.v2rayssr.com/tag/最新ssl证书申请)[科学上网](https://www.v2rayssr.com/tag/科学上网)[翻墙节点](https://www.v2rayssr.com/tag/翻墙节点)

[Xray](https://www.v2rayssr.com/xray)[优化加速](https://www.v2rayssr.com/v2ray-bbr)[客户端](https://www.v2rayssr.com/client)

## [【评测】机场推荐测评，老牌大机场8K翻墙无压力！生产环境翻墙必备，多地域原生IP看Netflix！](https://www.v2rayssr.com/airport.html)

2021-7-17 15:00:40

[客户端](https://www.v2rayssr.com/client)[技术教程](https://www.v2rayssr.com/skill)

## [最新科学上网客户端工具！Windows用户的福音，Clash.Net，clash内核，漂亮UI设计，强大的统计功能。](https://www.v2rayssr.com/clash_net.html)

2021-5-15 18:00:35