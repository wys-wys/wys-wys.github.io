

不需要cf加速

##  一键安装脚本

系统要求及脚本介绍
1、系统支持centos7+/debian9+/ubuntu16+

2、域名需要解析到VPS并生效。

3、脚本自动续签https证书

4、自动配置伪装网站，位于/usr/share/nginx/html/目录下，可自行替换其中内容

5、请不要在任何生产环境使用一键脚本，此条适用于本站所有脚本，专门用来科学上网的VPS可以随意使用。

6、trojan不能用CDN，不要开启CDN

7、如果你在用谷歌云、阿里云等产品的时候，需要在控制台开放80、443端口。

BBR一键安装代码：
wget –no-check-certificate https://raw.githubusercontent.com/cx9208/Linux-NetSpeed/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh

若报错运行以下代码，不报错跳过：

cetnos系统
yum -y install wget
rm -f /var/run/yum.pid

ubuntu系统

apt install wget

------

./tcp.sh

一、使用一键脚本安装
复制以下命令在VPS中执行，选择安装trojan，然后输入解析到VPS的域名并回车（不要带http://，只输入域名，例如atrandys.com或者xxx.atrandys.com），开始安装，然后等待安装完成即可。

注意：如果提示SELinux状态问题，请按要求输入Y重启VPS，然后再执行本脚本，否则可能https证书申请出错

curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh

二、下载Windows客户端
安装完成后，会展示一条下载地址，复制地址，并下载下来即可。

如果你真的忘记下载了，那么进入/usr/share/nginx/html/目录下，找到一个乱码文件夹，进入会看到客户端文件，使用sftp下载下来即可。

三、搭配浏览器插件使用
解压缩下载的trojan-cli.zip的压缩包，进入文件夹，双击start.bat，开启Trojan服务，Trojan会监听本地1080端口。然后下载SwitchyOmega

下载插件：SwitchyOmega

规则1：https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
规则2：https://raw.githubusercontent.com/atrandys/proV/master/fgfwlist.txt

电脑上其他软件如何使用Trojan
1、如果软件支持配置socks5，直接指向127.0.0.1：1080即可。

2、如果软件不支持配置socks5，可选择sstap/sockscap64/supercap等软件，曲线实现代理。

常见问题总结
1、Trojan客户端打开无法运行，提示缺少找不到vcruntime140.dll或找不到msvcp140.dll。

原因缺少运行库，下载链接中的两个软件，一个是32位一个是64位，请全部安装即可：
https://www.microsoft.com/en-us/download/details.aspx?id=48145

2、如果遇到vcruntime140_1的错误，下载下面的文件放到C:\windows\system32目录下即可

下载140_1.dll：https://github.com/atrandys/trojan/raw/master/vcruntime140_1.dll

3、trojan服务端怎么修改密码

trojan服务端配置文件路径如下，如需修改内容，修改以下文件即可。

/usr/src/trojan/server.conf
修改完成后，重启trojan服务端即可，同时客户端的密码也要同步修改哦。

systemctl restart trojan
4、chrome插件switchyomega无法安装

参考这篇文章，离线安装chrome插件方法：https://www.atrandys.com/2019/2149.html

5、关于申请证书没有成果的处理

可能的原因1：

一些原因导致使用nginx申请证书时出错，要么防火墙端口没开放，要么nginx未正常。建议用最纯净的系统安装。

可能的原因2:

出现这个问题最可能的原因之一是你的同一个域名多次申请证书，导致let’s encrypt官方的限制，同一域名每周最多5次申请。

最简单的Trojan一键脚本，效率高/速度快/延迟低，支持tls1.3，系统支持centos7+/debian9+/ubuntu16+

如果你的同一个域名申请了很多此证书，这个处理方法可能有用：更换二级域名，例如原来使用的域名是www.abc.com或abc.com或xyz.abc.com，那么现在你添加一个二级域名解析例如xxx.abc.com，安装时使用这个域名即可。