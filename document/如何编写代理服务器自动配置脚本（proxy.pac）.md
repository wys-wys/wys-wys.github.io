## **FindProxyForURL()函数**

格式：function FindProxyForURL(*url, host*){ ...}

功能：针对浏览器访问的URL及其中包含的HOST名，设置代理服务器

参数：

- url：在浏览器地址栏中输入的完整地址
- host：url中的主机名

返回值：

- DIRECT：不经由代理服务器，直接访问
- PROXY *host:port*：经由指定代理服务器及端口。可指定多个，分号分隔
- SOCKS *host:port*：经由指定的SOCKS服务器及端口。可指定多个，分号分隔

实例：

```js
function FindProxyForURL(url, host)
  {
    if (isPlainHostName(host))
      return "DIRECT";
    else
      return "PROXY proxy:80";
  }
```



## **localHostOrDomainIs()函数**

格式：localHostOrDomainIs(*host, hostdom*)

功能：判断本地主机或域名是否满足指定条件

参数：

- host：主机名
- hostdom：域名

返回值：

- 真
- 假

实例：

```text
localHostOrDomainIs("www.example.com", "www.example.com")
主机名与域名完全一致，返回真

localHostOrDomainIs("www", "www.example.com")
主机名一致，主机未指定域名，返回真

localHostOrDomainIs("www.mcom.com", "www.example.com")
主机名一致，域名不一致，返回假

localHostOrDomainIs("home.example.com", "www.example.com")
主机名不一致，返回假
```



## **isPlainHostName()函数**

格式：isPlainHostName(*host*)

功能：判断是否是本地主机名（不含域名）

返回值：

- 真（主机名中不含.）
- 假（主机名中包含.）



## **dnsDomainIs()函数**

格式：dnsDomainIs(*host, domain*)

功能：判断主机是否在指定域名内

返回值：

- 真（主机在指定域名内）
- 假（主机不在指定域名内）

实例：

```text
dnsDomainIs("www.mozilla.org", ".mozilla.org")
主机域名一致，返回真

dnsDomainIs("www", ".mozilla.org")
主机未指定域名，返回假
```



## **shExpMatch()函数**

格式：shExpMatch(*str, shexp*)

功能：按照shell规则比较字符串是否一致

返回值：

- 真
- 假

实例：

```text
shExpMatch("http://home.netscape.com/people/ari/index.html", "*/ari/*");
返回真

shExpMatch("127.0.0.0", "127.*.*.*")
返回真

shExpMatch("http://home.netscape.com/people/montulli/index.html", "*/ari/*");
返回假
```



## **isInNet()函数**

格式：isInNet(*host, pattern, mask*)

功能：判断主机IP是否在指定子网内

返回值：

- 真
- 假

实例：

```text
isInNet(host, "166.111.0.0", "255.255.0.0"))
如果host的IP是166.111.10.3的话，返回真
如果host的IP是160.111.0.0的话，返回假
```



## **myIpAddress()函数**

格式：myIpAddress()

功能：返回启动浏览器的PC的IP地址

IP地址检测工具：

