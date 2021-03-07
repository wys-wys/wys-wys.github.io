# [aircrack-ng无线网WIFI破解教程](https://www.cnblogs.com/thespace/p/12750450.html)

转载：http://www.vuln.cn/2674

### 　　　　　　　　　　　　　　　　　　　　　　WIFI破解原理

一直准备找个时间来写个wifi破解教程，因为很多人都想学wifi破解，但是网上的教程都太乱，而且弄来弄错容易错，那是对于wifi破解的原理没有充分的认识，这次准备纯码字给大家通俗的讲解wifi破解，破解工具以aircrack-ng为例，这是一个很强大且具有代表性的工具，网上很多其他的破解工具都是基于aircrack-ng的。

### 名词解释

无线AP：发射无线网的设备，一般是无线路由器

客户端：链接无线网的设备。

握手包：请看下面文章

### WIFI万能钥匙

wifi万能钥匙可以一句话概括一下：用户装了wifi万能钥匙一般会默认分享自己连的wifi密码，当你看到手机wifi万能钥匙里有可破解的wifi的时候，那都是被别人分享过的，“破解”其实就是用别人分享的密码连上了。

### 一般wifi破解原理

破解wifi，首先需要利用一些wifi破解软件，如aircrack-ng进行抓包，我们抓到的包成为握手包，握手包里面包含了加密后的wifi认证信息（包含密码），根据不同的加密方式，破解方式与难度也有所不同。

### wifi加密方式的区别

一般wifi加密方式分为两种wep与wpa/wpa2，详细加密算法有兴趣的可以百度一下。

wep加密方式比较简单，如aircrack-ng可直接读取到密码，这种加密方式已经逐渐淘汰，而且如今常见的路由器加密已经基本上都是wpa/wpa2加密，如图[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi.jpg)

 

wpa/wpa2的加密方式相对复杂，所以我们从抓到的包里得到的密钥是经过更加复杂的加密，没有wep那么简单，针对wpa/wpa2加密后的密钥只能通过暴力破解，比如，我们一般用的windows上的破解软件是EWSA，全称Elcomsoft Wireless Security Auditor。爆破一般都是基于字典的爆破，比如网上有很多wpa的字典下载，集合了很多弱口令或者人们常用的密码，下篇我会把字典发上来分享。

握手包爆破工具有很多，但原理是一样的，关键在于你的字典够不够强大，aircrack也是可以爆破的，我一般就直接用aircrack，简单方便。

**wpa/wpa2破解局限性：由于这种加密是需要基于字典爆破的，所以破解难度是与密码复杂程度成正比的，由此可见一个复杂的密码的安全性是多么重要。**

### 什么是握手包？

上面说了破解无线网需要先进行抓包，抓到的包被成为握手包，引用百科介绍：

> 1、当一个无线客户端与一个无线AP连接时，先发出连接认证请求（握手申请：你好！）
> 2、无线AP收到请求以后，将一段随机信息发送给无线客户端（你是？）
> 3、无线客户端将接收到的这段**随机信息进行加密之后**再发送给无线AP （这是我的名片）
> 4、无线AP检查加密的结果是否正确，如果正确则同意连接 （哦～ 原来是自己人呀！）
> 通常我们说的抓“握手包”，是指在无线AP与它的一个合法客户端在进行认证时，捕获“信息原文”和加密后的“密文”。

握手包的一般格式为.cap格式

其实握手包我也也可以用wireshark打开看一下：

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi1.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi1.jpg)

 

如上图，我们看到的是wifi连接最底层的信息，可以看到加密后的认证信息，由于是wpa加密，所以需要使用字典暴力破解。

### 如何抓到握手包？

这种抓包破解的方法的前提是需要有客户端连接的，比如你家隔壁有个网，但是他家没有任何一个设备连着这个无线网，抓包的时候也没人会去连，这种情况是无法抓包的，但是情况比较少。

之所以需要有客户端连接，是因为抓包的过程中会监测新设备连接这个网，有新设备连接就会有认证过程，就会有握手包，wifi破解工具比如aircrack-ng会有附加的功能：强制已连接的客户端与AP断开，这样客户端就会自动重新连接，也就能抓到包了。

PS：如果你输入一个错误密码也是能抓到包的，不过这个包的认证是没有成功的。

　　　　　　　　　　　　　　　　　　　　

### 　　　　　　　　　　　　　　　　　　　　　　　　　　WIFI破解实战

wpa字典：链接：http://pan.baidu.com/s/1nurkUfB 密码：ofit

这次实战演示的工具：电脑：surface pro3，usb无线网卡：TL-WN722N，虚拟机：vmware 12，虚拟机系统：kali2.0，破解工具：aircrack-ng

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi11.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi11.jpg)

### 准备工作

安装好vmware，在vmware上装好kali系统，加载好本机无线网卡或者USB无线网卡，确保处于连接状态。

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi12.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi12.jpg)

 

### 使用aircrack-ng抓包

iwconfig命令查看无线网卡有没有加载成功，如图，出现了wlan0的无线设备，即为加载成功
[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi2.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi2.jpg)

可以看到里面有个wlan0，那就是我的网卡，如果没有的话就把无线网卡拔了再插一下，直到找到那个wlan0为止。一定要保证它**现在没有连接到任何wifi**，上面那个wlan0里面**没有ip地址**什么的就说明现在不在连接中。

