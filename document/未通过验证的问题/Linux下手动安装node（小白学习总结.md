# Linux下手动安装node（小白学习总结）

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[晚i风](https://blog.csdn.net/qq_36836332) 2018-08-24 11:32:02 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 653 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

版权

1.官网浏览文档。  https://nodejs.org/en/

2.下载适合的版本。  https://nodejs.org/en/download/

3.通过vsftpd上传到阿里云服务器上

  1）安装vsftpdh 。 (root用户下家目录$ apt-get install vsftpd  修改配置文件/etc/vsftpd.conf的第31行 write_enable=YES最后一行追加allow_writeabler_chroot=YES,第122行的chroot_local_user=YES解开注释保存并退出，修改配置文件需要重启服务器)
  2）或者是在Windows本机上下载安装FTP软件,如filezilla或者xftp连接阿里云服务器，就可以上传或下载文件了。

   选择第一种nodejs - 02.安装Nodejs - 推荐方式 - 手动安装

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[iwanghang](https://iwanghang.blog.csdn.net/) 2019-07-23 15:58:50 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 220 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [Nodejs](https://blog.csdn.net/iwanghang/category_9156377.html)

版权

可以选择版本，可以选择安装模块

 

http://nodejs.cn/download/

 linux下手动安装nodejs

发表于2021 2020-02-24 | 分类于 [DevOps](https://www.dazhuanlan.com/devops/) | 没有评论

![img](https://cdn.shortpixel.ai/client/q_glossy,ret_img/https://www.dazhuanlan.com/webchat.jpg)
[8种机械键盘轴体对比](https://www.zhihu.com/zvideo/1357121327577534464)
[本人程序员，要买一个写代码的键盘，请问红轴和茶轴怎么选？](https://www.zhihu.com/question/417189701/answer/1497132213)

- 步骤：
  - [1、下载node源码](https://www.dazhuanlan.com/2020/02/24/5e532feca1519/#1下载node源码)
  - [2、解压](https://www.dazhuanlan.com/2020/02/24/5e532feca1519/#2解压)
  - [3、移动到指定的目录](https://www.dazhuanlan.com/2020/02/24/5e532feca1519/#3移动到指定的目录)
  - [4、删除原来的链接](https://www.dazhuanlan.com/2020/02/24/5e532feca1519/#4删除原来的链接)
  - [5、安装npm和node命令到系统](https://www.dazhuanlan.com/2020/02/24/5e532feca1519/#5安装npm和node命令到系统)

> 版本：ubuntu server 16.04

> 问题：直接使用apt-get安装后，发现指定的版本是v4.26，版本太低，需要手工下载后安装

### 步骤：

#### 1、下载node源码

```
sudo wget https://npm.taobao.org/mirrors/node/latest-v9.x/node-v9.11.1-linux-x64.tar.xz
```

#### 2、解压

```
tar -xJf node-v9.11.1-linux-x64.tar.xz
```

#### 3、移动到指定的目录

```
sudo mv node-v9.11.1-linux-x64 /opt/
```

#### 4、删除原来的链接

```
cd /usr/bin
sudo rm node
sudo rm npm
```

#### 5、安装npm和node命令到系统

```
sudo ln -s /opt/node-v9.11.1-linux-x64/bin/node /usr/bin/node
sudo ln -s /opt/node-v9.11.1-linux-x64/bin/npm /usr/bin/npm
```

[jquery 01](https://www.dazhuanlan.com/2020/02/24/5e532ff033d1d/)

[[面试题\] 微信的一道前端面试题](https://www.dazhuanlan.com/2020/02/24/5e532fe481d7d/)

10.16.0 Windows macOS 源代码(linux) 下载地址：

https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0-x64.msi

https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0.pkg

https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0.tar.gz

 

1.cd到下载目录

 

2.进行下载 （输入-c 允许断点下载）

wget -c https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0.tar.gz

wget -c https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0-linux-arm64.tar.gz

wget -c https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0-linux-x64.tar.gz

wget -c https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0-linux-x64.tar.xz

wget -c https://nodejs.org/dist/v10.16.0/node-v10.16.0-linux-x64.tar.gz

wget -c https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0.tar.gz

3.解压缩

tar -zvxf [node-v10.16.0.tar.gz](https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0.tar.gz)

tar -zvxf [node-v10.16.0-linux-arm64.tar.gz](https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0-linux-arm64.tar.gz)

tar -zvxf [node-v10.16.0-linux-x64.tar.gz](https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0-linux-x64.tar.gz)

tar -zvxf [node-v10.16.0.tar.gz](https://npm.taobao.org/mirrors/node/v10.16.0/node-v10.16.0.tar.gz)

4.进入解压缩以后的目录 (通过 configure 生成makefile)

cd node-v10.16.0

cd node-v10.16.0-linux-arm64

cd node-v10.16.0-linux-x64

cd node-v10.16.0

5.查看 configure 是否存在

ls configure

\5. 生成makefile(preifx是指定要安装到哪个目录下，一般安装到/usr/local/nodejs)

./configure --prefix=/usr/local/nodejs

6.运行一下生成makefile以后的python脚本

python tools/gyp_node.py --no-parallel -f make-linux

7.生成Makefile（无需关心Makefile里面的内容）

ls Makefile

8.用四个线程去编译

make -j4

9.将编译好的程序，安装（安装到上面5.指定的/usr/local/nodejs里面）

sudo make install

10.也可以把8.9.合并，编译并安装

make -j4 && sudo make install

11.进入安装好的路径

cd /usr/local/nodejs

12.查看一下（应该是有 bin include lib share 文件夹）

ls

13.进入bin

cd bin

14.查看一下（应该是有 node npm npx 文件夹）

ls

15.修改环境变量

vi ~/.bashrc

 

 

pwd

/usr/local/include/node

/usr/local/bin

 

unset GOROOT

export PATH=/usr/local/nodejs/bin:$PATH:/usr/local/bin

export GOPATH=/home/jialian/goWorkspace

 

unset GOROOT

export PATH=/usr/local/nodejs/bin:$PATH:/usr/local/coturn/bin:/home/garrylea/google-clound-sdk/bin

export GOPATH=/home/garrylea/goWorkspace

 

16.环境变量生效

source ~/.bashrc

17.检查配置

env | grep PATH

 

 

 

 

常用命令：

1.删除

rm -rf 被删除文件名

2.创建

mkdir 文件名/文件夹名

3.查看当前绝对路径

pwd

 





- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论](https://blog.csdn.net/iwanghang/article/details/97002411#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReward.png)打赏
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[*手动**安装*:node*-*sass](https://download.csdn.net/download/wengzilai/9826635)

04-26

[set SASS_BINARY_PATH=文件路经 例如： set SASS_BINARY_PATH=F:\WorksCode\lib\win32*-*x64*-*48_binding*.*node 查看环境是否合适：echo %SASS_BINARY_PATH% 如果打印出来您配置好的文件地址那就ok了， 最后再来试试*安装*：npm i *-*g node*-*sass](https://download.csdn.net/download/wengzilai/9826635)

[webstrom自己*手动**安装**Nodejs*提示](https://blog.csdn.net/gusy5188/article/details/80351782)

[gusy5188的博客](https://blog.csdn.net/gusy5188)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 1582

[因为要学Node了，但是没有代码提示，找了一大堆网上的教程都没有成功（因为是破解](https://blog.csdn.net/gusy5188/article/details/80351782)方式安装后，需要查看是否存在版本信息 $ vsftpd -version，再启动服务$ service vsftpd start，看一下服务是否是running状态，安装成功后测试连接，在Windows本机上打开cmd命令输入ftp 47.107.51.32连接到阿里云服务器，输入用户名密码，就可以上传或下载文件了；（如果连接失败检查阿里云防火墙是否有ftp服务端口号为21）这时$put node-v8.11.4-linux-x64.tar.xz上传下载好的node安装包，只能在本机的用户家目录与服务器用户的家目录之间互相传输文件。

4.解压。移动文件node-v8.11.4-linux-x64.tar.xz到/opt目录下，$ mv ~/node-v8.11.4-linux-x64.tar.xz /opt/node-v8.11.4   解压 $ sudo tar -xvf node-v8.11.4-linux-x64.tar.xz ,删除压缩包 sudo rm node-v8.11.4-linux-x64.tar.xz

5.配置环境变量。配置环境变量
       全局/etc/profile 追加export NODE_HOME=/opt/node-v8.11.4-linux-x64

​           export PATH=$PATH:NODE_HOME/bin
​       局部~/.bashrc ~/.profile进入到/opt/node-v8.11.4-linux-x64/bin目录下

6.测试。

# 如何在Linux上安装Node.js

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[shaonbean](https://wanghui.blog.csdn.net/) 2016-11-04 21:09:35 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 4492 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [【CentOS6】](https://blog.csdn.net/wh211212/category_6443643.html) 文章标签： [javascript](https://www.csdn.net/tags/OtDaQg2sNzExLWJsb2cO0O0O.html) [node.js](https://www.csdn.net/tags/OtTaMg1sNDE1LWJsb2cO0O0O.html) [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html)

版权

## Node.js简介

- Node.js是一个基于JavaScript的开源平台，用于开发服务器端和网络应用程序。
  Node.js是跨平台的，因此以Node.js编写的应用程序可以在任何平台上运行。它是建立在谷歌的V8 JavaScript引擎。
  Node.js是高度可扩展的，轻量级的，并且在代码执行速度非常快。它是开发服务器端应用程序的非常流行的脚本语言。

## 安装Node.js

- 有很多方法可以将Node.js安装到您的Linux机器上。 Node.js支持几乎所有的Linux发行版，但在本教程中，我们将学习如何在基于Ubuntu / Debian的机器以及基于CentOS /Fedora的机器上安装它。我们可以使用许多方法安装Node.js，但是建议您使用NodeSource二进制分发存储库或使用节点版本管理器（nvm）进行安装。一些Linux发行版（如Ubuntu）将Node.js包含在其默认存储库中。使用他们的默认存储库安装是超级容易，但你可能找不到最新的版本。

## 使用NodeSource二进制分布存储库

- 从官方NodeSource网站安装Node.js将为您提供最新版本的Node.js，NodeSource主动维护Node.js的官方存储库。

## 基于Debian / Ubuntu版本

- 有多个稳定版本的Node.js可用，您可以根据您的选择安装所需的版本。要安装Node.js 4x，请运行以下命令：

```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -1
```

- 以上命令将在您的计算机配置中添加存储库。执行以下命令在机器中安装Node.js。

```
sudo apt-get install -y nodejs  1
```

- 如果要安装Node.js v6，请执行以下命令：

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs12
```

- 如果要安装Node.js v6，请执行以下命令：ecute the following commands:

```
curl -sL https://deb.nodesource.com/setup | sudo -E bash -
sudo apt-get install -y nodejs12
```

- 安装nodejs也将安装npm，这是Node Package
  Manager。使用npm，您可以轻松地与其他开发人员共享JavaScript代码。有些npm包需要构建工具才能编译和安装。要安装构建工具，请执行以下命令：

```
sudo apt-get install -y build-essential1
```

## 基于RHEL/CentOS/Fedora版本

- 要在基于RHEL / CentOS /Fedora的发行版上添加NodeSource官方存储库，请运行以下命令。您将需要以root用户身份登录以执行以下命令。如果你不是root用户那么你可以在所有命令的开始使用sudo命令：

> For Node.js v4x

```
curl --silent --location https://rpm.nodesource.com/setup_4.x | bash -1
```

> For Node.js v6x

```
curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -1
```

> For Node.js 0.12x

```
curl --silent --location https://rpm.nodesource.com/setup | bash -1
```

- 一旦添加任何上述存储库，您可以执行以下命令来安装Node.js.

```
yum -y install nodejs1
```

- 要安装构建工具，请运行以下命令：

```
yum groupinstall 'Development Tools'1
```

## 使用节点版本管理器（nvm）

- nvm是一个简单的脚本，旨在安装多个版本的Node.js.在所有其他安装方法中，我们只获取该存储库中可用的最新版本的Node.js，但是使用nvm我们可以访问Node.js的所有可用版本。我们还可以使用nvm安装多个版本的Node.js。
- \> 要安装nvm，我们需要安装构建源包所需的工具。运行以下命令在Ubuntu / Debian中安装构建工具：

```
sudo apt-get update
sudo apt-get install build-essential libssl-dev12
```

- \> 如果你在CentOS / Fedora上安装，那么使用这些命令来安装构建工具：

```
sudo yum update
sudo yum groupinstall 'Development Tools'12
```

- 现在当安装构建工具时，您将需要从nvm的官方github存储库获取并执行安装脚本。

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash1
```

- 这将在您的机器上安装nvm。关闭并重新打开您的终端并运行以下命令检查nvm是否已成功安装。

```
command -v nvm1
```

- 这个命令应该简单地给你的终端输出npm。如果是，那么您已成功地将nvm安装到您的计算机上。
  要找出可以通过nvm安装的Node.js的可用版本，请运行以下命令。

```
nvm ls-remote1
```

- 上面的命令的输出将提供一个庞大的Node.js版本列表。

```
 ...
 v5.9.0
 v5.9.1
 v5.10.0
 v5.10.1
 v5.11.0
 v5.11.1
 v6.0.0
 v6.1.0
 v6.2.0
 v6.2.11234567891011
```

- 要安装这些版本，请使用以下命令：

```
nvm install version1
```

- 替换要安装的所需版本的Node.js的版本。例如，如果要安装当前可用的最新版本，请使用以下命令。

```
nvm install v6.2.11
```

- 这将安装版本6.2.1在您的机器，你会看到以下输出。

```
Downloading https://nodejs.org/dist/v6.2.1/node-v6.2.1-linux-x64.tar.xz...
######################################################################## 100.0%
Now using node v6.2.1 (npm v3.9.3)
Creating default alias: default -> v6.2.11234
```

- 我们可以在输出中看到nvm自动配置v6.2.1使用，并且它使这个版本成为默认版本。您可以使用上述命令安装多个版本的Node.js。每个版本的Node.js将安装和管理自己的npm。
- 您可以通过执行以下命令显式要求nvm使用特定版本：

```
nvm use v5.11.11
```

- 您可以用您选择的任何版本替换v5.11.1。您还可以通过发出以下命令更改默认版本：

```
nvm alias default v5.11.11
```

- 要查看所有已安装版本的列表，请运行以下命令：

```
nvm ls1
```

- 您将看到类似于此的输出

```
       v0.11.13
->      v5.11.1
         v6.2.1
default -> v5.11.1
node -> stable (-> v6.2.1) (default)
stable -> 6.2 (-> v6.2.1) (default)
unstable -> 0.11 (-> v0.11.13) (default)
iojs -> N/A (default)12345678
```

> In this output you can see a list of all installed versions. -> indicates the version which you are currently using. default -> tag indicates the default version of Node.js in your machine.

## Node.js入门

- 安装Node.js之后，您可以使用命令节点来执行JavaScript。如果节点使用没有任何文件名或参数，那么它将带您到JavaScript控制台，您可以在其中键入和执行JavaScript命令。从节点接口类型.exit命令退出。您还可以使用Node.js创建http服务器。创建一个新文件并将以下代码添加到其中。例如我们使用nano编辑器和myserver.js文件名。

> 要创建新文件，请运行以下代码：

```
nano myserver.js1
```

> 现在将以下代码添加到文件中：

```
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Node.js is running a server\nHi There');
}).listen(8080);
console.log('HTTP server running on port 8080.');123456
```

> 现在保存文件并退出编辑器。通过执行以下命令运行代码：

```
node myserver.js1
```

> 您将在终端上看到以下输出：

```
HTTP server running on port 8080.1
```

> 您现在可以转到浏览器并访问您的http服务器

```
http://your_ip_addr:80801
```

> ```
> 您将在页面上看到以下消息：
> ```

## 总结

> 在任何Linux机器上安装Node.js有几种不同的方法，但建议使用nvm，因为它提供了更多的灵活性，您可以在任何操作系统上使用安装程序脚本。