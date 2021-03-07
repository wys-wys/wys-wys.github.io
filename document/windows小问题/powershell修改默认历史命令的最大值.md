### ***在powershell的配置文件中添加$MaximumHistoryCount = 10000***



##### get-variable 查看首选项变量   ls env: 查看环境变量



powershell 命令历史记录文件存放路径：C:\Users\26575\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine

powershell 配置文件存放路径：

C:\Users\26575\Documents\WindowsPowerShell

C:\Windows\System32\WindowsPowerShell\v1.0

# powershell的命令历史记录存储位置

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[weixin_43659597](https://blog.csdn.net/weixin_43659597) 2021-01-12 23:41:46 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 16 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

文章标签： [windows](https://www.csdn.net/tags/MtTaEg0sNTAxMTMtYmxvZwO0O0OO0O0O.html) [windows 10](https://so.csdn.net/so/search/s.do?q=windows 10&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

win10 powershell的命令历史记录存储在

```powershell
%USERPROFILE%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine
1
```

地址下的`ConsoleHost_history.txt`

可以删除某些或全部历史记录

在powershell中可以按上下方向键查询历史命令

或使用命令

```powershell
get-history
```

# (23)Powershell中的首选项变量

[![img](https://s3.51cto.com//wyfs02/M00/0C/3A/wKiom1LOArHTlaNsAAAUCODD0gA333_middle.jpg)](https://blog.51cto.com/020618)

[ghcomeon](https://blog.51cto.com/020618)0人评论[2631人阅读](javascript:;)[2017-01-22 10:46:21](javascript:;)

  上一节介绍了 Powershell 中的环境变量，本节介绍 Powershell 中的首选项变量，这些变量的作用与环境变量类似，都是Powershell中的内置变量，也可以对这些值进行更改。需要注意的是，首选项变量影响 PowerShell 操作环境以及在该环境中运行的所有命令。在很多情况下，cmdlet 带有的参数可用于替代特定命令的首选行为。



  以下是 Powershell 中常见的首选项变量及其默认值。

| **首选项变量**              | **默认值及说明**                                             |
| --------------------------- | ------------------------------------------------------------ |
| $ConfirmPreference          | High                                                         |
| $DebugPreference            | SilentlyContinue                                             |
| $ErrorActionPreference      | Continue                                                     |
| $ErrorView                  | NormalView                                                   |
| $FormatEnumerationLimit     | 4                                                            |
| $LogCommandHealthEvent      | False（不写入日志），记录命令初始化和进行处理时产生的错误和异常 |
| $LogCommandLifecycleEvent   | False（不写入日志），记录命令和命令管道的启动和停止，以及命令发现过程中的安全异常。 |
| $LogEngineHealthEvent       | True（写入日志），记录会话的错误和故障。                     |
| $LogEngineLifecycleEvent    | True（写入日志），记录会话的打开和关闭。                     |
| $LogProviderLifecycleEvent  | True（写入日志）,记录添加和删除 Windows PowerShell 提供程序。 |
| $LogProviderHealthEvent     | True（写入日志）,记录提供程序错误，如读写错误、查找错误以及调用错误。 |
| $MaximumAliasCount          | 4096,确定在 Windows PowerShell 会话中允许多少个别名。可以使用命令 (get-alias).count 统计别名数量。 |
| $MaximumDriveCount          | 4096,确定在给定的会话中，允许多少个 Windows PowerShell 驱动器。可以使用命令 (get-psdrive).count统计数量。 |
| $MaximumErrorCount          | 256，确定在会话的错误历史记录中保存多少个错误。$Error[0]是最新的错误信息。 |
| $MaximumFunctionCount       | 4096，确定给定会话中允许多少个函数。可以使用(get-childitem function:).count 统计当前会话中的函数个数。 |
| $MaximumHistoryCount        | 64，确定当前会话的命令历史记录中保存多少条命令。             |
| $MaximumVariableCount       | 4096，确定给定会话中允许多少个变量，包括自动变量、首选项变量以及在命令和脚本中创建的变量。 |
| $OFS                        | ""(空格字符)，输出字段分隔符。指定在数组转换为字符串时，用来分隔数组元素的字符。 |
| $OutputEncoding             | ASCIIEncoding，PowerShell 在将文本发送给其他应用程序时，所使用的字符编码方法。 |
| $ProgressPreference         | Continue，显示操作执行的进度条，并继续执行。                 |
| $PSEmailServer              | (无)指定用于发送电子邮件的默认电子邮件服务器。               |
| $PSSessionApplicationName   | WSMAN                                                        |
| $PSSessionConfigurationName | [http://schemas.microsoft.com/powershell/microsoft.powershell  ](http://schemas.microsoft.com/powershell/microsoft.powershell，) 指定使用 WS-Management 技术的远程命令的默认应用程序名称。 |
| $VerbosePreference          | SilentlyContinue， 默认不显示命令操作的详细消息。继续执行。  |
| $WarningPreference          | Continue，默认显示操作执行的警告消息，然后继续执行。         |
| $WhatIfPreference           | 0，默认不自动启用 WhatIf。若要手动启用它，请使用命令的 WhatIf 参数。 |

  以上列出的是常见的首选项及其默认值，如果要查看全部的首选项变量，输入命令 Get-Variable 进行查看。

------

1. **首选项命令值的查看与更改**

  如果要查看某个具体的首选项的值，直接输入首选项变量的名称。例如

```ps
PS C:\> $ConfirmPreference
High
```

  如果要更改首选项变量的值，使用赋值语句，例如：

```ps
PS C:\> $ConfirmPreference = "Medium"
PS C:\> $ConfirmPreference
Medium
```

  需要注意的是，首选项变量与其他变量一样，在当前回话对值所做的更改，只针对当前窗口(会话)有效。如果需要使更改永久有效，需要把更改写入 Powershell 配置文件中。另外，Powershell 中的首选项往往有指定的可选值，即只能把可选值中的一个赋值给该变量，而不是可以赋值任何值。以下会对每个首选项变量做详细说明以及其所有的可选值。

------

**2. $ConfirmPreference**

  根据命令的名称可知，该命令与确认(Confirm)有关。Powershell 对每一个命令执行结果可能产生的影响划分了一个等级(High、Medium、Low 或 None),也就是对每一个命令都划分了风险(对当前系统可能产生的影响)等级。

  如果 $ConfirmPreference 值（High、Medium、Low 或 None）大于等于命令操作的风险（High、Medium、Low 或 None）时，PowerShell 会在执行该操作之前自动请求用户确认(告诉你输入的命令可能存在风险，是否要继续执行)。

  $ConfirmPreference 有以下有效可选值。

| 有效可选值 | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| None       | 不自动确认任何 cmdlet 操作。用户必须使用 Confirm 参数来请求确认特定命令。即Powershell认为你输入的每一条命令都有可能存在风险，每条命令都需要明确确认 |
| Low        | 对命令风险等级为低、中或高的命令操作自动提示确认。如果要阻止特定命令提示确认，可以使用通用参数 -Confirm:$false。 |
| Medium     | 对命令风险等级为中或高的命令操作自动提示确认。如果要为特定命令启用提示确认，可以使用 -confirm。如果要阻止特定命令提示确认，请使用 confirm:$false。 |
| High       | 默认值。对命令等级为高风险的命令操作自动提示确认。如果要为特定命令启用提示确认，可以使用 -confirm。如果要阻止特定命令提示确认，请使用 -confirm:$false。 |

  哪些行为在Powershell中会被认定为有风险行为？比如删除文件，停掉所有的Service，命令执行需要占用大量系统资源等。例如：

```ps
PS C:\> $ConfirmPreference
Medium
PS C:\> cd D:\MyPowerShell
PS D:\MyPowerShell> Remove-Item .\Test.ps1
确认
是否确实要执行此操作?
对目标“D:\MyPowerShell\Test.ps1”执行操作“删除文件”。
[Y] 是(Y)  [A] 全是(A)  [N] 否(N)  [L] 全否(L)  [S] 挂起(S)  [?] 帮助 (默认值为“Y”):
```

  在上面的例子中 $ConfirmPreference 的值为"Medium"。需要注意的是，Powershell中的大部分命令的风险等级为"Medium",而$ConfirmPreference 的默认值时"High",所以在大部分的时候，并不会自动提示。如果需要要激活自动提示，可以将$ConfirmPreference的值更改为"Medium"或者"Low"。

------

**3. $DebugPreference**

  从命令的名称可知，与调试(Debug)有关。Powershell 根据该值，确认如何对待调试信息(脚本、cmdlet 或提供程序生成的调试消息，或者 Write-Debug 命令在命令行上生成的调试消息)-是忽略还是继续执行。有以下可选值：

| 有效可选值       | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| Stop             | 显示调试信息并停止命令的执行，并把错误输出到控制台。         |
| Inquire          | 显示调试信息，并和你确认是否要继续执行。                     |
| Continue         | 显示调试信息，并继续执行。                                   |
| SilentlyContinue | 默认值。不显示调试信息，继续执行不发生中断,相当于直接忽视调试信息。如果要强制显示调试信息，请使用 -Debug 参数。 |

  调试信息通常是对开发人员有效，具有比较强的专业性(其他人看了也是一脸懵逼^_^),所以默认情况下不显示调试信息。例如例子说明了SilentlyContinue的作用：

```ps
PS C:\> $DebugPreference
SilentlyContinue
PS C:\> Write-Debug "This is debug message"
PS C:\> Write-Debug "This is debug message" -Debug
调试: This is debug message
确认
是否继续执行此操作?
[Y] 是(Y)  [A] 全是(A)  [H] 终止命令(H)  [S] 挂起(S)  [?] 帮助 (默认值为“Y”):
```

  以下示例说明了其他3个参数的用法及所代表的含义：

```ps
PS C:\> $DebugPreference = "Continue"
PS C:\> $DebugPreference
Continue
PS C:\> Write-Debug "This is debug message"
调试: This is debug message
PS C:\> Write-Debug "This is debug message" -Debug:$false
PS C:\> $DebugPreference = "Stop"
PS C:\> $DebugPreference
Stop
PS C:\> Write-Debug "This is debug message"
调试: This is debug message
Write-Debug : 已停止执行命令，因为首选项变量“DebugPreference”或通用参数被设置为 Stop。
所在位置 行:1 字符: 12
+ Write-Debug <<<<  "This is debug message"
    + CategoryInfo          : OperationStopped: (:) [Write-Debug], ParentContainsErrorReco
    + FullyQualifiedErrorId : ActionPreferenceStop,Microsoft.PowerShell.Commands.WriteDebu
PS C:\> Write-Debug "This is debug message" -Debug:$false
PS C:\> $DebugPreference = "Inquire"
PS C:\> Write-Debug "This is debug message"
调试: This is debug message
确认
是否继续执行此操作?
[Y] 是(Y)  [A] 全是(A)  [H] 终止命令(H)  [S] 挂起(S)  [?] 帮助 (默认值为“Y”): PS C:\>
PS C:\> Write-Debug "This is debug message" -Debug:$false
PS C:\>
```

  通过以上示例可知，对于任何调试信息都可以通过 -Debug:$false 或者 -Debug:$true 来阻止或是激活调试信息。

------

**4. $ErrorActionPreference**

  $ErrorActionPreference 与 $DebugPreference 非常类似，只是前者是用来处理错误信息，而不是调试信息。Powershell 根据 $ErrorActionPreference 的值，确定如何响应命令行、脚本、cmdlet 或提供程序中的非终止性错误(不会导致cmdlet 处理停止的错误)，如 Write-Error cmdlet 生成的错误。

  $ErrorActionPreference 提供了以下有效可选值：

| 有效值           | 说明                                   |
| ---------------- | -------------------------------------- |
| Stop             | 显示错误信息并停止执行                 |
| Inquire          | 显示错误信息，并和你确认是否要继续执行 |
| Continue         | 默认值。显示错误信息并继续执行         |
| SilentlyContinue | 不显示错误信息，继续执行不发生中断     |

  以下示例说明了不同值的不同作用。

```ps
PS C:\> $ErrorActionPreference
Continue
PS C:\> Write-Error "This is error message"
Write-Error "This is error message" : This is error message
    + CategoryInfo          : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException
PS C:\> Write-Error "This is error message" -ErrorAction:SilentlyContinue
PS C:\>
PS C:\>
PS C:\> $ErrorActionPreference = "SilentlyContinue"
PS C:\> $ErrorActionPreference
SilentlyContinue
PS C:\> Write-Error "This is error message"
PS C:\> Write-Error "This is error message" -ErrorAction:continue
Write-Error "This is error message" -ErrorAction:continue : This is error message
    + CategoryInfo          : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException
PS C:\>
PS C:\>
PS C:\> $ErrorActionPreference
SilentlyContinue
PS C:\> Get-ChildItem -path notExistFile.txt
PS C:\> $ErrorActionPreference = "Continue"
PS C:\> Get-ChildItem -path notExistFile.txt
Get-ChildItem : 找不到路径“C:\notExistFile.txt”，因为该路径不存在。
所在位置 行:1 字符: 14
+ Get-ChildItem <<<<  -path notExistFile.txt
    + CategoryInfo          : ObjectNotFound: (C:\notExistFile.txt:String) [Get-ChildItem], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetChildItemCommand
PS C:\> Get-ChildItem -path notExistFile.txt -ErrorAction:SilentlyContinue
PS C:\>
PS C:\>
PS C:\> $ErrorActionPreference = "Inquire"
PS C:\> $ErrorActionPreference
Inquire
PS C:\> Get-ChildItem -path notExistFile.txt
确认
找不到路径“C:\notExistFile.txt”，因为该路径不存在。
[Y] 是(Y)  [A] 全是(A)  [H] 终止命令(H)  [S] 挂起(S)  [?] 帮助 (默认值为“Y”):
```

------

**5. $ErrorView**

  Powershell 中错误信息的显示格式。有以下两个可选值：

| 有效可选值   | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| NormalView   | 默认值。错误信息的详细视图(View),包括错误描述、错误中所涉及对象的名称，以及指向命令中导致错误的词的箭头 (<<<<)。 |
| CategoryView | 错误信息的简明结构化视图。格式为：{Category}: ({TargetName}:{TargetType}):[{Activity}], {Reason} |

  以下例子说明了错误信息显示格式的不同：

```ps
PS C:\> $ErrorView
NormalView
PS C:\> Get-ChildItem -path notExistFile.txt
Get-ChildItem : 找不到路径“C:\notExistFile.txt”，因为该路径不存在。
所在位置 行:1 字符: 14
+ Get-ChildItem <<<<  -path notExistFile.txt
    + CategoryInfo          : ObjectNotFound: (C:\notExistFile.txt:String) [Get-ChildItem], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetChildItemCommand
PS C:\> $ErrorView = "CategoryView"
PS C:\> Get-ChildItem -path notExistFile.txt
ObjectNotFound: (C:\notExistFile.txt:String) [Get-ChildItem], ItemNotFoundException
```

  需要注意的是，ErrorView 的值只影响错误显示；它不会更改存储在 $error 自动变量中的错误对象的结构。

  $error 自动变动变量是包含错误信息的数组，第一个元素(下标为0)包含的是最新的错误信息。例如在上面的语句执行后，error[0]错误信息如下：

```ps
PS C:\> $Error[0] | Format-List -Property * -Force
PSMessageDetails      :
Exception             : System.Management.Automation.ItemNotFoundException: 找不到路径“C:\notExistFile.txt”，因为该路
                        径不存在。
                           在 System.Management.Automation.SessionStateInternal.GetChildItems(String path, Boolean recu
                        rse, CmdletProviderContext context)
                           在 System.Management.Automation.ChildItemCmdletProviderIntrinsics.Get(String path, Boolean r
                        ecurse, CmdletProviderContext context)
                           在 Microsoft.PowerShell.Commands.GetChildItemCommand.Proce***ecord()
TargetObject          : C:\notExistFile.txt
CategoryInfo          : ObjectNotFound: (C:\notExistFile.txt:String) [Get-ChildItem], ItemNotFoundException
FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetChildItemCommand
ErrorDetails          :
InvocationInfo        : System.Management.Automation.InvocationInfo
PipelineIterationInfo : {0, 1}
```

------

**6. $FormatEnumerationLimit**

  确定一次显示中包含多少个枚举项(显示多少项)。该变量不会影响基础对象；只影响显示。当$FormatEnumerationLimit 的值小于枚举项的数量时，PowerShell  会添加一个省略号(...)来指示还有其他项未显示。有效值：整数 (Int32),默认值：4 。 例如：

```ps
PS C:\> $FormatEnumerationLimit
4
PS C:\> Get-Service | Group-Object -Property Status | Format-List
Name   : Stopped
Count  : 62
Group  : {System.ServiceProcess.ServiceController, System.ServiceProcess.ServiceController, System.ServiceProcess.Servi
         ceController, System.ServiceProcess.ServiceController...}
Values : {Stopped}
Name   : Running
Count  : 41
Group  : {System.ServiceProcess.ServiceController, System.ServiceProcess.ServiceController, System.ServiceProcess.Servi
         ceController, System.ServiceProcess.ServiceController...}
Values : {Running}
PS C:\> $FormatEnumerationLimit = 6
PS C:\> Get-Service | Group-Object -Property Status | Format-List
Name   : Stopped
Count  : 62
Group  : {System.ServiceProcess.ServiceController, System.ServiceProcess.ServiceController, System.ServiceProcess.Servi
         ceController, System.ServiceProcess.ServiceController, System.ServiceProcess.ServiceController, System.Service
         Process.ServiceController...}
Values : {Stopped}
Name   : Running
Count  : 41
Group  : {System.ServiceProcess.ServiceController, System.ServiceProcess.ServiceController, System.ServiceProcess.Servi
         ceController, System.ServiceProcess.ServiceController, System.ServiceProcess.ServiceController, System.Service
         Process.ServiceController...}
Values : {Running}
```

------

**7. 总结**

  这节介绍了 Powershell中的首选项变量，这些变量的作用于环境变量类似，需要注意的是，更改首选项变量不只针对当前会话，对再次打开的窗体任然有效，这些首选项都提供了默认的参数值，对于刚开始不熟悉的，尽量不要去更改这些变量的默认值，了解每个变量的作用即可。

# PowerShell变量 			

​					作者： 					xntutor.com 				**Java技术QQ群：227270512 / Linux QQ群：479429477** 			



​					 				 				 				 			

变量是Windows PowerShell的基本部分。 我们可以将所有类型的值存储在PowerShell变量中。 例如，可以存储命令的结果以及在表达式和命令中使用的元素，例如路径，名称，设置和值。它们专门用于存储对象，即Microsoft .NET Framework对象。

变量是存储数据的内存单位。 在Windows PowerShell中，变量的名称以美元符号(`$`)开头，例如`$process`，`$var`。 变量的名称不区分大小写，并且包含空格和特殊字符。 默认情况下，PowerShell中所有变量的值均为`$null`。

> 注意：在Windows PowerShell中，特殊字符具有特殊含义。如果在变量名称中使用特殊字符，则需要将它们括在大括号`{}`中。

下面是一些有效和无效变量的示例：

| 有效的变量名称  | 无效的变量名称 |
| --------------- | -------------- |
| `$myVariable`   | `myVariable`   |
| `$MyVariable_1` | `$my-variable` |
| `{my-variable}` | `$my variable` |

## 1. 创建变量

使用赋值运算符(`=`)将指定的值赋给变量，我们可以通过给变量赋值来创建变量。

以下是一些创建变量的示例：

**示例1：**

```shell
$vrb = 122
Shell
```

本示例中的命令将整数值`122`分配给变量`$vrb`。

**示例2：**

```shell
$mySubject = "PowerShell"
Shell
```

本示例中的命令创建一个名为`$mySubject`的变量，并为其分配一个字符串值。 在此示例中，`$mySubject`是一个字符串对象。

## 2. 打印变量的值

要显示变量的值，只需要在美元符号`$`后跟变量的名称。

**示例：**

![img](http://www.xntutor.com/uploads/images/2020/02/03/172535_70823.png)

在本示例中，第二条命令`$str`将变量的值显示为：`"Welcome2XNTutor"`。

## 3. 修改变量的值

如果要更改变量的值，那么可以重新为变量分配一个新值。

**示例：**

![img](http://www.xntutor.com/uploads/images/2020/02/03/173145_13617.png)

上面屏幕中命令显示`$number`变量的值。

以下屏幕中将更改`$number`变量的值，并显示`$number`变量的新值。
![img](http://www.xntutor.com/uploads/images/2020/02/03/173353_37421.png)

## 4. 删除变量

如果要删除变量的值，可使用`clear-variable` cmdlet，或将变量的值设置为`$null`。

**示例：**

![img](http://www.xntutor.com/uploads/images/2020/02/03/174005_74013.png)

## 5. 变量类型

如果要查看变量的类型，可以使用`GetType()`方法。

![变量类型](http://www.xntutor.com/uploads/images/2020/02/03/174321_72892.png)

## 6. 变量作用域

PowerShell变量可以具有“作用域”，作用域确定了变量在何处可用。 要表示变量的作用域，请使用以下语法：

```shell
$[<scope-modifier>:]<name> = <value>
Shell
```

Windows PowerShell支持变量的以下范围修饰符：

- **全部变量：**全局变量是在任何地方都有效的变量，即使在脚本和函数之外也是如此。要表示全局变量，请使用以下格式：

  ```shell
  $global: variable = <value>
  Shell
  ```

- **局部变量：**可以在本地范围内创建的那些变量。默认情况下，变量具有局部作用域。 要表示局部变量，请使用以下格式：

  ```shell
  $variable = <value>
  Shell
  ```

- **脚本变量：** 在脚本过程中创建的那些变量。 这些变量仅可用于创建它们的脚本。 要表示脚本变量，请使用以下格式：

  ```shell
  $script: variable = <value>
  Shell
  ```

## 7. 变量类型

以下是Windows PowerShell中不同类型的变量：

- 用户创建的变量。
- 自动变量。
- 首选项变量。

**用户创建的变量**

由用户创建和维护的那些变量称为用户创建的变量。在PowerShell命令行中创建的变量仅在PowerShell窗口打开时存在。 关闭PowerShell窗口时，变量也会被删除。 我们可以在具有局部，全局或脚本作用域的脚本中创建变量。

**自动变量**

存储PowerShell状态的那些变量称为自动变量。 PowerShell创建此类型的变量，然后由PowerShell维护(更改)其值以保持其准确性。 用户无法更改这些变量的值。

**首选项变量**

首选项变量是存储Windows PowerShell用户首选项的那些变量。 Windows PowerShell创建这种类型的变量，并使用默认值填充它们。 任何用户都可以更改首选项变量的值。

//更多请阅读：https://www.yiibai.com/powershell/powershell-variables.html 

# (9)Powershell中的内置变量

[![img](https://s3.51cto.com//wyfs02/M00/0C/3A/wKiom1LOArHTlaNsAAAUCODD0gA333_middle.jpg)](https://blog.51cto.com/020618)

[ghcomeon](https://blog.51cto.com/020618)0人评论[11480人阅读](javascript:;)[2016-12-30 23:30:48](javascript:;)

上一节主要介绍了Powershell中变量的定义和使用，以及在变量中包含特殊字符，或是变量在输出时的一些技巧，详细内容参考[这里](http://020618.blog.51cto.com/6098149/1887506)。



**本节介绍Powershell中的内置变量，或是称为自动变量。**

在Powershell命令行中，可以输入 Get-Variable 命令查看Powershell中的所有内置变量

```ps
PS C:\> Get-Variable

Name                           Value
----                           -----
$                              cls
?                              True
^                              cls
_
args                           {}
ConfirmPreference              High
ConsoleFileName
DebugPreference                SilentlyContinue
...
```

------

**下面解释Powershell中经常使用到的内置变量的意思。**

| Powershell内置变量名称 | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| $$                     | 当前会话中收到的最后一行中的最后一个令牌(你可以理解为最后一条执行命令) |
| $?                     | 最后一个操作的执行状态。这个操作可以是Powershell命令，或是调用exe等的返回值，如果最后一个操作成功，则$?包含的值时True,否则包含的值是False。这个内置在判断上一个操作是否成功执行时，非常有用。 |
| $LastExitCode          | 最后一个基于 Windows 的程序的退出代码。注意区分该变量与$?的区别 |
| $True                  | 包含True，可以在命令或脚本中使用此内置变量来代替字符串"TRUE"。 |
| $False                 | 包含False,可以在命令或脚本中使用此内置变量来代替字符串"FALSE"。 |
| $NULL                  | 包含NULL或空值。可以在命令和脚本中使用此变量表示 NULL，而不是使用字符串"NULL"。如果该字符串转换为非空字符串或非零整数，则可将该字符串解释为TRUE。 |
| $_                     | 包含管道对象中的当前对象，在对管道中的对象做筛选或是执行相应的操作命令时，该内置变量尤其有用。如以下命令是筛选所有以 Get-Com 开头的命令Get-Command \| Where-Object {$_.Name -like "Get-Com*"} |
| $This                  | 在定义脚本属性或脚本方法的脚本块中，$This 变量引用要扩展的对象。这个和高级语言中的this一样，表示的是当前要引用的对象。注意该内置变量与$_的不同。 |
|                        |                                                              |
| $PID                   | 当前 Windows PowerShell 会话的进程的进程标识符 (PID)，一个整数表示的数字。 |
| $ShellID               | 当前Shell的标示符，如Microsoft.PowerShell                    |
| $PsUICulture           | 操作系统中当前所用的用户界面 (UI) 区域性的名称(例如，如果是简体中文，则该值是zh-CN)。UI 区域性确定哪些文本字符串用于用户界面元素（如菜单和消息）。这是系统的System.Globalization.CultureInfo.CurrentUICulture.Name 属性的值 |
| $PsCulture             | 操作系统中当前所用的区域性的名称(例如，如果是简体中文，则该值是zh-CN)。区域性确定数字、货币和日期等项的显示格式。这是系统的 System.Globalization.CultureInfo.CurrentCulture.Name 属性的值。 |
|                        |                                                              |
| $PsHome                | Windows PowerShell 的安装目录的完整路径（通常为 %windir%\System32\WindowsPowerShell\v1.0）。可以在 Windows PowerShell 文件的路径中使用此变量。 |
| $Home                  | 用户的主目录的完整路径，等效于 %homedrive%或%homepath% 环境变量 |
| $Pwd                   | 当前目录的完整路径                                           |
| $Host                  | 表示 Windows PowerShell 的当前主机应用程序(通俗点讲就是代表当前主机)。可以使用此变量在命令中表示当前主机，或者显示或更改主机的属性，如 $Host.version、$Host.CurrentCulture 或 $host.ui.rawui.setbackgroundcolor("Red")。 |
| $Profile               | 当前用户和当前主机应用程序的 Windows PowerShell 配置文件的完整路径。可以在命令中使用此变量表示配置文件。 |
|                        |                                                              |
| $PsVersionTable        | 只读哈希表，表示当前运行的Powershell版本的详细信息，该表包含下列项。 CLRVersion：        公共语言运行时 (CLR) 的版本BuildVersion：       当前版本的内部版本号PSVersion：         Windows PowerShell 版本号WSManStackVersion：     WS-Management 堆栈的版本号PSCompatibleVersions：   与当前版本兼容的 Windows PowerShell 版本SerializationVersion ：   序列化方法的版本PSRemotingProtocolVersion : Windows PowerShell 远程管理协议的版本 |

# Windows命令行设置永久环境变量

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[su1322339466](https://blog.csdn.net/su1322339466) 2016-10-31 16:28:38 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 32413 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 9

文章标签： [环境变量](https://www.csdn.net/tags/MtTaEg0sNDY3NzQtYmxvZwO0O0OO0O0O.html)

在cmd窗口中set设置的环境变量为临时变量，如：



```vb
set PATH=%PATH%;D:\Program Files\
```


使用setx设置为永久环境变量,适用于bat中：





```vb
setx PATH "%PATH%;D:\Program Files\"
```

此命令相当于在设置中添加环境变量 加上/m参数则是设置系统的环境变量，并不是设置powershell的首选项变量



### [Windows命令行cmd设置环境变量立即生效和永久生效](http://blog.jues.org.cn/post/windows-ming-ling-xing-cmd-she-zhi-huan-jing-bian-liang-yong-jiu-sheng-xiao.html)

[jues](http://blog.jues.org.cn/author/jues/) 2018-09-13 14:52:27 [Windows](http://blog.jues.org.cn/category-windows.html) 5610 [0](http://blog.jues.org.cn/post/windows-ming-ling-xing-cmd-she-zhi-huan-jing-bian-liang-yong-jiu-sheng-xiao.html#comments)

说明环境变量,大家都知道Windows在DOS窗口使用的set命令;

如下,使用set设置一个环境变量JUES,然后使用echo打印出来为个环境变量;

Bash

```bash
C:\Users\jues>set JUES=http://blog.jues.org.cn

C:\Users\jues>echo %JUES%
http://blog.jues.org.cn

C:\Users\jues>
```



但是以上的环境变量只能在当前的窗口中生效,关闭后再打开新的窗口就失效了;

如果我们需要永远生效该怎么办,当然你可以通过系统设置窗口加上,但是我们关注的重点是用程序实现的,不是吗?



然而我们难道想象到的命令setx这时开始登场,不错就是一个很相似的命令,可以把环境变量永远保存的命令;

**用户环境变量**:

Bash

```bash
C:\Users\jues>setx JUES http://blog.jues.org.cn

成功: 指定的值已得到保存。

C:\Users\jues>
```



然后在**新打开**的窗口中就可以查看到些环境变量值

Bash

```bash
C:\Users\jues>echo %JUES%
http://blog.jues.org.cn

C:\Users\jues>
```



**系统环境变量** 

Bash

```bash
C:\Users\jues>setx /M JUES http://blog.jues.org.cn

成功: 指定的值已得到保存。

C:\Users\jues>
```



**注意: setx命令是Windows Vista以上版本系统才有的,而且要在新窗口中才能查看到设置的结果;所以如果要在本窗口生效,以下才是正确的用法:**

**覆盖值正确用法:**



Bash

```bash
C:\Users\jues>setx /M JUES http://blog.jues.org.cn

成功: 指定的值已得到保存。

C:\Users\jues>set JUES=http://blog.jues.org.cn

C:\Users\jues>
```



**追加值的正确用法:**

Bash

```bash
C:\Users\zhong>set JUES=%JUES%;jues博客

C:\Users\zhong>setx /M JUES %JUES%

成功: 指定的值已得到保存。

C:\Users\zhong>
```



**注意: 如果使用set或echo %var% 打印变量时要注意,如果****用户环境变量** **和 系统环境变量 存在同样的变量时,默认会使用用户环境变量的值;**





setx命令很强大,不然可以设置本地还可以设置远程主机,想要了解更多用法,请查看帮助

Bash

```bash
C:\Users\jues>setx /?

SetX 有三种使用方式:

语法 1:
    SETX [/S system [/U [domain\]user [/P [password]]]] var value [/M]

语法 2:
    SETX [/S system [/U [domain\]user [/P [password]]]] var /K regpath [/M]

语法 3:
    SETX [/S system [/U [domain\]user [/P [password]]]]
         /F file {var {/A x,y | /R x,y string}[/M] | /X} [/D delimiters]

描述:
    在用户或系统环境创建或修改环境变量。能基于参数、注册表项或文件输
    入设置变量。

参数列表:
    /S     system          指定要连接到的远程系统。

    /U     [domain\]user   指定应该在哪个用户上下文执行命令。

    /P     [password]      指定给定用户上下文的密码。如果省略则
                           提示输入。

    var                    指定要设置的环境变量。

    value                  指定分配给环境变量的值。

    /K     regpath         指定变量是基于注册表项的信息而设置的。

                           路径的格式应该是 hive\key\...\value。例如
                           HKEY_LOCAL_MACHINE\System\CurrentControlSet\
                           Control\TimeZoneInformation\StandardName。

    /F     file            指定要使用的文本文件的文件名。

    /A     x,y             指定绝对文件坐标(线 X，项目 Y)作为在此文件
                           里搜索的参数。

    /R     x,y string      指定有关“字符串”作为搜索参数的相对文件坐标。

    /M                     指定应该在系统 (HKEY_LOCAL_MACHINE) 环境中设
                           置此变量。在 HKEY_CURRENT_USER 环境下，默认
                           将设置此变量。

    /X                     用 x，y 坐标显示文件内容。

    /D     delimiters      指定其他限定符，如 "," 或 "\"。
                           内置分隔符是空格、制表符、回车和换行符。所有
                           ASCII 字符都可作为限定符。限定符的最大数量，
                           包括内置分隔符，是 15。

    /?                     显示此帮助消息。

注意: 1) SETX 在注册表中将变量写入主机环境。

      2) 在本地系统，用此工具创建或修改的变量将在以后的命令窗口可用，但
         在当前的 CMD.exe 命令窗口。

      3) 在远程系统，用此工具创建或修改的变量在下次登录会话可用。

      4) 有效的注册表项数据类型是 REG_DWORD，REG_EXPAND_SZ，REG_SZ
         和 REG_MULTI_SZ。

      5) 受支持的配置单元:  HKEY_LOCAL_MACHINE (HKLM)，
         HKEY_CURRENT_USER (HKCU)。

      6) 限定符区分大小写。

      7) REG_DWORD 的值是从注册表里以十进制格式提取出来的。

示例:
    SETX MACHINE COMPAQ
    SETX MACHINE "COMPAQ COMPUTER" /M
    SETX MYPATH "%PATH%"
    SETX MYPATH ~PATH~
    SETX /S system /U user /P password  MACHINE COMPAQ
    SETX /S system /U user /P password MYPATH ^%PATH^%
    SETX TZONE /K HKEY_LOCAL_MACHINE\System\CurrentControlSet\
         Control\TimeZoneInformation\StandardName
    SETX BUILD /K "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows
         NT\CurrentVersion\CurrentBuildNumber" /M
    SETX /S system /U user /P password TZONE /K HKEY_LOCAL_MACHINE\
         System\CurrentControlSet\Control\TimeZoneInformation\
         StandardName
    SETX /S system /U user /P password  BUILD /K
         "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\
         CurrentVersion\CurrentBuildNumber" /M
    SETX /F ipconfig.out /X
    SETX IPADDR /F ipconfig.out /A 5,11
    SETX OCTET1 /F ipconfig.out /A 5,3 /D "#$*."
    SETX IPGATEWAY /F ipconfig.out /R 0,7 Gateway
    SETX /S system /U user /P password  /F c:\ipconfig.out /X

C:\Users\jues>
```