### **激活无线网卡至monitor即监听模式**

使用命令：

| `1`  | `airmon-ng start wlan0` |
| ---- | ----------------------- |
|      |                         |

 

  如果再次使用ifconfig可以发现，我们的网卡已经被重命名为wlan0mon

**获取当前网络概况：**

| `1`  | `airodump-ng wlan0mon` |
| ---- | ---------------------- |
|      |                        |

其中wlan0mon是已经激活监听状态的网卡。

查看需要破解的网在哪个频道（CH），数据传输量(Beacons)如何。

接下来开始抓我们想要的包：

**airodump -w sofia -c 3 wlan0**

解释：-w表示保存握手包，“sofia”为包的名称，可随意设置，最终的文件为sofia-01.cap，-c 3表示指定频道3，wlan0指定网卡设备。

如图，即开始在抓频道3上的包（包含我们需要破解的Tenda_5E93C0）

当然我们也可以指定破解我们想要的AP

**airodump -w sofia -c 3 –bssid C8:3A:35:5E:93:C0 wlan0**

解释：–bssid嗅探指定无线AP，后面跟着AP的bssid，如下图

这时候可以等待握手包的获取。

**英文解释：**

> 1.BSSID–无线AP（路由器）的MAC地址，如果你想PJ哪个路由器的密码就把这个信息记下来备用。
> 2.PWR–这个值的大小反应信号的强弱，越大越好。很重要！！！
> 3.RXQ–丢包率，越小越好，此值对PJ密码影响不大，不必过于关注、
> 4.Beacons–准确的含义忘记了，大致就是反应客户端和AP的数据交换情况，通常此值不断变化。
> 5.#Data–这个值非常重要，直接影响到密码PJ的时间长短，如果有用户正在下载文件或看电影等大量数据传输的话，此值增长较快。 
> 6.CH–工作频道。
> 7.MB–连接速度
> 8.ENC–编码方式。通常有WEP、WPA、TKIP等方式，本文所介绍的方法在WEP下测试100%成功，其余方式本人 并未验证。
> 9.ESSID–可以简单的理解为局域网的名称，就是通常我们在搜索无线网络时看到的列表里面的各个网络的名称。

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi5.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi5.jpg)

为了加速握手包的获取，我们可以使用aireplay来给AP发送断开包：

**aireplay-ng -0 0 -a C8:3A:35:5E:93:C0**

解释：-0为模式中的一种：冲突攻击模式，后面跟发送次数（设置为0，则为循环攻击，不停的断开连接，客户端无法正常上网，-a 指定无线AP的mac地址，即为该无线网的bssid值，上图可以一目了然。

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi6.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi6.jpg)

这时候我们在右上角可以看到WPA handshake字样，后面跟着bssid，即为抓到了该无线网的握手包，我们可以使用CTRL+C来停止嗅探握手包。

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi7.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi7.jpg)

### 使用字典爆破握手包

这一步是整个密码破解的关键，能否成功，取决与你的CPU是否强大，还有你字典的大小，以及字典的质量，密码的复杂程度。

**aircrack-ng sofia-01.cap -w /root/sofia/wifi-hack/dic/wpa专用.txt**

解释：“sofia-01.cap”为指定我们需要破解的握手包，直接写文件名表示文件在当前文件夹下，”-w”指定字典文件后面跟着字典的路径。

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi8.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi8.jpg)

如图正在爆破，

[![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi9.jpg)](http://www.vuln.cn/wp-content/uploads/2016/02/wifi9.jpg)由于这个密码比较简单，一会密码就出来了，为“11112222”
![aircrack-ngwifi破解](http://www.vuln.cn/wp-content/uploads/2016/02/wifi10.jpg)

以上就是教程的全部，对于从来没接触过的新手来说可能有一定的难度，如果在哪一步上出现意外也是正常的，无论我教程写的再详细，也敌不过现实中的意外情况，不同的电脑，不同的网络环境都可能会影响破解的差异性，所以希望大家能够多多练习，熟能生巧。

另外希望大家善用技术，不要做危害他人的事情，无论你技术怎样，做人还是要厚道的，因为螳螂捕蝉黄雀在后的事情还是很常见的（别人能嗅探你的流量）

另一方面希望大家能够通过上下篇教程能够意识到弱口令的危害，加强网络安全意识。

转载：http://www.vuln.cn/2683

本人小白，不接受任何合作，文章多为转载，如有侵权请联系。

分类: [KALI/LINUX](https://www.cnblogs.com/thespace/category/1656685.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1944028/20200216152640.png)](https://home.cnblogs.com/u/thespace/)

[the苍穹](https://home.cnblogs.com/u/thespace/)
[关注 - 4](https://home.cnblogs.com/u/thespace/followees/)
[粉丝 - 8](https://home.cnblogs.com/u/thespace/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/thespace/p/12736866.html)上一篇： [通过神秘代码登录自己的QQ](https://www.cnblogs.com/thespace/p/12736866.html)
[» ](https://www.cnblogs.com/thespace/p/12761591.html)下一篇： [arp欺骗攻击](https://www.cnblogs.com/thespace/p/12761591.html)