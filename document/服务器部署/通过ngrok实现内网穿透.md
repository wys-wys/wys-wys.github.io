#### 遇到得奇怪问题

* ***本地连接到服务器时提示：Failed to read message: remote error: bad certificate #250***
  * Using hostname instead of ip could solve this problem.
* 刚开始时一直连接不上，重新在服务器上编译了数次之后，无果。最后通过教程提供的go版本编译后成功
* 推测可能是因为使用服务器安装得最新版本的go导致
* 

# ngrok使用/踩坑分析-http代理

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[YongApple](https://blog.csdn.net/andylau00j) 2018-10-26 12:26:41 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 4725 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [thrift](https://blog.csdn.net/andylau00j/category_7005803.html) 文章标签： [ngrok 使用 踩坑](https://so.csdn.net/so/search/s.do?q=ngrok 使用 踩坑&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

研究了下 ngrok 的使用，坑还是挺多，随后再看看源码吧，看是否能做些修改和定制

**疑问1： 是否能支持 ecc 证书，目前用的脚本生成的自签RSA证书**

经过测试ngrok客户端+服务器支持 ecc证书。

![img](https://img-blog.csdnimg.cn/20181026175615996.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FuZHlsYXUwMGo=,size_27,color_FFFFFF,t_70)

**疑问2： 性能如何？**

**需要分析源码，完善优化**

 

好了，开始吧。

\1.  当前git上开源的代码版本，号称是1.0x版本，其实是2.1.7

const (

  Proto = "2"

  Major = "1"

  Minor = "7"

)

下载ngrok源码（ngrok代理服务的server/client都在同一份代码中），git上的最新版本是2.1.7，但是ngrok官方最新代码已经闭源，旧代码 凑合还能用。server和client，自己编译，证书自己搞定吧

git clone https://github.com/inconshreveable/ngrok.git

\2. 解压ngrok源码，mv ./ngork 到 /usr/local/ngrok 下

\3. cd /usr/local/ngrok

我的服务器环境:

[root@localhost ngrok]# cat /etc/redhat-release 
CentOS Linux release 7.5.1804 (Core) 

[root@localhost ngrok]# go version 
go version go1.9.4 linux/amd64


我的客户端运行环境:  windows7 X64 SP1

\4. 创建服务器自签名证书

在 /usr/local/ngrok 目录下 
创建 work.sh 脚本，用来创建服务器自签名证书，内容如下：

```bash
#!/bin/bash



 



#生成并替换源码里默认的证书，注意域名要修改为你自己的，这里是一个虚拟的测试域名



NGROK_DOMAIN="dev.mydomain.com"



 



#测试一下有没有设置成功



echo $NGROK_DOMAIN #输出ngrok.xxx.com表示成功



 



openssl genrsa -out rootCA.key 2048



openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem



openssl genrsa -out server.key 2048



openssl req -new -key server.key -subj "/CN=$NGROK_DOMAIN" -out server.csr



openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 5000



 



rm -rf ./server.csr
```

创建自签名证书有个重要的点，需要注意 work.sh 内的 NGROK_DOMAIN 可以设置为自己的域名，随后客户端配置文件ngrok.cfg内 server_addr 后面填写的域名也必须是 NGROK_DOMAIN 的值 

\5.  证书生成完后，需要拷贝指定证书到指定的位置

**下一步也就是第6步，ngrok通过bindata第三方库，将ngrok源码目录下的assets目录（资源文件）打包到可执行文件(ngrokd和ngrok)中 去，assets/client/tls和assets/server/tls下分别存放着用于ngrok和ngrokd的默认证书文件，我们需要将它们替换成我们自己生成的：(因此这一步务必放在编译可执行文件之前)**

```bash
#拷贝客户端要使用的签发服务器的根证书，也就是根证书



\cp rootCA.pem assets/client/tls/ngrokroot.crt -f



# 拷贝服务器证书到指定目录，替换默认证书



\cp server.crt assets/server/tls/snakeoil.crt  -f



\cp server.key assets/server/tls/snakeoil.key -f
```

这是使用了 \cp 因为 直接使用cp，依然会提示是否需要覆盖，比较麻烦，使用 \cp 强行覆盖，不提示

**6. 编译服务器、客户端**

```
sudo make release-server release-client
```

这个命令默认编译的是 linux 平台下 服务器、客户端。

linux服务器编译命令： sudo make release-server

我的客户端是win7，客户端需要交叉编译

[root@localhost ngrok]# GOOS=windows GOARCH=amd64 make release-client
生成的服务器可执行程序在      ./bin/ngrokd

生成的win7客户端可执行程序在  ./bin/windows_amd64/ngrok.exe

**需要其他平台编译的参考下面：**

不同平台使用不同的 GOOS 和 GOARCH，前面的编译选项就是指 go os , go 编译出来的操作系统 (windows,linux,darwin) ；go arch, 对应的构架 (386,amd64,arm)

Linux 平台 32 位系统：GOOS=linux GOARCH=386
Linux 平台 64 位系统：GOOS=linux GOARCH=amd64

Windows 平台 32 位系统：GOOS=windows GOARCH=386
Windows 平台 64 位系统：GOOS=windows GOARCH=amd64

MAC 平台 32 位系统：GOOS=darwin GOARCH=386
MAC 平台 64 位系统：GOOS=darwin GOARCH=amd64

ARM 平台：GOOS=linux GOARCH=arm
不同平台命令后跟上 make release-client / make release-server 就行编译指定平台 client / server

编译使用的go包说明：

- *go-bindata* 包，该库是一套将任意资源文件转成二进制数据反向生成到Go代码供hash调用的技术，Ngrok的源码利用这一技术将公网证书和密钥，以及站点的HTML生成到go代码中去了，使其变成了一堆byte数组，在程序中hash调用。这么做固然有它的好处，但缺点也显而易见，因为这套技术要提前用一个项目的程序生成另一个项目的Go代码，所以编译起来难免繁琐，于是Ngrok提供了makefile文件以供用户make编译，这就有点尴尬了，本来好好的跨平台Go语言项目，被make和makefile活生生憋成了只能Linux使用的了。
- *build -tags* 技术，通过Ngrok项目，我第一次知道Go的这个特性，可以在代码顶端加上`// +build !release`等标记，注明编译时的模式，比如前面这种表达方式，就是在非*release*编译模式下才会编译这个文件，然后使用`go build -tags 'release'`或者`go build -tags 'debug'`来控制是否编译这个代码文件。这个特性确实灵活，可以在项目中编写不同的编译模式下的代码，缺点呢，就是没有详细文档的情况下，第三方用户并不知道有哪些编译模式，加大了源码本地编译的复杂度，所以这也是原版Ngrok项目使用makefile文件的原因之一。
- *[equinox.io](https://www.equinox.io/)* 技术，这项技术可以让Go代码在编译和运行期间保持更新，代码作者更新代码后，能够在第三方用户实时更新，具体没有了解，我看原版Ngrok在进行*release*编译时增加了很多*equinox.io*令牌密钥，以连接远程仓库，保证代码更新。

\7.  下载客户端 执行程序到客户端执行环境

sz   ./bin/windows_amd64/ngrok.exe

注： sz 命令需要安装 yum install -y lrzsz

**此处有个坑，如果只下载 客户端执行文件是不行的。还需要把第5个步骤中的**

assets/client/tls/ngrokroot.crt 一并下载并覆盖到客户端执行环境下，提示，最好是把 assets 这个目录打包压缩，下载到客户端解压，给client使用。

客户端需要ngrok.exe ngrok.cfg 以及 assets 目录，直接把服务器端  覆盖过证书的这个目录 assets 也下载到客户端环境，执行程序同一级目录即可。

下面是客户端目录主要文件列表：

 --- ngrok.exe

 --- ngrok.cfg

 --- assets

 ---  --- client

 ---  ---  --- tls 

 ---  ---  ---  ---  ngrokroot.crt

\8.  执行 服务端

[root@localhost ngrok]# ./bin/ngrokd -tlsKey=./server.key -tlsCrt=./server.crt -domain="dev.mydomain.com" -httpAddr=":80" -httpsAddr=":443" -tunnelAddr=":4443"
[15:09:40 CST 2018/10/26] [INFO] (ngrok/log.(*PrefixLogger).Info:83) [registry] [tun] No affinity cache specified
[15:09:40 CST 2018/10/26] [INFO] (ngrok/log.(*PrefixLogger).Info:83) [metrics] Reporting every 30 seconds
[15:09:40 CST 2018/10/26] [INFO] (ngrok/log.Info:112) Listening for public http connections on [::]:80
[15:09:40 CST 2018/10/26] [INFO] (ngrok/log.Info:112) Listening for public https connections on [::]:443
[15:09:40 CST 2018/10/26] [INFO] (ngrok/log.Info:112) Listening for control and proxy connections on [::]:4443

**服务端参数解析：**

a. 可以看到 侦听 80 443 4443

b. ngrok客户端连接的是客户端配置文件：ngrok.cfg 内配置的端口 4443 

   server_addr: "dev.mydomain.com:4443"

c. `-domain`为你的服务域名，`-httpAddr`为http服务端口地址，访问形式为`xxx.`dev.mydomain.com`:`4443，也可设置为80默认端口，`-httpsAddr`为https服务，同上。

ngrokd还会开一个端口用来跟客户端通讯（可通过`-tunnelAddr=":xxx"` 指定），如果你配置了 iptables 规则，需要放行这个通讯端口(4443)上的 TCP 协议。

```bash
firewall-cmd --zone=public --add-port=4443/tcp --permanent



firewall-cmd --reload
```

\9.  启动客户端

此处客户端配置文件是个大坑，按照网上大量分享的配置

server_addr:"dev.mydomain.com:4443"

trust_host_root_certs:false

> 经测试其实也是可行的

类似这种配置完全不行，各种问题，原因是网上大家分享的是最新版本ngrok的配置。

而我们编译的是开源版本 2.1.7 版本，是较旧版本，需要配置按照yaml方式设置

```bash
server_addr: "dev.mydomain.com:4443"



trust_host_root_certs: false



tunnels:



  abc:



    proto:



      http: 8081



    subdomain: ngrok
```

这配置也是个坑。。里面不许用tab，只能用空格， 不然客户端就启动失败。

\10.  连接成功

客户端 cmd 命令行

C:\ngrok>.\ngrok.exe -config=ngrok.cfg -log=out.log -subdomain=abc 8081

这个子域名 subdomain=abc 作用是，最终生成的映射域名是 abc.dev.mydomain.com 

客户端启动一个http服务，端口8081。此客户端是需要被映射到ngrok上，提供给别人访问的服务。

如果跟ngrok连接success，ngrok客户端会输出下图内容：

![img](https://img-blog.csdnimg.cn/2018102615143446.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FuZHlsYXUwMGo=,size_27,color_FFFFFF,t_70)

隧道状态绿色字体： online 即为成功。

此时，浏览器输入 http://abc.dev.mydomain.com/ 可以测试验证，

如果想实现其他局域网内终端访问该内网http服务， 则需要，其他网络内的终端，把本机dns 设置下，

C:\windows\System32\drivers\etc\hosts

文件内需要新增dns解析记录 10.8.0.1 abc.dev.mydomain.com

10.8.0.1 即为 ngrok server 服务器IP地址。

![img](https://img-blog.csdnimg.cn/2018102615501879.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FuZHlsYXUwMGo=,size_27,color_FFFFFF,t_70)

\11. ngrok启动后，内部会提供一个http服务，浏览器内输入http://localhost:4040/http/in

就可以查看，当前状态

![img](https://img-blog.csdnimg.cn/20181026155444786.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FuZHlsYXUwMGo=,size_27,color_FFFFFF,t_70)

**12.  还有个大坑！**

 **证书重新生成后，居然客户端/服务器可执行程序，需要重新编译。**

***\*否则会输出\**** 

***\*Failed to read message: remote error: bad certificate\****

 

先写这么多，回头继续。

[VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商](https://www.vediotalk.com/archives/336)

2018.03.27 [VLOG](https://www.vediotalk.com/archives/category/feature) 54  [29 ](https://www.vediotalk.com/archives/336#comments) 75273 

目录



[视频介绍](https://www.vediotalk.com/archives/336#视频介绍)[所需要的文件：下载所需文件](https://www.vediotalk.com/archives/336#所需要的文件：下载所需文件)[What?](https://www.vediotalk.com/archives/336#What)[Why?](https://www.vediotalk.com/archives/336#Why)[How?](https://www.vediotalk.com/archives/336#How)[准备工作：](https://www.vediotalk.com/archives/336#准备工作：)[一、域名泛解析](https://www.vediotalk.com/archives/336#一、域名泛解析)[二、go环境搭建](https://www.vediotalk.com/archives/336#二、go环境搭建)[1).下载源码:](https://www.vediotalk.com/archives/336#1)_下载源码)[2).将其解压到/usr/local目录下：](https://www.vediotalk.com/archives/336#2)_将其解压到/usr/local目录下：)[3). 在root环境下执行如下命令：](https://www.vediotalk.com/archives/336#3)_在root环境下执行如下命令：)[三、安装git环境](https://www.vediotalk.com/archives/336#三、安装git环境)[方式一：自动安装git环境](https://www.vediotalk.com/archives/336#方式一：自动安装git环境)[方式二：手动安装git环境(此方法可以安装git的最新版本)](https://www.vediotalk.com/archives/336#方式二：手动安装git环境(此方法可以安装git的最新版本))[四、获取ngrok源码](https://www.vediotalk.com/archives/336#四、获取ngrok源码)[五、编译](https://www.vediotalk.com/archives/336#五、编译)[1). 配置环境变量](https://www.vediotalk.com/archives/336#1)_配置环境变量)[2). 生成自签名ssl证书](https://www.vediotalk.com/archives/336#2)_生成自签名ssl证书)[3). 替换证书](https://www.vediotalk.com/archives/336#3)_替换证书)[4).设置变量：](https://www.vediotalk.com/archives/336#4)_设置变量：)[5).生成服务端](https://www.vediotalk.com/archives/336#5)_生成服务端)[六、交叉编译生成windows客户端、mac客户端](https://www.vediotalk.com/archives/336#六、交叉编译生成windows客户端、mac客户端)[1).windows客户端编译；](https://www.vediotalk.com/archives/336#1)_windows客户端编译；)[2).mac客户端编译；](https://www.vediotalk.com/archives/336#2)_mac客户端编译；)[3).linux客户端编译；](https://www.vediotalk.com/archives/336#3)_linux客户端编译；)[4).arm客户端编译；](https://www.vediotalk.com/archives/336#4)_arm客户端编译；)[七、ngrokd服务启动与使用](https://www.vediotalk.com/archives/336#七、ngrokd服务启动与使用)[1).启动ngrokd服务端](https://www.vediotalk.com/archives/336#1)_启动ngrokd服务端)[2).启动ngrokd客户端](https://www.vediotalk.com/archives/336#2)_启动ngrokd客户端)[八 、公司用代理上网，修改ngrok监听端口，并设置代理既可使用](https://www.vediotalk.com/archives/336#八_、公司用代理上网，修改ngrok监听端口，并设置代理既可使用)[1.ngrok修改端口启动：](https://www.vediotalk.com/archives/336#1_ngrok修改端口启动：)[临时启动：](https://www.vediotalk.com/archives/336#临时启动：)[后台一直运行启动：](https://www.vediotalk.com/archives/336#后台一直运行启动：)[2.创建ngrok.cfg配置文件](https://www.vediotalk.com/archives/336#2_创建ngrok_cfg配置文件)[九、ngrok绑定多个顶级域名、多个二级域名及转发tcp同时启动的方法](https://www.vediotalk.com/archives/336#九、ngrok绑定多个顶级域名、多个二级域名及转发tcp同时启动的方法)[一、配置ngrok.cfg文件](https://www.vediotalk.com/archives/336#一、配置ngrok_cfg文件)[没有使用代理上网配置如下：](https://www.vediotalk.com/archives/336#没有使用代理上网配置如下：)[在公司使用了代理上网的配置如下：](https://www.vediotalk.com/archives/336#在公司使用了代理上网的配置如下：)[二、启动方式](https://www.vediotalk.com/archives/336#二、启动方式)[Linux/Mac 启动命令：](https://www.vediotalk.com/archives/336#Linux/Mac_启动命令：)[Linux/Mac 后台保持启动命令：](https://www.vediotalk.com/archives/336#Linux/Mac_后台保持启动命令：)[windows 启动命令](https://www.vediotalk.com/archives/336#windows_启动命令)

收藏 2

[![VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/3424.jpg)](https://www.vediotalk.com/wp-content/uploads/2018/03/3424.jpg)



 

[国内播放节点](https://www.bilibili.com/video/av21336992)

------

#### 视频介绍

通过搭建ngrok内网穿透服务器，可实现web服务器本地化，tcp、udp转发、微信开发等

------

### 所需要的文件：[下载所需文件](https://pan.baidu.com/s/1FUZdVawurB8To5h9XlltKQ)

# What?

ngrok 是一个反向代理，通过在公共的端点和本地运行的 Web 服务器之间建立一个安全的通道。ngrok 可捕获和分析所有通道上的流量，便于后期分析和重放。简单来说就是可以让你的本地服务暴露在外网上面，可以通过外网访问，这是我们经常需要用到的功能。

# Why?

作为一个Web开发者，我们有时候会需要临时地将一个本地的Web网站部署到外网，以供它人体验评价或协助调试等等，通常我们会这么做：

- 找到一台运行于外网的Web服务器
- 服务器上有网站所需要的环境，否则自行搭建
- 将网站部署到服务器上
- 调试结束后，再将网站从服务器上删除
- 只不过是想向朋友展示一下网站而已，要不要这么麻烦，累感不爱

在国内开发微信公众号、企业号以及做前端开发的朋友想必对ngrok都不陌生吧，就目前来看，ngrok可是最佳的在内网调试微信服务的tunnel工具。之前，ngrok.com提供的服务还一切正常，后来就被墙了 。没有了ngrok tunnel，一切开始变得困难且没有效率起来。内网到外部主机部署和调试是一件慢的让人想骂街的事情。后来就想着自己搭一个ngrok服务。

# How?

如何搭建ngrok服务呢？

下面是我在阿里云centOS7上面的搭建过程。

------

# 准备工作：

1、一台拥有公网ip的服务器或者vps
2、把需要做的主域名解析到服务器上面
软件下载地址：
go的下载地址：http://www.golangtc.com/download
git的下载地址：http://git-scm.com/downloads 绝对下载地址：https://www.kernel.org/pub/software/scm/git/git-2.6.0.tar.gz
ngrok克隆地址：https://github.com/inconshreveable/ngrok.git
准备映射的域名：ngrok.10086ol.com

------

# 一、域名泛解析

[![VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/fdffg.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/fdffg.png)

------

# 二、go环境搭建

go环境安装可以通过源码安装或安装EPEL扩展源后使用yum安装，由于使用yum安装的go不能进行交叉编译，不能够编译生成Windows客户端，所以推荐使用通过源码安装。
源码安装go的详细过程如下：

## 1).下载源码:

可以在http://www.golangtc.com/download 上找到自己系统对应的源码。由于我的vps系统是centos的，所以下载的是：go1.9.2.linux-amd64.tar.gz。

## 2).将其解压到/usr/local目录下：

```
wget https://www.golangtc.com/static/go/1.9.2/go1.9.2.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.9.2.linux-amd64.tar.gz
```

注：如果是64位的系统下载了32位的安装包，后面的构建会出现 /lib/ld-linux.so.2: bad ELF interpreter 类似这样的错误 解决方法：yum install glibc.i686。安装一个32bit的glibc就可以了。

## 3). 在root环境下执行如下命令：

```
mkdir $HOME/go
echo 'export GOROOT=/usr/local/go'>> ~/.bashrc
echo 'export GOPATH=$HOME/go'>> ~/.bashrc
echo 'export PATH=$PATH:$GOROOT/bin'>> ~/.bashrc
source $HOME/.bashrc
```

------

# 三、安装git环境

### 方式一：自动安装git环境

```
yum install mercurial git bzr subversion
```

### 方式二：手动安装git环境(此方法可以安装git的最新版本)

1.下载编译工具

```
yum -y groupinstall "Development Tools"
```

2.下载依赖包

```
yum -y install zlib-devel perl-ExtUtils-MakeMaker asciidoc xmlto openssl-devel
```

3.下载git最新版本源代码
登录

```
https://github.com/git/git/releases
```

查看git的最新版。不要下载带有-rc的，因为它代表了一个候选发布版本。

[![VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-03-26-%E4%B8%8B%E5%8D%888.50.42.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/屏幕快照-2018-03-26-下午8.50.42.png)

如图，可以看出，目前git最新的版本是2.16.3

然后进入

```
https://mirrors.edge.kernel.org/pub/software/scm/git/
```

查找到对应版本下载

[![VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-03-26-%E4%B8%8B%E5%8D%889.00.49.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/屏幕快照-2018-03-26-下午9.00.49.png)

```
wget https://www.kernel.org/pub/software/scm/git/git-2.16.3.tar.gz
```

4.解压

```
tar -zxvf git-2.16.3.tar.gz
```

5.进入目录配置

```
cd git-2.16.3
./configure --prefix=/usr/local/git
```

6.编译安装

```
make && make install
```

7.配置全局路径

```
export PATH="/usr/local/git/bin:$PATH"
source /etc/profile
```

8.查看git版本

```
git --version
```

------

# 四、获取ngrok源码

获取源码：

```
git clone https://github.com/inconshreveable/ngrok.git
```

如果获取源码速度较慢，可以进入https://github.com/inconshreveable/ngrok.git 下载源码到本地，上传至目录/root/ngrok

------

# 五、编译

## 1). 配置环境变量

```
cd
cd ngrok
export NGROK_DOMAIN="ngrok.10086ol.com"
```

ngrok.10086ol.com替换成你自己的域名

## 2). 生成自签名ssl证书

```
openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out device.key 2048
openssl req -new -key device.key -subj "/CN=$NGROK_DOMAIN" -out device.csr
openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000
```

## 3). 替换证书

```
cp rootCA.pem assets/client/tls/ngrokroot.crt
cp device.crt assets/server/tls/snakeoil.crt
cp device.key assets/server/tls/snakeoil.key
```

替换时系统会提示是否替换，输入“y”后回车确定替换

## 4).设置变量：

```
GOOS=linux GOARCH=amd64
```

如果是32位系统，这里 GOARCH=386

## 5).生成服务端

```
make release-server release-client
```

注：上述编译的过程会需要去github、google code下载其余依赖项目的源码，因此需要挂VPN。当然，如果VPS不能挂vpn可以在本地进行上面介绍的操作过程，然后将编译后的源码复制到vps上重新编译即可。 还有一种最简单的解决办法就是，修改源码，将需要连接google code的地址改为连接github上的地址:
找到 /root/ngrok/src/ngrok/log/logger.go ，看到里面有一个import中引用了google code，将其改为：”github.com/keepeye/log4go” 。
*（在本地操作方法：*
*1.使用winscp进入本地centos目录，找到/root/ngrok/src里面的github.com、gopkg.in两个文件夹上传至对应目录下*
*2.进入root权限ssh root@192.156.35.3*
*3.`cd ngrokGOOS=linux GOARCH=amd64make release-server release-client`）*

编译之后，就会在ngrok源码的bin目录下生成两个可执行文件：ngrokd、ngrok。其中ngrokd就是ngrok的服务端程序，ngrok就是ngrok的客户端程序。由于现在生成的客户端ngrok只能在linux下运行，因此如果想要生成windows下的客户端程序，需要继续进行交叉编译。

------

 

# 六、交叉编译生成windows客户端、mac客户端

## 1).windows客户端编译；

进入go目录，进行环境配置

```
cd /usr/local/go/src/
GOOS=windows GOARCH=amd64 CGO_ENABLED=0 ./make.bash
```

进入ngrok目录重新编译

```
cd
cd ngrok
GOOS=windows GOARCH=amd64 make release-server release-client
```

编译后，就会在/root/ngrok/bin目录下生成windows_amd64目录，其中就包含着windows下运行的服务器和客户端程序。

## 2).mac客户端编译；

进入go目录，进行环境配置

```
cd /usr/local/go/src/
GOOS=darwin GOARCH=amd64 CGO_ENABLED=0 ./make.bash
```

进入ngrok目录重新编译

```
cd
cd ngrok
GOOS=darwin GOARCH=amd64 make release-server release-client
```

编译后，就会在/root/ngrok/bin目录下生成mac客户端目录，其中就包含着windows下运行的服务器和客户端程序。

## 3).linux客户端编译；

进入go目录，进行环境配置

```
cd /usr/local/go/src/
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 ./make.bash
```

进入ngrok目录重新编译

```
cd
cd ngrok
GOOS=linux GOARCH=amd64 make release-server release-client
```

编译后，就会在/root/ngrok/bin目录下生成mac客户端目录，其中就包含着windows下运行的服务器和客户端程序。

## 4).arm客户端编译；

进入go目录，进行环境配置

```
cd /usr/local/go/src/
GOOS=linux GOARCH=arm CGO_ENABLED=0 ./make.bash
```

进入ngrok目录重新编译

```
cd
cd ngrok
GOOS=linux GOARCH=arm make release-server release-client
```

编译后，就会在/root/ngrok/bin目录下生成mac客户端目录，其中就包含着windows下运行的服务器和客户端程序。

------

 

# 七、ngrokd服务启动与使用

## 1).启动ngrokd服务端

临时启动：

```
cd ngrok
bin/ngrokd -domain="ngrok.10086ol.com" -httpAddr=":80"
```

注：ngrok.10086ol.com更换为你自己的域名

后台一直运行启动：

```
cd ngrok
nohup bin/ngrokd -domain="ngrok.10086ol.com" -httpAddr=":80" &
```

注：ngrok.10086ol.com更换为你自己的域名
想要结束后台进程
`ps -A #找到PIDkill xxx`

## 2).启动ngrokd客户端

创建ngrok.cfg配置文件

```
server_addr: "ngrok.10086ol.com:4443"
trust_host_root_certs: false
```

注：ngrok.10086ol.com更换为你自己的域名
ngrok.cfg配置文件和ngrok客户端放在本地同一文件夹内

windows客户端启动方式
1.打开CMD命令
2.如果ngrok.cfg配置文件和ngrok客户端放在本地桌面，那么输入命令

```
cd desktop
ngrok -config=ngrok.cfg -subdomain veecolor 80
```

veecolor是你自定义地址
3.如果你自己有顶级域名，想通过自己的域名来访问本机的项目，那么先将自己的顶级域名解析到你自己服务器的ip：119.29.113.146(域名需要已备案哦)，然后执行 `ngrok -config=ngrok.cfg -hostname xxx.xxx.xxx 80` //(xxx.xxx.xxx是你自定义的顶级域名)

Linux/Mac客户端启动方式
1.打开终端
2.如果ngrok.cfg配置文件和ngrok客户端放在本地桌面，那么输入命令

```
cd desktop
./ngrok -config=ngrok.cfg -subdomain=veecolor 80
```

veecolor是你自定义地址
3.如果你自己有顶级域名，想通过自己的域名来访问本机的项目，那么先将自己的顶级域名解析到你自己的服务器ip:119.29.113.146(域名需要已备案哦)，然后执行 `./ngrok -config=ngrok.cfg -hostname xxx.xxx.xxx 80` //(xxx.xxx.xxx是你自定义的顶级域名)

看到这样以下界面就说明成功了：

[![VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2018/03/fde.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/fde.png)

# 

4.保持后台启动

```
cd desktop
setsid ./ngrok -config=ngrok.cfg -subdomain=veecolor 80
```

------

 

# 八 、公司用代理上网，修改ngrok监听端口，并设置代理既可使用

注意：大家在看视频教程的时候，这里的域名ngrok.veecolor.com与之前的ngrok.10086ol.com,不一样是因为我在做这个节教程的时候换了域名了，不影响，大家把域名替换成你自己的就行。

## 1.ngrok修改端口启动：

### 临时启动：

```
cd ngrok
bin/ngrokd -domain="ngrok.10086ol.com" -httpAddr=":80" -httpsAddr=":8081" -tunnelAddr=":443"
```

注：ngrok.10086ol.com更换为你自己的域名
把默认端口4443修改为443，在原来的启动命令中加入-tunnelAddr=”:443″

### 后台一直运行启动：

```
cd ngrok
nohup bin/ngrokd -domain="ngrok.10086ol.com" -httpAddr=":80" -httpsAddr=":8081" -tunnelAddr=":443" &
注：ngrok.10086ol.com更换为你自己的域名
把默认端口4443修改为443，在原来的启动命令中加入-tunnelAddr=":443"
```

## 2.创建ngrok.cfg配置文件

```
server_addr: "ngrok.10086ol.com:443"
trust_host_root_certs: false
http_proxy: http://10.168.57.241:8088
```

注：ngrok.10086ol.com更换为你自己的域名
ngrok.cfg配置文件和ngrok客户端放在本地同一文件夹内
把原来的端口号4443修改为443，并加入公司代理上网地址及端口，http://10.168.57.241:8088替换为你们公司的代理地址。

------

# 九、ngrok绑定多个顶级域名、多个二级域名及转发tcp同时启动的方法

 

上次ngrok的配置教程中只讲解了配置一个二级域名及一个顶级域名的方法，这个教程教大家配置多个顶级域名、多个二级域名及转发tcp同时启动的方法。
server_addr: 服务器地址
tunnels:连接隧道
subdomain: 想服务器分配的域名
proto:转发服务
http: http模式
remote_port: 远程端口，当做tcp转发的时候如果不设置将有服务器自动分配
tcp: tcp模式
hostname: 绑定顶级域名
auth: 需要身份验证
http_proxy: 使用代理

# 一、配置ngrok.cfg文件

## 没有使用代理上网配置如下：

 

```
server_addr: "ngrok.10086ol.com:443"
tunnels:
  vee:
    subdomain: "vee"
    auth: "vee:admin1993"
    proto:
     http: 192.168.1.108:80
  vee1:
    subdomain: "vee1"
    proto:
     http: 192.168.1.104:80
  ssh:
    remote_port: 50000
    proto:
     tcp: 192.168.1.120:22
  test:
    hostname: "test.10086ol.com"
    proto:
     http: 80
  test1:
    hostname: "10086ol.com"
    proto:
     http: 192.168.1.104:80
  test2:
    hostname: "www.10086ol.com"
    proto:
     http: 192.168.1.104:80
```

## 在公司使用了代理上网的配置如下：

```
server_addr: "ngrok.10086ol.com:443"
http_proxy: http://10.168.57.241:8088
tunnels:
  test1:
    hostname: "www.10086ol.com"
    proto:
     http: 127.0.0.1:80
  test2:
    hostname: "10086ol.com"
    proto:
     http: 127.0.0.1:80
```

http_proxy: http://10.168.57.241:8088修改为你们公司的代理地址即可

# 二、启动方式

## Linux/Mac 启动命令：

```
./ngrok -config=ngrok.cfg start vee vee1 ssh test test1 test2
```

## Linux/Mac 后台保持启动命令：

```
setsid ./ngrok -config=ngrok.cfg start vee vee1 ssh test test1 test2
```

## windows 启动命令

```
ngrok -config=ngrok.cfg start vee vee1 ssh test test1 test2
```

转载原创文章请注明，转载自: [Vedio Talk ](https://www.vediotalk.com/)- [VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 ](https://www.vediotalk.com/archives/336)(https://www.vediotalk.com/archives/336)

[54](javascript:;)

分享到：  

上一篇: [LINUX | 开启ubuntu 17.04下的SSH远程连接](https://www.vediotalk.com/archives/318)

下一篇: [群晖 | DSM6.1.5设置ROOT密码，获取ROOT权限](https://www.vediotalk.com/archives/346)



[VLOG | 送粉丝福利！DIY手工SSD高速U盘，写150MB/S 读200MB/S](https://www.vediotalk.com/archives/39997)

[VLOG](https://www.vediotalk.com/archives/category/feature)2021.04.25

- [![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png) vee](https://www.vediotalk.com/archives/author/vee)
-  556
-  3
-  3



[VPS | 甲骨文如何正确开放端口](https://www.vediotalk.com/archives/39863)

[VPS](https://www.vediotalk.com/archives/category/vt笔记/vps)2021.04.23

- [![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png) vee](https://www.vediotalk.com/archives/author/vee)
-  322
-  0
-  0



[ESXI | 6.7/7.0如何把U盘设置为存储](https://www.vediotalk.com/archives/39786)

[ESXI](https://www.vediotalk.com/archives/category/vt笔记/esxi)2021.04.22

- [![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png) vee](https://www.vediotalk.com/archives/author/vee)
-  356
-  0
-  0

### 留言

要发表评论，您必须先[登录](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)。

评论(29)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  [内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商 – Veido-T资源社区 - 分享科技、改变生活！](http://www.ubxb.cn/23/123.html)

  […] 转载原创文章请注明，转载自: Vedio Talk – VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商…(https://www.vediotalk.com/archives/336) […]

  [02-23-2020 ](https://www.vediotalk.com/archives/336#comment-23427)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  卢练焕

  配置git的时候，我文件夹名称改成GIT，方便记录，然后在输入./configure –prefix=/usr/local/git这一步出现-bash: ./configure: No such file or directory，请问文该怎么处理啊？？

  [01-13-2020](https://www.vediotalk.com/archives/336#comment-17731)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](https://www.vediotalk.com/)

    推荐用FRP了 NGROK已经过时了

    [01-20-2020](https://www.vediotalk.com/archives/336#comment-18593)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  [VLOG丨内网穿透手把手教你自建ngrok服务器，从此抛弃花生壳公云等DDNS服务商–转载 – 开心ucu-电脑](http://dis.ucu520.top/2019/10/23/vlog%e4%b8%a8%e5%86%85%e7%bd%91%e7%a9%bf%e9%80%8f%e6%89%8b%e6%8a%8a%e6%89%8b%e6%95%99%e4%bd%a0%e8%87%aa%e5%bb%bangrok%e6%9c%8d%e5%8a%a1%e5%99%a8%ef%bc%8c%e4%bb%8e%e6%a)

  […] https://www.vediotalk.com/archives/336 […]

  [10-23-2019 ](https://www.vediotalk.com/archives/336#comment-11605)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  sheldon

  大佬请教一下, $NGROK_DOMAIN 所设定的域名是否需要经过备案呢?
  我这边按照流程走下来, 发现无法连接到我的阿里云服务器上面, ngrokd服务是正常跑的
  客户端的报错信息是
  [2019/07/11 13:33:48 CST] [EROR] (ngrok/log.Error:120) control recovering from failure dial tcp 106.15.94.31:4443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.

  [07-11-2019](https://www.vediotalk.com/archives/336#comment-8352)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](https://www.vediotalk.com/)

    国内服务器都需要备案

    [07-18-2019](https://www.vediotalk.com/archives/336#comment-8383)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  zhe

  如何实现https访问呢

  [03-19-2019](https://www.vediotalk.com/archives/336#comment-7999)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  yu_an

  你好，请问为什么我跟着教程走却提示这个？
  我用这种方式可以正常启动（bin/ngrokd -domain=”ngrok.10086ol.com” -httpAddr=”:80″ -httpsAddr=”:8081″ -tunnelAddr=”:443″），但是我想用来转发TCP所以无法用这个来启动；
  用ngrok -config=ngrok.cfg start来启动就如图报错，请问是什么原因？
  错误信息：Tunnel mstsc does not specify any protocols to tunnel.
  ngrok version：1.7 Centos7

  [![img](https://www.vediotalk.com/wp-content/uploads/2018/03/profile-300x214.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/profile.png)

  [02-05-2019](https://www.vediotalk.com/archives/336#comment-7893)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![img](https://secure.gravatar.com/avatar/9f5ffcdffe62b96d09de6ab1cc7e0af2?s=48)

  [Hirsi](https://www.miwunet.com/)

  非常感谢，搭建成功了，但是有个问题：
  昨日，在搭建成功之后，启动成功了，然后发现自己服务器上的网站不能访问了，我猜原因是端口冲突。
  今天，我将服务器重启之后，网站可以访问了，但是在启动ngrok服务器的时候出现“panic: listen tcp :80: bind: address already in use”，80端口冲突；于是我启动ngrok的时候使用8181端口，然后又出现了443端口冲突，请问443端口冲突怎么解决呢。期待您的回复

  [![img](https://www.vediotalk.com/wp-content/uploads/2018/03/TIM20190203102202-300x157.png)](https://www.vediotalk.com/wp-content/uploads/2018/03/TIM20190203102202.png)

  [02-03-2019](https://www.vediotalk.com/archives/336#comment-7891)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](https://www.vediotalk.com/)

    一般情况不会冲突啊 是不是你服务器搭建了有其他服务再用443端口的

    [07-18-2019](https://www.vediotalk.com/archives/336#comment-8384)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  [zhengrt](http://www.zdaoyun.com/)

  大佬，非常感谢，搭建成功了！！！终于摆脱花生壳了！！谢谢

  [01-29-2019](https://www.vediotalk.com/archives/336#comment-7884)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  轩硕科技

  编译安装那一步时出错了，复制粘贴 make && make install 命令然后回车，下面显示
  CC credential-store.o
  In file included from credential-store.c:1:0:
  cache.h:44:18: fatal error: zlib.h: No such file or directory
  \#include
  ^
  compilation terminated.
  …这是啥情况？

  [01-20-2019](https://www.vediotalk.com/archives/336#comment-7866)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  [群晖使用ngrok内网穿透解决方案，适用于黑白群晖 | zero博客](http://www.s028c.tk/2018/11/17/qun-hui-shi-yong-ngrok-nei-wang-chuan-tou-jie-jue-fang-an-shi-yong-yu-hei-bai-qun-hui/)

  […] 搭建方案直通车 […]

  [11-17-2018 ](https://www.vediotalk.com/archives/336#comment-7742)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  流浪神

  非常感谢已经搭建成功了，问下，这个跟商业的好像有区别，怎么让路由器穿透？

  [11-02-2018](https://www.vediotalk.com/archives/336#comment-7727)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](https://www.vediotalk.com/)

    没区别的 路由器穿透？

    [11-06-2018](https://www.vediotalk.com/archives/336#comment-7728)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  Apstaiz

  非常感谢，经过一天一夜的琢磨，终于成功了！

  [04-16-2018](https://www.vediotalk.com/archives/336#comment-50)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  匿名

  楼主利好，生成服务端那个步骤做不出来了，安装出口留学软件什么鬼，再说你那两个文件没看见你发下载地址啊，

  [04-08-2018](https://www.vediotalk.com/archives/336#comment-40)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](http://www.vediotalk.com/)

    出国留学就是您能上youtube 那你就出国留学了，说的隐晦点。

    [04-09-2018](https://www.vediotalk.com/archives/336#comment-42)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](http://www.vediotalk.com/)

    下载地址在这篇文章的视频下方，把这两个文件上传，就可以生成服务端了

    [04-09-2018](https://www.vediotalk.com/archives/336#comment-41)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  zjkzwh

  你好 在中间过程我遇到了一个问题就是找不到go1.4不知道该怎么继续？

  [04-03-2018](https://www.vediotalk.com/archives/336#comment-31)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

    [vee](http://www.vediotalk.com/)

    能具体说下是操作到哪一步吗？

    [04-03-2018](https://www.vediotalk.com/archives/336#comment-33)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

    - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

      [vee](http://www.vediotalk.com/)

      好的 过段时间我出个 这方面的教程

      [04-06-2018](https://www.vediotalk.com/archives/336#comment-39)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

    - ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

      zjkzwh

      make release-server release-client
      好像是这一步附近

      [04-03-2018](https://www.vediotalk.com/archives/336#comment-34)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

      - ![vee](https://www.vediotalk.com/wp-content/uploads/2018/09/%E8%87%AA%E5%AA%92%E4%BD%93LOGO-150x150-100x100.png)

        [vee](http://www.vediotalk.com/)

        我视频里面也有找不到go1.4的提示，但是没有关系不影响，直接下一步操作就可以了

        [04-04-2018](https://www.vediotalk.com/archives/336#comment-35)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

        - ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

          zjkzwh

          小哥哥 求出个树莓派lnmp环境的搭建 四次了没搭成

          [04-05-2018](https://www.vediotalk.com/archives/336#comment-37)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

        - ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

          zjkzwh

          = =‘’ ojbk Thanks♪(･ω･)ﾉ

          [04-05-2018](https://www.vediotalk.com/archives/336#comment-36)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

- ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

  [fans](http://vediotalk.com/)

  很感谢你的教程 在你的教程里最后本地客户端已经成为了外网服务器 在穿透使用后 是客户端用多少流量 腾讯云服务器就用多少流量吗 还是节省了服务器的压力

  [03-30-2018](https://www.vediotalk.com/archives/336#comment-27)[登录以回复](https://www.vediotalk.com/login?redirect_to=https%3A%2F%2Fwww.vediotalk.com%2Farchives%2F336)

  - ![头像](https://www.vediotalk.com/wp-content/plugins/wp-user-avatar/images/wpua-96x96.png)

    vee

    是的本地服务器用多少流量，腾讯云就是使用多少流量

    [03-30-2018](https://www.vediotalk.com/archives/336#comment-28)

# 搭建自己的ngrok服务(内网穿透 使用简单)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[高效编程](https://blog.csdn.net/zkf9044) 2017-10-14 12:01:17 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 26284 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 5

分类专栏： [java](https://blog.csdn.net/zkf9044/category_6914009.html) 文章标签： [内网穿透](https://so.csdn.net/so/search/s.do?q=内网穿透&t=blog&o=vip&s=&l=&f=&viparticle=)

在国内开发微信公众号、企业号以及做前端开发的朋友想必对ngrok都不陌生吧，就目前来看，ngrok可是最佳的在内网调试微信服务的tunnel工 具。记得今年春节前，ngrok.com提供的服务还一切正常呢，但春节后似乎就一切不正常了。ngrok.com无法访问，ngrok虽然能连上 ngrok.com提供的服务，但微信端因为无法访问ngrok.com，导致消息一直无法发送到我们的服务地址上，比如xxxx.ngrok.com。 这一切都表明，ngork被墙了。没有了ngrok tunnel，一切开始变得困难且没有效率起来。内网到外部主机部署和调试是一件慢的让人想骂街的事情。

ngrok不能少。ngrok以及其服务端ngrokd都是开源的，之前我也知道通过源码可以自搭建ngrok服务。请求搜索引擎后，发现国内有个朋友已经搭建了一个www.tunnel.mobi的ngrok公共服务，与ngrok.com类似，我也实验了一下。

编写一个ngrok.cfg，内容如下：

server_addr: “tunnel.mobi:44433”
trust_host_root_certs: true

用ngrok最新客户端1.7版本执行如下命令：

$ngrok -subdomain tonybaiexample -config=ngrok.cfg 80

可以顺利建立一个tunnel，用于本机向外部提供”tonybaiexample.tunnel.mobi”服务。

Tunnel Status online
Version 1.7/1.7
Forwarding [http://tonybaiexample.tunnel.mobi](http://tonybaiexample.tunnel.mobi/) -> 127.0.0.1:80
Forwarding [https://tonybaiexample.tunnel.mobi](https://tonybaiexample.tunnel.mobi/) -> 127.0.0.1:80
Web Interface 127.0.0.1:4040
\# Conn 0
Avg Conn Time 0.00ms

而且国内的ngrok服务显然要远远快于ngrok.com提供的服务，消息瞬间即达。

但这是在公网上直接访问的结果。放在公司内部，我看到的却是另外一个结果：

Tunnel Status reconnecting
Version 1.7/
Web Interface 127.0.0.1:4040
\# Conn 0
Avg Conn Time 0.00ms

我们无法从内网建立tunnel，意味着依旧不方便和低效，因为很多基础服务都在内网部署，内外网之间的交互十分不便。但内网连不上tunnel.mobi也是个事实，且无法知道原因，因为看不到server端的连接错误日志。

于是我决定自建一个ngrok服务。

一、准备工作

搭建ngrok服务需要在公网有一台vps，去年年末曾经在Amazon申请了一个体验主机EC2，有公网IP一个，这次就打算用这个主机作为ngrokd服务端。

需要一个自己的域名。已有域名的，可以建立一个子域名，用于关联ngrok服务，这样也不会干扰原先域名提供的服务。(不用域名的方式也许可以，但我没有试验过。）

搭建的参考资料主要来自下面三个：
1) ngrok的官方SELFHOST指南：https://github.com/inconshreveable/ngrok/blob/master/docs/SELFHOSTING.md
2) 国外一哥们的博客：http://www.svenbit.com/2014/09/run-ngrok-on-your-own-server/
3) “海运的博客”中的一篇文章：http://www.haiyun.me/archives/1012.html

二、实操步骤

我的AWS EC2实例安装的是Ubuntu Server 14.04 x86_64，并安装了golang 1.4（go version go1.4 linux/amd64）。Golang是编译ngrokd和ngrok所必须的，建议直接从golang官方下载对应平台的二进制安装包（国内可以从 golangtc.com上下载，速度慢些罢了）。

1、下载ngrok源码

（GOPATH=~/goproj)
mkdir /goproj/src/github.com/inconshreveablemkdir /goproj/src/github.com/inconshreveable git clone https://github.com/inconshreveable/ngrok.git
$ export GOPATH=~/goproj/src/github.com/inconshreveable/ngrok

2、生成自签名证书

使用ngrok.com官方服务时，我们使用的是官方的SSL证书。自建ngrokd服务，我们需要生成自己的证书，并提供携带该证书的ngrok客户端。

证书生成过程需要一个NGROK_BASE_DOMAIN。 以ngrok官方随机生成的地址693c358d.ngrok.com为例，其NGROK_BASE_DOMAIN就是”ngrok.com”，如果你要 提供服务的地址为”example.tunnel.tonybai.com”，那NGROK_BASE_DOMAIN就应该 是”tunnel.tonybai.com”。

我们这里以NGROK_BASE_DOMAIN=”tunnel.tonybai.com”为例，生成证书的命令如下：

cd /goproj/src/github.com/inconshreveable/ngrokcd /goproj/src/github.com/inconshreveable/ngrok openssl genrsa -out rootCA.key 2048
opensslreq−x509−new−nodes−keyrootCA.key−subj“/CN=tunnel.tonybai.com”−days5000−outrootCA.pemopensslreq−x509−new−nodes−keyrootCA.key−subj“/CN=tunnel.tonybai.com”−days5000−outrootCA.pem openssl genrsa -out device.key 2048
opensslreq−new−keydevice.key−subj“/CN=tunnel.tonybai.com”−outdevice.csropensslreq−new−keydevice.key−subj“/CN=tunnel.tonybai.com”−outdevice.csr openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

执行完以上命令，在ngrok目录下就会新生成6个文件：

-rw-rw-r– 1 ubuntu ubuntu 1001 Mar 14 02:22 device.crt
-rw-rw-r– 1 ubuntu ubuntu 903 Mar 14 02:22 device.csr
-rw-rw-r– 1 ubuntu ubuntu 1679 Mar 14 02:22 device.key
-rw-rw-r– 1 ubuntu ubuntu 1679 Mar 14 02:21 rootCA.key
-rw-rw-r– 1 ubuntu ubuntu 1119 Mar 14 02:21 rootCA.pem
-rw-rw-r– 1 ubuntu ubuntu 17 Mar 14 02:22 rootCA.srl

ngrok通过bindata将ngrok源码目录下的assets目录（资源文件）打包到可执行文件(ngrokd和ngrok)中 去，assets/client/tls和assets/server/tls下分别存放着用于ngrok和ngrokd的默认证书文件，我们需要将它们替换成我们自己生成的：(因此这一步务必放在编译可执行文件之前)

cp rootCA.pem assets/client/tls/ngrokroot.crt
cp device.crt assets/server/tls/snakeoil.crt
cp device.key assets/server/tls/snakeoil.key

3、编译ngrokd和ngrok

在ngrok目录下执行如下命令，编译ngrokd：

$ make release-server

不过在我的AWS上，出现如下错误：

GOOS=”” GOARCH=”” go get github.com/jteeuwen/go-bindata/go-bindata
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/client/assets/assets_release.go \
assets/client/…
make: bin/go-bindata: Command not found
make: *** [client-assets] Error 127

go-bindata被安装到了GOBIN下了，go编译器找不到了。修正方法是将GOBIN下了，go编译器找不到了。修正方法是将GOBIN/go-bindata拷贝到当前ngrok/bin下。

$ cp /home/ubuntu/.bin/go14/bin/go-bindata ./bin

再次执行make release-server。

~/goproj/src/github.com/inconshreveable/ngrok$ make release-server
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/client/assets/assets_release.go \
assets/client/…
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/server/assets/assets_release.go \
assets/server/…
go get -tags ‘release’ -d -v ngrok/…
code.google.com/p/log4go (download)
go: missing Mercurial command. See http://golang.org/s/gogetcmd
package code.google.com/p/log4go: exec: “hg”: executable file not found in $PATH
github.com/gorilla/websocket (download)
github.com/inconshreveable/go-update (download)
github.com/kardianos/osext (download)
github.com/kr/binarydist (download)
github.com/inconshreveable/go-vhost (download)
github.com/inconshreveable/mousetrap (download)
github.com/nsf/termbox-go (download)
github.com/mattn/go-runewidth (download)
github.com/rcrowley/go-metrics (download)
Fetching https://gopkg.in/yaml.v1?go-get=1
Parsing meta tags from https://gopkg.in/yaml.v1?go-get=1 (status code 200)
get “gopkg.in/yaml.v1”: found meta tag main.metaImport{Prefix:”gopkg.in/yaml.v1”, VCS:”git”, RepoRoot:”https://gopkg.in/yaml.v1“} at https://gopkg.in/yaml.v1?go-get=1
gopkg.in/yaml.v1 (download)
make: *** [deps] Error 1

又出错！提示找不到hg，原来是aws上没有安装hg。install hg后（sudo apt-get install mercurial），再编译。

$ make release-server
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/client/assets/assets_release.go \
assets/client/…
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/server/assets/assets_release.go \
assets/server/…
go get -tags ‘release’ -d -v ngrok/…
code.google.com/p/log4go (download)
go install -tags ‘release’ ngrok/main/ngrokd

同样编译ngrok:

$ make release-client
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/client/assets/assets_release.go \
assets/client/…
bin/go-bindata -nomemcopy -pkg=assets -tags=release \
-debug=false \
-o=src/ngrok/server/assets/assets_release.go \
assets/server/…
go get -tags ‘release’ -d -v ngrok/…
go install -tags ‘release’ ngrok/main/ngrok

AWS上ngrokd和ngrok被安装到了$GOBIN下。

三、调试

1、启动ngrokd

$ ngrokd -domain=”tunnel.tonybai.com” -httpAddr=”:8080” -httpsAddr=”:8081”
[03/14/15 04:47:24] [INFO] [registry] [tun] No affinity cache specified
[03/14/15 04:47:24] [INFO] [metrics] Reporting every 30 seconds
… …

2、公网连接ngrokd

将生成的ngrok下载到自己的电脑上。

创建一个配置文件ngrok.cfg，内容如下：

server_addr: “tunnel.tonybai.com:4443”
trust_host_root_certs: false

执行ngrok：
$ ngrok -subdomain example -config=ngrok.cfg 80

Tunnel Status reconnecting
Version 1.7/
Web Interface 127.0.0.1:4040
、# Conn 0
Avg Conn Time 0.00ms

连接失败。此刻我的电脑是在公网上。查看ngrokd的日志，没有发现连接到达Server端。试着在本地ping tunnel.tonybai.com这个地址，发现地址不通。难道是DNS设置的问题。之前我只是设置了”*.tunnel.tonybai.com”的A地址，并未设置”tunnel.tonybai.com”。于是到DNS管理页面，添加了”tunnel.tonybai.com”的A记录。

待DNS记录刷新OK后，再次启动ngrok：

Tunnel Status online
Version 1.7/1.7
Forwarding [http://epower.tunnel.tonybai.com:8080](http://epower.tunnel.tonybai.com:8080/) -> 127.0.0.1:80
Forwarding [https://epower.tunnel.tonybai.com:8080](https://epower.tunnel.tonybai.com:8080/) -> 127.0.0.1:80
Web Interface 127.0.0.1:4040
\# Conn 0
Avg Conn Time 0.00ms

这回连接成功了！

3、内网连接ngrokd

将ngrok拷贝到内网的一台PC上，这台PC设置了公司的代理。

按照同样的步骤启动ngrok：

$ ngrok -subdomain example -config=ngrok.cfg 80

Tunnel Status reconnecting
Version 1.7/
Web Interface 127.0.0.1:4040
\# Conn 0
Avg Conn Time 0.00ms

不巧，怎么又失败了！从Server端来看，还是没有收到客户端的连接，显然是连接没有打通公司内网。从我自己的squid代理服务器来看，似乎只有443端口的请求被公司代理服务器允许通过，4443则无法出去。

1426301143.558 9294 10.10.126.101 TCP_MISS/000 366772 CONNECT api.equinox.io:443 – DEFAULT_PARENT/proxy.xxx.com - 通过了
1426301144.441 27 10.10.126.101 TCP_MISS/000 1185 CONNECT tunnel.tonybai.com:4443 – DEFAULT_PARENT/proxy.xxx.com - 似乎没有通过

只能修改server监听端口了。将-tunnelAddr由4443改为443(注意AWS上需要修改防火墙的端口规则，这个是实时生效的，无需重启实例)：

$ sudo ngrokd -domain=”tunnel.tonybai.com” -httpAddr=”:8080” -httpsAddr=”:8081” -tunnelAddr=”:443”
[03/14/15 04:47:24] [INFO] [registry] [tun] No affinity cache specified
[03/14/15 04:47:24] [INFO] [metrics] Reporting every 30 seconds
… …

将ngrok.cfg中的地址改为443：

server_addr: “tunnel.tonybai.com:443”

再次执行ngrok客户端：

Tunnel Status online
Version 1.7/1.7
Forwarding [http://epower.tunnel.tonybai.com:8080](http://epower.tunnel.tonybai.com:8080/) -> 127.0.0.1:80
Forwarding [https://epower.tunnel.tonybai.com:8080](https://epower.tunnel.tonybai.com:8080/) -> 127.0.0.1:80
Web Interface 127.0.0.1:4040
\# Conn 0
Avg Conn Time 0.00ms

这回成功连上了。

4、80端口

是否大功告成了呢？我们看看ngrok的结果，总感觉哪里不对呢？噢，转发的地址怎么是8080端口呢？为何不是80？微信公众号/企业号可只是支持80端口啊！

我们还需要修改一下Server端的参数，将-httpAddr从8080改为80。

$ sudo ngrokd -domain=”tunnel.tonybai.com” -httpAddr=”:80” -httpsAddr=”:8081” -tunnelAddr=”:443”

这回再用ngrok连接一下：
Tunnel Status online
Version 1.7/1.7
Forwarding [http://epower.tunnel.tonybai.com](http://epower.tunnel.tonybai.com/) -> 127.0.0.1:80
Forwarding [https://epower.tunnel.tonybai.com](https://epower.tunnel.tonybai.com/) -> 127.0.0.1:80
Web Interface 127.0.0.1:4040
\# Conn 0
Avg Conn Time 0.00ms

这回与我们的需求匹配上了。

5、测试

在内网的PC上建立一个简单的http server 程序：hello

//hello.go
package main

import “net/http”

func main() {
http.HandleFunc(“/”, hello)
http.ListenAndServe(“:80”, nil)
}

func hello(w http.ResponseWriter, r *http.Request) {
w.Write([]byte(“hello!”))
}

gobuild−ohellohello.gogobuild−ohellohello.go sudo ./hello

通过公网浏览器访问一下“[http://epower.tunnel.tonybai.com](http://epower.tunnel.tonybai.com/)”这个地址，如果你看到浏览器返回”hello!”字样，那么你的ngrokd服务就搭建成功了！

四、注意事项

客户端ngrok.cfg中server_addr后的值必须严格与-domain以及证书中的NGROK_BASE_DOMAIN相同，否则Server端就会出现如下错误日志：

[03/13/15 09:55:46] [INFO] [tun:15dd7522] New connection from 54.149.100.42:38252
[03/13/15 09:55:46] [DEBG] [tun:15dd7522] Waiting to read message
[03/13/15 09:55:46] [WARN] [tun:15dd7522] Failed to read message: remote error: bad certificate
[03/13/15 09:55:46] [DEBG] [tun:15dd7522] Closing

手把手教你搭建ngrok服务－轻松外网调试本机站点

上传日期：2019.06.01

1880

ngrok的核心功能：能够将你本机的HTTP服务（站点）或TCP服务，通过部署有ngrok服务的外网伺服器暴露给外网访问！

半年多没用ngrok，然后昨天发现它被墙了，艸～。

<!-- more -->

## ngrok是什么鬼？

做前端开发的童鞋或许不会太陌生。 如果你完全不知道它是什么东西，可以在它的github项目上了解下： [https://github.com/inconshreveable/ngrok ](https://github.com/inconshreveable/ngrok)这里只提下它的核心功能：能够将你本机的HTTP服务（站点）或TCP服务，通过部署有ngrok服务的外网伺服器暴露给外网访问！

如上封面图所示，举一个栗子。

1. 橘色屏幕的笔记本是你的工作机器，安装了ngrok客户端
2. ngrok.com所在的服务器安装了ngrok的服务端（ngrokd）
3. 利用ngrok 8080命令可以将你本机的8080端口暴露给反向代理至ngrok.com的某个二级域名如：xxx.ngrok.com
4. 别人通过xxx.ngrok.com就可以访问你本机8080端口上的站点内容了。

由此可见，除了Weinre、browsersync 这些惯用的手段外，借助ngrok，也一样可以解决前端开发过程经常遇到的“本地开发，外网调试”老大难题。

囧的是：ngrok.com被墙了，我们已无法用它官方的服务～ 国内虽然有一些第三方的ngrok服务，但是也无法保证其稳定性。 还好ngrok是开源的，我们可以通过它的源码在自己的外网服务器上搭建自己的ngrok服务。

前提条件是：一台外网可访问的主机，且有域名解析至该主机上。

## 搭建服务端ngrokd

### 1.安装go语言开发环境

ngrok是利用go语言开发的，所以先要在服务器上安装go语言开发环境。 以CentOS的服务器示例，安装Go语言很简单的：

```javascript
sudo yum install golang
```

安装完毕后，利用go version来验证是否安装成功。 go安装好后，我们再设置下go的环境变量：

在`~/.zshrc`或`~/.bash_profile`文件内，加入以下环境变量配置内容：

```
export GOPATH=$HOME/go
PATH=$PATH:$HOME/.local/bin:$HOME/bin:$GOPATH/bin
```

保存后，重新给shell加载下配置文件：`source ~/.zshrc`

最后可通过go env查看是否配置成功。

### 2.安装git

安装过程略。后面我们需要利用git拉取源码。

### 3.fork并拉取ngrok的源码

下面编译过程需要改官方的部分源码，所以最好fork一份源码至自己的github账户。

```
$ mkdir -p ~/go/src/github.com/mamboer
$ cd ~/go/src/github.com/mamboer
$ git clone https://github.com/mamboer/ngrok.git
```

源码拉取下来后，需要修改一个地方： 打开`src/ngrok/log/logger.go`文件 将`code.google.com/p/log4go` 修改为：`github.com/alecthomas/log4go`

googlecode已经寿终了，我们将依赖的log4go替换成github的版本。

在编译ngrok的源码之前，我们还需要改下官方源码用到的签名证书。

### 4.生成自签名证书

使用ngrok.com官方服务时，我们使用的是官方的SSL证书。自建ngrokd服务，如果不想买SSL证书，我们需要生成自己的自签名证书，并编译一个携带该证书的ngrok客户端。

证书生成过程需要一个NGROK_BASE_DOMAIN。 以ngrok官方随机生成的地址693c358d.ngrok.com为例，其NGROK_BASE_DOMAIN就是"ngrok.com"，如果你要 提供服务的地址为"example.ngrok.xxx.com"，那NGROK_BASE_DOMAIN就应该 是”ngrok.xxx.com"。

我们这里以NGROK_BASE_DOMAIN=“ngrok.fex.im"为例，生成证书的命令如下：

```
$ cd ngrok
$ openssl genrsa -out rootCA.key 2048
$ openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=ngrok.fex.im" -days 5000 -out rootCA.pem
$ openssl genrsa -out device.key 2048
$ openssl req -new -key device.key -subj "/CN=ngrok.fex.im" -out device.csr
$ openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000
```

执行完以上命令，在ngrok目录下就会新生成6个文件：

```
-rw-rw-r-- 1 lv lv  985 Feb 17 19:04 device.crt
-rw-rw-r-- 1 lv lv  895 Feb 17 19:04 device.csr
-rw-rw-r-- 1 lv lv 1679 Feb 17 19:03 device.key
-rw-rw-r-- 1 lv lv 1675 Feb 17 19:01 rootCA.key
-rw-rw-r-- 1 lv lv 1103 Feb 17 19:03 rootCA.pem
-rw-rw-r-- 1 lv lv   17 Feb 17 19:04 rootCA.srl
```

ngrok通过bindata将ngrok源码目录下的assets目录（资源文件）打包到可执行文件(ngrokd和ngrok)中 去，assets/client/tls和assets/server/tls下分别存放着用于ngrok和ngrokd的默认证书文件，我们需要将它们替换成我们自己生成的：(因此这一步务必放在编译可执行文件之前)

```
cp rootCA.pem assets/client/tls/ngrokroot.crt
cp device.crt assets/server/tls/snakeoil.crt
cp device.key assets/server/tls/snakeoil.key
```

### 5.编译客户端程序ngrok和服务端程序ngrokd

在ngrok目录下执行如下命令，编译ngrokd：

```
$ make release-server
```

类似的，利用以下命令编译ngrok:

```
$ make release-client
```

成功编译后，会在bin目录下找到`ngrokd`和`ngrok`这两个文件。

我们将ngrokd文件拷贝至`~/go/bin`目录下，以方便在其他目录内也可以直接通过ngrokd来访问该执行程序。

### 6.运行ngrokd服务

```
ngrokd -domain="ngrok.fex.im" -httpAddr=":8088" -httpsAddr=":8089"
[15:08:52 CST 2016/02/18] [INFO] (ngrok/log.(*PrefixLogger).Info:83) [registry] [tun] No affinity cache specified
[15:08:52 CST 2016/02/18] [INFO] (ngrok/log.(*PrefixLogger).Info:83) [metrics] Reporting every 30 seconds
[15:08:52 CST 2016/02/18] [INFO] (ngrok/log.Info:112) Listening for public http connections on [::]:8088
[15:08:52 CST 2016/02/18] [INFO] (ngrok/log.Info:112) Listening for public https connections on [::]:8089
[15:08:52 CST 2016/02/18] [INFO] (ngrok/log.Info:112) Listening for control and proxy connections on [::]:4443
```

### 7.为ngrok.fex.im添加dns解析

添加两条A记录：`ngrok.fex.im`和`*.ngrok.fex.im`，指向fex.im所在的服务器ip。

至此为止，我们的ngrokd服务端搭建配置完成，同时我们在CentOS系统的服务器上编译了一份客户端的执行程序－一个ngrok文件。 如果你的开发机器系统也是CentOS，是可以直接将ngrok这个客户端执行文件拷贝到本地开发机器中来使用的。 但如果你的机器是Mac 或者windows，我们还需要在自己的电脑中编译一份相同签名文件的客户端程序！

注意：请记得提交已更改的源码至github，一会还要用到。

## 在MAC中编译ngrok客户端

服务器是CentOS，自己的工作电脑是Mac，所以得在自己的电脑中编译一份相同签名文件的客户端程序！

### 1.安装go

与服务器的步骤类似，我们首先要安装go语言环境：

```
brew update
brew install go
```

### 2.设置go的环境变量（略）

### 3.拉取源码并编译客户端（略）

最后将编译好的ngrok文件，拷贝至$GOPATH/bin目录内，以便在命令行内任意目录内均可以直接通过ngrok运行程序。

## 最后的验证

ngrokd服务配置好了，客户端程序也有了，下面测试下ngrok是否能够正常使用。

1. 创建一个ngrok配置文件：ngrok.cfg

   ```
   server_addr: “ngrok.fex.im:4443"
   trust_host_root_certs: false
   ```

2. 运行客户端，暴露8080端口的站点

   ```
   $ ngrok -subdomain demo -config=/Users/lv/bin/ngrok.cfg 8080
   ```

3. 在8080端口下建一个测试站点

   方便起见，我们拉取 [git@github.com ](http://mailto:git@github.com/):o2team/brand.git做测试：

   ```
   npm i -g node-static
   git clone git@github.com:o2team/brand.git
   cd brand
   static
   ```

4. 在浏览器中输入demo.ngrok.fex.im:8088

   bingo!

   

   ![img](https://img10.360buyimg.com/ling/jfs/t1/36495/29/12573/67953/5d084babEb3dd1d1b/bf53f49b77fb1016.jpg)

   

5. 在浏览器中输入：localhost:4040

   可以查看所有的请求情况！

   ![img](https://img10.360buyimg.com/ling/jfs/t1/54563/16/2710/46427/5d084bc9E84e5e228/92c7342a06da7a14.jpg)

   

## 注意事项

客户端ngrok.cfg中server_addr后的值必须严格与-domain以及证书中的`NGROK_BASE_DOMAIN`相同，否则Server端就会出现如下错误日志：

```
[03/13/15 09:55:46] [INFO] [tun:15dd7522] New connection from 54.149.100.42:38252
[03/13/15 09:55:46] [DEBG] [tun:15dd7522] Waiting to read message
[03/13/15 09:55:46] [WARN] [tun:15dd7522] Failed to read message: remote error: bad certificate
[03/13/15 09:55:46] [DEBG] [tun:15dd7522] Closing
```

## 参考资料

- 自建ngrok服务

1. http://tonybai.com/2015/03/14/selfhost-ngrok-service/
2. https://github.com/inconshreveable/ngrok/blob/master/docs/SELFHOSTING.md

- go的安装

1. https://blog.starkandwayne.com/2014/12/04/how-to-install-go-on-digital-ocean/

## 结语

本文主要介绍了ngrok服务的自行搭建。同时为大家免费提供我搭建好的ngrok服务：ngrok.fex.im。 fex.im所在的机器是digitalocean的一个主机，虽然国内速度慢但是还算稳定。

## 如何使用ngrok.fex.im?

### 安装client

Linux 下载: [http://fex.im/files/ngrok ](http://fex.im/files/ngrok)Mac OSX 下载： https://github.com/mamboer/ngrok/releases/download/1.7.2/ngrok

放在 `/usr/local/bin` 目录下

### 设置所有者

```
sudo chown $(whoami):staff ngrok
```

### 设置权限

```
sudo chmod 777 ngrok
```

### 运行客户端

```
$ ngrok -subdomain demo -config=/Users/lv/bin/ngrok.cfg 8080
```

### 配置文件

```
server_addr: “ngrok.fex.im:4443"
trust_host_root_certs: false
```



文章标签