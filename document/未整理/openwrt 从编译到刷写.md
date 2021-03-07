#   从零开始学习OpenWrt完美教程



![OpenWRT](http://zhidx.com/wp-content/uploads/2014/01/9427541855_103a0dfdaa.jpg)

Cisco/Linksys在2003年发布了WRT54G这款无线路由器，同年有人发现它的IOS是基于Linux的，然而Linux是基于GPL许可证发布的，按照该许可证Cisco应该把WRT54G 的IOS的源代码公开。2003年3月， Cisco迫于公众压力公开了WRT54G的源代码。此后就有了一些基于Cisco源码的第三方路由器固件，OpenWrt就是其中的一个。

OpenWrt的特点：

- 可扩展性好，可以在线安装您所需要的功能，目前有1000多个功能包可选；
- 是一台完整的Linux工作站，文件系统可读可写，便于开发者学习和实践；

现在有越来越多的Maker开始折腾OpenWrt，但作为一个Maker新手来讲，在网上还是很难找到一份系统的入门级资料。查找资料很辛苦，而且OpenWrt的门槛相对较高，希望这篇文章所提供的从零开始学OpenWrt编译 + 刷机 + 使用教程能降低新手们的入门难度，当然，编译过程非必须，一般的路由都可找到可用的稳定固件直接刷机。

第一部分：搭建编译环境

1、安装Ubuntu（编译需要Linux环境），到其[官网](http://www.ubuntu.org.cn/desktop/get-ubuntu/download/)下载，版本根据自己所需选择即可。可以选择安装到虚拟机或者物理机，图形化安装而且是中文版，连安装都搞不定的，可以关闭本页面了；

2、切记不要改动软件源，同时按住Ctrl + Alt + T，调出终端；

3、逐条输入下列命令（及时验证是否安装成功）：

```php
sudo apt-get install g++
sudo apt-get install libncurses5-dev
sudo apt-get install zlib1g-dev
sudo apt-get install bison
sudo apt-get install flex
sudo apt-get install unzip
sudo apt-get install autoconf
sudo apt-get install gawk
sudo apt-get install make
sudo apt-get install gettext
sudo apt-get install gcc
sudo apt-get install binutils
sudo apt-get install patch
sudo apt-get install bzip2
sudo apt-get install libz-dev
sudo apt-get install asciidoc
sudo apt-get install subversion
sudo apt-get install sphinxsearch
sudo apt-get install libtool
sudo apt-get install sphinx-common
sudo apt-get install libssl-dev
sudo apt-get install libssl0.9.8
```

至此编译环境搭建完成。

第二部分：下载OpenWrt源码并编译

OpenWrt源码分两种，一种是最新但不是最稳定的Trunk开发版，一种是最稳定的Backfire版，建议下载官方源码。下载前先在本地创建文件夹：

```php
mkdir openwrt
sudo chmod 777 openwrt
cd openwrt
```

选择你想要的版本然后执行下载命令，下载结束会显示版本号：

Trunk版下载命令：

```php
svn co svn://svn.openwrt.org/openwrt/trunk/
```

Backfire版下载命令：

```php
svn co svn://svn.openwrt.org/openwrt/branches/backfire/
```

添加软件扩展包，将feeds.conf.default修改为feeds.conf：

```php
cp feeds.conf.default feeds.conf
```

更新扩展，安装扩展：

```php
./scripts/feeds update -a
./scripts/feeds install -a
```

注：如果不是刚下载的源码，为保持代码为最新状态，应定期运行svn update命令更新源码。



测试编译环境：



```php
make defconfig
```

到这里就可以开始编译自己的固件了。进入定制界面：

```php
make menuconfig
```

如果一切正常，会出现一个配置菜单，可以选择要编译的固件平台（芯片类型）、型号，还能选择固件中要添加的功能和组件，配置好后保存并退出菜单即可。

![openwrt-make](http://zhidx.com/wp-content/uploads/2014/01/openwrt-make.jpg)

如果你想修改源码，应该在此步进行，如支持大容量Flash之类的修改，自己上网查到修改什么文件什么地方后，就在ubuntu图形界面上进去找到文件，双击打开文本编辑器修改保存。

开始编译：

```php
make
```

或者

```php
make  V=99
```

或者

```php
make -j V=99
```

> make是编译命令，V=99表示输出debug信息，V一定要大写，如果要让CPU全速编译，就加上 -j 参数，第一次编译最好不带-j参数。

编译过程保持联网（会从网上下载一些源码包），所以断网可能造成编译中断，编译所需时间与电脑CPU及网络环境有很大关系，第一次编译时间较久，快则半小时长则2、3个小时，之后的编译所需时间较短。编译完成后会在源码文件目录出现bin文件夹（如trunk/bin/XXXX），如果你手里的路由是原版固件需要刷OpenWrt需要选用XXX-factory.bin固件，如果路由已经刷了OpenWrt，选用升级固件XXXX-sysupgrade.bin升级用的，在升级界面升级即可。进到文件夹找到你需要的固件传出（通过邮箱、网盘、U盘等），开始刷机吧。

第三部分：将OpenWrt刷入路由器

要在路由器上使用OpenWrt，首先要将路由器固件刷新为OpenWrt，即相当于OpenWrt 系统的安装，不同型号的路由器的安装方法可能也会不一样，但一般常用的有三种方法：

- Web上传固件更新
- PFTP上传固件更新
- 编程器写入固件

具体型号的路由器适用于哪种或哪几种方法，需自行尝试。

第四部分：开始使用OpenWrt

要对OpenWrt进行配置，一般有两条途径：

- SSH登录通过命令行控制
- Web登录通过Web界面设置

首次安装OpenWrt后，需要设置密码才可以使用SSH登录，方法是使用telnet登录或者Web登录设置密码。在Windows下面telnet和SSH登录可以使用Putty，在Linux或Mac下可分别使用如下命令：

```php
ssh –l root 192.168.1.1 //Linux
ssh root@192.168.1.1 //Mac
```

![openwrt-ssh](http://zhidx.com/wp-content/uploads/2014/01/openwrt-ssh.jpg)

一般指令与常见Linux发行版相同，但是OpenWrt使用自己的包管理器：opkg，使用“opkg –help”查看帮助信息。以下是一些常用操作命令：

```php
opkg update //更新软件包列表
opkg install  //在线安装软件包
opkg remove  //移除软件包
```

登录Web管理界面，前提是该OpenWrt系统中要安装了Web界面，一般是Luci，登录方式与普通路由器无异，打开浏览器，输入路由器IP即可进入登录界面，OpenWrt的默认IP是192.168.1.1。

![openwrt-web](http://zhidx.com/wp-content/uploads/2014/01/openwrt-web.jpg)

到此，OpenWrt的大门已为你敞开。接下来，开始尝试利用OpenWrt实现更多智能应用吧，比如单号多拨榨取运营商带宽、绑定域名远程控制、挂载大容量硬盘、搭建BT下载机、搭建网络摄像头、Samba/DLNA家庭NAS共享、私有云同步、FTP、个人网站/服务器…



make作为trunk版本的编译命令，只能在trunk目录执行，进入配置菜单界面，键盘上下是移动光标，左右是选择底部按键，回车是确认，空格是设置选择模式，选项最前面的选择模式有[*]表示编译进固件，[M]表示编译成安装包，[ ]表示不选择，esc是返回上级菜单，按?是帮助，按/是搜索。

自己看openwrt的源码获取方法
https://dev.openwrt.org/wiki/GetSource

还有就是正式版也会升级的，具体请看
https://dev.openwrt.org/browser/branches





搜索结果说明：


Symbol: PACKAGE_l7-protocols [=Y]——包的名字，以及有被选中
 Dedfined at tmp/.config-package.in:14725——表示这个包概况
 Depeds on: \——这个包依赖哪个包
PACKAGE_iptables-mod-filter [=Y]——被依赖的这个包有选中
 Location:——指明l7-protocols这包在menuconfig的界面的哪层菜单中，方便查找
   -> Network
    -> Firewall
 Selects: \——可以附带选择哪几个包
 Selected by: \——同时选择以下几个包，那l7-protocols会被自动一起选中


2.12.重置配置


选择配置菜单界面底部的重置菜单项“Reset to Defaults”，恢复默认所有选择模式；


2.13.选择组件


这里仅增加支持IPv6的组件和Web管理界面LuCI，选择项目如下：


Target System (Atheros AR7xxx/AR9xxx) ————主控芯片


Target Profile (Buffalo WHR-G301N) ————路由器型号


LuCI——Web管理界面LuCI
 Collections
  luci-ssl        ——安全链接
 Applications
  luci-app-ddns      ——动态域名
  luci-app-multiwan    ——多拨
  luci-app-radvd     ——IPv6广播
  luci-app-upnp      ——upnp端口映射
  luci-app-wol      ——在线唤醒
 Translations
  luci-i18n-chinese    ——中文语言支持
 Protocols
  luci-proto-ipv6     ——增加IPv6支持
 Server Interfaces
  luci-sgi-uhttpd     ——自动运行LuCI的服务
 Kernel Modules
  Network Devices
   kmod-macvlan     ——为mac虚拟局域网增加内核支持
  Network Support
   kmod-sched      ——为TC命令增加内核支持
 Network
  tc           ——增加TC功能
 
其它可选择功能


LuCI
 Applications
  luci-app-p2pblock    ——可增加Layer 7、ipp2p支持
 Themes
  luci-theme-bootstrap  ——可增加主题


 其它选项一般保持默认就可以。



2.14.选择主菜单最底部“Save Configuration to an Alternate File”命令保存设置一下你的设置，可以自定义文件名，以方便以后调用。


2.15.按两次“esc”键退出配置菜单界面，提示是否保存，按Yes表示把当前编译设置保存下来。


2.16.自定义路由器的默认设置，可进入编译目录/trunk/package/base-file/files/etc/config，修改里面的配置文件，一般可以不用定义。


3.进行编译


3.1.输入以下命令开始编译


make V=99


V=99参数表示输出详细的debug信息；编译时得保持联网在线，因为会下载很多数据包（放在./dl目录下），而且容量不小，整个过程耗时比较久，一般第一次编译耗时要一个半钟到两个钟，以后编译耗时约三十分钟。


注：如只想清除/编译某个模块，您可以做如下类似操作make package/qos/clean, make package/qos/compile, make package/qos/install。


3.2.编译成功后，用于刷机的固件会保存在/home/openwrt/trunk/bin/主控芯片系列/目录下，有3个对应不同刷机模式的bin文件：


*factory.bin


*tftp.bin


*sysupgrade.bin


建议马上备份这三个文件到别的地方，以便用于刷机。


4.编译后继工作


4.1.清除当前编译作业


make clean


特别注意，这会删除上面编译的成果——bin文件，请作好备份。


4.2.恢复默认编译环境


make defconfig







================================

添加wifidog：



在项目下终端：vim feeds.conf.default    增加这一行：src-git wifidog https://github.com/wifidog/wifidog-gateway.git  然后重新：./scripts/feeds update -a            ./scripts/feeds install -a  终端执行 make menuconfig   在Network/captive portals/下选择wifidog 就有选择 WiFiDog 这一项了。