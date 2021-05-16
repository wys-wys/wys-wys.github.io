# 怎么给CentOS Linux 8更换国内源（阿里源）

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[9Tristone](https://blog.csdn.net/dengshulei) 2019-12-25 23:43:38 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 13879 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 34

分类专栏： [CentOS](https://blog.csdn.net/dengshulei/category_9619565.html) 文章标签： [centos](https://www.csdn.net/tags/MtTaEg0sMzk5NjctYmxvZwO0O0OO0O0O.html) [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [yum](https://www.csdn.net/tags/MtTaEg0sNDk5NzYtYmxvZwO0O0OO0O0O.html) [dnf](https://www.csdn.net/tags/MtzaMg0sOTgwNjYtYmxvZwO0O0OO0O0O.html) [服务器](https://www.csdn.net/tags/MtTaEg0sNDcxOTgtYmxvZwO0O0OO0O0O.html)

版权

# 概述

CentOS Linux长期以来一直存在一个不和谐的问题：Python2和Python3如何共存。在CentOS Linux 8以前，系统默认的Python版本是2.x，装上个3.x还跟后娘养的一样没有什么地位，稍有不慎不是这里不好用就是那里不好用。最夸张的是手动将Python2.6升级到2.7，YUM直接挂了。如果想配置成运行命令“python ”直接执行的是3.x版本，有一堆的文件需要跟着更改。一个不幸的消息是YUM是用Python2.x写成的，而DNF是用Python3.x写成的。这样的话CentOS Linux 8把默认的Python版本改成了3.x，对应的软件包管理器也就顺理成章的从YUM改成了DNF。所以CentOS Linux 8的默认RPM软件包管理器从YUM变成了DNF。好在所有的安装包配置文件都没有变更，都跟当时YUM时代没有什么太大区别，这样去切换到DNF不会有太大的不适应。
为什么要说这些，因为安装软件的时候会用到DNF（YUM命令也存在，但只是一个指向DNF的链接，9Tristone注）。下面的更改内容可以理解为将DNF的配置文件进行更改，从默认下载国外的内容改为了默认下载国内服务器（阿里的服务器）上的内容。

# 什么是DNF？为什么替换YUM？

DNF是Linux上的下一代包管理工具，它替换的对象是YUM。DNF使用SUSE创建和维护的libsolv进行依赖解析，而使用公共API来解决依赖关系的YUM相对更难维护。YUM的代码有56K行但没有相关文档，而DNF的代码行数仅有29K行而且有API文档，所以很容易构建新的特性。虽然DNF的代码量少，但是DNF支持更多的扩展，而YUM只支持Python扩展。
总的来说DNF由Python3写成，降低了内存占用，提高了运行速度，加强了依赖分析能力，提高了用户的体验。所以代替YUM是一个必然的结果。

# DNF/YUM源配置文件替换为阿里家的

由于系统安装的包管理配置文件链接的国外的服务器，导致我们安装软件、升级内核和升级软件的时候会从国外的服务器下载相关文件。由于众所周知的原因，国外服务器的网速真的不敢恭维，所以我们要把他们替换为国内的服务器，这样安装和升级软件的速度就会提高，降低维护人员在等待上所花费的时间。
因为阿里源文件里面已经包含了AppStream、Base、centosplus、Extras和PowerTools的相关内容，所以需要把这些文件改名为bak，不让系统执行。

```bash
cd /etc/yum.repos.d/
mv /etc/yum.repos.d/CentOS-AppStream.repo /etc/yum.repos.d/CentOS-AppStream.repo.bak
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
mv /etc/yum.repos.d/CentOS-centosplus.repo /etc/yum.repos.d/CentOS-centosplus.repo.bak
mv /etc/yum.repos.d/CentOS-Extras.repo /etc/yum.repos.d/CentOS-Extras.repo.bak
mv /etc/yum.repos.d/CentOS-PowerTools.repo /etc/yum.repos.d/CentOS-PowerTools.repo.bak
123456
```

做完以上修改以后，就可以下载新的阿里源文件了，因为默认没有装wget，我们可以用curl来执行以下命令：

```bash
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
1
```

如果有wget也可以执行以下命令

```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
1
```

如果没有安装wget，运行这个命令会提示“bash: wget: 未找到命令”，那就用curl的那个命令来执行好了。或者你也可以先安装wget，很简单，只需要下面一个命令即可（前提是在将上面的文件改为“.bak”之前，如果已经改了，先改回去再执行下述命令）

```bash
yum -y install wget
1
```

查看一下是否安装完成，执行命令

```bash
ls -l /etc/yum.repos.d/
1
```

将会看到如下内容

```bash
-rw-r--r--. 1 root root  731 8月  14 14:42 CentOS-AppStream.repo.bak
-rw-r--r--. 1 root root 2595 12月 25 19:44 CentOS-Base.repo
-rw-r--r--. 1 root root  712 8月  14 14:42 CentOS-Base.repo.bak
-rw-r--r--. 1 root root  798 8月  14 14:42 CentOS-centosplus.repo.bak
-rw-r--r--. 1 root root 1320 8月  14 14:42 CentOS-CR.repo
-rw-r--r--. 1 root root  668 8月  14 14:42 CentOS-Debuginfo.repo
-rw-r--r--. 1 root root  756 8月  14 14:42 CentOS-Extras.repo.bak
-rw-r--r--. 1 root root  338 8月  14 14:42 CentOS-fasttrack.repo
-rw-r--r--. 1 root root  928 8月  14 14:42 CentOS-Media.repo
-rw-r--r--. 1 root root  736 8月  14 14:42 CentOS-PowerTools.repo.bak
-rw-r--r--. 1 root root 1382 8月  14 14:42 CentOS-Sources.repo
-rw-r--r--. 1 root root   74 8月  14 14:42 CentOS-Vault.repo
123456789101112
```

再执行以下命令查看一下内容，确认是否更改成功

```bash
cat /etc/yum.repos.d/CentOS-Base.repo
1
```

如果看到如下内容，则代表升级成功了。

```bash
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#
#
 
[base]
name=CentOS-$releasever - Base - mirrors.aliyun.com
failovermethod=priority
baseurl=https://mirrors.aliyun.com/centos/$releasever/BaseOS/$basearch/os/
        http://mirrors.aliyuncs.com/centos/$releasever/BaseOS/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/centos/$releasever/BaseOS/$basearch/os/
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-Official
 
#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras - mirrors.aliyun.com
failovermethod=priority
baseurl=https://mirrors.aliyun.com/centos/$releasever/extras/$basearch/os/
        http://mirrors.aliyuncs.com/centos/$releasever/extras/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/centos/$releasever/extras/$basearch/os/
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-Official
 
#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus - mirrors.aliyun.com
failovermethod=priority
baseurl=https://mirrors.aliyun.com/centos/$releasever/centosplus/$basearch/os/
        http://mirrors.aliyuncs.com/centos/$releasever/centosplus/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/centos/$releasever/centosplus/$basearch/os/
gpgcheck=1
enabled=0
gpgkey=https://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-Official
 
[PowerTools]
name=CentOS-$releasever - PowerTools - mirrors.aliyun.com
failovermethod=priority
baseurl=https://mirrors.aliyun.com/centos/$releasever/PowerTools/$basearch/os/
        http://mirrors.aliyuncs.com/centos/$releasever/PowerTools/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/centos/$releasever/PowerTools/$basearch/os/
gpgcheck=1
enabled=0
gpgkey=https://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-Official


[AppStream]
name=CentOS-$releasever - AppStream - mirrors.aliyun.com
failovermethod=priority
baseurl=https://mirrors.aliyun.com/centos/$releasever/AppStream/$basearch/os/
        http://mirrors.aliyuncs.com/centos/$releasever/AppStream/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/centos/$releasever/AppStream/$basearch/os/
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-Official
12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152535455565758596061
```

这样就完成了将本地CentOS Linux 8的yum安装源更换为国内源（阿里源）。
运行以下命令生成以下缓存

```bash
yum makecache
1
```

执行以下命令升级所有的软件包试试看速度如何：

```bash
yum -y update
1
```

主要是习惯了YUM，你也可以用这个命令“dnf -y update”。如果你是网络安装的CentOS Linux 8，系统应该不会有什么软件包需要升级，提示内容如下：

```bash
上次元数据过期检查：0:06:18 前，执行于 2019年12月25日 星期三 23时34分12秒。
依赖关系解决。
无需任何处理。
完毕！
```