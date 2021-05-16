# 保姆级教程 玩客云 刷armbian 挂甜糖CDN GIF动图教程

2020-10-21 23:00:57 320点赞 3119收藏 477评论

**追加修改(2020-11-04 16:15:48):**
抱歉各位，下载地址忘了放了，刷机软件、固件打包：https://cloud.189.cn/t/FriqqmqeiIVr（访问码：re25） 11月4日，玩客云/n1 armbian一键部署甜糖脚本已发布：https://post.smzdm.com/p/alp6l8qo/



**追加修改(2020-10-22 08:52:17):**
抱歉各位，下载地址忘了放了，刷机软件、固件打包：https://cloud.189.cn/t/FriqqmqeiIVr（访问码：re25）



## 前言

前些天研究 矿渣玩客云 刷openwrt 单臂/旁路由 与N1能否一战？在恩山潜水许久，看到有关于玩客云刷armbian跑甜糖CDN的教程，我作为赚钱宝时代就开始共享限制宽带补贴套餐费的玩家，对这个非常感兴趣，于是刷机亲身体验了几天，收益相当可观，所以出一个折腾教程，鉴于图文教程比较杂乱，花了点时间录制GIF教程，造福小白玩家，一起玩转废旧矿渣！

## 刷机教程

玩客云刷机我录制了刷机教程，不会刷机的先详细观看下面视频。



视频相关文件、软件关注本人后私信关键字：玩客云 免费获取。

## 配置教程

我把配置教程大致分为4个步骤：

- 挂载磁盘
- 部署甜糖，修改、固定mac地址
- 设置守护脚本
- 绑定APP、上线

我们开始配置，文字描述我只简单的讲一下流程和命令，具体操作请看动图。

### 一、挂载磁盘





