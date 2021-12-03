

# windows定时任务schtasks命令详细解

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[tglhmily1](https://blog.csdn.net/tglhmily1) 2019-05-21 22:34:24 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 4226 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 4

分类专栏： [cmd](https://blog.csdn.net/tglhmily1/category_8969435.html)

SCHTASKS /Create [/S system [/U username [/P [password]]]]

  [/RU username [/RP password]] /SC schedule [/MO modifier] [/D day]

  [/M months] [/I idletime] /TN taskname /TR taskrun [/ST starttime]

  [/RI interval] [ {/ET endtime | /DU duration} [/K] [/XML xmlfile] [/V1]]

  [/SD startdate] [/ED enddate] [/IT | /NP] [/Z] [/F]

 

描述:

   允许管理员在本地或远程系统上创建计划任务。

 

参数列表:

  /S  system     指定要连接到的远程系统。如果省略这个

​            系统参数，默认是本地系统。

 

  /U  username    指定应在其中执行 SchTasks.exe 的用户上下文。

 

  /P  [password]   指定给定用户上下文的密码。如果省略则

​            提示输入。

 

  /RU  username    指定任务在其下运行的“运行方式”用户

​            帐户(用户上下文)。对于系统帐户，有效 

​            值是 ""、"NT AUTHORITY\SYSTEM" 或 

​            "SYSTEM"。

​            对于 v2 任务，"NT AUTHORITY\LOCALSERVICE"和

​            "NT AUTHORITY\NETWORKSERVICE"以及常见的 SID

​             对这三个也都可用。

 

  /RP  [password]   指定“运行方式”用户的密码。要提示输

​            入密码，值必须是 "*" 或无。系统帐户会忽略该

​            密码。必须和 /RU 或 /XML 开关一起使用。

 

/RU/XML   /SC  schedule   指定计划频率。

​            有效计划任务:  MINUTE、 HOURLY、DAILY、WEEKLY、 

​            MONTHLY, ONCE, ONSTART, ONLOGON, ONIDLE, ONEVENT.

 

  /MO  modifier   改进计划类型以允许更好地控制计划重复

​            周期。有效值列于下面“修改者”部分中。

 

  /D   days     指定该周内运行任务的日期。有效值: 

​            MON、TUE、WED、THU、FRI、SAT、SUN

​            和对 MONTHLY 计划的 1 - 31

​            (某月中的日期)。通配符“*”指定所有日期。

 

  /M   months    指定一年内的某月。默认是该月的第一天。

​            有效值: JAN、FEB、MAR、APR、MAY、JUN、

​            JUL、 AUG、SEP、OCT、NOV  和 DEC。通配符

​            “*” 指定所有的月。

 

  /I   idletime   指定运行一个已计划的 ONIDLE 任务之前

​            要等待的空闲时间。

​            有效值范围: 1 到 999 分钟。

 

  /TN  taskname   指定唯一识别这个计划任务的名称。

 

  /TR  taskrun    指定在这个计划时间运行的程序的路径

​            和文件名。

​            例如: C:\windows\system32\calc.exe

 

  /ST  starttime   指定运行任务的开始时间。

​            时间格式为 HH:mm (24 小时时间)，例如 14:30 表示

​            2:30 PM。如果未指定 /ST，则默认值为

​            当前时间。/SC ONCE 必需有此选项。

 

  /RI  interval   用分钟指定重复间隔。这不适用于

​            计划类型: MINUTE、HOURLY、

​            ONSTART, ONLOGON, ONIDLE, ONEVENT.

​            有效范围: 1 - 599940 分钟。

​            如果已指定 /ET 或 /DU，则其默认值为

​            10 分钟。

 

  /ET  endtime    指定运行任务的结束时间。

​            时间格式为 HH:mm (24 小时时间)，例如，14:50 表示 2:50 PM。

​            这不适用于计划类型: ONSTART、

​            ONLOGON, ONIDLE, ONEVENT.

 

  /DU  duration   指定运行任务的持续时间。

​            时间格式为 HH:mm。这不适用于 /ET 和

​            计划类型: ONSTART, ONLOGON, ONIDLE, ONEVENT.

​            对于 /V1 任务，如果已指定 /RI，则持续时间默认值为

​            1 小时。

 

  /K         在结束时间或持续时间终止任务。

​            这不适用于计划类型: ONSTART、

​            ONLOGON, ONIDLE, ONEVENT. 

​            必须指定 /ET 或 /DU。

 

  /SD  startdate   指定运行任务的第一个日期。

​            格式为 yyyy/mm/dd。默认值为

​            当前日期。这不适用于计划类型: ONCE、

​            ONSTART, ONLOGON, ONIDLE, ONEVENT.

 

  /ED  enddate    指定此任务运行的最后一天的日期。

​            格式是 yyyy/mm/dd。这不适用于计划类型: 

​            ONCE、ONSTART、ONLOGON、ONIDLE。

 

  /EC  ChannelName  为 OnEvent 触发器指定事件通道。

 

  /IT         仅有在 /RU 用户当前已登录且

​            作业正在运行时才可以交互式运行任务。

​            此任务只有在用户已登录的情况下才运行。

 

  /NP         不储存任何密码。任务以给定用户的身份

​            非交互的方式运行。只有本地资源可用。

 

  /Z         标记在最终运行完任务后删除任务。

 

  /XML  xmlfile    从文件的指定任务 XML 中创建任务。

​            可以组合使用 /RU 和 /RP 开关，或者在任务 XML 已包含

​            主体时单独使用 /RP。

 

  /V1         创建 Vista 以前的平台可以看见的任务。

​            不兼容 /XML。

 

  /F         如果指定的任务已经存在，则强制创建

​            任务并抑制警告。

 

  /RL  level     为作业设置运行级别。有效值为

​            LIMITED 和 HIGHEST。默认值为 LIMITED。

 

  /DELAY delaytime  指定触发触发器后延迟任务运行的

​            等待时间。时间格式为

​            mmmm:ss。此选项仅对计划类型

​            ONSTART, ONLOGON, ONEVENT.

 

  /?         显示此帮助消息。

 

修改者: 按计划类型的 /MO 开关的有效值:

  MINUTE:  1 到 1439 分钟。

  HOURLY:  1 - 23 小时。

  DAILY:  1 到 365 天。

  WEEKLY:  1 到 52 周。

  ONCE:   无修改者。

  ONSTART: 无修改者。

  ONLOGON: 无修改者。

  ONIDLE:  无修改者。

  MONTHLY: 1 到 12，或

​       FIRST, SECOND, THIRD, FOURTH, LAST, LASTDAY。

 

  ONEVENT:  XPath 事件查询字符串。

示例:

  ==> 在远程机器 "ABC" 上创建计划任务 "doc"，

​    该机器每小时在 "runasuser" 用户下运行 notepad.exe。

 

​    SCHTASKS /Create /S ABC /U user /P password /RU runasuser

​         /RP runaspassword /SC HOURLY /TN doc /TR notepad 

 

  ==> 在远程机器 "ABC" 上创建计划任务 "accountant"，

​    在指定的开始日期和结束日期之间的开始时间和结束时间内，

​    每隔五分钟运行 calc.exe。

 

​    SCHTASKS /Create /S ABC /U domain\user /P password /SC MINUTE

​         /MO 5 /TN accountant /TR calc.exe /ST 12:00 /ET 14:00

​         /SD 06/06/2006 /ED 06/06/2006 /RU runasuser /RP userpassword

 

  ==> 创建计划任务 "gametime"，在每月的第一个星期天 

​    运行“空当接龙”。

 

​    SCHTASKS /Create /SC MONTHLY /MO first /D SUN /TN gametime 

​         /TR c:\windows\system32\freecell

 

  ==> 在远程机器 "ABC" 创建计划任务 "report"，

​    每个星期运行 notepad.exe。

 

​    SCHTASKS /Create /S ABC /U user /P password /RU runasuser

​         /RP runaspassword /SC WEEKLY /TN report /TR notepad.exe

 

  ==> 在远程机器 "ABC" 创建计划任务 "logtracker"，

​    每隔五分钟从指定的开始时间到无结束时间，

​    运行 notepad.exe。将提示输入 /RP 

​    密码。

 

​    SCHTASKS /Create /S ABC /U domain\user /P password /SC MINUTE

​         /MO 5 /TN logtracker 

​         /TR c:\windows\system32\notepad.exe /ST 18:30

​         /RU runasuser /RP

 

  ==> 创建计划任务 "gaming"，每天从 12:00 点开始到

​    14:00 点自动结束，运行 freecell.exe。

 

​    SCHTASKS /Create /SC DAILY /TN gaming /TR c:\freecell /ST 12:00

​         /ET 14:00 /K

  ==> 创建计划任务“EventLog”以开始运行 wevtvwr.msc

​    只要在“系统”通道中发布事件 101

 

​    SCHTASKS /Create /TN EventLog /TR wevtvwr.msc /SC ONEVENT

​         /EC System /MO *[System/EventID=101] 

  ==> 文件路径中可以加入空格，但需要加上两组引号，

​    一组引号用于 CMD.EXE，另一组用于 SchTasks.exe。用于 CMD

​    的外部引号必须是一对双引号；内部引号可以是一对单引号或

​    一对转义双引号:

​    SCHTASKS /Create 

​      /tr "'c:\program files\internet explorer\iexplorer.exe' 

​      \"c:\log data\today.xml\"" ... 





# [windows定时任务schtasks命令详细解](https://www.cnblogs.com/Sumarua/p/11774129.html)

SCHTASKS /Create [/S system [/U username [/P [password]]]]
[/RU username [/RP password]] /SC schedule [/MO modifier] [/D day]
[/M months] [/I idletime] /TN taskname /TR taskrun [/ST starttime]
[/RI interval] [ {/ET endtime | /DU duration} [/K] [/XML xmlfile] [/V1]]
[/SD startdate] [/ED enddate] [/IT | /NP] [/Z] [/F]

描述:
允许管理员在本地或远程系统上创建计划任务。

参数列表:
/S system 指定要连接到的远程系统。如果省略这个
系统参数，默认是本地系统。

```
/U   username      指定应在其中执行 SchTasks.exe 的用户上下文。

/P   [password]    指定给定用户上下文的密码。如果省略则
                   提示输入。

/RU  username      指定任务在其下运行的“运行方式”用户
                   帐户(用户上下文)。对于系统帐户，有效 
                   值是 ""、"NT AUTHORITY\SYSTEM" 或 
                   "SYSTEM"。
                   对于 v2 任务，"NT AUTHORITY\LOCALSERVICE"和
                   "NT AUTHORITY\NETWORKSERVICE"以及常见的 SID
                     对这三个也都可用。

/RP  [password]    指定“运行方式”用户的密码。要提示输
                   入密码，值必须是 "*" 或无。系统帐户会忽略该
                   密码。必须和 /RU 或 /XML 开关一起使用。
```

/RU/XML /SC schedule 指定计划频率。
有效计划任务: MINUTE、 HOURLY、DAILY、WEEKLY、
MONTHLY, ONCE, ONSTART, ONLOGON, ONIDLE, ONEVENT.

```
/MO   modifier     改进计划类型以允许更好地控制计划重复
                   周期。有效值列于下面“修改者”部分中。

/D    days         指定该周内运行任务的日期。有效值: 
                   MON、TUE、WED、THU、FRI、SAT、SUN
                   和对 MONTHLY 计划的 1 - 31
                   (某月中的日期)。通配符“*”指定所有日期。

/M    months       指定一年内的某月。默认是该月的第一天。
                   有效值: JAN、FEB、MAR、APR、MAY、JUN、
                   JUL、 AUG、SEP、OCT、NOV  和 DEC。通配符
                   “*” 指定所有的月。

/I    idletime     指定运行一个已计划的 ONIDLE 任务之前
                   要等待的空闲时间。
                   有效值范围: 1 到 999 分钟。

/TN   taskname     指定唯一识别这个计划任务的名称。

/TR   taskrun      指定在这个计划时间运行的程序的路径
                   和文件名。
                   例如: C:\windows\system32\calc.exe

/ST   starttime    指定运行任务的开始时间。
                   时间格式为 HH:mm (24 小时时间)，例如 14:30 表示
                   2:30 PM。如果未指定 /ST，则默认值为
                   当前时间。/SC ONCE 必需有此选项。

/RI   interval     用分钟指定重复间隔。这不适用于
                   计划类型: MINUTE、HOURLY、
                   ONSTART, ONLOGON, ONIDLE, ONEVENT.
                   有效范围: 1 - 599940 分钟。
                   如果已指定 /ET 或 /DU，则其默认值为
                   10 分钟。

/ET   endtime      指定运行任务的结束时间。
                   时间格式为 HH:mm (24 小时时间)，例如，14:50 表示 2:50 PM。
                   这不适用于计划类型: ONSTART、
                   ONLOGON, ONIDLE, ONEVENT.

/DU   duration     指定运行任务的持续时间。
                   时间格式为 HH:mm。这不适用于 /ET 和
                   计划类型: ONSTART, ONLOGON, ONIDLE, ONEVENT.
                   对于 /V1 任务，如果已指定 /RI，则持续时间默认值为
                   1 小时。

/K                 在结束时间或持续时间终止任务。
                   这不适用于计划类型: ONSTART、
                   ONLOGON, ONIDLE, ONEVENT. 
                   必须指定 /ET 或 /DU。

/SD   startdate    指定运行任务的第一个日期。
                   格式为 yyyy/mm/dd。默认值为
                   当前日期。这不适用于计划类型: ONCE、
                   ONSTART, ONLOGON, ONIDLE, ONEVENT.

/ED   enddate      指定此任务运行的最后一天的日期。
                   格式是 yyyy/mm/dd。这不适用于计划类型: 
                    ONCE、ONSTART、ONLOGON、ONIDLE。

/EC   ChannelName  为 OnEvent 触发器指定事件通道。

/IT                仅有在 /RU 用户当前已登录且
                   作业正在运行时才可以交互式运行任务。
                   此任务只有在用户已登录的情况下才运行。

/NP                不储存任何密码。任务以给定用户的身份
                   非交互的方式运行。只有本地资源可用。

/Z                 标记在最终运行完任务后删除任务。

/XML  xmlfile      从文件的指定任务 XML 中创建任务。
                   可以组合使用 /RU 和 /RP 开关，或者在任务 XML 已包含
                   主体时单独使用 /RP。

/V1                创建 Vista 以前的平台可以看见的任务。
                   不兼容 /XML。

/F                 如果指定的任务已经存在，则强制创建
                   任务并抑制警告。

/RL   level        为作业设置运行级别。有效值为
                   LIMITED 和 HIGHEST。默认值为 LIMITED。

/DELAY delaytime   指定触发触发器后延迟任务运行的
                   等待时间。时间格式为
                   mmmm:ss。此选项仅对计划类型
                   ONSTART, ONLOGON, ONEVENT.

/?                 显示此帮助消息。
```

修改者: 按计划类型的 /MO 开关的有效值:
MINUTE: 1 到 1439 分钟。
HOURLY: 1 - 23 小时。
DAILY: 1 到 365 天。
WEEKLY: 1 到 52 周。
ONCE: 无修改者。
ONSTART: 无修改者。
ONLOGON: 无修改者。
ONIDLE: 无修改者。
MONTHLY: 1 到 12，或
FIRST, SECOND, THIRD, FOURTH, LAST, LASTDAY。

```
ONEVENT:  XPath 事件查询字符串。
```

示例:
==> 在远程机器 "ABC" 上创建计划任务 "doc"，
该机器每小时在 "runasuser" 用户下运行 notepad.exe。

```
    SCHTASKS /Create /S ABC /U user /P password /RU runasuser
             /RP runaspassword /SC HOURLY /TN doc /TR notepad 

==> 在远程机器 "ABC" 上创建计划任务 "accountant"，
    在指定的开始日期和结束日期之间的开始时间和结束时间内，
    每隔五分钟运行 calc.exe。

    SCHTASKS /Create /S ABC /U domain\user /P password /SC MINUTE
             /MO 5 /TN accountant /TR calc.exe /ST 12:00 /ET 14:00
             /SD 06/06/2006 /ED 06/06/2006 /RU runasuser /RP userpassword

==> 创建计划任务 "gametime"，在每月的第一个星期天 
    运行“空当接龙”。

    SCHTASKS /Create /SC MONTHLY /MO first /D SUN /TN gametime 
             /TR c:\windows\system32\freecell

==> 在远程机器 "ABC" 创建计划任务 "report"，
    每个星期运行 notepad.exe。

    SCHTASKS /Create /S ABC /U user /P password /RU runasuser
             /RP runaspassword /SC WEEKLY /TN report /TR notepad.exe

==> 在远程机器 "ABC" 创建计划任务 "logtracker"，
    每隔五分钟从指定的开始时间到无结束时间，
    运行 notepad.exe。将提示输入 /RP 
    密码。

    SCHTASKS /Create /S ABC /U domain\user /P password /SC MINUTE
             /MO 5 /TN logtracker 
             /TR c:\windows\system32\notepad.exe /ST 18:30
             /RU runasuser /RP

==> 创建计划任务 "gaming"，每天从 12:00 点开始到
    14:00 点自动结束，运行 freecell.exe。

    SCHTASKS /Create /SC DAILY /TN gaming /TR c:\freecell /ST 12:00
             /ET 14:00 /K
==> 创建计划任务“EventLog”以开始运行 wevtvwr.msc
    只要在“系统”通道中发布事件 101

    SCHTASKS /Create /TN EventLog /TR wevtvwr.msc /SC ONEVENT
             /EC System /MO *[System/EventID=101] 
==> 文件路径中可以加入空格，但需要加上两组引号，
    一组引号用于 CMD.EXE，另一组用于 SchTasks.exe。用于 CMD
    的外部引号必须是一对双引号；内部引号可以是一对单引号或
    一对转义双引号:
    SCHTASKS /Create 
       /tr "'c:\program files\internet explorer\iexplorer.exe' 
       \"c:\log data\today.xml\"" ...
```

支持原创，转发请附链接：https://www.cnblogs.com/Sumarua/

标签: [schtasks.exe](https://www.cnblogs.com/Sumarua/tag/schtasks.exe/), [schtasks](https://www.cnblogs.com/Sumarua/tag/schtasks/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1525853/20191018172451.png)](https://home.cnblogs.com/u/Sumarua/)

[Sumarua](https://home.cnblogs.com/u/Sumarua/)
[关注 - 4](https://home.cnblogs.com/u/Sumarua/followees/)
[粉丝 - 2](https://home.cnblogs.com/u/Sumarua/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/Sumarua/p/11773477.html)上一篇： [TCP/IP 详解7 Ping指令](https://www.cnblogs.com/Sumarua/p/11773477.html)

# win10定时关机听语音

- 原创
- |
- 浏览：9757
- |
- 更新：2019-11-26 10:15

61条相关视频

- ![img](https://ksv-video-picture.cdn.bcebos.com/16ad916217d23ba0b41430376c750046b8b65fbf.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  win10怎么定时关机

  ![img](https://himg.bdimg.com/sys/portrait/item/public.1.e620fd5d.ew5k4kx5ps8PxWuG6GphSA.jpg)病毒执行官

- ![img](https://ksv-video-picture.cdn.bcebos.com/2746618e05fd64418fe7ae5bf0e3e97b2008130a.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  win10如何通过命令提示符...

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/291f78bb287ad589264bdde2a0b67d2429618169.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  Win10怎么关机

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/cae3085648d75e9e6d4fdaeec3e22c4d6c650bef.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  Win10怎么设置定时关机

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/e60547595606cfac622353027a5c2dc2280c9b87.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fquality%2Cq_80)

  win10如何设置定时关机

  ![img](https://himg.bdimg.com/sys/portrait/item/public.1.5ee6e9de.yyGGt6XkgilvfhUBanJCNw.jpg)鑫1325

- ![img](https://ksv-video-picture.cdn.bcebos.com/93bdbcd4317a0f27384999255dcc58d0bf58e8f1.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fquality%2Cq_80)

  win10怎么设置定时关机

  ![img](https://exp-picture.cdn.bcebos.com/604e9556ad042e68c7d8245785f85856d43dd18b.jpg)脑栋大开

- ![img](https://ksv-video-picture.cdn.bcebos.com/e9c874980b7b302d1a6964546941e41d1d07ece7.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑怎么设置定时关机及开...

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/00e48cf7fbb3dc77cf57401197eb209434dfd949.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  Windows10 电脑自动关机怎...

  ![img](https://himg.bdimg.com/sys/portrait/item/public.1.e6702d9e.FmrHC27HhaSy_UjMFFeQmg.jpg)欧巴桑sund...

- ![img](https://ksv-video-picture.cdn.bcebos.com/1971ab84fc893b385385257f516ec5ac1ba56b38.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fquality%2Cq_80)

  win10怎么设置定时关机

  ![img](https://exp-picture.cdn.bcebos.com/604e9556ad042e68c7d8245785f85856d43dd18b.jpg)脑栋大开

- ![img](https://ksv-video-picture.cdn.bcebos.com/7453f1195befb01489a4ed7180d507511a338362.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  360怎么设置定时关机

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/ab49f2de5642368ed59508a07fc353d8989065ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑怎么设置自动（记时）...

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/b46c2cc8d526c77d8e617efd8ff998ad015cfc45.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑自动关机在哪里设置

  ![img](https://himg.bdimg.com/sys/portrait/item/public.1.ccd5202.IjbY8T4TE8UEQSpIHMYv2Q.jpg)蹦蹦阀12

- ![img](https://ksv-video-picture.cdn.bcebos.com/35d3f828f66b31907c2e216467938100255126b1.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑定时关机设置（含如何...

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/68165315295ce1801219ef62e39ed2fce2b02875.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  win10定时关机怎么设置

  ![img](http://pic.rmb.bdstatic.com/fb234d3e97e75573afadcd5af43d3169.jpeg)太平洋电脑...

- ![img](https://ksv-video-picture.cdn.bcebos.com/edbf443eb12edc08c2fc0e27463f8561cb534012.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  windows10电脑自动关机怎么...

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/f03882c969a698befa7f61bf7897376241e68053.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑定时关机设置（含如何...

  ![img](http://pic.rmb.bdstatic.com/eccd23d9da0c7a7e2b6461fe083a8605.jpeg@c_1,w_250,h_250,x_9,y_9)小熊科技视...

- ![img](https://ksv-video-picture.cdn.bcebos.com/2abbfa8672dc5572c8ef759854c579c20ac2518a.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fquality%2Cq_80)

  电脑怎么设置定时关机

  ![img](https://cambrian-images.cdn.bcebos.com/2b288f4e2155e2eb389b3abb097d92dd_1559120099689.jpeg)小白系统

- ![img](https://ksv-video-picture.cdn.bcebos.com/c7c4016b8e9032788e5d941557097f129b62981e.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fquality%2Cq_80)

  电脑怎么定时关机win7

  ![img](https://himg.bdimg.com/sys/portrait/item/public.1.f6b328f0.pKycH1mxYGetxDnU8RVT0w.jpg)装机吧软件

- ![img](https://ksv-video-picture.cdn.bcebos.com/b3974d394bce2a10acdb7e37a50ec3fb8089a522.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑定时关机怎么设置

  ![img](http://pic.rmb.bdstatic.com/fb234d3e97e75573afadcd5af43d3169.jpeg)太平洋电脑...

- ![img](https://ksv-video-picture.cdn.bcebos.com/21075ef7b9eb8cd22468358c1556f4f3e6bddf28.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_640%2Ch_360%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

  电脑怎样设置自动关机

  ![img](http://pic.rmb.bdstatic.com/e01fc4c2c29bad7063f0edbfe177668d.jpeg)中关村在线

加载更多～

1090184人看了这个视频

- [![win10定时关机](https://exp-picture.cdn.bcebos.com/df087f0f8b56ad047788fc5adae10ef85956d077.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=1)1
- [![win10定时关机](https://exp-picture.cdn.bcebos.com/0fb94656d53da824b8092761306651598440cb77.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=2)2
- [![win10定时关机](https://exp-picture.cdn.bcebos.com/116b1ae23ea23a42c99a4ba33733ec3835bbc077.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=3)3
- [![win10定时关机](https://exp-picture.cdn.bcebos.com/bd72f23834bb19efcdbfe7a7497bd28287893a74.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=4)4
- [![win10定时关机](https://exp-picture.cdn.bcebos.com/87c8bf46b7b1eef9085da7cfbfb33c4132ba3274.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=5)5
- [![win10定时关机](https://exp-picture.cdn.bcebos.com/3d002dbad341037d9fd722c5a9bc7dc5ce672d74.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=6)6
- [![win10定时关机](https://exp-picture.cdn.bcebos.com/23fd63c5cf672b5f51a6ee253314f4d0b4032774.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html?picindex=7)7

[分步阅读](http://jingyan.baidu.com/album/08b6a5911c452054a809228d.html)

如何设置Win10定时关机，亲测分享

## 工具/原料

- Win10系统

## 方法/步骤

1. 

   桌面左下角搜索“管理工具”→“任务管理程序”或者“此电脑”→“计算机”→“管理”

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/df087f0f8b56ad047788fc5adae10ef85956d077.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

2. 

   打开“任务计划程序”→“创建基本任务”，进入任务设置向导。

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/0fb94656d53da824b8092761306651598440cb77.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

3. 

   “创建基本任务”栏，输入名称“定时关机”，点击“下一步”

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/116b1ae23ea23a42c99a4ba33733ec3835bbc077.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

4. 

    触发器，选择“每天”，点击“下一步”；在“每日”栏中，输入需要定时关机的时间，如22:00

   点击“下一步”

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/bd72f23834bb19efcdbfe7a7497bd28287893a74.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

5. 

   操作，选择“启动程序”

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/87c8bf46b7b1eef9085da7cfbfb33c4132ba3274.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

6. 

   “启动程序”中“浏览”，输入“shutdown.exe”→“打开”，在程序框中加上“shutdown.exe –s –t 10 ”点击下一步，弹出对话框，选择“是”，“完成”

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/3d002dbad341037d9fd722c5a9bc7dc5ce672d74.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/23fd63c5cf672b5f51a6ee253314f4d0b4032774.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   ![win10定时关机](https://exp-picture.cdn.bcebos.com/b955ead0b503c8d2cc1eacfd498333bf3aef2174.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   END

## 注意事项

- "shutdown.exe -s -t 10"一定要加上“-s -t ”代表多少秒后启动关机程序，数字可任意更换，单位是秒

经验内容仅供参考，如果您需解决具体问题(尤其法律、医学等领域)，建议您详细咨询相关领域专业人士。