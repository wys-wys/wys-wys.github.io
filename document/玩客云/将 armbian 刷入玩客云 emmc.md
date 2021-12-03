## 将 armbian 刷入玩客云 emmc

 发表于 2019-12-16  更新于 2020-03-07  分类于 [硬件 ](https://7th-heaven.me/categories/硬件/)， [嵌入式 ](https://7th-heaven.me/categories/硬件/嵌入式/) 阅读次数： 8563
 本文字数： 5.9k  阅读时长 ≈ 5 分钟

玩客云使用的主板是晶晨 s805，而晶晨 s805 开发板单买很贵。此刻玩客云挖矿已经凉了，而将玩客云刷成 linux 后，就可以有无限的可能。由于目前刷 linux 的方法刚有人成功，在某宝、某东和并夕夕平台仍然只要 40 块，加上一张 32g 的 tf 卡，成本 60 块左右就能有一个四线程的 linux 开发板。

目前还没有人来分享一个比较详细的、猴子都能学会的教程，所以我觉得我有必要写一个，我们开始。



# 所需工具

## 硬件工具

### 1. 双公头 usb 线

### 2.usb 转 ttl 线及四条公对母杜邦线

### 3. 十字螺丝刀

### 4.hdmi 视频线

### 5.hdmi 口显示器

### 6.sd 卡或 TF 卡加卡套、读卡器

### 7. 电烙笔

### 8.（可选）美工刀、一字螺丝刀

## 软件工具

### 1. 晶晨 s805 刷机工具

### 2.USBWriter

### 3.putty

### 3.s805 通用安卓镜像 update.img

### 4. 支持玩客云有线网卡驱动 dtb 文件

### 5. 支持 s805 的 armbian 系统镜像

### 6. 支持玩客云有线网卡驱动 u-boot.bin

### 7.fstab 及 install.sh 文件

1-4 软件下载地址：

https://pan.baidu.com/s/1Jz8MCUwHfYsm-whp2-zYZg 密码：qnys

5 软件下载地址：

https://yadi.sk/d/DnCkh3KBvAFES/Linux/Armbian/5.67/20181207

下载 Armbian_5.67_Aml-s805_Debian_stretch_default_3.10.108_20181207.img.xz 即可，没必要下载带桌面的，本身硬件配置不高，装桌面占内存和 cpu。下载完后可以使用 7z 等解压工具解压得到 img 镜像文件。

6-7 软件下载地址（需魔法上网）：

https://mega.nz/#F!IDQjTahb!0hw34e9BZru4ap3AlMkEwQ

# 刷机步骤：

## 1. 拆机

使用美工刀和一字螺丝刀撬开玩客云屁股后面的塑料板，直接大力出奇迹即可，塑料板是用双面胶粘帖的。取下后再用十字螺丝刀拧下 6 颗螺丝来拆下塑料盖，最后拔出玩客云主板。

## 2. 获取开机时 uboot 的控制权

这样可以设置从 tf 卡启动。玩客云官方系统屏蔽了开机的 uboot 控制，所以第一步是夺取 uboot 控制权。

安装晶晨 s805 刷机工具（注意使用文件夹里的破解）、putty。

usb 转 ttl 线注意点：如果转接板支持 vcc 切换，要记得将拨片拨到 3.3v，因为玩客云主板上 ttl 线刷 vcc 电压是 3.3v 的。

![usb转ttl线](https://7th-heaven.me/images/usb_to_ttl.png)

玩客云主板常见的有两种，一种是 1.2 版本的，一种是 1.3 版本的。这两种版本都可以刷，但是短接的地方不同

### 1.2 主板

背面短接点

![1.2版本玩客云主板短接](https://7th-heaven.me/images/1.2_board.png)

正面 ttl 线刷针脚

![1.2版本正面ttl线刷针脚](https://7th-heaven.me/images/1.2_board_pin.png)

### 1.3 主板

正面短接点

![1.3版本玩客云主板短接](https://7th-heaven.me/images/1.3_board.png)

正面 ttl 线刷针脚

![1.3版本正面ttl针脚](https://7th-heaven.me/images/1.3_board_pin.png)

1.2 主板的 ttl 针脚在主板上没有标注，但是可以直接插转接板的杜邦线。1.3 主板的 ttl 针脚在主板上有直接标注，但出厂时已被焊上锡，刷机前需要先使用电烙笔拆焊。

转接板接线到玩客云主板方法：转接板 TX 接玩客云主板 RX，转接板 RX 接玩客云主板 TX，转接板 3.3v VCC 接玩客云主板 VCC，转接板 GND 接玩客云主板 GND。

将转接板和玩客云接好后，将转接板的 usb 一端插入电脑 usb 口。

使用公对公 usb 线，一头插入电脑，一头插到玩客云**靠近 HDMI 接口的那个 usb 口**。注意一定要插到这个 usb 口，如果错了线刷工具将无法认出设备。

![双公头usb线](https://7th-heaven.me/images/usb.png)

这时候玩客云主板仍然不要接电源

在 “我的电脑” 上右键 -》管理，打开设备管理器。找到 COM 口设备，双击切换到 “端口设置” 选项卡按如下设置：

![设备管理器](https://7th-heaven.me/images/device_manager.png)

![com设置](https://7th-heaven.me/images/com_settings.png)

打开 putty，按如下设置：

![putty设置](https://7th-heaven.me/images/putty_settings.png)

![putty设置2](https://7th-heaven.me/images/putty_settings2.png)

然后点击 Open 按钮，此时 putty 将打开一个黑窗口，屏幕上没有输出。

打开线刷工具，按上面所说的短接点，使用导线短接玩客云上两个点不动，同时插上玩客云的电源。操作正确的话，线刷工具界面上会出现连接成功字样，此时就可以将短接的线松开。

![进入线刷模式时烧录工具](https://7th-heaven.me/images/burn_tool.png)

连接成功时，这时 putty 界面也会有输出：

![进入线刷模式putty输出](https://7th-heaven.me/images/putty_output.png)

点击上图线刷工具界面菜单的 “文件”-》导入烧录包，选择之前下载的安卓通用刷机包 update.img，然后勾选 “擦除 flash”、“擦除 bootloader”

![烧写前最后一步](https://7th-heaven.me/images/last_step_before_burning.png)

确认后，点击开始按钮刷机，刷机成功后显示如下

![烧录成功](https://7th-heaven.me/images/brun_success.png)

此时 putty 也会显示如下：

![烧录成功putty](https://7th-heaven.me/images/brun_success_putty.png)

这里提醒下，很多人会出现这种情况，刷机工具报错：

![使用win10的人常见烧写失败情况](https://7th-heaven.me/images/burn_failed.png)

出现这种情况的原因不是因为什么人品、运气，它是因为刷机工具准备刷机会先卸载玩客云主板，然后重新加载 usb 设备时，被你系统的杀毒软件抢先拦截。解决方法也不是什么换电脑、换系统、换 usb 线，就是关掉所有杀毒软件。还有在装刷机工具的时候，安装程序会安装 usb 驱动，如果被拦截也是无法检测到 usb 设备的。所以在刷机过程最好全程关闭杀毒软件。

此时新的 uboot 已经刷入，拔掉玩客云电源，关闭线刷工具，putty 不要关。

## 3. 将 armbian 镜像刷入 tf 卡

使用 USBWriter.exe 将 Armbian_5.67_Aml-s805_Debian_stretch_default_3.10.108_20181207.img 烧录到 tf 卡。推荐使用 SandDisk 的 A1 TF 卡，这也是 armbian 团队推荐的 tf 卡牌子，兼顾兼容性、速度和成本。最好别搞一些来历不明很便宜的山寨卡，某宝上太多了，如果因为卡的问题出现各种莫名其妙的错误就得不偿失，会浪费很多时间。

将下载的 meson8b_m201_1G.dtb 文件覆盖到 tf 卡根目录下的 dtb 目录下同名文件，其他目录的同名文件不管。

将下载的 u-boot.bin 文件拷贝到 tf 卡根目录下。

将下载的 fstab 和 install.sh 文件拷贝到 tf 卡根目录下。

## 4. 更新支持有线网卡的 uboot

玩客云的千兆有线网卡很怪，原生 armbian 暂不识别，需要刷一个新的支持网卡的 uboot

给玩客云主板插上 tf 卡，重新插上玩客云电源，然后立刻快速不停地按键盘的回车键，大概有 3 秒的机会，错过了拔电源重新上电再试。

成功后 putty 上显示如下：

![开机按enter进入uboot](https://7th-heaven.me/images/enter_uboot.png)

此时可以使用键盘输入了，输入以下代码来更新支持有线网卡的 uboot：

```
mmcinfo;fatload mmc 0 12000000 u-boot.bin
store rom_write 12000000 0 60000
saveenv
```

成功后会显示如下：

![烧入支持网卡的uboot](https://7th-heaven.me/images/burn_uboot.png)

拔掉玩客云电源

## 5. 设置 uboot 让主板从 tf 卡启动 armbian 系统

重新插上玩客云电源，快速按回车键，在 putty 中断后，输入如下命令来设置 uboot 从 tf 卡启动：

```
setenv bootfromrecovery 0
setenv bootfromnand 0
setenv start_mmc_autoscript 'if fatload mmc 0 11000000 s805_autoscript; then autoscr 11000000; fi;'
setenv start_usb_autoscript "if fatload usb 0 11000000 s805_autoscript; then autoscr 11000000; fi; if fatload usb 1 11000000 s805_autoscript; then autoscr 11000000; fi;"

setenv start_autoscript 'if mmcinfo; then run start_mmc_autoscript; fi; if usb start; then run start_usb_autoscript; fi;'
setenv bootcmd 'run start_autoscript; run storeboot'
saveenv
```

拔掉玩客云电源

## 6. 将 armbian 系统刷入玩客云 EMMC

现在**将玩客云上的公头 usb 线和刷机 ttl 杜邦线都拔下来**，如果你把它们留在上面，继续下面步骤玩客云开机画面会停在 s805 的 logo 那里不动了。

将玩客云用 HDMI 视频线接到显示器上，再把网线接上。注意网线最好用玩客云自带的，我尝试出现了自己做的可以用的网线玩客云却不识别的问题。

将键盘接在**远离 HDMI 接口的那个 usb 口**上，如果接在靠近 HDMI 口的那个 usb，开机可能会卡在 s805 的 logo 那里不动了。

现在插上玩客云电源，此时玩客云上接的东西有：网线、HDMI 线、电源线、键盘、tf 卡，其余不要接任何东西。

开机后经过一段时间的等待，会出现 armbian 系统的登录，让你换密码，先换成 12345678 方便操作。armbian 对密码复杂度还有一些简单的限制，不过 12345678 就可以，为方便操作，先改成这个密码，后面自己再换。

进入系统后，如果正常的话，此时应该玩客云已经获取了 ip，会打印出来

![成功启动tf卡上系统](https://7th-heaven.me/images/boot_from_tf_card.png)

此时先别急着配置系统，先把系统装到 EMMC 上，然后就可以随心设置了。

使用 su 命令切换到 root 用户，***以下命令都使用 root 身份执行\***

先删掉之前更新用的 u-boot.bin，现在不需要了，删掉节省空间。

```
rm -f /boot/u-boot.bin
```

将 fstab 和 install.sh 文件移动到 /root/ 目录，并给予权限

```
mv /boot/fstab /root/
mv /boot/install.sh /root/
chmod 755 /root/fstab
chmod 755 /root/install.sh
```

在进一步执行安装脚本前，我们需要安装 abootimg 这个依赖的软件包，使用如下命令安装：

```
apt-get install -y abootimg
```

如果网络正常的话，就安装了这个软件

下面正式开始将 armbian 系统从 tf 卡装到 EMMC，使用如下命令：

```
/root/install.sh
```

如果操作正确的话，此时安静等待，文件拷贝需要一阵子，不要断开电源，拷贝 /usr 目录的时候会时间比较长点。

执行完成后如果没有显示什么错误的话，说明成功了，此时输入以下命令安全关闭系统：

```
halt -p
```

等待系统完全关闭后，拔下玩客云电源，拔下 tf 卡。重新插上玩客云电源，此时如果没有问题的话，armbian 将直接从玩客云主板的 EMMC 上启动。此时 tf 卡已经使用完毕，可以格掉当玩客云的扩展硬盘，或者可以重新拷入 u-boot.bin、fstab、install.sh 文件来再刷下一个玩客云。

## 7.（可选）设置 uboot 直接从 EMMC 启动

经过之前 6 步，现在如果不插 tf 卡，那么玩客云就从 EMMC 启动了，如果插上 tf 卡，则玩客云就从 tf 卡启动，相当于一个双系统。但是我不需要双系统，我想把系统装在 EMMC，然后 tf 卡用来存东西。目前开机如果 tf 卡插在玩客云上，系统还是会从 tf 卡启动。我想玩客云忽略 tf 卡直接从 EMMC 启动，这样一来我不需要双系统（趁玩客云便宜，我屯了 N 个玩客云，不需要什么双系统），二来启动更快。

参考上面第 5 步，不过命令换成如下：

```
setenv bootfromrecovery 0
setenv bootfromnand 0
setenv bootcmd 'run storeboot'
saveenv
```

这样玩客云以后就都从 EMMC 启动了，如果想再次从 tf 卡启动，就重复第 5 步就行。

## 8. 已知问题

在 tf 卡上运行玩客云时，1080p 分辨率没有什么问题，但是安装 armbian 到 emmc 后，可能在 1080p 会花屏，可以修改 /boot/hdmi.sh 文件为以下内容来将分辨率降为 720p 显示，这个文件内容来自于旧版本的 armbian：

```
#!/bin/sh

#bpp=32
bpp=24

#mode=1080p
mode=720p

echo "$mode" > /sys/class/display/mode

# Disable framebuffer scaling
echo 0 > /sys/class/ppmgr/ppscaler
echo 0 > /sys/class/graphics/fb0/free_scale
echo 1 > /sys/class/graphics/fb0/freescale_mode
echo 0 > /sys/class/graphics/fb1/free_scale

# Set framebuffer geometry to match the resolution
case $mode in
  720*)
	fbset -fb /dev/fb0 -g 1280 720 1280 1440 $bpp
    ;;
  1080*)
	fbset -fb /dev/fb0 -g 1920 1080 1920 2160 $bpp
    ;;
esac

# Enable framebuffer device
echo 0 > /sys/class/graphics/fb0/blank

# Blank fb1 to prevent static noise
echo 1 > /sys/class/graphics/fb1/blank

#echo 0 > /sys/devices/virtual/graphics/fbcon/cursor_blink

#su -c 'hciattach /dev/ttyS1 any'
```

至于完全解决花屏问题支持 1080p 分辨率的事情就交给其他人了，我不想在这上面花时间。

## 9. 后记

将玩客云刷成 linux 后，可以安装 ups nut 客户端，这样就可以和群晖的 UPS 服务器或者其他 UPS 服务器连接，达到停电时安全关机的目的。因为玩客云没有电源开关，所以在来电时，玩客云也会自动开机，这样就达到了全自动的效果，不需要人工维护，时间很宝贵！

安装完 NFS 客户端后，可以挂载群晖或者其他服务器的 NFS 共享硬盘，此时这个 s805 的小板子硬盘容量将没有上限了，不过一般这种需求都是用来下载什么的。实测玩客云的板子运行时负载大概在 2-5w 之间。基本不超过 5w，所以还是很节能的。

据说因为硬件不够强大，docker 在玩客云上跑不起来，我没有尝试过，也没有这个需求。在这种嵌入式板子上跑 docker 简直蛋疼，还不如在电脑上装个虚拟机靠谱。

在安装系统完成后，基本上 EMMC 可用的空间是 5.4G，系统大概占用硬盘 11%（什么软件都不装的情况下）。cpu 是 4 线程，内存总量是 894M，什么软件都不装系统占用内存大概在 6%。如果安装的软件多了估计内存就不够用了，这时候开虚拟内存就行了，linux 开虚拟内存很简单。考虑到虚拟内存开在 EMMC 上会减少板子寿命，你可以把虚拟内存开在 tf 卡或者 u 盘上，现在 tf 卡太便宜了，32G 搞活动时也就二十块不到，坏了扔了换一个就行了。

**玩客云主板不会被刷砖，除非因电压电流问题主板烧掉，否则可任意重复以上刷机步骤，不必担心变砖。**

喜欢这篇文章的话，在下面给个五星好评

**Happy Hacking, bro.**

相关文章

- [玩客云刷机顶盒](https://7th-heaven.me/2020/03/07/OneThingCloudToTVBox/)
- [守夜人 - 自动按时卸载玩客云硬盘无人值守工具](https://7th-heaven.me/2020/02/06/Automatically-Unmount-Disks-Of-OneThingCloud/)
- [狐仙链路由 (FoxGodChain) 刷 openwrt](https://7th-heaven.me/2020/12/05/flash-openwrt-to-foxgodchain-router/)

- **本文作者：** Cloud
- **本文链接：** https://7th-heaven.me/2019/12/16/SetupArmbianToTheEMCCOfOneThingCloud/
- **版权声明：** 本博客所有文章除特别声明外，均采用 [BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh) 许可协议。转载请注明出处！