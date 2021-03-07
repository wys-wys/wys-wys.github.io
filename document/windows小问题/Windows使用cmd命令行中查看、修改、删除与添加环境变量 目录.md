随笔 - 845, 文章 - 1, 评论 - 33, 阅读 - 61万

## [Windows使用cmd命令行中查看、修改、删除与添加环境变量](https://www.cnblogs.com/springsnow/p/12610417.html)



**目录**

- 一、查看环境变量
  - [1、查看当前所有可用的环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label0_0)
  - [2、查看某个环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label0_1)
- 二、修改环境变量
  - [1、修改环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label1_0)
  - [2、设置为空：](https://www.cnblogs.com/springsnow/p/12610417.html#_label1_1)
  - [3、给变量追加内容](https://www.cnblogs.com/springsnow/p/12610417.html#_label1_2)
- [三、一些常用的环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label2)

 

------

您可以在cmd中使用SET,显示或设置环境变量。

## 一、查看环境变量



### 1、查看当前所有可用的环境变量

输入 set 即可查看。

[![image](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091834275-1832507858.png)](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091833830-179372823.png)



### 2、查看某个环境变量

输入 “set 变量名”即可。比如想查看path变量的值，即输入 set path

[![image](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091834938-495275966.png)](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091834618-38337214.png)

## 二、修改环境变量

注意：所有的在cmd命令行下对环境变量的修改只对当前窗口有效，不是永久性的修改。也就是说当关闭此cmd命令行窗口后，将不再起作用。

永久性修改环境变量的方法有两种：一种是直接修改注册表，另一种是通过我的电脑-〉属性-〉高级，来设置系统的环境变量（查看详细）。



### 1、修改环境变量

输入 “set 变量名=变量内容”即可。比如将path设置为“d:\nmake.exe”，只要输入set path="d:\nmake.exe"。

注意，此修改环境变量是指用现在的内容去覆盖以前的内容，并不是追加。比如当我设置了上面的path路径之后，如果我再重新输入set path="c"，再次查看path路径的时候，其值为“c:”，而不是“d:\nmake.exe”；“c”。



### 2、设置为空：

如果想将某一变量设置为空，输入“set 变量名=”即可。

如“set path=” 那么查看path的时候就为空。注意，上面已经说了，只在当前命令行窗口起作用。因此查看path的时候不要去右击“我的电脑”——“属性”........



### 3、给变量追加内容

输入“set 变量名=%变量名%;变量内容”。（不同于3，那个是覆盖）。如，为path添加一个新的路径，输入“ set path=%path%;d:\nmake.exe”即可将d:\nmake.exe添加到path中，再次执行"set path=%path%;c:"，那么，使用set path语句来查看的时候，将会有：d:\nmake.exe;c:，而不是像第3步中的只有c:。

## 三、一些常用的环境变量

- %**AllUsersProfile**%: 局部 返回所有“用户配置文件”的位置。 {所有用户文件目录 – C:\Documents and Settings\All Users}

- %**AppData**%: 局部 返回默认情况下应用程序存储数据的位置。 {当前用户数据文件夹 – C:\Documents and Settings\wy\Application Data}

- %**Cd**%: 局部 返回当前目录字符串。

- %**CmdCmdLine**%: 局部 返回用来启动当前的 Cmd.exe 的准确命令行。

- %**CmdExtVersion**%: 系统 返回当前的“命令处理程序扩展”的版本号。

- %**CommonProgramFiles**%: {文件通用目录 – C:\Program Files\Common Files}

- %**ComputerName**%: 系统 返回计算机的名称。 {计算机名 – IBM-B63851E95C9}

- %**ComSpec**%: 系统 返回命令行解释器可执行程序的准确路径。 C:\WINDOWS\system32\cmd.exe

- %**Date**%: 系统 返回当前日期。使用与 date /t 命令相同的格式。由 Cmd.exe 生成。有关 date 命令的详细信息，请参阅 Date。

- %**ErrorLevel**%: 系统 返回最近使用过的命令的错误代码。通常用非零值表示错误。

- %**HomeDrive**%: 系统 返回连接到用户主目录的本地工作站驱动器号。基于主目录值的设置。用户主目录是在“本地用户和组”中指定的。 {当前用户根目录 – C:}

- %**HomePath**%: 系统 返回用户主目录的完整路径。基于主目录值的设置。用户主目录是在“本地用户和组”中指定的。 {当前用户路径 – \Documents and Settings\wy}

- %**HomeShare**%: 系统 返回用户的共享主目录的网络路径。基于主目录值的设置。用户主目录是在“本地用户和组”中指定的。

- %**LogonSever**%: 局部 返回验证当前登录会话的域控制器的名称。

- %**Number_Of_Processors**%: 系统 指定安装在计算机上的处理器的数目。 {处理器个数 – 1}

- %**Os**%: 系统 返回操作系统的名称。Windows 2000 将操作系统显示为 Windows_NT。 {操作系统名 – Windows_NT}

- %**Path**%: 系统 指定可执行文件的搜索路径。

- %**PathExt**%: 系统 返回操作系统认为可执行的文件扩展名的列表。

- %**Processor_Architecture**%: 系统 返回处理器的芯片体系结构。值: x86，IA64。 {处理器芯片架构 – x86}

- %**Processor_Identfier**%: 系统 返回处理器说明。

- %**Processor_Level**%: 系统 返回计算机上安装的处理器的型号。 {处理器型号 – 6}

- %**Processor_Revision**%: 系统 返回处理器修订号的系统变量。 {处理器修订号 – 0905}

- %**ProgramFiles**%: {程序默认安装目录 – C:\Program Files}

- %**Prompt**%: 局部 返回当前解释程序的命令提示符设置。由 Cmd.exe 生成。 $P$G

- %**Random**%: 系统 返回 0 到 32767 之间的任意十进制数字。由 Cmd.exe 生成。

- %**SystemDrive**%: 系统 返回包含 Windows XP 根目录（即系统根目录）的驱动器。 {系统根目录 – C:}

- %**SystemRoot**%: 系统 返回 Windows XP 根目录的位置。 {系统目录 – C:\WINDOWS}

- %**Temp**%: 系统和用户 返回对当前登录用户可用的应用程序所使用的默认临时目录。有些应用程序需要 TEMP，而其它应用程序则需要 TMP。 {当前用户临时文件夹 – C:\DOCUME~1\wy\LOCALS~1\Temp}

- %**Time**%: 系统 返回当前时间。使用与 time /t 命令相同的格式。由 Cmd.exe 生成。9:16:25.05

- %**UserDomain**%: 局部 返回包含用户帐户的域的名称。 {包含用户帐号的域 – IBM-B63851E95C9}

- %**UserName**%: 局部 返回当前登录的用户的名称。 {当前用户名 – wy}

- %**UserProfile**%: 局部 返回当前用户的配置文件的位置。 {当前用户目录 – C:\Documents and Settings\wy}

- %**WinDir**%: 系统 返回操作系统目录的位置。 {系统目录 – C:\WINDOWS}随笔 - 845, 文章 - 1, 评论 - 33, 阅读 - 61万

  ## [Windows使用cmd命令行中查看、修改、删除与添加环境变量](https://www.cnblogs.com/springsnow/p/12610417.html)

  

  **目录**

  - 一、查看环境变量
    - [1、查看当前所有可用的环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label0_0)
    - [2、查看某个环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label0_1)
  - 二、修改环境变量
    - [1、修改环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label1_0)
    - [2、设置为空：](https://www.cnblogs.com/springsnow/p/12610417.html#_label1_1)
    - [3、给变量追加内容](https://www.cnblogs.com/springsnow/p/12610417.html#_label1_2)
  - [三、一些常用的环境变量](https://www.cnblogs.com/springsnow/p/12610417.html#_label2)

   

  ------

  您可以在cmd中使用SET,显示或设置环境变量。

  ## 一、查看环境变量

  

  ### 1、查看当前所有可用的环境变量

  输入 set 即可查看。

  [![image](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091834275-1832507858.png)](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091833830-179372823.png)

  

  ### 2、查看某个环境变量

  输入 “set 变量名”即可。比如想查看path变量的值，即输入 set path

  [![image](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091834938-495275966.png)](https://img2020.cnblogs.com/blog/24244/202004/24244-20200401091834618-38337214.png)

  ## 二、修改环境变量

  注意：所有的在cmd命令行下对环境变量的修改只对当前窗口有效，不是永久性的修改。也就是说当关闭此cmd命令行窗口后，将不再起作用。

  永久性修改环境变量的方法有两种：一种是直接修改注册表，另一种是通过我的电脑-〉属性-〉高级，来设置系统的环境变量（查看详细）。

  

  ### 1、修改环境变量

  输入 “set 变量名=变量内容”即可。比如将path设置为“d:\nmake.exe”，只要输入set path="d:\nmake.exe"。

  注意，此修改环境变量是指用现在的内容去覆盖以前的内容，并不是追加。比如当我设置了上面的path路径之后，如果我再重新输入set path="c"，再次查看path路径的时候，其值为“c:”，而不是“d:\nmake.exe”；“c”。

  

  ### 2、设置为空：

  如果想将某一变量设置为空，输入“set 变量名=”即可。

  如“set path=” 那么查看path的时候就为空。注意，上面已经说了，只在当前命令行窗口起作用。因此查看path的时候不要去右击“我的电脑”——“属性”........

  

  ### 3、给变量追加内容

  输入“set 变量名=%变量名%;变量内容”。（不同于3，那个是覆盖）。如，为path添加一个新的路径，输入“ set path=%path%;d:\nmake.exe”即可将d:\nmake.exe添加到path中，再次执行"set path=%path%;c:"，那么，使用set path语句来查看的时候，将会有：d:\nmake.exe;c:，而不是像第3步中的只有c:。

  ## 三、一些常用的环境变量

  - %**AllUsersProfile**%: 局部 返回所有“用户配置文件”的位置。 {所有用户文件目录 – C:\Documents and Settings\All Users}
  - %**AppData**%: 局部 返回默认情况下应用程序存储数据的位置。 {当前用户数据文件夹 – C:\Documents and Settings\wy\Application Data}
  - %**Cd**%: 局部 返回当前目录字符串。
  - %**CmdCmdLine**%: 局部 返回用来启动当前的 Cmd.exe 的准确命令行。
  - %**CmdExtVersion**%: 系统 返回当前的“命令处理程序扩展”的版本号。
  - %**CommonProgramFiles**%: {文件通用目录 – C:\Program Files\Common Files}
  - %**ComputerName**%: 系统 返回计算机的名称。 {计算机名 – IBM-B63851E95C9}
  - %**ComSpec**%: 系统 返回命令行解释器可执行程序的准确路径。 C:\WINDOWS\system32\cmd.exe
  - %**Date**%: 系统 返回当前日期。使用与 date /t 命令相同的格式。由 Cmd.exe 生成。有关 date 命令的详细信息，请参阅 Date。
  - %**ErrorLevel**%: 系统 返回最近使用过的命令的错误代码。通常用非零值表示错误。
  - %**HomeDrive**%: 系统 返回连接到用户主目录的本地工作站驱动器号。基于主目录值的设置。用户主目录是在“本地用户和组”中指定的。 {当前用户根目录 – C:}
  - %**HomePath**%: 系统 返回用户主目录的完整路径。基于主目录值的设置。用户主目录是在“本地用户和组”中指定的。 {当前用户路径 – \Documents and Settings\wy}
  - %**HomeShare**%: 系统 返回用户的共享主目录的网络路径。基于主目录值的设置。用户主目录是在“本地用户和组”中指定的。
  - %**LogonSever**%: 局部 返回验证当前登录会话的域控制器的名称。
  - %**Number_Of_Processors**%: 系统 指定安装在计算机上的处理器的数目。 {处理器个数 – 1}
  - %**Os**%: 系统 返回操作系统的名称。Windows 2000 将操作系统显示为 Windows_NT。 {操作系统名 – Windows_NT}
  - %**Path**%: 系统 指定可执行文件的搜索路径。
  - %**PathExt**%: 系统 返回操作系统认为可执行的文件扩展名的列表。
  - %**Processor_Architecture**%: 系统 返回处理器的芯片体系结构。值: x86，IA64。 {处理器芯片架构 – x86}
  - %**Processor_Identfier**%: 系统 返回处理器说明。
  - %**Processor_Level**%: 系统 返回计算机上安装的处理器的型号。 {处理器型号 – 6}
  - %**Processor_Revision**%: 系统 返回处理器修订号的系统变量。 {处理器修订号 – 0905}
  - %**ProgramFiles**%: {程序默认安装目录 – C:\Program Files}
  - %**Prompt**%: 局部 返回当前解释程序的命令提示符设置。由 Cmd.exe 生成。 $P$G
  - %**Random**%: 系统 返回 0 到 32767 之间的任意十进制数字。由 Cmd.exe 生成。
  - %**SystemDrive**%: 系统 返回包含 Windows XP 根目录（即系统根目录）的驱动器。 {系统根目录 – C:}
  - %**SystemRoot**%: 系统 返回 Windows XP 根目录的位置。 {系统目录 – C:\WINDOWS}
  - %**Temp**%: 系统和用户 返回对当前登录用户可用的应用程序所使用的默认临时目录。有些应用程序需要 TEMP，而其它应用程序则需要 TMP。 {当前用户临时文件夹 – C:\DOCUME~1\wy\LOCALS~1\Temp}
  - %**Time**%: 系统 返回当前时间。使用与 time /t 命令相同的格式。由 Cmd.exe 生成。9:16:25.05
  - %**UserDomain**%: 局部 返回包含用户帐户的域的名称。 {包含用户帐号的域 – IBM-B63851E95C9}
  - %**UserName**%: 局部 返回当前登录的用户的名称。 {当前用户名 – wy}
  - %**UserProfile**%: 局部 返回当前用户的配置文件的位置。 {当前用户目录 – C:\Documents and Settings\wy}
  - %**WinDir**%: 系统 返回操作系统目录的位置。 {系统目录 – C:\WINDOWS}