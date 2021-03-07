TOC[1. 简介](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#简介)[2. 下载安装](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#下载安装)[3. 快速上手](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#快速上手)[4. 更多](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#更多)[4.1. 怎样确认自己是否连接成功？怎样判断是否分流成功？](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#怎样确认自己是否连接成功？怎样判断是否分流成功？)[4.2. 代理生效了，但就是进不去游戏？](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#代理生效了，但就是进不去游戏？)[4.3. 代理模式种没有我想玩的游戏？](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#代理模式种没有我想玩的游戏？)[4.4. Win10 开启代理后 CPU 占用很高](https://wiki.kache.moe/2019/11/19/Windows-SSTap/#Win10-开启代理后-CPU-占用很高)

# Windows - SSTap 使用教程

2019-11-19 

- [Windows](https://wiki.kache.moe/categories/Windows/)

 26703

## 简介

SSTap 全称 SOCKSTap, 是一款利用虚拟网卡技术在网络层实现的代理工具。SSTap 能在网络层拦截所有连接并转发给 HTTP, SOCKS4/5, SHADOWSOCKS(R) 代理，而无需对被代理的应用程序做任何修改或设置。它能同时转发 TCP, UDP 数据包，非常适合于游戏玩家使用。

这是一个免费的工具，仅有应用内常驻非弹出式广告，并不会影响使用体验。（也有第三方去广告版本）

作者声称硬盘损坏，数据丢失，现已停止开发。所以后续不会再有更新了，未来也许会不可用。

整理教程时的系统环境：

Windows 10 1903
SSTap KYO （去广告免安装版）

此文档适用于：`卡车极速/N3RO`
文档中的某些内容可能随时间变化而失效。

## 下载安装

各历史版本收藏：https://github.com/solikethis/SSTap-backup

若您不清楚如何在 Github 下载软件，可参考下图：

- **下载单个文件:** 点击想要下载的版本 → 点击右侧的 **Download**

  ![下载单个版本.jpg](https://i.loli.net/2019/11/21/A2dqpfG9US8Bikl.jpg)

  下载单个版本.jpg

- **下载所有文件：**点击绿色的 **Clone or Download** → 选择 **Download ZIP** 即可打包下载所有文件。

  ![下载全部.jpg](https://i.loli.net/2019/11/21/IaxDXf73VihpvAF.jpg)

  下载全部.jpg

**软件官网：** https://www.sockscap64.com/

第一次安装的话会弹出提示安装一个虚拟网卡驱动， 这是因为 SSTap 需要使用 OpenVPN 的 TAP 设备驱动来创建虚拟网卡以实现类似 VPN 的效果。 点击“安装”即可。

![SSTAP安装虚拟网卡.jpg](https://i.loli.net/2019/11/19/DQW4F9cxRVCYeKa.jpg)

SSTAP安装虚拟网卡.jpg

仅推荐 **1.0.9.7 版本** 及 **KYO 去广告版本**，不推荐最新的版本（1.1.0.1），因为限制了网页/浏览器加速功能。

如果 使用的是免安装版本，运行时提示没有 TAP 适配器或无法运行，可以直接安装 [Tap-Windows](https://build.openvpn.net/downloads/releases/latest/tap-windows-latest-stable.exe) 适配器。
或者通过安装 [OpenVPN](https://openvpn.net/community-downloads/) 的方式获得该适配器。
也可以直接使用安装版 SSTap 。

SSTap 本身使用了版本较旧的 .NET Framework 且使用的代码写法已经过时，因此不支持 TLSv1.0 以上的版本。

## 快速上手

以 KYO (1.0.9.7) 去广告版本为例。此版本直接双击运行主程序即可。

![免安装版本直接双击运行.jpg](https://i.loli.net/2019/11/19/CQtSvhyK54wuYmH.jpg)

免安装版本直接双击运行.jpg

![SSTap主界面.png](https://i.loli.net/2019/11/19/txF9bo21RzTi6Yy.png)

SSTap主界面.png

### 添加节点

SSTap 添加节点主要有两个入口：**“代理”右边的绿色加号 & 右下角的小齿轮**

#### 通过绿色加号添加节点：

![SSTap添加节点.jpg](https://i.loli.net/2019/11/19/1isgGkJwMeT9qyc.jpg)

SSTap添加节点.jpg

- SOCKS5

  如果你是使用 SS/SSR 代理，那么建议直接使用下面的 SS/SSR 代理添加，不推荐使用 SOCKS5 去 连接 SS/SSR 的 SOCKS5 本地端口，因为这样的话你还需要额外将 SS/SSR 的服务器 IP 添加到代理 排除列表中，十分麻烦。 如果你是在路由器里挂的仅 ss-local 那么就当然可以这样做。

- SS/SSR

  手动输入你的 SS/SSR 服务器的参数。 SSR 支持目前新的chain_a和chain_b协议。

- 通过 SS/SSR 链接批量添加（推荐） 十分懒人，复制链接进去一键添加。

#### 通过订阅链接添加（强烈推荐）：

N3RO/卡车极速用户请在官网用户中心快速导入区域复制 SSR 订阅链接。

点击右下角的小齿轮按钮，这个按钮是设置按钮。

![SSTAP小齿轮.jpg](https://i.loli.net/2019/11/19/FB2HDIeMpPyTN3x.jpg)

SSTAP小齿轮.jpg

在弹出的菜单中选择 **“SSR 订阅”** – **“SSR 订阅管理”**

在新的窗口中，将提前复制好的订阅链接粘贴到 **“URL”** 中，然后点击 **“添加”**。

![SSTap添加订阅.jpg](https://i.loli.net/2019/11/19/kR9N6y7tfa8xWFJ.jpg)

SSTap添加订阅.jpg

添加成功后如图所示：

![SSTap添加订阅2.jpg](https://i.loli.net/2019/11/19/ZBO65lW9Vxhj3Jt.jpg)

SSTap添加订阅2.jpg

“频率”是指节点订阅链接自动更新的频率。视个人喜好设定。

关闭订阅管理窗口。稍等若干秒，等待同步节点信息。

订阅成功后如图所示：

![SSTap订阅成功.jpg](https://i.loli.net/2019/11/19/KgpZHP4C59AzRJx.jpg)

SSTap订阅成功.jpg

### 选择代理模式

节点添加完毕后，在 **“代理”** 中选择所需的接入点，然后在 **“模式”** 中选择所需的模式，非游戏用户的话，一般我们选择 **“不代理中国 IP”**，此模式会自动分流（指国内服务不会被代理）。 游戏用户请自行选择要加速的游戏。

![SSTap选择模式.jpg](https://i.loli.net/2019/11/19/4kFhRcdEwgpuX91.jpg)

SSTap选择模式.jpg

### 启动 SSTap

选择代理模式之后，点击 **“连接”** 即可通过 SSTap 连接到代理服务器，助力电脑出国留学。连接成功后 SSTap 会自动最小化。

在连接之前可以先点击 **“代理”** 这一栏最右侧的闪电标志来进行延迟测试，以检测节点是否可用。

![SSTap测试延迟.jpg](https://i.loli.net/2019/11/19/ZRo8MvUI5KtpxS9.jpg)

SSTap测试延迟.jpg

## 更多

### 怎样确认自己是否连接成功？怎样判断是否分流成功？

可以访问此网站： https://ip.skk.moe/

得到如图所示的结果：

![检查IP.jpg](https://i.loli.net/2019/11/19/LUeyRSZngOT9adx.jpg)

检查IP.jpg

正常情况下，从国内查IP应显示你当前的IP地址。从国外查询应当显示你所连接的节点的出口IP地址。

千万不要再用百度查询IP了，原因就不展开了。

### 代理生效了，但就是进不去游戏？

可能性大概有三种：

- 节点IP不符合游戏的要求：此时更换节点尝试即可。
- 未开启 UDP 转发：请点击 **“设置”** ，将 **“不转发UDP”** 取消勾选。并取消勾选 **“代理DNS服务器”**。然后手动选择一个国内的 **“预选DNS”**。
- 软件 BUG ：如果是这种情况，建议直接更换客户端，尝试使用 **Netch** ： https://merlinblog.xyz/wiki/netch.html

### 代理模式种没有我想玩的游戏？

请参考 Github 项目： https://github.com/FQrabbit/SSTap-Rule

### Win10 开启代理后 CPU 占用很高

这是由 Windows 10 的一个网络检测服务所致，SSTap 虚拟网卡创建的连接被误认为是受限网络，从而触发了检测。无需理会，数分钟以后会恢复正常。