[![保姆级教程 玩客云 刷armbian 挂甜糖CDN GIF动图教程](https://qnam.smzdm.com/202010/21/5f901abb8ab137737.gif_e680.jpg)](https://post.smzdm.com/p/awx4rqkk/pic_2/)

1.插入储存设备，U盘或者移动硬盘都可以，格式推荐ext4。

2.通过ssh连接刷好armbian的玩客云（首次登陆要修改密码，我打包的armbian默认密码1234）。

3.在根目录创建 mnts 目录

cd /.
mkdir mnts

4.通过 lsblk 命令获取磁盘分区，并挂载磁盘到mnts目录。

lsblk
mount /dev/sda1 /mnts/

5.通过 blkid 命令获取存储设备UUID

blkid /dev/sda1

6.通过winscp编辑 /etc/fstab 文件，在fstab最后添加存储设备信息，实现开机自动加载

UUID=722059EC2059B835 /mnts ext4 defaults 0 0

7.通过mount -a命令重新加载 /etc/fstab 内容

mount -a

### 二、部署甜糖，修改、固定mac地址

[![保姆级教程 玩客云 刷armbian 挂甜糖CDN GIF动图教程](https://qnam.smzdm.com/202010/21/5f901add652d84814.gif_e680.jpg)](https://post.smzdm.com/p/awx4rqkk/pic_3/)

1.winscp在 /usr目录建立 node 文件夹（动图文件夹名打错了，注意，新建目录名为 node）

2.把我打包文件中 甜糖的三个文件 ttnode、log.log、crash_monitor.sh 拖进/usr/node文件夹，并修改权限为0777

3.winscp打开 /etc/rc.local 文件，在exit 0 上方添加如下代码

service sshd start
/usr/node/ttnode -p /mnts

4.用winscp打开 /etc/network/interfaces 文件，将玩客云本身MAC地址写入网卡

hwaddress B0:D5:9D:xx:xx:xx

5.重启用 ifconfig 命令查看修改是否成功（据说不修改Mac地址会乱跳，没测试）

ifconfig

### 三、设置守护脚本

[![保姆级教程 玩客云 刷armbian 挂甜糖CDN GIF动图教程](https://qnam.smzdm.com/202010/21/5f901b1298fd98885.gif_e680.jpg)](https://post.smzdm.com/p/awx4rqkk/pic_4/)

1.通过命令 crontab -e 打开定时任务文件，并按 1 用nano编辑器编辑

crontab -e
1

2.按方向键定位到文件末尾，添加一行代码

\* * * * * /usr/node/crash_monitor.sh

3.按 Ctrl+O 保存文件，Ctrl+X 退出编辑

4.通过 crontab -l 命令显示 crontab 文件内容

crontab -l

5.通过命令查看进程运行状态（我这里第二步新建文件夹名称弄错，所以程序没跑起来，改过来以后重启就好了，还是要细心啊）

ps -ef|grep ttnode

### 四、绑定APP、上线

[![保姆级教程 玩客云 刷armbian 挂甜糖CDN GIF动图教程](https://am.zdmimg.com/202010/21/5f901b77746439280.gif_e680.jpg)](https://post.smzdm.com/p/awx4rqkk/pic_5/)

这个比较简单，点这里下载安装APP、注册登录后，点击右上角+号，同局域网的甜糖设备就会自动识别，绑定后系统部署时间在15分钟左右，期间系统会测试网络，储存设备状况，然后就可以安心挂机赚糖果了。

## 总结

教程动画是我10月15日录制，我于当天晚上9点上线第一台设备，网络环境200M电信大内网没有外网IP，上行带宽40M，同网段还有2台64G[京东云](https://pinpai.smzdm.com/44504/)路由，收益情况京东云从每天50左右京豆降到40，甜糖除了第一天89星愿，后期稳步135-180星愿上升，可想而知如果有外网IP、同时缓存到位，收益不会少到哪去、关键是玩客云可以说是白菜价了，此时不折腾更待何时？

> 本教程参考恩山玩客云、N1等盒子刷机配置教程，在此对前辈大佬表示感谢。配置部署教程是建立在玩客云刷armbian成功，并在路由后台看到设备上线为基础的，如果无法连接后台请仔细观看上面刷机视频，如果有解决不了的也可以留言，尽量为大家解答。



未经授权，不得转载

# 玩客云 N1 armbian 一键脚本 部署甜糖CDN 附问题总结

2020-11-02 21:30:44 73点赞 446收藏 249评论

> 如何才能快速换一种生活方式？参加[**#牛年Flag#**](https://www.smzdm.com/tag/tr0lp4e/post/)征稿活动，征集你2021年的购物学习生活计划！>>[**点击查看活动详情**](https://post.smzdm.com/p/a9gdrq6p/)<<本次征稿活动欢迎你的敢出敢买Flag、学习Flag以及各种生活Flag，优秀的投稿文章能获得优厚的大奖，让我们一起努力实现目标吧！

## 前言

之前 保姆级教程 玩客云 刷armbian 挂甜糖CDN GIF动图教程 文章引发很多小伙伴的折腾，很多小伙伴反馈命令部署还是比较麻烦，所以一直考虑做个一键部署脚本，这不今天有空现学现卖写了个一键部署脚本，同时解答一些小伙伴折腾遇到的常规问题。

## 一键部署

先放上一键部署脚本运行效果吧



[![玩客云 N1 armbian 一键脚本 部署甜糖CDN 附问题总结](https://qnam.smzdm.com/202011/04/5fa2b0765abcf9540.gif_e680.jpg)](https://post.smzdm.com/p/alp6l8qo/pic_2/)

> wget -O node.sh https://dachui.co/ttnode/node.sh && sh node.sh

**2020年11月04日更新：**

**手动设置挂载分区，自动判断32位还是64位系统，全自动部署。**

**PS：建议全新刷机部署，自己折腾过的可能有冲突。还有什么需求可以留言，尽量满足。**

按上一篇视频教程刷机完成后，直接运行一键部署命令即可完成部署，实现U盘自动挂载，自动设置守护脚本，自动随机设定Mac地址，运行过后直接手机绑定就可以了，是不是非常简单呢。

## 核心命令解释

> cp -pdr /etc/rc.local /etc/rc.local.default
> cp -pdr /etc/crontab /etc/crontab.default
> \#备份两个文件，出问题可以自行恢复一下
>
> rm -rf /mnts
> mkdir /mnts
> mount /dev/sda1 /mnts/
> \#挂载sda1到新建的文件夹 mnts，暂时只支持U盘第一分区，SD卡名字不一样。
>
> rm -rf /usr/node
> mkdir /usr/node
> cd /usr/node/
> wget https://dachui.co/ttnode/crash_monitor.sh
> wget https://dachui.co/ttnode/log.log
> wget https://dachui.co/ttnode/ttnode
> chmod -R 777 *
> \#下载甜糖主程序和监控脚本，并赋予777权限
>
> sed -i "12a mount /dev/sda1 /mnts/nservice sshd startn/usr/node/ttnode -p /mnts" /etc/rc.local
> \#在/etc/rc.local 第12行写入自动挂载和甜糖主程序自动运行命令
>
> mac=00:60:2F$(dd bs=1 count=3 if=/dev/random 2>/dev/null |hexdump -v -e '/1 ":%02X"')
> \#随机生成Mac地址
>
> sed -i "6a hwaddress $mac" /etc/network/interfaces
> \#在/etc/network/interfaces 写入自定义mac地址
>
> sed -i '14a */1 * * * * root /usr/node/crash_monitor.sh' /etc/crontab
> \#在/etc/crontab插入周期任务，一分钟运行一次监控脚本

## 疑问解答

[![玩客云 N1 armbian 一键脚本 部署甜糖CDN 附问题总结](https://am.zdmimg.com/202011/02/5fa001bf89e55787.jpg_e680.jpg)](https://post.smzdm.com/p/alp6l8qo/pic_3/)

1.上图这个应该是遇到最多的吧，刷机的时候遇到设备枚举异常。

解决方案：先加载固件，点开始烧录，然后再连USB，长按复位键直至出现刷机进度条松开按键，百分百成功。

2.遇到ROM解析失败的，重新下载固件包。

3.还有一些奇怪的问题，请换到后置USB接口，或者USB2接口刷机，这个年代了确实有一些因为USB口不兼容导致刷机失败的，多尝试一下。

## 总结

[![玩客云 N1 armbian 一键脚本 部署甜糖CDN 附问题总结](https://qnam.smzdm.com/202011/02/5fa00329904522177.png_e680.jpg)](https://post.smzdm.com/p/alp6l8qo/pic_4/)

本人没有shell脚本开发经验，找了个基础教程现学现卖写了这个面向流程脚本 - -，脚本非常简陋，好在我运行了两台机器都部署成功，后续会继续完善升级。新加入的小伙伴可以填我**发财码：587888** 免费获取15张加速卡，让我更有折腾的动力，有疑问我也会尽量解答，有需求也会尽量开发，感谢支持！