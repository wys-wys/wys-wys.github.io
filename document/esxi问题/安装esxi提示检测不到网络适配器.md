[VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁](https://www.vediotalk.com/archives/12070)

2020.04.03 [VLOG](https://www.vediotalk.com/archives/category/feature) 67  [30 ](https://www.vediotalk.com/archives/12070#comments) 44964 

目录



[视频简介](https://www.vediotalk.com/archives/12070#视频简介)[一、下载ESXI6.7-7.0最新版本的离线包](https://www.vediotalk.com/archives/12070#一、下载ESXI6_77_0最新版本的离线包)[二、下载ESXi-Customizer-PS最新版本](https://www.vediotalk.com/archives/12070#二、下载ESXiCustomizerPS最新版本)[三、下载需要的驱动](https://www.vediotalk.com/archives/12070#三、下载需要的驱动)[四、开始打驱动补丁及封装](https://www.vediotalk.com/archives/12070#四、开始打驱动补丁及封装)

收藏 29

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/04/feretewt1-1.jpg)](https://www.vediotalk.com/wp-content/uploads/2020/04/feretewt1-1.jpg)

<iframe title="ESXI6.7-7.0最新版本如何封装网卡驱动补丁" width="500" height="281" src="https://www.youtube.com/embed/PA3OGBFmAiU?feature=oembed" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="-webkit-tap-highlight-color: transparent; box-sizing: border-box; border: none; display: block; max-width: 100%; margin: 12px auto;"></iframe>

[国内播放节点](https://www.ixigua.com/i6811350475229626894/?logTag=d7srEOQpIBYmX9ZIDGzZ-)

#### 视频简介

借着ESXI发布了最新版本7.0，这边再教大家用最新的方法来封装网卡驱动，让你的老设备也可以安装ESXI最新版本。

------

## 一、下载ESXI6.7-7.0最新版本的离线包

[本站下载 ESXU6.7 U3b离线包](https://veelove.i234.me:5001/d/f/542065659568238687)

[本站下载 ESXU7.0离线包](https://veelove.i234.me:5001/d/f/546336012404568091)

1.登录官网注册账号：[https://www.vmware.com](https://www.vmware.com/sg.html)

2.登录后点击回到首页

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.02.02-1024x293.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.02.02-1024x293.png)

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.02.37-1024x265.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.02.37-1024x265.png)

3.点击下载

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.04.04-1024x421.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.04.04-1024x421.png)

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.05.57-1024x687.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.05.57-1024x687.png)

4.下载最新的离线包

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.07.32-1024x770.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.07.32-1024x770.png)

## 二、下载ESXi-Customizer-PS最新版本

官网下载：https://www.v-front.de/p/esxi-customizer-ps.html

本站下载ESXi-Customizer-PS

## 三、下载需要的驱动

下载地址：https://vibsdepot.v-front.de/wiki/index.php/List_of_currently_available_ESXi_packages

这里以Realtek8111的驱动为例

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.32.56-1024x870.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.32.56-1024x870.png)

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%888.33.30-1024x447.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午8.33.30-1024x447.png)

## 四、开始打驱动补丁及封装

1.需要一个win10的系统

2.以管理员身份打开windows PowerShell，安装依赖

```
Install-Module -Name VMware.PowerCLI
```

3.调整PowerShell的执行策略来让脚本可以正常运行。默认的执行策略是无法运行这个脚本的。

```
Set-ExecutionPolicy Unrestricted
```

4.开始打驱动补丁并自动封装为ISO

```
.\ESXi-Customizer-PS-v2.6.0.ps1 -izip .\ESXi670-201912001.zip -pkgDir C:\Users\vee\Desktop\nic\pkg

ESXi-Customizer-PS-v2.6.0.ps1：为最新的工具命令
ESXi670-201912001.zip：为最新的ESXI6.7的离线包
C:\Users\vee\Desktop\nic\pkg：为VIB驱动的路径
```

[![VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 – Vedio Talk - VLOG、科技、生活、乐分享](https://www.vediotalk.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-10%E4%B8%8B%E5%8D%889.58.19-1024x868.png)](https://www.vediotalk.com/wp-content/uploads/2020/03/截屏2020-03-10下午9.58.19-1024x868.png)

转载原创文章请注明，转载自: [Vedio Talk ](https://www.vediotalk.com/)- [VLOG | ESXI6.7-7.0最新版本如何封装网卡驱动补丁 ](https://www.vediotalk.com/archives/12070)(https://www.vediotalk.com/archives/12070)

[67](javascript:;)