# [powershell创建并加载配置文件](https://www.cnblogs.com/dreamer-fish/p/3738513.html)

$pshome ：powershell的主目录

$profile ：显示 Windows PowerShell 配置文件的路径

test-path $profile ：确定是否已经在系统上创建了 Windows PowerShell 配置文件


powershell.exe 主机配置文件（在 Windows Vista 中）的位置如下所示：
**%windir%\system32\Windows­PowerShell\v1.0\profile.ps1** 用于计算机的所有用户和所有外壳。
**%windir%\system32\Windows­PowerShell\v1.0\Microsoft.Power­Shell_profile.ps1** 用于计算机的所有用户，但仅用于 Microsoft.PowerShell 外壳。
**%UserProfile%\Documents\Windows­PowerShell\profile.ps1** 仅用于当前用户和所有外壳。
**%UserProfile%\Documents\WindowsPowerShell\Micro­soft.PowerShell_profile.ps1** 仅用于当前用户和 Microsoft.PowerShell 外壳。


启动时按顺序加载，最后一个优先级最高，会覆盖之前的配置文件
这些配置文件并不是在默认情况下创建的。必须在您手动创建后，它们才会出现。

例，创建适用于所有用户和所有 shell 的配置文件，键入：
new-item -path $env:windir\System32\WindowsPowerShell\v1.0\profile.ps1 -itemtype file -force
notepad $env:windir\System32\WindowsPowerShell\v1.0\profile.ps1
如输入：
c:
cd c:\
function pp
{
write-host "ppc"
}
编辑后保存，然后再重新运行powershell.exe，会加载profile.ps1中的内容，在启动后会自动跳转到C:路径下，还会自动加载函数 pp

 

==============================================

创建自定义控制台

要创建自定义控制台，首先应查找要处理的每个管理单元的全名。确保所有必需的管理工具都已安装在计算机中。然后，在 Windows PowerShell 中运行 Get-PSSnapin –registered。这将列出所有已注册但却未加载的可用管理单元。然后创建或编辑相应的 Windows Power­Shell 配置文件。添加 Add-PS­Snapin 命令，加载希望始终可用的每个管理单元。这可能包括用于 Exchange Server、System Center 产品以及第三方管理单元（如 Power­Shell Community Extensions）的管理单元。然后保存配置文件（请记住，如果 Windows Power­Shell 执行策略需要，则对配置文件进行数字签名）并关闭外壳。重新打开外壳，它会自动加载配置文件中列出的所有管理单元。

另一种技术是将所有管理单元加载到外壳中（使用 Add-PSSnapin 和管理单元的名称），然后运行 Export-Console 创建一个 .psc1 控制台文件，其中包含当前正在使用的所有管理单元。然后，可使用这一 .psc1 控制台文件创建一个新的 Windows PowerShell 快捷方式，以指定 PSConsole­File 参数和自定义的 .psc1 文件。该快捷方式随后会使用您的控制台，并自动加载所有指定的管理单元。

分类: [PowerShell](https://www.cnblogs.com/dreamer-fish/category/444520.html)