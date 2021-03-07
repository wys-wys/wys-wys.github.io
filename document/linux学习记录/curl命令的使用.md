1.  curl -I选项，只获得对方的响应首部信息；

   例：curl -I http://www.baidu.com

   curl www.baidu.com访问网页

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/05e24be983aee8d779c46d5c6b781431deb66641.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/1570c1b6326c5766be218ce0a4632385e1366141.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

2. 

   curl -v www.baidu.com显示一次HTTP请求的通信过程

   如下，请求内容包括请求头和请求内容等详细信息

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/46a92de039723d038a04b035bb486143d6d45741.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

3. 

   Curl执行GET/POST/PUT/DELETE操作 hou

   -X后跟指定的命令参数去执行

   curl -X PUT www.baidu.com 

   curl -X DELETE www.baidu.com

   curl -X POST www.baidu.com 

   curl -X GET www.baidu.com

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/49701aebf6a75f0fb8c5fa5d97324b18502c4c41.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

4. 

   使用curl时，有两个超时时间：一个是连接超时时间，另一个是数据传输的最大允许时间。

   连接超时时间用 –connect-timeout 参数来指定，数据传输的最大允许时间用 -m 参数来指定。

   curl -connect-timeout 10 -m 20 “http://outofmemory.cn/”

   下面是数据传输超过20s的常见报错

   curl: (28) Operation timed out after 20000 milliseconds with 0 bytes received

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/506d92f1d8a726330a6a4350c02c56ee7a7f4441.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/57af657f860e7c75ac1a7246650d3aceabd7bf41.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

