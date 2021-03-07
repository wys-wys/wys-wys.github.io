# Windows 常用命令(Win+R)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[技术码](https://me.csdn.net/e_online) 2009-11-01 21:56:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 2032 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

文章标签： [windows](https://www.csdn.net/gather_28/OtDaQgysNTkwNy1ibG9n.html) [service](https://www.csdn.net/gather_22/MtTaEg0sNTE0NzEtYmxvZwO0O0OO0O0O.html) [query](https://www.csdn.net/gather_24/MtTaEg0sMTIyMTEtYmxvZwO0O0OO0O0O.html) [command](https://www.csdn.net/gather_26/MtTaEg0sMzkxMjItYmxvZwO0O0OO0O0O.html) [工具](https://www.csdn.net/gather_21/MtTaEg0sNDgyMzktYmxvZwO0O0OO0O0O.html) [string](https://www.csdn.net/gather_27/MtTaEg0sMDc0OTEtYmxvZwO0O0OO0O0O.html)

版权

 运行处进行的（windows键+R）

​    'cmd'   这个命令是调用类似dos的命令窗口的命令，在这里你可以像操作DOS一样操作Windows.

​    'inetmgr'  这个命令相信做过网站的都知道，对了这就是调用IIS的快捷命令。

​    'mstsc'   这个是用来启动远程桌面连接的快捷命令，相信搞过网络的人对此不会陌生。

​    'regedit'  这个命令大家都很熟悉，是用来调用注册表的。

​    'appwiz.cpl'   进入添加和删除程序的快捷命令

​    'control userpasswords2'     进入用户账户设置界面的命令

​    'cleanmgr'            磁盘垃圾清理快捷命令

   'command.com'        调用的则是系统内置的 NTVDM，一个 DOS虚拟机。它完全是一个类似 Virtual PC 的 虚拟环

境，和系统本身联系不大。当我们在命令提示符下运行 DOS 程序时，实际上也 是自动转移到 NTVDM虚拟机下，和 CMD

本身没什么关系。

   'calc'      启动计算器

   'chkdsk.exe'         磁盘检查

   'compmgmt.msc'      计算机管理

   'devmgmt.msc'        设备管理器

   diskmgmt.msc       磁盘管理实用程序

   'dfrg.msc '           磁盘碎片整理程序

   'drwtsn32'       系统医生

   'dvdplay'        Windows Media Player

   'explorer'        资源管理器

   'dxdiag'          DirectX Diagnostic Tool

   'gpedit.msc'      组策略编辑器

   'gpupdate /target:computer /force'        强制刷新组策略

   'eventvwr.exe'            事件查看器

   'logoff'          注销命令

   'lusrmgr.msc'      本地用户和组  

   'msinfo32'          系统信息

   'msconfig'          系统配置实用程序

   'net start (servicename)'    启动该服务

   'net stop (servicename)'停止该服务

   'notepad'      记事本

   'nusrmgr.cpl'    同control userpasswords，打开用户帐户控制面板

   'Nslookup'      IP地址侦测器

   'oobe/msoobe /a'       检查XP是否激活

   'perfmon'        计算机性能监视器

   'regedit'          系统注册表

   'regedt32'         注册表编辑器

   'regsvr32 /u *.dll'   停止dll文件运行

   'route print'       查看路由表

   'rononce -p'       15秒快速关机

   'rsop.msc'        组策略结果集

   'rundll32.exe rundll32.exe %Systemroot%/System32/shimgvw.dll,ImageView_Fullscreen'  启动一个空白的Windows 图

片和传真查看器

   ' secpol.msc'       本地安全策略

   'services.msc'      本地服务设置

   'sfc /scannow'     启动系统文件检查器

   'sndrec32'        录音机

   'taskmgr'         任务管理器

   'tsshutdn'        60秒倒记时关机命令

   'winchat'         winxp自带局域网聊天

   'winmsd'         系统信息

   'winver'         显示About Windows 窗口

   'wupdmgr'         update

   'firewall.cpl'       防火墙

   'magnify'         放大镜

   'sysdm.cpl'        系统属性

   'sysdm.cpl'        windows系统安全工具

   'write'           写字板

   'tourstart'        Windows XP 漫游

   'utilman'          辅助工具管理器

  'spider'           蜘蛛牌游戏

   'sysedit'          系统配置编辑器

  系统文件检查工具(立即扫描) sfc /scannow

  系统文件检查工具(下次启动时扫描) sfc /scanonce

  系统文件检查工具(每次启动时扫描) sfc /scanboot

  系统文件检查工具(返回默认设置) sfc /revert

  系统文件检查工具(清除文件缓存) sfc /purgecache

  系统文件检查工具(设置缓存大小=x) sfc /cachesize=x

  'cliconfg'        SQL Client客户端网络实用工具

  'mmsys.cpl'       声音和音频设备属性    

 'shutdown'        关闭windows

 'fsmgmt.msc'      共享文件夹

  'wscui.cpl'       Windows安全中心

  'control schedtasks'    任务计划

  'sticpl.cpl'        扫描仪与相机

  'ntmsmgr.msc'     可移动存储

  'intl.cpl'       区域的语言选择

  'eudcedit'     TrueType造字程序

  'control printers'  打印机和传真

  'powercfg.cpl'     电源选项属性

  'telephon.cpl'   电话与调制解调器选项

  'osk'      屏幕键盘

  'odbccp32.cpl'      ODBC数据源管理器

  'packager'       对象包装程序

  'ncpa.cpl' /'control netconnections'      网络连接

  'netsetup.cpl'    网络连接向导

  'main.cpl' /'control mouse'     鼠标属性

  'winmine'         扫雷游戏

  'secpol.msc'      本地安全设置

  'control keyboard'     键盘属性

  IP配置实用程序(显示连接配置) ipconfig /all
 IP配置实用程序(显示DNS缓存内容) ipconfig /displaydns
 IP配置实用程序(删除DNS缓存内容) ipconfig /flushdns
 IP配置实用程序(释放全部(或指定)适配器的由DHCP分配的动态IP地址) ipconfig /release
 IP配置实用程序(为全部适配器重新分配IP地址) ipconfig /renew
 IP配置实用程序(刷新DHCP并重新注册DNS) ipconfig /registerdns
 IP配置实用程序(显示DHCP Class ID) ipconfig /showclassid
 IP配置实用程序(修改DHCP Class ID) ipconfig /setclassid

 'inetcpl.cpl'        internet属性

  'ciadv.msc'         索引服务

 'winver'           检查windows版本号

 'mplayer2'         简易widnows media player

  'mspaint'           画图板

  'mem.exe'        显示内存使用状况

  'compmgmt.msc'        计算机管理

  'wmimgmt.msc'          打开windows管理体系结构(WMI)

  'ntbackup'             系统备份与还原

 'narrator'             屏幕“讲述人”

 'netstat -an'          (TC)命令检查接口

 'syncapp'           创建一个公文包

  'sigverif'            文件签名验证程序

  'certmgr.msc'        证书管理实用程序

  'iexpress'           木马捆绑工具，系统自带

  'access.cpl'          辅助功能选项

  'fsquirt'         Bluetooth文件传送向导

  'dcomcnfg'           组件服务

   'timedate.cpl'         日期时间属性

   'ddeshare'             DDE共享

   'control desktop'       显示属性

   'desk.cpl'            显示属性

   'control.cpl'         显示属性的外观选项卡

   'sigverif'           文件签名验证 

  快速查找 findfast.cpl

  文件夹选项 control folders

  字体文件夹 control fonts

  字体文件夹 fonts

  'freecell'     空档接龙游戏 

  'joy.cpl'       游戏控制 

--------------------------------------------------------SC（server control）命令详解------------------------------------------------------

 

作为一个命令很工具，SC.exe可以用来测试你自己的系统，你可以设置一个批处理文件来使用不同的参数调用

SC.exe来控制服务。这个很有用，如果你想看看你的服务不断的启动和停止，我没有试过哦！让一个服务一下子

打开，一下子关闭，听上去很不错的。如果你的服务进程里面有多个进程的话，你可以保持一个进程继续运行不

让它走开，然后让另一个不断的打开在关闭，还可以寻找一下内存缺乏导致不完全清楚的证据。
下面介绍SC，SC QC，and SC QUERY

SC使用这样的语法：
\1. SC [Servername] command Servicename [Optionname= Optionvalues]

\2. SC [command]

这里使用第一种语法使用SC，使用第二种语法显示帮助。

下面介绍各种参数。

Servername
可选择：可以使用双斜线，如myserver，也可以是192.168.0.1来操作远程计算机。如果在本地计算机上操作

就不用添加任何参数。

Command
下面列出SC可以使用的命令。

config----改变一个服务的配置。（长久的）

continue--对一个服务送出一个继续控制的要求。

control----对一个服务送出一个控制。

create----创建一个服务。（增加到注册表中）

delete----删除一个服务。（从注册表中删除）

EnumDepend--列举服务的从属关系。

GetDisplayName--获得一个服务的显示名称。

GetKeyName--获得一个服务的服务键名。

interrogate--对一个服务送出一个询问控制要求。

pause----对一个服务送出一个暂停控制要求。

qc----询问一个服务的配置。

query----询问一个服务的状态，也可以列举服务的状态类型。

start----启动一个服务。

stop----对一个服务送出一个停止的要求。

Servicename
在注册表中为service key制定的名称。注意这个名称是不同于显示名称的（这个名称可以用net start和服务控

制面板看到），而SC是使用服务键名来鉴别服务的。

Optionname
这个optionname和optionvalues参数允许你指定操作命令参数的名称和数值。注意，这一点很重要在操作名称和等

号之间是没有空格的。一开始我不知道，结果………………，比如，start= optionvalues，这个很重要。

optionvalues可以是0，1，或者是更多的操作参数名称和数值对。
如果你想要看每个命令的可以用的optionvalues，你可以使用sc command这样的格式。这会为你提供详细的帮助。

Optionvalues
为optionname的参数的名称指定它的数值。有效数值范围常常限制于哪一个参数的optionname。如果要列表请用

sc command来询问每个命令。

Comments
很多的命令需要管理员权限，所以我想说，在你操作这些东西的时候最好是管理员。呵呵！

当你键入SC而不带任何参数时，SC.exe会显示帮助信息和可用的命令。当你键入SC紧跟着命令名称时，你可以得

到一个有关这个命令的详细列表。比如，键入sc create可以得到和create有关的列表。
但是除了一个命令，sc query，这会导出该系统中当前正在运行的所有服务和驱动程序的状态。

当你使用start命令时，你可以传递一些参数（arguments）给服务的主函数，但是不是给服务进程的主函数。

SC create
这个命令可以在注册表和服务控制管理数据库建立一个入口。

语法1
sc [servername] create Servicename [Optionname= Optionvalues]

这里的servername，servicename，optionname，optionvalues和上面的一样，这里就不多说了。这里我们详细说

明一下optionname和optionvalues。

Optionname--Optionvalues
描述

type=----own, share, interact, kernel, filesys
关于建立服务的类型，选项值包括驱动程序使用的类型，默认是share。

start=----boot, sys tem, auto, demand, disabled
关于启动服务的类型，选项值包括驱动程序使用的类型，默认是demand（手动）。

error=----normal, severe, critical, ignore
当服务在导入失败错误的严重性，默认是normal。

binPath=--(string)
服务二进制文件的路径名，这里没有默认值，这个字符串是必须设置的。

group=----(string)
这个服务属于的组，这个组的列表保存在注册表中的ServiceGroupOrder下。默认是nothing。

tag=----(string)
如果这个字符串被设置为yes，sc可以从CreateService call中得到一个tagId。然而，SC并不显示这个标签，所

以使用这个没有多少意义。默认是nothing

depend=----(space separated string)有空格的字符串。
在这个服务启动前必须启动的服务的名称或者是组。

obj=----(string)
账号运行使用的名称，也可以说是登陆身份。默认是localsys tem

Displayname=--(string)
一个为在用户界面程序中鉴别各个服务使用的字符串。

password=--(string)
一个密码，如果一个不同于localsys tem的账号使用时需要使用这个。

Optionvalues
Optionname参数名称的数值列表。参考optionname。当我们输入一个字符串时，如果输入一个空的引用这意味着

一个空的字符串将被导入。

Comments
The SC CREATE command perFORMs the operations of the CreateService API function.
这个sc create命令执行CreateService API函数的操作。详细请见CreateService。

例1
下面这个例子在一台叫做（myserver）的计算机上为一个叫“NewService”的服务建立的一个注册表登记。
sc myserver create NewService binpath= c:winntsys tem32NewServ.exe

按照默认，这个服务会建立一个WIN32_SHARE_PROCESS使用SERVICE_DEMAND_START启动方式。这将不会有任何从属

关系，也将会按照localsys tem安全上下关系来运行。

例2
下面这个例子将在本地计算机上，建立一个服务，它将会是一个自动运行服务，并且运行在他自己的进程上。它

从属于TDI组和NetBios服务上。注意，你必须在从属中间增加一个空格的引用。

sc create NewService binpath= c:winntsys tem32NewServ.exe type= own
start= auto depend= '+TDI Netbios'

例3
服务开发者可以通过临时改变二进制路径（影像路径）的方式来将这个服务运行在内核调试器的上下关系中。下

面这个例子就可以让我们看到如何改变服务的配置。

sc config NewService binpath= 'ntsd -d c:winntsys tem32Newserv.exe'
这个例子会引起服务控制管理器调用ntsd.exe使用下例的参数字符串：
'-d c: tsys tem32NewServ.exe'

当系统装入newserv.exe时ntsd将会转而打断调试器，所以断点可以被设置在服务代码里。

SC QC
这个SC QC“询问配置”命令可以列出一个服务的配置信息和QUERY_SERVICE_CONFIG结构。

语法1
sc [Servername] qc Servicename [Buffersize]

Parameters
servername和servicename前面已经介绍过了，这里不再多说。

Buffersize，可选择的，列出缓冲区的尺寸。

Comments

SC QC命令显示了QUERY_SERVICE_CONFIG结构的内容。

以下是QUERY_SERVICE_CONFIG相应的区域。
TYPE------dwServiceType
START_TYPE----dwStartType
ERROR_CONTROL----dwErrorControl
BINARY_PATH_NAME--lpBinaryPathName
LOAD_ORDER_GROUP--lpLoadOrderGroup
TAG------dwTagId
DISPLAY_NAME----lpDisplayName
DEPENDENCIES----lpDependencies
SERVICE_START_NAME--lpServiceStartName

例1

下面这个例子询问了在上面例子中建立的“NewService”服务的配置：

sc myserver qc NewService

sc显示下面的信息：

SERVICE_NAME: NewService
TYPE : 20 WIN32_SHARE_PROCESS
START_TYPE : 3 DEMAND_START
ERROR_CONTROL : 1 NORMAL
BINARY_PATH_NAME : c:winntsys tem32NewServ.exe
LOAD_ORDER_GROUP :
TAG : 0
DISPLAY_NAME : NewService
DEPENDENCIES :
SERVICE_START_NAME : Localsys tem

NewService有能力和其他的服务共享一个进程。但是它不是自动启动的。二进制文件名是NewServ.exe。这个服务

不依靠与其它的的服务，而且运行在lcoalsys tem的安全上下关系中。这些都是调用QueryServiceStatus基本的返

回，如果还需要更多的细节届时，可以看看API函数文件。

SC QUERY

SC QUERY命令可以获得服务的信息。

语法：
sc [Servername] query { Servicename | Optionname= Optionvalues... }

参数：

servername, servicename, optionname, optionvalues不在解释。只谈一下这个命令提供的数值。

Optionname--Optionvalues
Description

type=----driver, service, all
列举服务的类型，默认是service

state=----active, inactive, all
列举服务的状态，默认是active

bufsize=--(numeric values)
列举缓冲区的尺寸，默认是1024 bytes

ri=----(numeric values)
但开始列举时，恢复指针的数字，默认是0

Optionvalues
同上。

Comments

SC QUERY命令可以显示SERVICE_STATUS结构的内容。

下面是SERVICE_STATUS结构相应的信息：
TYPE------dwServiceType
STATE------dwCurrentState, dwControlsAccepted
WIN32_EXIT_CODE----dwWin32ExitCode
SERVICE_EXIT_CODE--dwServiceSpecificExitCode
CHECKPOINT----dwCheckPoint
WAIT_HINT----dwWaitHint

在启动计算机后，使用SC QUERY命令会告诉你是否，或者不是一个启动服务的尝试。如果这个服务成功启动，WIN32_EXIT_CODE区间会将会包含一个0，当尝试不成功时，当它意识到这个服务不能够启动时，这个区间也会提供一个退出码给服务。

例子

查询“NewService'服务状态，键入：

sc query NewService

显示一下信息：

SERVICE_NAME: NewService
TYPE : 20 WIN32_SHARE_PROCESS
STATE : 1 STOPPED
(NOT_STOPPABLE,NOT_PAUSABLE,IGNORES_SHUTDOWN)
WIN32_EXIT_CODE : 1077 (0x435)
SERVICE_EXIT_CODE : 0 (0x0)
CHECKPOINT : 0x0
WAIT_HINT : 0x0

注意，这里存在一个给这个服务的退出码，即使这个服务部不在运行，键入net helpmsg 1077，将会得到对1077错误信息的说明：

上次启动之后，仍未尝试引导服务。

所以，这里我想说一句，希望大家可以活用net helpmsg，这会对你的学习有很大的帮助。

下面在对SC query的命令在说明一下：

列举活动服务和驱动程序状态，使用以下命令：
sc query

显示messenger服务，使用以下命令：
sc query messenger

只列举活动的驱动程序，使用以下命令：
sc query type= driver

列举Win32服务，使用以下命令：
sc query type= service

列举所有的服务和驱动程序，使用以下命令：
sc query state= all

用50 byte的缓冲区来进行列举，使用以下命令：
sc query bufsize= 50

在恢复列举时使用index=14，使用以下命令：
sc query ri=14

列举所有的交互式服务，使用以下命令：
sc query type= service type= interact

好了，说到这里。SC命令基本上已经说完了。希望大家好好看看，呵呵！相信会有帮助的！！