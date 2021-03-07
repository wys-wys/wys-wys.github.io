# Aircrack-ng 1.6版本 Centos7和mac安装

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[wank1259162](https://blog.csdn.net/wank1259162) 2020-03-15 12:17:07 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1127 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [Aircrack-ng ](https://blog.csdn.net/wank1259162/category_9806553.html)

版权

Aircrack- NG是一个完整的工具套件，以评估无线网络的安全性。

它着重于WiFi安全的不同领域：

- 监视：数据包捕获并将数据导出到文本文件，以供第三方工具进行进一步处理
- 攻击：通过数据包注入来重放攻击，取消身份验证，伪造的接入点和其他攻击
- 测试：检查WiFi卡和驱动程序功能（捕获和注入）
- 破解：WEP和WPA PSK（WPA 1和2）

所有工具都是命令行，可以进行大量脚本编写。许多GUI都利用了此功能。它主要适用于Linux，但也适用于Windows，OS X，FreeBSD，OpenBSD，NetBSD，以及Solaris等。

# Aircrack- NG的安装

##  1. mac安装方式

### 1.1 macport安装方式

Mac的安装方式比较简单，需要借助macport，macport 是一个工具 管理软件包的一个工具， 我们也可以通过别的方式安装Aircrack-ng。macport的官网地址： https://www.macports.org/install.php

 

1.安装xcode

2.安装Apple's Command Line Developer Tools

```
xcode-select --instal
```

3.需要授权Xcode EULA 

```
xcodebuild -license
```

4.通过macport安装Aircrack-ng，执行

```
sudo port install aircrack-ng
```

### 1.2 brew安装方式

也可以通过brew方式安装，

 

1.查找aircrack-ng

```
brew search aircrack-ng
```

2.查看信息

```
brew info aircrack-ng
```

3.安装

```
brew install aircrack-ng
```

## 2. centos 7 的安装方式

centos 7直接通过增加源来安装，通过官方已经编译好的包，可以很简单的安装官网发行包地址：https://packagecloud.io/aircrack-ng/release；

\1. 添加源

```
curl -s https://packagecloud.io/install/repositories/aircrack-ng/release/script.rpm.sh | sudo bash
```

\2. 安装需要wireless-tools，

 iwconfig命令在默认的base、extras、updates源下不存在，但在epel源下存在，

```
vim /etc/yum.repos.d/CentOS-Base.repo
```

 增加以下内：

```
[epel]



name=epel packages



baseurl=https://dl.fedoraproject.org/pub/epel/7/x86_64/



gpgcheck=0



enable=1
```

 安装wireless-tools

```
yum install wireless-tools 
```

\3. 安装aircrack-ng

```
yum install aircrack-ng
```

4.查看版本

```
# aircrack-ng 



 



Aircrack-ng 1.6  - (C) 2006-2020 Thomas d'Otreppe



  https://www.aircrack-ng.org
```

 