5. 

   curl命令上传和下载用法(还支持文件的断点续传和分块下载）

   curl -o [文件名] www.sina.com保存网页

   curl -T filename ftp://user:pass@ip/docs #上传

   curl -O ftp://user:pass@ip/filename #下载

   -o和-O的区别在于小写o是保存到命令行中指定文件名，大写O是使用URL中文件名作为输出文件

   ![curl命令使用详解](https://exp-picture.cdn.bcebos.com/ef4c24ceaad7726b430ceb54bf0f64781523b941.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

# curl 的用法指南

作者： [阮一峰](http://www.ruanyifeng.com/)

日期： [2019年9月 5日](http://www.ruanyifeng.com/blog/2019/09/)

## 简介

curl 是常用的命令行工具，用来请求 Web 服务器。它的名字就是客户端（client）的 URL 工具的意思。

它的功能非常强大，命令行参数多达几十种。如果熟练的话，完全可以取代 Postman 这一类的图形界面工具。

![img](https://www.wangbase.com/blogimg/asset/201909/bg2019090501.jpg)

本文介绍它的主要命令行参数，作为日常的参考，方便查阅。内容主要翻译自[《curl cookbook》](https://catonmat.net/cookbooks/curl)。为了节约篇幅，下面的例子不包括运行时的输出，初学者可以先看我以前写的[《curl 初学者教程》](http://www.ruanyifeng.com/blog/2011/09/curl.html)。

不带有任何参数时，curl 就是发出 GET 请求。

> ```bash
> $ curl https://www.example.com
> ```

上面命令向`www.example.com`发出 GET 请求，服务器返回的内容会在命令行输出。

## **-A**

`-A`参数指定客户端的用户代理标头，即`User-Agent`。curl 的默认用户代理字符串是`curl/[version]`。

> ```bash
> $ curl -A 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.100 Safari/537.36' https://google.com
> ```

上面命令将`User-Agent`改成 Chrome 浏览器。

> ```bash
> $ curl -A '' https://google.com
> ```

上面命令会移除`User-Agent`标头。

也可以通过`-H`参数直接指定标头，更改`User-Agent`。

> ```bash
> $ curl -H 'User-Agent: php/1.0' https://google.com
> ```

## **-b**

`-b`参数用来向服务器发送 Cookie。

> ```bash
> $ curl -b 'foo=bar' https://google.com
> ```

上面命令会生成一个标头`Cookie: foo=bar`，向服务器发送一个名为`foo`、值为`bar`的 Cookie。

> ```bash
> $ curl -b 'foo1=bar;foo2=bar2' https://google.com
> ```

上面命令发送两个 Cookie。

> ```bash
> $ curl -b cookies.txt https://www.google.com
> ```

上面命令读取本地文件`cookies.txt`，里面是服务器设置的 Cookie（参见`-c`参数），将其发送到服务器。

## **-c**

`-c`参数将服务器设置的 Cookie 写入一个文件。

> ```bash
> $ curl -c cookies.txt https://www.google.com
> ```

上面命令将服务器的 HTTP 回应所设置 Cookie 写入文本文件`cookies.txt`。

## **-d**

`-d`参数用于发送 POST 请求的数据体。

> ```bash
> $ curl -d'login=emma＆password=123'-X POST https://google.com/login
> # 或者
> $ curl -d 'login=emma' -d 'password=123' -X POST  https://google.com/login
> ```

使用`-d`参数以后，HTTP 请求会自动加上标头`Content-Type : application/x-www-form-urlencoded`。并且会自动将请求转为 POST 方法，因此可以省略`-X POST`。

`-d`参数可以读取本地文本文件的数据，向服务器发送。

> ```bash
> $ curl -d '@data.txt' https://google.com/login
> ```

上面命令读取`data.txt`文件的内容，作为数据体向服务器发送。

## **--data-urlencode**

`--data-urlencode`参数等同于`-d`，发送 POST 请求的数据体，区别在于会自动将发送的数据进行 URL 编码。

> ```bash
> $ curl --data-urlencode 'comment=hello world' https://google.com/login
> ```

上面代码中，发送的数据`hello world`之间有一个空格，需要进行 URL 编码。

## **-e**

`-e`参数用来设置 HTTP 的标头`Referer`，表示请求的来源。

> ```bash
> curl -e 'https://google.com?q=example' https://www.example.com
> ```

上面命令将`Referer`标头设为`https://google.com?q=example`。

`-H`参数可以通过直接添加标头`Referer`，达到同样效果。

> ```bash
> curl -H 'Referer: https://google.com?q=example' https://www.example.com
> ```

## **-F**

`-F`参数用来向服务器上传二进制文件。

> ```bash
> $ curl -F 'file=@photo.png' https://google.com/profile
> ```

上面命令会给 HTTP 请求加上标头`Content-Type: multipart/form-data`，然后将文件`photo.png`作为`file`字段上传。

`-F`参数可以指定 MIME 类型。

> ```bash
> $ curl -F 'file=@photo.png;type=image/png' https://google.com/profile
> ```

上面命令指定 MIME 类型为`image/png`，否则 curl 会把 MIME 类型设为`application/octet-stream`。

`-F`参数也可以指定文件名。

> ```bash
> $ curl -F 'file=@photo.png;filename=me.png' https://google.com/profile
> ```

上面命令中，原始文件名为`photo.png`，但是服务器接收到的文件名为`me.png`。

## **-G**

`-G`参数用来构造 URL 的查询字符串。

> ```bash
> $ curl -G -d 'q=kitties' -d 'count=20' https://google.com/search
> ```

上面命令会发出一个 GET 请求，实际请求的 URL 为`https://google.com/search?q=kitties&count=20`。如果省略`--G`，会发出一个 POST 请求。

如果数据需要 URL 编码，可以结合`--data--urlencode`参数。

> ```bash
> $ curl -G --data-urlencode 'comment=hello world' https://www.example.com
> ```

## **-H**

`-H`参数添加 HTTP 请求的标头。

> ```bash
> $ curl -H 'Accept-Language: en-US' https://google.com
> ```

上面命令添加 HTTP 标头`Accept-Language: en-US`。

> ```bash
> $ curl -H 'Accept-Language: en-US' -H 'Secret-Message: xyzzy' https://google.com
> ```

上面命令添加两个 HTTP 标头。

> ```bash
> $ curl -d '{"login": "emma", "pass": "123"}' -H 'Content-Type: application/json' https://google.com/login
> ```

上面命令添加 HTTP 请求的标头是`Content-Type: application/json`，然后用`-d`参数发送 JSON 数据。

## **-i**

`-i`参数打印出服务器回应的 HTTP 标头。

> ```bash
> $ curl -i https://www.example.com
> ```

上面命令收到服务器回应后，先输出服务器回应的标头，然后空一行，再输出网页的源码。

## **-I**

`-I`参数向服务器发出 HEAD 请求，然会将服务器返回的 HTTP 标头打印出来。

> ```bash
> $ curl -I https://www.example.com
> ```

上面命令输出服务器对 HEAD 请求的回应。

`--head`参数等同于`-I`。

> ```bash
> $ curl --head https://www.example.com
> ```

## **-k**

`-k`参数指定跳过 SSL 检测。

> ```bash
> $ curl -k https://www.example.com
> ```

上面命令不会检查服务器的 SSL 证书是否正确。

## **-L**

`-L`参数会让 HTTP 请求跟随服务器的重定向。curl 默认不跟随重定向。

> ```bash
> $ curl -L -d 'tweet=hi' https://api.twitter.com/tweet
> ```

## **--limit-rate**

`--limit-rate`用来限制 HTTP 请求和回应的带宽，模拟慢网速的环境。

> ```bash
> $ curl --limit-rate 200k https://google.com
> ```

上面命令将带宽限制在每秒 200K 字节。

## **-o**

`-o`参数将服务器的回应保存成文件，等同于`wget`命令。

> ```bash
> $ curl -o example.html https://www.example.com
> ```

上面命令将`www.example.com`保存成`example.html`。

## **-O**

`-O`参数将服务器回应保存成文件，并将 URL 的最后部分当作文件名。

> ```bash
> $ curl -O https://www.example.com/foo/bar.html
> ```

上面命令将服务器回应保存成文件，文件名为`bar.html`。

## **-s**

`-s`参数将不输出错误和进度信息。

> ```bash
> $ curl -s https://www.example.com
> ```

上面命令一旦发生错误，不会显示错误信息。不发生错误的话，会正常显示运行结果。

如果想让 curl 不产生任何输出，可以使用下面的命令。

> ```bash
> $ curl -s -o /dev/null https://google.com
> ```

## **-S**

`-S`参数指定只输出错误信息，通常与`-s`一起使用。

> ```bash
> $ curl -s -o /dev/null https://google.com
> ```

上面命令没有任何输出，除非发生错误。

## **-u**

`-u`参数用来设置服务器认证的用户名和密码。

> ```bash
> $ curl -u 'bob:12345' https://google.com/login
> ```

上面命令设置用户名为`bob`，密码为`12345`，然后将其转为 HTTP 标头`Authorization: Basic Ym9iOjEyMzQ1`。

curl 能够识别 URL 里面的用户名和密码。

> ```bash
> $ curl https://bob:12345@google.com/login
> ```

上面命令能够识别 URL 里面的用户名和密码，将其转为上个例子里面的 HTTP 标头。

> ```bash
> $ curl -u 'bob' https://google.com/login
> ```

上面命令只设置了用户名，执行后，curl 会提示用户输入密码。

## **-v**

`-v`参数输出通信的整个过程，用于调试。

> ```bash
> $ curl -v https://www.example.com
> ```

`--trace`参数也可以用于调试，还会输出原始的二进制数据。

> ```bash
> $ curl --trace - https://www.example.com
> ```

## **-x**

`-x`参数指定 HTTP 请求的代理。

> ```bash
> $ curl -x socks5://james:cats@myproxy.com:8080 https://www.example.com
> ```

上面命令指定 HTTP 请求通过`myproxy.com:8080`的 socks5 代理发出。

如果没有指定代理协议，默认为 HTTP。

> ```bash
> $ curl -x james:cats@myproxy.com:8080 https://www.example.com
> ```

上面命令中，请求的代理使用 HTTP 协议。

## **-X**

`-X`参数指定 HTTP 请求的方法。

> ```bash
> $ curl -X POST https://www.example.com
> ```

上面命令对`https://www.example.com`发出 POST 请求。

 

**一.curl工具概述**

```
　　curl是基于URL语法在命令行方式下工作的文件传输工具，它支持FTP，FTPS，HTTP，HTTPS，GOPHER，TELNET，DICT，FILE及LDAP等协议;

　　curl支持HTTPS认证，并且支持HTTP的POST、PUT等方法， FTP上传， kerberos认证，HTTP上传，代理服务器，cookies，用户名/密码认证， 下载文件断点续传，上载文件断点续传, http代理服务器管道（ proxy tunneling）;

　　curl还支持IPv6，socks5代理服务器，通过http代理服务器上传文件到FTP服务器等，功能十分强大。
```

 

**二.curl工具常用选项高数**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
语法格式：
　　curl [options] [URL...]


常用选项如下所示:
　　-A/--user-agent <string>:
　　　　设置用户代理发送给服务器

　　-e/--referer <URL>:
　　　　来源网址

　　--cacert <file>:
　　　　CA证书 (SSL)

　　-k/--insecure:
　　　　允许忽略证书进行 SSL 连接

　　--compressed:
　　　　要求返回是压缩的格式

　　-H/--header <line>:
　　　　自定义首部信息传递给服务器

　　-i:
　　　　显示页面内容，包括报文首部信息

　　-I/--head:
　　　　只显示响应报文首部信息

　　-D/--dump-header <file>:
　　　　将url的header信息存放在指定文件中

　　--basic:
　　　　使用HTTP基本认证
　　-u/--user <user[:password]>:
　　　　设置服务器的用户和密码
　　-L:
　　　　如果有3xx响应码，重新发请求到新位置
　　　　-O:
　　　　使用URL中默认的文件名保存文件到本地
　　-o <file>:
　　　　将网络文件保存为指定的文件中
　　--limit-rate <rate>:
　　　　设置传输速度
　　-0/--http1.0:
　　　　数字0，使用HTTP 1.0
　　-v/--verbose:
　　　　更详细

　　-C:
　　　　选项可对文件使用断点续传功能
　　-c/--cookie-jar <file name>:
　　　　将url中cookie存放在指定文件中
　　-x/--proxy <proxyhost[:port]>:
　　　　指定代理服务器地址
　　-X/--request <command>:
　　　　向服务器发送指定请求方法
　　-U/--proxy-user <user:password>:
　　　　代理服务器用户和密码
　　-T:
　　　　选项可将指定的本地文件上传到FTP服务器上
　　--data/-d:
　　　　方式指定使用POST方式传递数据
　　-b name=data:
　　　　从服务器响应set-cookie得到值，返回给服务器
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

**三.\**\*\*curl命令测试\*\*HTTP协议实战案例\*\*\*\*\****

**1>."-A/--user-agent <string>"案例**

```
[root@node101.yinzhengjie.org.cn ~]# curl -A 'Chrome/78.0.3904.108 Safari/537.36' http://node107.yinzhengjie.org.cn          #设置用户代理发送给服务器,其实就是封装了请求报文中的"User-Agent"参数，可以结合"-v"选项查看的更详细。
<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# curl --user-agent 'Firefox/108 ' http://node107.yinzhengjie.org.cn 
<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]#
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) [root@node107.yizhengjie.org.cn ~]# tail -10f /var/log/httpd/access_log 　　　　　　　　　　　　　　#查看服务端日志，观察请求日志信息，观察服务端是否有上面记录中的User-Agent参数记录。

**2>."-v/--verbose"案例显示一次的http请求的通信过程**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# curl -A 'Chrome/78.0.3904.108 Safari/537.36' http://node107.yinzhengjie.org.cn -v　　　　　　#显示http请求的通信过程，包括request，response，以及正文。
* About to connect() to node107.yinzhengjie.org.cn port 80 (#0)
*   Trying 172.30.1.107...
* Connected to node107.yinzhengjie.org.cn (172.30.1.107) port 80 (#0)
> GET / HTTP/1.1
> User-Agent: Chrome/78.0.3904.108 Safari/537.36
> Host: node107.yinzhengjie.org.cn
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Tue, 10 Dec 2019 14:18:12 GMT
< Server: Apache/2.4.6 (CentOS) PHP/5.4.16
< Last-Modified: Tue, 10 Dec 2019 14:17:04 GMT
< ETag: "1f-5995a2a997640"
< Accept-Ranges: bytes
< Content-Length: 31
< Content-Type: text/html; charset=UTF-8
< 
<h1>尹正杰到此一游</h1>
* Connection #0 to host node107.yinzhengjie.org.cn left intact
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**3>."-e/--referer <URL>"案例**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# curl -e "www.baidu.com" http://node107.yinzhengjie.org.cn -v             #指定来源网址为"www.baidu.com"
* About to connect() to node107.yinzhengjie.org.cn port 80 (#0)
*   Trying 172.30.1.107...
* Connected to node107.yinzhengjie.org.cn (172.30.1.107) port 80 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.29.0
> Host: node107.yinzhengjie.org.cn
> Accept: */*
> Referer: www.baidu.com
> 
< HTTP/1.1 200 OK
< Date: Tue, 10 Dec 2019 14:45:15 GMT
< Server: Apache/2.4.6 (CentOS) PHP/5.4.16
< Last-Modified: Tue, 10 Dec 2019 14:17:04 GMT
< ETag: "1f-5995a2a997640"
< Accept-Ranges: bytes
< Content-Length: 31
< Content-Type: text/html; charset=UTF-8
< 
<h1>尹正杰到此一游</h1>
* Connection #0 to host node107.yinzhengjie.org.cn left intact
[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) [root@node107.yizhengjie.org.cn ~]# tail -10f /var/log/httpd/access_log 　　　　　　　　　　　　　　#查看服务端日志，观察请求日志信息，观察服务端是否有上面记录中的User-Agent参数记录。

**4>."-I/--head"案例** 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# curl -I http://node107.yinzhengjie.org.cn 　　　　　　　　　　#只显示响应报文首部信息
HTTP/1.1 200 OK
Date: Tue, 10 Dec 2019 14:52:36 GMT
Server: Apache/2.4.6 (CentOS) PHP/5.4.16
Last-Modified: Tue, 10 Dec 2019 14:17:04 GMT
ETag: "1f-5995a2a997640"
Accept-Ranges: bytes
Content-Length: 31
Content-Type: text/html; charset=UTF-8

[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# curl --head http://node107.yinzhengjie.org.cn 
HTTP/1.1 200 OK
Date: Tue, 10 Dec 2019 14:52:45 GMT
Server: Apache/2.4.6 (CentOS) PHP/5.4.16
Last-Modified: Tue, 10 Dec 2019 14:17:04 GMT
ETag: "1f-5995a2a997640"
Accept-Ranges: bytes
Content-Length: 31
Content-Type: text/html; charset=UTF-8

[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) [root@node107.yizhengjie.org.cn ~]# tail -10f /var/log/httpd/access_log 　　　　　　　　　　　　　　#查看服务端日志，观察请求日志信息，观察服务端是否有上面记录中的User-Agent参数记录。

**5>."-i"案例** 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# curl -i http://node107.yinzhengjie.org.cn         　　　　　　#显示页面内容，包括报文首部信息
HTTP/1.1 200 OK
Date: Tue, 10 Dec 2019 14:54:52 GMT
Server: Apache/2.4.6 (CentOS) PHP/5.4.16
Last-Modified: Tue, 10 Dec 2019 14:17:04 GMT
ETag: "1f-5995a2a997640"
Accept-Ranges: bytes
Content-Length: 31
Content-Type: text/html; charset=UTF-8

<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) [root@node107.yizhengjie.org.cn ~]# tail -10f /var/log/httpd/access_log 　　　　　　　　　　　　　　#查看服务端日志，观察请求日志信息，观察服务端是否有上面记录中的User-Agent参数记录。

**6>."--cacert <file>"案例**

```
[root@node101.yinzhengjie.org.cn ~]# curl https://www.yinzhengjie.org.cn --cacert /etc/httpd/conf.d/ssl/cacert.pem 　　　　　　　 #使用证书检查访问网页
<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]# 
```

**7>."-k/--insecure"案例** 

```
[root@node101.yinzhengjie.org.cn ~]# curl -k https://www.yinzhengjie.org.cn --cacert /etc/httpd/conf.d/ssl/cacert.pem 　　　　　　#忽略证书检查访问网页
<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]# 
```

**8>."-c/--cookie-jar <file name>"案例**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# curl -c /root/cookie.txt http://node107.yinzhengjie.org.cn/setcookie.php         #　将url中cookie存放在指定文件中
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# cat /root/cookie.txt 
# Netscape HTTP Cookie File
# http://curl.haxx.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

node107.yinzhengjie.org.cn    FALSE    /    FALSE    0    department    IT
node107.yinzhengjie.org.cn    FALSE    /    FALSE    1575993782    user    Jason
[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**9>."-X/--request <command>"案例**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# curl -X PUT www.baidu.com　　　　　　　　　　#向服务端发送指定请求的方法，此处我们指定的方法是PUT，下面依次提交的方法是GET,DELETE以及POST方法。
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# curl -X GET www.baidu.com
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# curl -X DELETE www.baidu.com
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# curl -X POST www.baidu.com
[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**10>."-D/--dump-header <file>"案例**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@node101.yinzhengjie.org.cn ~]# ll
total 0
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# curl -D yinzhengjie.html http://node107.yinzhengjie.org.cn               #显示整个网页数据，并将响应头信息存入yinzhengjie.html
<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# ll
total 4
-rw-r--r-- 1 root root 252 Dec 10 23:35 yinzhengjie.html
[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# cat yinzhengjie.html 
HTTP/1.1 200 OK
Date: Tue, 10 Dec 2019 15:35:18 GMT
Server: Apache/2.4.6 (CentOS) PHP/5.4.16
Last-Modified: Tue, 10 Dec 2019 14:17:04 GMT
ETag: "1f-5995a2a997640"
Accept-Ranges: bytes
Content-Length: 31
Content-Type: text/html; charset=UTF-8

[root@node101.yinzhengjie.org.cn ~]# 
[root@node101.yinzhengjie.org.cn ~]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**11>."-u/--user <user[:password]>"案例**

```
　　如下图所示,我用自己的用户名登陆我们公司的OA账号信息。
```

![img](https://images2015.cnblogs.com/blog/795254/201612/795254-20161220205658089-4869544.png)

**12>.查看帮助**

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) [root@node101.yinzhengjie.org.cn ~]# curl --help

 

**四.elinks工具**

**1>.安装elinks工具**

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) [root@node101.yinzhengjie.org.cn ~]# yum -y install elinks

**2>.使用elinks访问网页**

```
[root@node101.yinzhengjie.org.cn ~]# elinks http://node107.yinzhengjie.org.cn　　　　　　　　　　#执行该命令后会弹出一个字符界面的对话框。
```

![img](https://img2018.cnblogs.com/blog/795254/201912/795254-20191210231844840-578102841.png)

**3>.使用"-source"选项**

```
[root@node101.yinzhengjie.org.cn ~]# elinks -source http://node107.yinzhengjie.org.cn　　　　　　　　#可以打印网页源码
<h1>尹正杰到此一游</h1>
[root@node101.yinzhengjie.org.cn ~]# 
```

**4>.使用"-dump:"选项案例** 

```
[root@node101.yinzhengjie.org.cn ~]# elinks -dump http://node107.yinzhengjie.org.cn　　　　　　　　　　#非交互式模式，将URL的内容输出至标准输出
                                 尹正杰到此一游
[root@node101.yinzhengjie.org.cn ~]# 
```

 