# Windows Linux子系统Windows 10安装指南

- 2020/09/15
- 10分钟阅读
- - [![img](https://github.com/craigloewen-msft.png?size=32)](https://github.com/craigloewen-msft)
  - [![img](https://github.com/mattwojo.png?size=32)](https://github.com/mattwojo)
  - [![img](https://github.com/ElmarJ.png?size=32)](https://github.com/ElmarJ)
  - [![img](https://github.com/benhillis.png?size=32)](https://github.com/benhillis)
  - [![img](https://github.com/DCtheGeek.png?size=32)](https://github.com/DCtheGeek)
  - 

有两个选项可用于安装Linux的Windows子系统（WSL）：

- **[简化安装](https://docs.microsoft.com/en-us/windows/wsl/install-win10#simplified-installation-for-windows-insiders)** *（预览版）*：`wsl --install`

  该`wsl --install`简化的安装命令要求您加入[的Windows业内人士程序](https://insider.windows.com/getting-started)并安装Windows 10（OS构建20262或更高）的预览构建，但无需按照手册安装步骤。您需要做的就是打开一个具有管理员权限的命令窗口，然后运行`wsl --install`，重新启动后即可使用WSL。

- **[手动安装](https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps)**：请按照以下六个步骤进行操作。

  下面列出了WSL的手动安装步骤，可用于在Windows 10的任何版本上安装Linux。

## Windows Insiders的简化安装

在Windows 10的最新Windows Insiders预览版本中，用于Linux的Windows子系统的安装过程已得到显着改进，用单个命令替换了下面的手动步骤。

为了使用`wsl --install`简化的安装命令，您必须：

- 加入[Windows Insiders计划](https://insider.windows.com/getting-started)
- 安装Windows 10的预览版本（操作系统内部版本20262或更高版本）。
- 使用管理员权限打开命令行窗口

满足这些要求后，安装WSL：

- 在以管理员方式打开的命令行中输入以下命令： `wsl.exe --install`
- 重新启动机器

首次启动新安装的Linux发行版时，将打开一个控制台窗口，并要求您等待文件解压缩并存储在PC上。以后所有的发射都将花费不到一秒钟的时间。

然后，您需要[为新的Linux发行版创建一个用户帐户和密码](https://docs.microsoft.com/en-us/windows/wsl/user-support)。

**恭喜！您已经成功安装并设置了与Windows操作系统完全集成的Linux发行版！**

--install命令执行以下操作：

- 启用可选的WSL和虚拟机平台组件
- 下载并安装最新的Linux内核
- 将WSL 2设置为默认值
- 下载并安装Linux发行版*（可能需要重新启动）*

默认情况下，已安装的Linux发行版将是Ubuntu。可以使用更改`wsl --install -d <Distribution Name>`。*（替换`<Distribution Name>`为所需发行版的名称。）*在首次安装后，可以使用以下`wsl --install -d <Distribution Name>`命令将其他Linux发行版添加到您的计算机中。

要查看可用的Linux发行版列表，请输入`wsl --list --online`。

## 手动安装步骤

如果您不在Windows Insiders构建中，则需要按照以下步骤手动启用WSL所需的功能。

## 步骤1-为Linux启用Windows子系统

在Windows上安装任何Linux发行版之前，必须首先启用“ Linux的Windows子系统”可选功能。

以管理员身份打开PowerShell并运行：

电源外壳复制

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

我们建议现在转到第2步，更新为WSL 2，但是如果您只想安装WSL 1，则现在可以**重新启动**计算机并转到[第6步-安装您选择的Linux发行版](https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-6---install-your-linux-distribution-of-choice)。要更新到WSL 2，请**等待重新启动**计算机，然后继续下一步。

## 步骤2-检查运行WSL 2的要求

要更新到WSL 2，您必须正在运行Windows 10。

- 对于x64系统：**版本1903**或更高版本，以及**内部版本18362**或更高版本。
- 对于ARM64系统：**2004**或更高版本，**内部****版本**19041或更高。
- 低于18362的内部版本不支持WSL2。使用[Windows Update Assistant](https://www.microsoft.com/software-download/windows10)来更新Windows版本。

要检查您的版本和内部版本号，请选择**Windows徽标键+ R**，键入**winver**，然后选择**确定**。（或`ver`在Windows命令提示符中输入命令）。在“设置”菜单中[更新为最新的Windows版本](ms-settings:windowsupdate)。

 注意

如果您运行的是Windows 10版本1903或1909，请从Windows菜单中打开“设置”，导航至“更新和安全”，然后选择“检查更新”。您的内部版本号必须为18362.1049+或18363.1049+，且内部版本号为.1049以上。阅读更多：[Windows 10版本1903和1909即将提供WSL 2支持](https://devblogs.microsoft.com/commandline/wsl-2-support-is-coming-to-windows-10-versions-1903-and-1909/)。请参阅[故障排除说明](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#im-on-windows-10-version-1903-and-i-still-do-not-see-options-for-wsl-2)。

## 步骤3-启用虚拟机功能

在安装WSL 2之前，必须启用**虚拟机平台**可选功能。您的计算机将需要[虚拟化功能](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed)才能使用此功能。

以管理员身份打开PowerShell并运行：

电源外壳复制

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**重新启动**计算机以完成WSL安装并更新到WSL 2。

## 步骤4-下载Linux内核更新程序包

1. 下载最新的软件包：

   - [用于x64机器的WSL2 Linux内核更新程序包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

    注意

   如果您使用的是ARM64计算机，请改为下载[ARM64软件包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)。如果不确定所用的机器类型，请打开“命令提示符”或“ PowerShell”并输入：`systeminfo | find "System Type"`。

2. 运行在上一步中下载的更新程序包。（双击运行-系统将提示您提升权限，选择“是”以批准此安装。）

安装完成后，继续下一步-在安装新的Linux发行版时将WSL 2设置为默认版本。（如果要将新的Linux安装设置为WSL 1，请跳过此步骤）。

 注意

有关更多信息，请阅读[Windows命令行博客](https://aka.ms/cliblog)上有关[更新WSL2 Linux内核](https://devblogs.microsoft.com/commandline/wsl2-will-be-generally-available-in-windows-10-version-2004)的文章[更改](https://devblogs.microsoft.com/commandline/wsl2-will-be-generally-available-in-windows-10-version-2004)。

## 步骤5-将WSL 2设置为默认版本

打开PowerShell并运行以下命令，以在安装新的Linux发行版时将WSL 2设置为默认版本：

电源外壳复制

```powershell
wsl --set-default-version 2
```

## 第6步-安装您选择的Linux发行版

1. 打开[Microsoft商店，](https://aka.ms/wslstore)然后选择您喜欢的Linux发行版。

   ![Microsoft Store中Linux发行版的视图](https://docs.microsoft.com/en-us/windows/wsl/media/store.png)

   以下链接将打开每个发行版的Microsoft商店页面：

   - [Ubuntu 16.04 LTS](https://www.microsoft.com/store/apps/9pjn388hp8c9)
   - [Ubuntu 18.04 LTS](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
   - [Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)
   - [openSUSE Leap 15.1](https://www.microsoft.com/store/apps/9NJFZK00FGKV)
   - [SUSE Linux Enterprise Server 12 SP5](https://www.microsoft.com/store/apps/9MZ3D1TRP8T1)
   - [SUSE Linux Enterprise Server 15 SP1](https://www.microsoft.com/store/apps/9PN498VPMF3Z)
   - [卡利Linux](https://www.microsoft.com/store/apps/9PKR34TNCV07)
   - [Debian GNU / Linux](https://www.microsoft.com/store/apps/9MSVKQC78PK6)
   - [Fedora Remix for WSL](https://www.microsoft.com/store/apps/9n6gdm4k2hnc)
   - [彭文](https://www.microsoft.com/store/apps/9NV1GV1PXZ6P)
   - [鹏运企业](https://www.microsoft.com/store/apps/9N8LP0X93VCP)
   - [高山WSL](https://www.microsoft.com/store/apps/9p804crf0395)

2. 在发行版页面中，选择“获取”。

   ![Microsoft商店中的Linux发行版](https://docs.microsoft.com/en-us/windows/wsl/media/ubuntustore.png)

首次启动新安装的Linux发行版时，将打开一个控制台窗口，并且将要求您等待一两分钟以将文件解压缩并存储在PC上。以后所有的发射都将花费不到一秒钟的时间。

然后，您需要[为新的Linux发行版创建一个用户帐户和密码](https://docs.microsoft.com/en-us/windows/wsl/user-support)。

![Windows控制台中的Ubuntu解压缩](https://docs.microsoft.com/en-us/windows/wsl/media/ubuntuinstall.png)

**恭喜！您已经成功安装并设置了与Windows操作系统完全集成的Linux发行版！**

## 安装Windows Terminal（可选）

Windows Terminal启用多个选项卡（在多个Linux命令行，Windows命令提示符，PowerShell，Azure CLI等之间快速切换），创建自定义键绑定（用于打开或关闭选项卡的快捷键，复制+粘贴等），使用搜索功能和自定义主题（配色方案，字体样式和大小，背景图片/模糊/透明度）。[了解更多。](https://docs.microsoft.com/en-us/windows/terminal)

[安装Windows Terminal](https://docs.microsoft.com/en-us/windows/terminal/get-started)。

![Windows终端](https://docs.microsoft.com/en-us/windows/wsl/media/terminal.png)

## 将发行版本设置为WSL 1或WSL 2

您可以通过打开PowerShell命令行并输入命令来检查分配给已安装的每个Linux发行版的WSL版本（仅在[Windows Build 18362或更高版本中](ms-settings:windowsupdate)可用）：`wsl -l -v`

电源外壳复制

```powershell
wsl --list --verbose
```

要将发行版设置为由任一版本的WSL支持，请运行：

电源外壳复制

```powershell
wsl --set-version <distribution name> <versionNumber>
```

确保`<distribution name>`用发行版的实际名称和`<versionNumber>`数字“ 1”或“ 2”代替。您可以随时通过运行与上面相同的命令将其替换为WSL 1，但将“ 2”替换为“ 1”。

 注意

从WSL 1到WSL 2的更新可能需要几分钟才能完成，具体取决于目标发行版的大小。如果您正在从Windows 10周年更新或创建者更新中运行WSL 1的较旧（旧版）安装，则可能会遇到更新错误。请按照以下说明[卸载和删除所有旧发行版](https://docs.microsoft.com/en-us/windows/wsl/install-legacy#uninstallingremoving-the-legacy-distro)。

如果`wsl --set-default-version`结果为无效命令，请输入`wsl --help`。如果`--set-default-version`未列出，则表明您的操作系统不支持它，您需要更新到版本1903，内部版本18362或更高版本。

如果在运行命令后看到此消息：`WSL 2 requires an update to its kernel component. For information please visit https://aka.ms/wsl2kernel`。您仍然需要安装MSI Linux内核更新程序包。

另外，如果要将WSL 2设置为默认体系结构，则可以使用以下命令：

电源外壳复制

```powershell
wsl --set-default-version 2
```

这将设置安装到WSL 2的任何新发行版的版本。

## 安装疑难解答

以下是相关的错误和建议的修复程序。有关其他常见错误及其解决方案，请参阅[WSL故障排除页面](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting)。

- **安装失败，错误0x80070003**
  - Linux的Windows子系统仅在系统驱动器上运行（通常是您的`C:`驱动器）。确保分发存储在系统驱动器上：
  - 打开**设置**-> **系统->**存储**->**更多存储设置：更改新内容的保存位置** ![在C：驱动器上安装应用程序的系统设置图片](https://docs.microsoft.com/en-us/windows/wsl/media/appstorage.png)
- **WslRegisterDistribution失败，错误为0x8007019e**
  - 未启用Windows Subsystem for Linux可选组件：
  - 打开**控制面板**->**程序和功能**->**打开或关闭Windows功能**->检查**Linux的Windows子系统，**或使用本文开头提到的PowerShell cmdlet。
- **安装失败，错误0x80070003或错误0x80370102**
  - 请确保在计算机的BIOS中启用了虚拟化。有关如何执行此操作的说明因计算机而异，并且很可能在与CPU相关的选项下。
- **尝试升级时出错： `Invalid command line option: wsl --set-version Ubuntu 2`**
  - 确保已启用Linux的Windows子系统，并且您使用的是Windows Build 18362版或更高版本。要启用WSL，请在具有管理员权限的PowerShell提示符下运行此命令：`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`。
- **由于虚拟磁盘系统限制，请求的操作无法完成。虚拟硬盘文件必须是未压缩和未加密的，并且不能稀疏。**
  - 通过打开Linux发行版的配置文件文件夹，取消选择“压缩内容”（以及选中“加密内容”）。它应该位于Windows文件系统上的文件夹中，例如：`USERPROFILE%\AppData\Local\Packages\CanonicalGroupLimited...`
  - 在此Linux发行配置文件中，应该有一个LocalState文件夹。右键单击此文件夹以显示选项菜单。选择“属性”>“高级”，然后确保未选中“压缩内容以节省磁盘空间”和“加密内容以保护数据”复选框（未选中）。如果系统询问您将其仅应用于当前文件夹还是所有子文件夹和文件，请选择“仅此文件夹”，因为您仅清除了compress标志。此后，该`wsl --set-version`命令应起作用。

![WSL发行版属性设置的屏幕截图](https://docs.microsoft.com/en-us/windows/wsl/media/troubleshooting-virtualdisk-compress.png)

 注意

就我而言，我的Ubuntu 18.04发行版的LocalState文件夹位于C：\ Users <我的用户名> \ AppData \ Local \ Packages \ CanonicalGroupLimited.Ubuntu18.04onWindows_79rhkp1fndgsc

检查[WSL Docs GitHub线程＃4103](https://github.com/microsoft/WSL/issues/4103)，在该[线程](https://github.com/microsoft/WSL/issues/4103)中已跟踪此问题以获取更新的信息。

- **术语“ wsl”不被视为cmdlet，函数，脚本文件或可运行程序的名称。**

  - 确保[已安装Windows子系统（用于Linux的可选组件）](https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-3---enable-virtual-machine-feature)。此外，如果您使用的是ARM64设备并通过PowerShell运行此命令，则会收到此错误。而是`wsl.exe`从[PowerShell Core](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-windows)或命令提示符运行。

- **错误：此更新仅适用于装有Windows子系统（用于Linux）的计算机。**

  - 要安装Linux内核更新MSI软件包，WSL是必需的，应首先启用。如果失败，您将看到消息：`This update only applies to machines with the Windows Subsystem for Linux`。
  - 您看到此消息的三个可能原因：

  1. 您仍处于不支持WSL 2的Windows旧版本中。有关版本要求和更新链接，请参阅步骤2。
  2. 未启用WSL。您将需要返回到步骤1，并确保在计算机上启用了可选的WSL功能。
  3. 启用WSL后，需要重新启动才能生效，重新启动计算机，然后重试。

- **错误：WSL 2需要对其内核组件进行更新。有关信息，请访问https://aka.ms/wsl2kernel。**

  - 如果％SystemRoot％\ system32 \ lxss \ tools文件夹中缺少Linux内核软件包，则将遇到此错误。通过在这些安装说明的步骤4中安装Linux内核更新MSI软件包来解决该问题。您可能需要从[“添加或删除程序”中](ms-settings:appsfeatures-app)卸载MSI ，然后重新安装。