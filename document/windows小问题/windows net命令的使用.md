2

[![返回主页](https://www.cnblogs.com/skins/custom/images/logo.gif)](https://www.cnblogs.com/iriczhao/)

# [原来，都很美好](https://www.cnblogs.com/iriczhao/)

## 当害怕失去一样东西时，这意味着你必须要努力.....

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/iriczhao/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/Iriczhao)
- [订阅](javascript:void(0))
- [管理](https://i.cnblogs.com/)

# [Windows net命令使用方法](https://www.cnblogs.com/iriczhao/p/10469143.html)

net命令大全,net命令用法,net网络命令,net命令使用,net命令集,net命令介绍,net常用命令,net命令的使用技巧，net命令如何使用

　大家在操作Windows 9X/NT/2000/XP/2003系统的过程中，都会或多或少会遇到这样或那样的问题；特别是网管员在维护单位的局域网或广域网时候，如果能掌握一些Windows 系统的网络命令使用技巧，常常会给工作带来极大的方便，有时能起到事倍功半的效果；本文就Net 网络命令在实际操作中使用技巧，供大家参考。



| 本 文 主 要 内 容 | NET View     | NET User   | NET Use        | NET Time       | Net Start |
| ----------------- | ------------ | ---------- | -------------- | -------------- | --------- |
| Net Pause         | Net Continue | NET Stop   | Net Statistics | Net Share      |           |
| Net Session       | Net Send     | Net Print  | Net Name       | Net Localgroup |           |
| Net Group         | Net File     | Net Config | Net Computer   | Net Accounts   |           |


　我们知道NET命令是一个命令行命令，Net 命令有很多函数用于实用和核查计算机之间的NetBIOS连接，可以查看我们的管理网络环境、服务、用户、登陆等信息内容；要想获得Net 的HELP可以(1)在Windows下可以用图形的方式，开始->帮助->索引->输入NET；(2)在COMMAND下可以用字符方式：NET /?或NET或NET HELP取得相应的方法的帮助。所有Net命令接受选项/yes和/no(可缩写为/y和/n)。

下面对NET命令的不同参数的使用技巧介绍如下：

**1、Net View**
　　作用：显示域列表、计算机列表或指定计算机的共享资源列表。


　　命令格式：Net view [\\computername | /domain[:domainname]]
　　有关参数说明：
　　 （1）键入不带参数的Net view显示当前域的计算机列表
　　 （2）\\computername 指定要查看其共享资源的计算机
　　 （3）/domain[:domainname]指定要查看其可用计算机的域
　　例如：Net view \\GHQ查看GHQ计算机的共享资源列表。
　　　　　Net view /domain:XYZ 查看XYZ域中的机器列表。

　　2、Net User
　　作用：添加或更改用户帐号或显示用户帐号信息。


　　命令格式：Net user [username [password | *] [options]] [/domain]
　　有关参数说明：
　　（1）键入不带参数的Net user查看计算机上的用户帐号列表
　　（2）username添加、删除、更改或查看用户帐号名
　　（3）0password为用户帐号分配或更改密码
　　（4）提示输入密码
　　（5）/domain在计算机主域的主域控制器中执行操作。该参数仅在 Windows NT Server 域成员的 Windows NT Workstation 计算机上可用。默认情况下，Windows NT Server 计算机在主域控制器中执行操作。注意：在计算机主域的主域控制器发生该动作。它可能不是登录域。
　　例如：Net user ghq123查看用户GHQ123的信息。

　　3、Net Use
　　作用：连接计算机或断开计算机与共享资源的连接，或显示计算机的连接信息。


　　命令格式：Net use [devicename | *] [\\computername\sharename[\volume]] [password|*]][/user:[domainname\]username][[/delete]| [/persistent:{yes | no}]]
　　有关参数说明：
　　·键入不带参数的Net use列出网络连接
　　·devicename指定要连接到的资源名称或要断开的设备名称
　　·\\computername\sharename服务器及共享资源的名称
　　·password访问共享资源的密码
　　·*提示键入密码
　　·/user指定进行连接的另外一个用户
　　·domainname指定另一个域
　　·username指定登录的用户名
　　·/home将用户连接到其宿主目录
　　·/delete取消指定网络连接
　　·/persistent控制永久网络连接的使用。
　　例如：Net use f: \\GHQ\TEMP 将\\GHQ\TEMP目录建立为F盘
　　　　　Net use f: \GHQ\TEMP /delete 断开连接。

　　4、Net Time
　　作用：使计算机的时钟与另一台计算机或域的时间同步。


　　命令格式：Net time [\\computername | /domain[:name]] [/set]
　　有关参数说明：
　　·\\computername要检查或同步的服务器名
　　·/domain[:name]指定要与其时间同步的域
　　·/set使本计算机时钟与指定计算机或域的时钟同步。

　　5、Net Start
　　作用：启动服务，或显示已启动服务的列表。


　　命令格式：Net start service

　　6、Net Pause
　　作 用：暂停正在运行的服务。
　　命令格式：Net pause service

　　7、Net Continue
　　作 用：重新激活挂起的服务。
　　命令格式：Net continue service 　　

　　8、Net Stop
　　作 用：停止 Windows NT/2000/2003 网络服务。
　　命令格式：Net stop service
　　下面我们来看看上面四条命令里服务包含哪些服务：

　　(1)alerter(警报)；
　　(2)client service for Netware(Netware 客户端服务)
　　(3)clipbook server(剪贴簿服务器)
　　(4)computer browser(计算机浏览器)
　　(5)directory replicator(目录复制器)
　　(6)ftp publishing service (ftp )(ftp 发行服务)
　　(7)lpdsvc
　　(8)Net logon(网络登录)
　　(9)Network dde(网络 dde)
　　(10)Network dde dsdm(网络 dde dsdm)
　　(11)Network monitor agent(网络监控代理)
　　(12)ole(对象链接与嵌入)
　　(13)remote access connection manager(远程访问连接管理器)
　　(14)remote access isnsap service(远程访问 isnsap 服务)
　　(15)remote access server(远程访问服务器)
　　(16)remote procedure call (rpc) locator(远程过程调用定位器)
　　(17)remote procedure call (rpc) service(远程过程调用服务)
　　(18)schedule(调度)
　　(19)server(服务器)
　　(20)simple tcp/ip services(简单 TCP/IP 服务)
　　(21)snmp
　　(22)spooler(后台打印程序)
　　(23)tcp/ip Netbios helper(TCP/IP NETBIOS 辅助工具)
　　(24)ups
　　(25)workstation(工作站)
　　(26)messenger(信使)
　　(27)dhcp client

　　9、Net Statistics
　　作用：显示本地工作站或服务器服务的统计记录。
　　命令格式：Net statistics [workstation | server]
　　有关参数说明：
　　·键入不带参数的Net statistics列出其统计信息可用的运行服务
　　·workstation显示本地工作站服务的统计信息
　　·server显示本地服务器服务的统计信息
　　例如：Net statistics server | more显示服务器服务的统计信息。

　　10、Net Share
　　作用：创建、删除或显示共享资源。
　　命令格式：Net share sharename=drive:path [/users:number | /unlimited] [/remark:"text"]
　　有关参数说明：
　　· 键入不带参数的Net share显示本地计算机上所有共享资源的信息
　　· sharename是共享资源的网络名称
　　· drive:path指定共享目录的绝对路径
　　· /users:number设置可同时访问共享资源的最大用户数
　　· /unlimited不限制同时访问共享资源的用户数
　　· /remark:"text "添加关于资源的注释，注释文字用引号引住
　　例如： Net share yesky=c:\temp /remark:"my first share"
　　以yesky为共享名共享C:\temp
　　Net share yesky /delete停止共享yesky目录

　　11、Net Session
　　作用：列出或断开本地计算机和与之连接的客户端的会话。
　　命令格式：Net session [\\computername] [/delete]
　　有关参数说明：
　　·键入不带参数的Net session显示所有与本地计算机的会话的信息。
　　·\\computername标识要列出或断开会话的计算机。
　　·/delete结束与 \computername 计算机会话并关闭本次会话期间计算机的所有打开文件。如果省略\computername 参数，将取消与本地计算机的所有会话。
　　例如：Net session [url=file://\\GHQ]\\GHQ[/url]要显示计算机名为GHQ的客户端会话信息列表。

　12、Net Send
　　作用：向网络的其他用户、计算机或通信名发送消息。
　　命令格式：Net send {name | * | /domain[:name] | /users} message
　　有关参数说明：
　　·name要接收发送消息的用户名、计算机名或通信名
　　·* 将消息发送到组中所有名称
　　·/domain[:name]将消息发送到计算机域中的所有名称
　　·/users将消息发送到与服务器连接的所有用户
　　·message作为消息发送的文本
　　例如：Net send /users server will shutdown in 10 minutes.给所有连接到服务器的用户发送消息。

　　13、Net Print
　　作用：显示或控制打印作业及打印队列。
　　命令格式：Net print [\\computername ] job# [/hold | /release | /delete]
　　有关参数说明：
　　·computername共享打印机队列的计算机名
　　·sharename打印队列名称
　　·job#在打印机队列中分配给打印作业的标识号
　　·/hold使用 job# 时，在打印机队列中使打印作业等待
　　·/release释放保留的打印作业
　　·/delete从打印机队列中删除打印作业
　　例如：Net print \\GHQ\HP8000列出[url=file://\\GHQ]\\GHQ[/url]计算机上HP8000打印机队列的目录。

　　14、Net Name
　　作用：添加或删除消息名（有时也称别名），或显示计算机接收消息的名称列表。
　　命令格式：Net name [name [/add | /delete]]
　　有关参数说明：
　　·键入不带参数的Net name列出当前使用的名称
　　·name指定接收消息的名称
　　·/add将名称添加到计算机中
　　·/delete从计算机中删除名称

　　15、Net Localgroup
　　作 用：添加、显示或更改本地组。
　　命令格式：Net localgroup groupname {/add [/comment:"text "] | /delete} [/domain]
　　有关参数说明：

　　·键入不带参数的Net localgroup显示服务器名称和计算机的本地组名称
　　·groupname要添加、扩充或删除的本地组名称
　　·/comment: "text "为新建或现有组添加注释
　　·/domain在当前域的主域控制器中执行操作，否则仅在本地计算机上执行操作
　　·name [ ...]列出要添加到本地组或从本地组中删除的一个或多个用户名或组名
　　·/add将全局组名或用户名添加到本地组中
　　·/delete从本地组中删除组名或用户名
　　例如：Net localgroup ggg /add 将名为ggg的本地组添加到本地用户帐号数据库；
　　Net localgroup ggg 显示ggg本地组中的用户。

　　16、Net Group
　　作 用：在 Windows NT/2000/2003 Server 域中添加、显示或更改全局组。
　　命令格式：Net group groupname {/add [/comment:"text "] | /delete} [/domain]
　　有关参数说明：
　　·键入不带参数的Net group显示服务器名称及服务器的组名称
　　·groupname要添加、扩展或删除的组
　　·/comment:"text "为新建组或现有组添加注释
　　·/domain在当前域的主域控制器中执行该操作，否则在本地计算机上执行操作
　　·username[ ...]列表显示要添加到组或从组中删除的一个或多个用户
　　·/add添加组或在组中添加用户名
　　·/delete删除组或从组中删除用户名
　　例如：Net group ggg GHQ1 GHQ2 /add将现有用户帐号GHQ1和GHQ2添加到本地计算机的ggg组。

　　17、Net File
　　作用：显示某服务器上所有打开的共享文件名及锁定文件数。
　　命令格式：Net file [id [/close]]
　　有关参数说明：
　　·键入不带参数的Net file获得服务器上打开文件的列表
　　·id文件标识号
　　·/close关闭打开的文件并释放锁定记录

　　18、Net Config
　　作用：显示当前运行的可配置服务，或显示并更改某项服务的设置。
　　命令格式：Net config [service [options]]
　　有关参数说明：
　　·键入不带参数的Net config显示可配置服务的列表
　　·service通过Net config命令进行配置的服务(server或workstation)
　　·options服务的特定选项

　　19、Net Computer
　　作用：从域数据库中添加或删除计算机。
　　命令格式：Net computer \\computername {/add | /del}
　　有关参数说明：
　　·\\computername指定要添加到域或从域中删除的计算机
　　·/add将指定计算机添加到域
　　·/del将指定计算机从域中删除
　　例如：Net computer \\js /add将计算机js 添加到登录域。

　　20、Net Accounts
　　作用：更新用户帐号数据库、更改密码及所有帐号的登录要求。
　　命令格式：Net accounts [/forcelogoff:{minutes | no}] [/minpwlen:length] [/maxpwage:{days | unlimited}] [/minpwage:days] [/uniquepw:number] [/domain]
　　有关参数说明：
　　·键入不带参数的Net accounts显示当前密码设置、登录时限及域信息
　　·/forcelogoff:{minutes | no}设置当用户帐号或有效登录时间过期时
　　·/minpwlen:length设置用户帐号密码的最少字符数
　　·/maxpwage:{days | unlimited}设置用户帐号密码有效的最大天数
　　·/minpwage:days设置用户必须保持原密码的最小天数
　　·/uniquepw:number要求用户更改密码时，必须在经过number次后才能重复使用与之相同的密码
　　·/domain在当前域的主域控制器上执行该操作
　　·/sync当用于主域控制器时，该命令使域中所有备份域控制器同步
　　例如：Net accounts /minpwlen:8 将用户帐号密码的最少字符数设置为8。
　　当然Net命令具体在Win98/NT/2000/XP/2003环境中使用，可能会存在一些差异，请大家参考有关的资料说明，在此就不多说了。
　　下面是一个将Net、ping 和ipconfig 命令组合起来使用，测试局域网的连通性，判定远程计算机Microsoft 网络服务的文件和打印机有无共享的实际例子。仅供同志们在学习操作Net网络命令做参考，具体步骤如下：
　　1）首先我们要使用 Ping 命令测试 TCP/IP 的连接性，然后用 ipconfig 命令的显示，以确保网卡不处于“媒体已断开”状态。
　　2）打开DOS命令提示符，然后使用IP地址对所需主机进行 Ping 命令测试。
　　如果 Ping 命令失败，出现“Request timed out”消息，请验证主机 IP 地址是否正确，主机是否运行，以及该计算机和主机之间的所有网关（路由器）是否运行。
　　3）要使用 Ping 命令测试主机名称解析功能，请使用主机名称 ping 所需的主机。
如果 Ping 命令失败，出现“Unable to resolve target system name”消息，请验证主机名称是否正确，以及主机名称是否能被 DNS 服务器解析。
　　4）要使用Net view 命令测试 TCP/IP 连接，请打开命令提示符，然后键入 Net view\\计算机名称。Net view 命令将通过建立临时连接，列出使用 Windows XP/NT/2000/2003 的计算机上的文件和打印共享。如果在指定的计算机上没有文件或打印共享， Net view 命令将显示“There are no entries in the list”消息。
如果 Net view 命令失败，出现“System error 53 has occurred”消息，请验证计算机名称是否正确，使用 Windows XP/NT/2000/2003 的计算机是否运行，以及该计算机和使用 Windows XP/NT/2000/2003 的计算机之间的所有网关（路由器）是否运行。
　　如果Net view 命令失败，出现“System error 5 has occurred.Access is denied.”消息，请验证您登录所用的帐户是否具有查看远程计算机上共享的权限。
　　要进一步解决连通性问题，请执行以下操作：
　　a)使用 Ping 命令 ping 计算机名称。
　　如果 Ping 命令失败，出现“Unable to resolve target system name”消息，则计算机名称无法解析为 IP 地址。
　　b)使用Net view 命令和运行 Windows XP/NT/2000/2003 的计算机的 IP 地址，如下所示：
　　Net view \\IP 地址；如果Net view 命令成功，那么计算机名称解析成错误的 IP 地址。
　　如果Net view 命令失败，出现“System error 53 has occurred”消息，则说明远程计算机可能没有运行 Microsoft 网络服务的文件和打印机共享。

 

远程桌面连接： 开始——运行——mstsc

分类: [其他](https://www.cnblogs.com/iriczhao/category/1410744.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1441101/20190222184835.png)](https://home.cnblogs.com/u/iriczhao/)

[Iriczhao](https://home.cnblogs.com/u/iriczhao/)
[关注 - 8](https://home.cnblogs.com/u/iriczhao/followees/)
[粉丝 - 6](https://home.cnblogs.com/u/iriczhao/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/iriczhao/p/10466399.html)上一篇： [MySQL数据库操作技术大全](https://www.cnblogs.com/iriczhao/p/10466399.html)
[» ](https://www.cnblogs.com/iriczhao/p/10469707.html)下一篇： [MySQL网络配置](https://www.cnblogs.com/iriczhao/p/10469707.html)

posted @ 2019-03-04 10:14 [Iriczhao](https://www.cnblogs.com/iriczhao/) 阅读(5346) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=10469143) [收藏](javascript:void(0))





[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/iriczhao/p/10469143.html#)[返回顶部](https://www.cnblogs.com/iriczhao/p/10469143.html#top)

注册用户登录后才能发表评论，请 [登录](javascript:void(0);) 或 [注册](javascript:void(0);)， [访问](https://www.cnblogs.com/) 网站首页。

### 公告

昵称： [Iriczhao](https://home.cnblogs.com/u/iriczhao/)
园龄： [2年1个月](https://home.cnblogs.com/u/iriczhao/)
粉丝： [6](https://home.cnblogs.com/u/iriczhao/followers/)
关注： [8](https://home.cnblogs.com/u/iriczhao/followees/)

[+加关注](javascript:void(0))

| [<](javascript:void(0);)2020年9月[>](javascript:void(0);) |      |      |      |      |      |      |
| --------------------------------------------------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 日                                                        | 一   | 二   | 三   | 四   | 五   | 六   |
| 30                                                        | 31   | 1    | 2    | 3    | 4    | 5    |
| 6                                                         | 7    | 8    | 9    | 10   | 11   | 12   |
| 13                                                        | 14   | 15   | 16   | 17   | 18   | 19   |
| 20                                                        | 21   | 22   | 23   | 24   | 25   | 26   |
| 27                                                        | 28   | 29   | 30   | 1    | 2    | 3    |
| 4                                                         | 5    | 6    | 7    | 8    | 9    | 10   |

### 搜索

 

 

### 常用链接

- [我的随笔](https://www.cnblogs.com/iriczhao/p/)
- [我的评论](https://www.cnblogs.com/iriczhao/MyComments.html)
- [我的参与](https://www.cnblogs.com/iriczhao/OtherPosts.html)
- [最新评论](https://www.cnblogs.com/iriczhao/RecentComments.html)
- [我的标签](https://www.cnblogs.com/iriczhao/tag/)

### 随笔分类

- [C(4)](https://www.cnblogs.com/iriczhao/category/1407276.html)
- [Qt(9)](https://www.cnblogs.com/iriczhao/category/1560708.html)
- [电路基础(2)](https://www.cnblogs.com/iriczhao/category/1507623.html)
- [其他(3)](https://www.cnblogs.com/iriczhao/category/1410744.html)
- [嵌入式硬件(16)](https://www.cnblogs.com/iriczhao/category/1406698.html)
- [软件设计(7)](https://www.cnblogs.com/iriczhao/category/1406701.html)

### 随笔档案

- [2020年8月(2)](https://www.cnblogs.com/iriczhao/archive/2020/08.html)
- [2020年1月(1)](https://www.cnblogs.com/iriczhao/archive/2020/01.html)
- [2019年12月(3)](https://www.cnblogs.com/iriczhao/archive/2019/12.html)
- [2019年11月(3)](https://www.cnblogs.com/iriczhao/archive/2019/11.html)
- [2019年10月(3)](https://www.cnblogs.com/iriczhao/archive/2019/10.html)
- [2019年9月(5)](https://www.cnblogs.com/iriczhao/archive/2019/09.html)
- [2019年8月(10)](https://www.cnblogs.com/iriczhao/archive/2019/08.html)
- [2019年7月(5)](https://www.cnblogs.com/iriczhao/archive/2019/07.html)
- [2019年6月(5)](https://www.cnblogs.com/iriczhao/archive/2019/06.html)
- [2019年5月(2)](https://www.cnblogs.com/iriczhao/archive/2019/05.html)
- [2019年4月(2)](https://www.cnblogs.com/iriczhao/archive/2019/04.html)
- [2019年3月(9)](https://www.cnblogs.com/iriczhao/archive/2019/03.html)
- [2019年2月(2)](https://www.cnblogs.com/iriczhao/archive/2019/02.html)

### 最新评论

- [1. Re:解决Qt与MySQL连接过程中出现“QSqlDatabase: QMYSQL driver not loaded”问题](https://www.cnblogs.com/iriczhao/p/11710693.html)
- 写的太好了!!!!
- --我是张洪铭我是熊博士

### 阅读排行榜

- [1. Nand Flash 和Nor Flash的区别详解(5915)](https://www.cnblogs.com/iriczhao/p/12128451.html)
- [2. Windows net命令使用方法(5346)](https://www.cnblogs.com/iriczhao/p/10469143.html)
- [3. 差分放大电路知识总结(3579)](https://www.cnblogs.com/iriczhao/p/11387242.html)
- [4. Qt-解决Qt与MySQL连接过程中出现“QSqlDatabase: QMYSQL driver not loaded”问题(3374)](https://www.cnblogs.com/iriczhao/p/11710693.html)
- [5. GPIO 8种工作模式小结(3228)](https://www.cnblogs.com/iriczhao/p/10918833.html)

### 评论排行榜

- [1. Qt-解决Qt与MySQL连接过程中出现“QSqlDatabase: QMYSQL driver not loaded”问题(1)](https://www.cnblogs.com/iriczhao/p/11710693.html)

### 推荐排行榜

- [1. 差分放大电路知识总结(1)](https://www.cnblogs.com/iriczhao/p/11387242.html)
- [2. C语言-C语言和硬件的邂逅(1)](https://www.cnblogs.com/iriczhao/p/11589189.html)
- [3. 嵌入式之驱动开发简述(1)](https://www.cnblogs.com/iriczhao/p/10479648.html)
- [4. 使用Navicat连接MySQL时出现2059报错的解决方法(1)](https://www.cnblogs.com/iriczhao/p/11707269.html)
- [5. Qt-解决Qt与MySQL连接过程中出现“QSqlDatabase: QMYSQL driver not loaded”问题(1)](https://www.cnblogs.com/iriczhao/p/11710693.html)

Copyright © 2020 Iriczhao
Powered by .NET Core on Kubernetes

你都复制了些什么呀，转载要记得加上出处哦

<iframe id="blockbyte-bs-sidebar" class="notranslate" aria-hidden="true" __idm_frm__="226" data-pos="right" style="margin: 0px; padding: 0px; opacity: 0; pointer-events: none; position: fixed; top: 0px; left: auto; width: 350px; max-width: none; height: 0px; z-index: 2147483646; speak: none; border: none; transform: translate3d(350px, 0px, 0px); transition: width 0s ease 0.3s, height 0s ease 0.3s, opacity 0.3s ease 0s, transform 0.3s ease 0s; background-color: rgba(255, 255, 255, 0.8) !important; display: block !important; right: 0px; color: rgb(85, 85, 85); font-family: &quot;PingFang SC&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, &quot;Microsoft Yahei&quot;, sans-serif; font-size: 12px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

