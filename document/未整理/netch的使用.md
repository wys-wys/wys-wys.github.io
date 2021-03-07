# Netch 游戏&网页加速器教程|Windows代理工具

- 博主： [Sabrina](https://merlinblog.xyz/author/1/)
-  

- 发布时间：2019 年 11 月 10 日
-  

- 2569次浏览
-  

- [18 条评论](https://merlinblog.xyz/wiki/netch.html#comments)
-  

- 6131字数
-  

- 分类： [教程·知识共享](https://merlinblog.xyz/category/wiki/)

1. [首页](https://merlinblog.xyz/)
2. 正文 

本文较长，强烈建议使用页面右侧的目录导航栏，提高效率。

## 1. 简单介绍一下 Netch

Netch 是一款运行在 Windows 系统上的开源游戏加速工具，简单易上手。也可以用于日常的网页浏览等。
Github 项目地址：https://github.com/NetchX/Netch

- 不同于SSTap那样需要通过添加规则来实现黑名单代理，Netch原理更类似[Sockscap64](https://www.sockscap64.com/homepage/)，通过扫描游戏目录获得需要代理的进程名进行代理。 也可以实现 [SSTap](https://github.com/mayunbaba2/SSTap-beta-setup) 那样的全局 TUN/TAP 代理，和 [shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows) 那样的本地 Socks5，HTTP 和系统代理。
- 在日常网页浏览方面，可以进行分流设置
- 支持的代理协议：Socks5 / Shadowsocks / ShadowsocksR / Vmess
- UDP NAT FullCone
- 指定进程加速

注： 对于 `V2Ray VMess` 的支持有一些玄学问题，欢迎到 [Github](https://github.com/NetchX/Netch) 提 Pull Request 。

## 2. 整理教程时的系统环境

Windows 10 1903
Netch 1.3.4

文档中的某些内容可能随时间变化而失效。



## 3. 下载和安装 Netch

点击下方标签以下载最新版 Netch 软件
Netch-1.6.6-64位版本
Netch-1.4.3-64位-简化版本
Netch-1.4.3-64位版本
Netch-1.4.3-32位版本
Netch-1.4.2-64位版本
Netch-1.4.2-32位版本





- 此软件为免安装版本，解压后即可运行
- Windows 64 位系统使用 x64 版本
- Windows 32 位系统使用 x86 版本
- 否则你会遇到驱动问题



此软件运行需要 **.NET Framework 4.8** 支持，
非 Windows 10 系统可能需要[点此进行安装](https://dotnet.microsoft.com/download/dotnet-framework/net48)
仍在使用 Windows 7 的用户需要安装 KB4503292 这个补丁才可以使用 Netch





如无必要，请勿选择TUN/TAP模式。否则运行时会提示没有 TAP 适配器或无法运行。
如果有需求，可以直接安装 [Tap-Windows](https://build.openvpn.net/downloads/releases/latest/tap-windows-latest-stable.exe) 适配器。
或者通过安装 [OpenVPN](https://openvpn.net/community-downloads/) 的方式获得该适配器。
或通过安装SSTap来获取。



## 4. 快速配置 Netch

下载压缩包后进行完整解压，并双击运行主程序 Netch.exe 。

[![Netch-1.png](https://merlinblog.xyz/usr/uploads/2020/09/4167606216.png)](https://merlinblog.xyz/usr/uploads/2020/09/4167606216.png)

[Netch-1.png](https://merlinblog.xyz/usr/uploads/2020/09/4167606216.png)



添加服务器的方式主要有三种：

1. 复制节点链接后从剪贴板导入。
2. 手动填写服务器配置。
3. 从**订阅链接**导入。

这里仅对订阅做出说明。**请先复制好自己的订阅链接再阅读接下来的步骤**。

[![Netch-2.png](https://merlinblog.xyz/usr/uploads/2020/09/3247312193.png)](https://merlinblog.xyz/usr/uploads/2020/09/3247312193.png)

[Netch-2.png](https://merlinblog.xyz/usr/uploads/2020/09/3247312193.png)



点击**订阅**，选择**管理订阅连接**。

[![Netch-3.png](https://merlinblog.xyz/usr/uploads/2020/09/1499190690.png)](https://merlinblog.xyz/usr/uploads/2020/09/1499190690.png)

[Netch-3.png](https://merlinblog.xyz/usr/uploads/2020/09/1499190690.png)



在对应的地方粘贴自己的订阅链接，备注可以自行填写。点击**添加**后再点击**保存**。初次配置时不建议勾选左下角的选项。

[![Netch-4.jpg](https://merlinblog.xyz/usr/uploads/2020/09/3704554944.jpg)](https://merlinblog.xyz/usr/uploads/2020/09/3704554944.jpg)

[Netch-4.jpg](https://merlinblog.xyz/usr/uploads/2020/09/3704554944.jpg)





添加订阅后，需要回到主界面选择更新订阅，将服务器信息同步到本地。



[![Netch-5.png](https://merlinblog.xyz/usr/uploads/2020/09/679900875.png)](https://merlinblog.xyz/usr/uploads/2020/09/679900875.png)

[Netch-5.png](https://merlinblog.xyz/usr/uploads/2020/09/679900875.png)



在节点列表选择一个节点。节点后方的数字为延迟。

[![Netch-6.png](https://merlinblog.xyz/usr/uploads/2020/09/3882384657.png)](https://merlinblog.xyz/usr/uploads/2020/09/3882384657.png)

[Netch-6.png](https://merlinblog.xyz/usr/uploads/2020/09/3882384657.png)



选择自己需要的代理模式。这里推荐 `Bypass LAN and China` ，此模式下可以进行自动分流，不影响国内服务速度。

[![Netch-7.png](https://merlinblog.xyz/usr/uploads/2020/09/44266604.png)](https://merlinblog.xyz/usr/uploads/2020/09/44266604.png)

[Netch-7.png](https://merlinblog.xyz/usr/uploads/2020/09/44266604.png)



点击**启动**。



此时你的电脑已经可以进行出国留学活动。



[![Netch-8.png](https://merlinblog.xyz/usr/uploads/2020/09/2400007540.png)](https://merlinblog.xyz/usr/uploads/2020/09/2400007540.png)

[Netch-8.png](https://merlinblog.xyz/usr/uploads/2020/09/2400007540.png)



[![Netch-9.png](https://merlinblog.xyz/usr/uploads/2020/09/1080294565.png)](https://merlinblog.xyz/usr/uploads/2020/09/1080294565.png)

[Netch-9.png](https://merlinblog.xyz/usr/uploads/2020/09/1080294565.png)



------

## 5. 可能遇到的问题

### 5.1 为自己的游戏添加进程代理

如果你的游戏的模式已经被收录，也可以考虑在模式菜单中，选择使用已收录的模式。所有模式的文件，都在 ./mode/ 文件夹下，如果你需要多个模式的合并文件，可以使用记事本将其打开，将多个文件合并。

ping 值未必准确，因为这只是你本地到代理服务器而非游戏服务器的延迟。

如果你的游戏的模式没被收录，可以看接下来的扫描步骤来手动创建模式。

请点击菜单栏上的 **模式** ，然后点击 **创建进程模式**。

[![Netch-10.png](https://merlinblog.xyz/usr/uploads/2020/09/1332375388.png)](https://merlinblog.xyz/usr/uploads/2020/09/1332375388.png)

[Netch-10.png](https://merlinblog.xyz/usr/uploads/2020/09/1332375388.png)



在弹出的窗口中点击扫描

[![Netch-11.png](https://merlinblog.xyz/usr/uploads/2020/09/3819703143.png)](https://merlinblog.xyz/usr/uploads/2020/09/3819703143.png)

[Netch-11.png](https://merlinblog.xyz/usr/uploads/2020/09/3819703143.png)



选择你要加速的游戏的安装路径，根据游戏不同，可能需要选择多个不同的目录进行扫描。
由于博主不打游戏，所以此处用 Chome 浏览器来演示，原理是相同的。

[![Netch-12.png](https://merlinblog.xyz/usr/uploads/2020/09/481776576.png)](https://merlinblog.xyz/usr/uploads/2020/09/481776576.png)

[Netch-12.png](https://merlinblog.xyz/usr/uploads/2020/09/481776576.png)



比如 Chrome 的安装根目录为 C:Program Files (x86)GoogleChrome ，点击扫描可得

[![Netch-13.png](https://merlinblog.xyz/usr/uploads/2020/09/3021641618.png)](https://merlinblog.xyz/usr/uploads/2020/09/3021641618.png)

[Netch-13.png](https://merlinblog.xyz/usr/uploads/2020/09/3021641618.png)



输入备注名后点击保存。

[![Netch-14.png](https://merlinblog.xyz/usr/uploads/2020/09/2280926864.png)](https://merlinblog.xyz/usr/uploads/2020/09/2280926864.png)

[Netch-14.png](https://merlinblog.xyz/usr/uploads/2020/09/2280926864.png)



此时已经可以在代理模式窗口看到刚添加的进程模式了。

[![Netch-15.png](https://merlinblog.xyz/usr/uploads/2020/09/3646698982.png)](https://merlinblog.xyz/usr/uploads/2020/09/3646698982.png)

[Netch-15.png](https://merlinblog.xyz/usr/uploads/2020/09/3646698982.png)



- 启动 Netch 后，再去游戏根目录或者别的启动器如 Steam，Uplay 启动游戏即可。此时游戏就已经被代理了
- 如果在 Netch 启动前就启动了游戏，建议重启游戏。
- 如果需要 Steam，Uplay 等启动器也被代理，参照前面的方式对 Steam，Uplay 根目录也进行扫描即可
- 如果出现了启动失败，或者无法代理成功的情况，请先尝试 **选项** - **重启服务或选项** - **卸载服务**，或者在退出 Netch 以后，点击运行在 Netch 根目录下的 **DriverUpdater.exe** 程序进行驱动更新。

### 5.2 部分网页视频无法正常加载/加载慢

建议尝试开启 Netch 的 TUN/TAP 模式

### 5.3 TUN/TAP启动失败

仅用于解决`tun2socks`日志中有 `CryptAcquireContext failed with error -2146893809` 错误的问题

如何解决：同时按下`Win`键和`R`键，然后输入 `%appdata%\Microsoft\Crypto` 运行。打开后移动RSA文件夹至C盘根目录备份以防万一，然后再重启Netch，RSA文件夹在启动成功后会自动重新创建。

### 5.4 NAT 类型限制

> - Q： xxx 游戏对 NAT 类型有要求，你们这个加速器代理后 NAT 类型还是严格 xxx ，我甚至用 NATTypeTester 测过了，还是不行 xxx
> - A：经过测试这款软件是可以做到 Full Cone 的 NATType 。如果你自己测试不行，需要考虑三个方面的问题
>   - 第一个是你的服务器是否支持 Full Cone 的 NATType ，这可以通过其他软件的测试来佐证，譬如使用 Sockscap64 之类
>   - 第二个是你本地的网络环境问题，首先，**关闭 windows 防火墙**，经测试 windows 防火墙会将 Full Cone 限制到 Port Restricted Cone，无论你是使用 TUN/TAP 模式，还是进程模式，除非你的游戏对 NAT 不敏感，否则请务必先把 windows 防火墙关闭。其次，某些杀软的防火墙可能也会影响到 NAT
>
> 类型，根据情况你可以关闭杀软的防火墙，或者卸载杀软来避免问题发生
>
> - 第三个是运营商的网络问题，经测试联通数据和长宽等网络，即使在代理后也无法做到 Full cone ，就算服务器是支持 Full cone 的。这种情况下你可能需要切换全局的 VPN 代理工具（WireGuard ， Badvpn ， Openvpn ，
>
> tinyfecVPN 等），也可以尝试 Netch 的 TUN/TAP 模式，或者更换本地网络环境
>
> - 第四个是某些游戏的代理模式有问题，可能遇到各种玄学问题。

### 5.5 Steam / 浏览器无法正常打开页面

> - Q：用来加速 Steam / 浏览器，结果无法正常打开页面
> - A：有人测试可行有人测试不可行。首先声明一下，本软件的功能主要不是用来代理 Steam / 浏览器打开页面的，建议使用专门的工具，如 [SteamCommunity 302](https://www.dogfight360.com/blog/686/)，浏览器则建议用
>
> shadowsocks-windows， Clash for Windows 等等

### 5.6 UWP 应用无法代理

> - Q：UWP 应用 xxx 无法代理
> - A：请按照[此方法](https://nekosc.com/technology/uwp_fiddler.html)设置即可

### 5.7 V2Ray使用TUN/TAP模式DNS查询慢

[![v2rayDNS查询慢.png](https://merlinblog.xyz/usr/uploads/2020/09/881869528.png)](https://merlinblog.xyz/usr/uploads/2020/09/881869528.png)

[v2rayDNS查询慢.png](https://merlinblog.xyz/usr/uploads/2020/09/881869528.png)


解决方案：在设置中使用自定义 DNS 默认1.1.1.1