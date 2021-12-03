# PAC自动代理文件格式，教你如何写PAC文件

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[weixin_30502965](https://blog.csdn.net/weixin_30502965) 2014-12-14 02:36:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 405 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

文章标签： [javascript](https://www.csdn.net/tags/OtDaQg2sNzExLWJsb2cO0O0O.html) [操作系统](https://www.csdn.net/tags/MtTacg0sNTgzNi1ibG9n.html)

版权

[![img](https://img-operation.csdnimg.cn/csdn/silkroad/img/1630299969017.png)微众银行第三届金融科技高校技术大赛正式拉开帷幕，邀你共上人生巅峰！人工智能、区块链两大热门赛道，专业大咖两次线上分享互动，立即组队，和小伙伴一起赢大奖、进大厂。](https://fintech.webank.com/fintechathon/campus2021/?utm_source=AD)

**PAC文件格式**

PAC文件是纯文本格式的，实际上就是JavaScript文件。Chrome/Chromium的扩展Switchy!的"Auto Switch Mode"功能实际上也是创建和维护一个简单的PAC文件，但功能比较弱。

对于一般的应用，即使你几乎不懂JavaScript和编程，也可以通过本文的介绍实现基本的功能。

**PAC文件FindProxyForURL函数** 

PAC文件中必须包含一个函数：FindProxyForURL(url, host)。

参数url是用户输入的url，参数host是url中的主机名。

比如url为http://www.truevue.org/javascript/pac-proxy-setting，那么host就是www.truevue.org

一个最简单的PAC文件内容如下：

 

```javascript
function FindProxyForURL(url, host) {



 return "DIRECT"; 



} 
```

 

这个PAC文件实际上什么也没做，对任何URL，都将"DIRECT"（直接连网）。

**PAC文件返回值类型**

**除了可以return "DIRECT"以外，还有两种常用方式：**

PROXY proxysample.com:8080

http代理的主机和端口，主机也可以用IP表示

SOCKS5 socks5sample.com:1080

socks5代理的主机和端口，主机也可以用IP表示

那么，我们可以猜测到，用pac指定一个http代理应该这样写

 

```javascript
function FindProxyForURL(url, host) {



  return "PROXY 192.168.1.1:3128"; 



}
```

 

甚至可以指定多个代理 ` `

 

```javascript
function FindProxyForURL(url, host) {



  return "DIRECT; PROXY 192.168.1.1:3128; SOCKS5 lilinux.net:1080"; 



} 
```

 

这句语句的意思是： 

1. 对所有URL，都直接连接； 
2. 如果不能直接连接，那么就使用192.168.1.1:3128这个http代理连接；
3. 如果还是不能连接，则使用lilinux.net:1080这个socks5代理连接。

使用不同连接的顺序和语句中的顺序一致，你可以根据自己的实际情况更改。

也许你明确知道哪些网站不能直连，必须用PROXY或者SOCKS5连接，那么可以对站点分别指定代理配置 

 

```javascript
function FindProxyForURL(url, host) {



   if (shExpMatch(url,"*.google.com/*")) {



     return "PROXY 192.168.1.1:3128";



   }



   if (shExpMatch(url, "*.wikipedia.com:*/*")) {



     return "SOCKS5 lilinux.net:1080";



   }



   if (isInNet(host, "10.0.0.0",  "255.0.0.0")){



     return "DIRECT";



   }



   return "DIRECT; PROXY 192.168.1.1:3128; SOCKS5 lilinux.net:1080"; 



}
```

 

这个PAC文件中引入了两个新的函数，但从字面意思上，我们也可以猜出代码的大概意思：

1. 当url是*.google.com/* 时，自动使用PROXY代理；
2. 当url是*.wikipedia.cm/*时，自动使用SOCKS5代理；
3. 当host是10.0.0.0 /255.0.0.0的子网内时，自动直连；
4. 如果都不匹配，则依次按DIRECT、PROXY、SOCKS5的次序尝试。 

shExpMatch函数用来匹配url或者host，匹配的方式和DOS的通配符相似。例如前面用到的"*.google.com/*"可以匹配任意包含".google.com/"的字符串。 

Chrome/Chromium 的扩展Switchy!创建的pac文件还自定义了一个函数，可以用来匹配正则表达式，不过个人认为在url匹配上通常不需要使用强大的正则表达式。 

isInNet函数用来返回请求的host是否在指定的域内。值得注意的是，isInNet的第二个参数必须是 IP，不能是主机名。因此需要把主机名转换成IP。比如"isInNet(host, dnsResolve([www.google.com](http://www.google.com/)), "255.255.255.0")"讲到这里，应该可以解决你的问题了吧。

**PAC文件可以使用的JavaScript函数**

当然PAC也不止这么简单，它还提供了不少其它函数，在本文就不详细讲述了。http://www.truevue.org/javascript/pac-functions 中列出了PAC代理文件中可以使用的JavaScript函数。

你也许想把pac文件发布到Internet上，这样其它用户就只需要在浏览器中指定pac文件的url即可。你得配置你的服务器映射 .pac 文件后缀到MIME类型： application/x-ns-proxy-autoconfig 如果使用的是Netscape服务器，编辑 config 目录下的 mime.types 文 件。如果是Apache, CERN or NCSA服务器，使用 AddType 指令。

转载于:https://www.cnblogs.com/kzd666/p/4162166.html

相关资源：[*代理*脚本(proxy.*pac*)_*代理*脚本,*代理*脚本怎么*写*-Proxy文档类资源...](https://download.csdn.net/download/hgyxb/2857180?spm=1001.2101.3001.5697)





 前些天，同事给我抱怨，公司的GPO强制更改了笔记本的IE代理服务器，在办公室还好，一回家就上不了网了，必须手动更改代理设置，真是麻烦。我想了想，proxy.pac自动代理文件应该可以解决这个问题，于是想到就做。

Proxy.pac文件的本质是javascript的一个函数，通过设定各种条件（域名，IP等等），从而让浏览器加载的时候自动去寻找对应的代理服务器。比如说

function FindProxyForURL(url, host) {

​        if(isInNet(myIpAddress(), "10.71.80.0", "255.255.255.0")){

​                return"PROXY 112.186.227.85:8080";
​        }


        return"DIRECT";
}

当浏览器加载这个proxy.pac文件之后，就会自动比较自己的IP地址，如果属于10.71.80.0/24 这个范围，那么他就使用代理服务器112.186.227.85:8080，否则直接连接网络。

以IE为例，可以在Option->Connection->LAN setting 中进行设置。注意IE的格式是[url=file:///C:/proxy.pac]file://c:/proxy.pac[/url], 而在某些浏览器里面需要改成[url=file:///C:/proxy.pac]file:///c:/proxy.pac[/url]





Proxy.pac文件写好以后，就需要配置在一个共享的服务器上以供下载。我把他放在文件服务器fileserver的一个共享文件夹中，我的思路是域用户登录客户机时，自动下载proxy.pac到本地文件夹中，同时通过配置GPO中的IE选项让IE绑定该文件。
我找了一个现成的vb脚本下载，稍加改动路径以便满足自己的需要。同时因为我要把文件拷贝到C:\WINDOWS\system32\drivers\etc\，默认普通用户是没有权限访问的，我还必须更改这个文件夹的权限。


Copy.vbs

Option Explicit
Dim WshShell
Dim fso
Dim USERPROFILE
Dim srcPath
Dim tgtPath
Dim computername

On Error Resume Next
Set WshShell =WScript.CreateObject("Wscript.Shell")
Set fso =WScript.CreateObject("Scripting.FilesystemObject")
USERPROFILE =WshShell.ExpandEnvironmentStrings("%USERPROFILE%")

'Set wshShell = WScript.CreateObject("WScript.Shell" )
'computername= wshShell.ExpandEnvironmentStrings("%COMPUTERNAME%" )
'WScript.Echo "Computer Name: " & computername

srcPath = "\\fileserver\it\proxy\proxy.pac"
tgtPath = "C:\WINDOWS\system32\drivers\etc\proxy.pac"

If Not fso.FileExists(tgtPath) Then

fso.CopyFile srcPath, tgtPath, True
'wscript.echo "Copy to "+tgtPath

ElseIf fso.FileExists(srcPath) Then
ReplaceIfNewer srcPath, tgtPath

End If

Sub ReplaceIfNewer(strSourceFile, strTargetFile)
Const OVERWRITE_EXISTING = True
Dim objFso
Dim objTargetFile
Dim dtmTargetDate
Dim objSourceFile
Dim dtmSourceDate
Set objFso =WScript.CreateObject("Scripting.FileSystemObject")
Set objTargetFile = objFso.GetFile(strTargetFile)
dtmTargetDate = objTargetFile.DateLastModified
Set objSourceFile = objFso.GetFile(strSourceFile)
dtmSourceDate = objSourceFile.DateLastModified


If (dtmTargetDate < dtmSourceDate) Then
objFso.CopyFile objSourceFile.Path,objTargetFile.Path,OVERWRITE_EXISTING


End If
Set objFso = Nothing
End Sub

最后是GPO配置结果
一个是针对文件夹权限的，需要在用户电脑的OU配置

一个是用户的登录脚本，比较更新时间下载最新版本的proxy.pac,同时绑定IE



经测试，在我的TMG代理服务器上能够成功检测到连接的客户session。客户机访问My IP显示的也是代理服务器的公网地址。Done！

http://m.blog.csdn.net/article/details?id=41650719

 

相关资源：[*代理*脚本(proxy.*pac*)_*代理*脚本,*代理*脚本怎么*写*-Proxy文档类资源...](https://download.csdn.net/download/hgyxb/2857180?spm=1001.2101.3001.5697)