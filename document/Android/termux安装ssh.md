# 电脑端连接安卓手机用Termux编程

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Leon_George](https://blog.csdn.net/liangzc1124) 2019-02-18 21:56:20 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 95 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

版权

我的目标是mobile coding，需要在Termux上搭建一个dev环境，以Go环境为例。

### 1 Termux上安装ssh服务

- 在搭建和配置阶段，如果直接通过Android上的软键盘操作，即便屏再大，那个体验也是较差的。我们最好通过PC连到termux上去安装和配置，这就需要我们在Termux上搭建一个sshd server。下面是步骤：

```
$apt install openssh



$sshd
```

- 就这么简单，一个sshd的server就在termux的后台启动起来了。由于Termux没有root权限，无法listen数值小于1024的端口，因此termux上sshd默认的listen端口是8022。

### 2 导入PC端公钥到手机端

- 另外termux上的sshd server不支持用户名+密码的方式进行登录，只能用免密登录的方式，即将PC上的`~/.ssh/id_rsa.pub`写入termux上的`~/.ssh/authorized_keys`文件中。关于免密登录的证书生成方法和导入方式，网上资料已经汗牛充栋，这里就不赘述了。

### 3 PC端利用ssh登录手机ssh服务器

- 导入PC端的公钥至手机中之后，PC就可以通过下面命令登录termux了：

```
$ssh 10.88.46.79  -p 8022



Welcome to Termux!



 



Wiki:            https://wiki.termux.com



Community forum: https://termux.com/community



IRC channel:     #termux on freenode



Gitter chat:     https://gitter.im/termux/termux



Mailing list:    termux+subscribe@groups.io



 



Search packages:   pkg search <query>



Install a package: pkg install <package>



Upgrade packages:  pkg upgrade



Learn more:        pkg help
```

- 其中10.88.46.79是手机的wlan0网卡的IP地址，可以在termux中使用ip addr命令获得:

```
$ip addr show wlan0



34: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 3000



    ... ...



    inet 10.88.46.79/20 brd 10.88.47.255 scope global wlan0



       valid_lft forever preferred_lft forever
```