- [What is my IP address? How do I find my IP address?](https://link.zhihu.com/?target=http%3A//www.myipaddress.com/)
- [What Is My IP Address? IP Address Tools and More](https://link.zhihu.com/?target=https%3A//whatismyipaddress.com/)
- [What is my IP address?](https://link.zhihu.com/?target=https%3A//www.iplocation.net/find-ip-address)
- [What Is My IP? Shows your real IP - IPv4 - IPv6 - WhatIsMyIP.com®](https://link.zhihu.com/?target=https%3A//www.whatismyip.com/)
- [What is My IP | Detailed IP Address Information](https://link.zhihu.com/?target=http%3A//whatismyip.host/my-ip-address-details)
- [What is My IP Address](https://link.zhihu.com/?target=http%3A//www.toolsvoid.com/what-is-my-ip-address)
- [IP Address Info](https://link.zhihu.com/?target=https%3A//ipinfo.info/)

编辑于 2018-07-27

# 自动代理proxy.pac

 转载

[海无崖](https://blog.51cto.com/plong)2013-09-29 14:53:43©著作权

*文章标签*[proxy.pac](https://blog.51cto.com/search/result?q=proxy.pac+)[自动代理](https://blog.51cto.com/search/result?q=自动代理)*阅读数*14591

首先，这博文要是在知道什么是代理或如何使用代理的基础上的。如果不清楚，请查看下代理的有关方面的知识。

在这里主要是讲代理动态配置PAC（proxy auto config）,它实际上是一个 Script；经由编写这个 Script，我们可以让系统判断在怎么样的情形下，要利用哪一台 Proxy 来进行联机。这样做主要的好处有：

1.分散 Proxy 的流量，避免 Proxy Server 负载过高

2.针对个别条件设定进行代理、加快浏览速度

3.设定要求顺序，在某台 Proxy 无法联机时，可自动尝试别种联机方式



**Proxy Auto Config File** **的格式**



基本上 Proxy Auto Config File（以下简称 PAC）是一个纯文字文件，他的语法采用 JavaScript；所以建议要学习编写 PAC 的人，最好先学习基本的 JavaScript。一个 PAC 档必需是单独的JavaScript，其中不能包含任何 HTML 标签。

在 PAC 档中，一定要定义 Function FindProxyForURL 如下：

function FindProxyForURL( url, host )

{

...

}

如果使用了 PAC 档，则浏览器在接受我们要求的网址后，会去执行

ret = FindProxyForURL( url, host );

这样的指令。其中，url 是所要求网址的完整路径，host 是对方的计算机名称（就是在 :// 和 / 之中的部份）；而 return 值 ret 则是 Proxy 的组态，它的格式有下列三种：





·**DIRECT**直接联机而不透过 Proxy

·**PROXY host:port**使用指定的 Proxy 伺服机

·**SOCKS host:port**使用指定的 Socks 伺服机


比如说当浏览器得到的是**Proxy proxy.a.com:3128; Proxy proxy.b.com:3128; DIRECT**的话，那浏览器会先尝试透过 proxy.a.com 来开启网页，如果无法使用，则尝试proxy.b.com，还是不行的话，就直接联机。



\######################################### 函数介绍 #################################





**PAC** **中特别的** **Function**

在 PAC 中，除了可以使用一般 JavaScript 的 Function 外，它还定义了一些特别的 Function 可以使用：

·isPlainHostName()

·dnsDomainIs()

·localHostOrDomainIs()

·isResolvable()

·isInNet()

·dnsResolve()

·myIpAddress()

·dnsDomainLevels()

·shExpMatch()

·weekdayRange()

·dateRange()

·timeRange()



**isPlainHostName( host )**

**host**由网址取得的主机名称。

此 Function 会判断 host 是否为不包含网域 (Domain)。如果是，则 return true；如果包含，则return false。

范例：

1.isPlainHostName("www") 会 return true

2.isPlainHostName("www.netscape.com") 会 return false



**dnsDomainIs( host, domain )**

**host**由网址取得的主机名称。
**domain**指定的网域。

此 Function 会判断 host 是否属于网域 domain。如果是，则 return true；否，则 return false。

范例：

1.dnsDomainIs("www.netscape.com", ".netscape.com") 会 return true

2.dnsDomainIs("www", ".netscape.com") 会 return false

3.dnsDomainIs("www.mcom.com", ".netscape.com") 会 return false



**localHostOrDomainIs( host, hostdom )**

**host**由网址取得的主机名称。
**hostdom**完整的网域名称。

此 Function 会判断 host 是否为 hostdom，或 host 是否为 hostdom 的主机名称。如果是，则 return true；否，则 return false。

范例：

1.localHostOrDomainIs("www.netscape.com", "www.netscape.com") 会 return true （完全相同）

2.localHostOrDomainIs("www", "www.netscape.com") 会 return true （主机名称相同）

3.localHostOrDomainIs("www.mcom.com", "www.netscape.com") 会 return false （网域不同）

4.localHostOrDomainIs("home.netscape.com", "www.netscape.com") 会 return false （主机名称不同）



**isResolvable( host )**

**host**由网址取得的主机名称。

此 Function 会尝试透过 DNS 去解析 host，如果解析成功，则 return true；否则 return false。

范例：

1.isResolvable("www.netscape.com") 会 return true （除非 DNS 无法正常运作）

2.isResolvable("bogus.domain.foobar") 会 return false （除非真的冒出这个 domain 出来…）



**isInNet( host, pattern, mask )**

**host**主机名称，可以是 Domain Name 或 IP。如果是 Domain Name，则会透过 DNS 查出 IP。
**pattern** IP。
**mask**对应于 pattern 的屏蔽。

此 Function 会 host 是否在指定的 IP 范围内，如果是，则 return true；否则 return false。

范例：

1.isInNet(host, "198.95.249.79", "255.255.255.255") 当 host 为 198.95.249.79 时，会 return true。

2.isInNet(host, "140.115.0.0", "255.255.0.0") 当 host 为 140.115.*.* 时，会 return true。



**dnsResolve( host )**

**host**要透过 DNS 解晰的主机名称。

此 Function 会透过 DNS 去解析 host，return 值即为解析之结果。

范例：

1.dnsResolve("www.math.ncu.edu.tw") 会 return "140.115.25.9"。



**myIpAddress()**

此 Function 会 return 浏览器所在计算机之 IP 地址。



**dnsDomainLevels( host )**

**host**由网址取得的主机名称。

此 Function 会 return host 的 Domain 层数（点的数目）。

范例：

1.dnsDomainLevels("www") 会 return 0。

2.dnsDomainLevels("www.netscape.com") 会 return 2。



**shExpMatch( str, shexp )**

**str**要进行比对的字符串。
**shexp**比对的条件。

此 Function 会比对 str 是否符合 shexp 的表示式（此表示式为 shell expression 而非 regular expressions）。如果是，则 return true；否则 return false。

范例：

1.shExpMatch("http://home.netscape.com/people/ari/index.html", "*/ari/*") 会 return true

2.shExpMatch("http://home.netscape.com/people/montulli/index.html", "*/ari/*") 会 return false



**weekdayRange()****、****dateRange()****、****timeRange()**

这三个 Function 的功用都是检查线在时间是否在指定范围内，用这些 Function 就可以设定分时段使用 Proxy Server。但由于较为繁琐，如有兴趣或需要，请参考[原始文件](http://wp.netscape.com/eng/mozilla/2.0/relnotes/demo/proxy-live.html#weekdayRange)





\################################ 事例proxy.pac ###############################





function FindProxyURL(url,host){



if(

dnsDomainIs(host,"www.qq.com") ||

dnsDomainIs(host,"www.weibo.com")

){

return "PROXY proxy.a.com:80" ;

}



return "DIRECT";



}

解释：如果访问的主机名是"www.qq.com"或者"www.weibo.com"的就使用代理服务器（proxy.a.com:80）进行访问,其他的则可以直接访问。



至此，自动代理的配置文件基本上可以写完了。剩下的就是使用部分了.



在浏览器中都会有使用代理功能，如Chrome下图:

[![144157885.png](https://s4.51cto.com/attachment/201309/144157885.png)](https://s4.51cto.com/attachment/201309/144157885.png)




可以看到有“更改代理服器设置”的按钮，点击就会弹出右边的“Internet 连接”的属性选项卡，其中的“连接部分”。

因为在这里的局域网使用的本地连接上网，所以我使用的是“局域网网设置”，就会弹出其设置的对话框，如下图：



[![145224258.png](https://s4.51cto.com/attachment/201309/145224258.png)](https://s4.51cto.com/attachment/201309/145224258.png)



**按上面的配置，在“地址”处填写代理的配置文件的url路径，本地和网络的都可以，只要能访部到就可以了。**

**
**

**至此，已经大功告成了.**