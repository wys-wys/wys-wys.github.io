# 在Linux的纯命令行模式观看视频听语音

- 浏览：4877
- |
- 更新：2018-06-04 20:33
- |
- 标签：[LINUX](https://jingyan.baidu.com/tag?tagName=LINUX) [视频](https://jingyan.baidu.com/tag?tagName=视频) 

- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/9b2098254193cee8a75d81a85a0ff2260c9aa8ec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=1)1
- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/05e24be983aee8d78072365c6b781431deb666ec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=2)2
- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/332d496699cf0253cd3bf6366b36e29146e85fec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=3)3
- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/e3d059e833e03972d45b6e59b5863048604356ec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=4)4
- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/31097f43d7d44831f4b32314d40f822b75ee51ec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=5)5
- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/836a6aee1c324b18a674594253a72633498448ec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=6)6
- [![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/cca2552c56ee7b7f8657a9c66ef4fcf5ef0d41ec.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html?picindex=7)7

[分步阅读](http://jingyan.baidu.com/album/2fb0ba4081900c00f2ec5f8d.html)

MPlayer 是我在 Linux 系统中用到的相当好的媒体播放程序，它因支持播放广泛的音/视频文件格式而著称。在纯命令行模式下，我们依然可以使用它来播放视频，当然，是 ASCII 码拼成的视频。这个经验虽然无用，却很有趣。下面的命令在Linux的图形界面也可以用，但显示效果没有在纯命令行模式下的好。

![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/9b2098254193cee8a75d81a85a0ff2260c9aa8ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

## 工具/原料

- Linux
- Mplayer

## 方法/步骤

1. 

   先将要播放的视频重命名以英文字母开头的形式，并放入主目录。因为在纯命令行模式下不容易输入中文。进入命令行模式。我使用的是Linux发行版是Fedora，进入方式为Ctrl+Alt+F3～F6中任意一个。

   ![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/05e24be983aee8d78072365c6b781431deb666ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

2. 

   输入自己的用户名，按回车后，输入自己的密码。

   ![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/332d496699cf0253cd3bf6366b36e29146e85fec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

3. 

   有两个库文件支持该特性：aa 和 caca。使用 libaa，你只能在黑白 ASCII 中观看电影。而 libcaca 支持色彩。然而，libaa 支持更广泛。输入命令：mplayer -vo aa 文件名，输入文件名字时可以只打出前面的英文，随后按Tab键进行文件名补全。

   ![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/e3d059e833e03972d45b6e59b5863048604356ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

4. 

   如果你在播放时发现视频只有一部分被显示，可以调整纵横比，可以加上-aspect选项，后面加上合适的比例，如3：1，4：1等。示例命令：mplayer -vo aa -aspect 4:1。

   ![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/31097f43d7d44831f4b32314d40f822b75ee51ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

5. 

   使用libcaca，命令为：mplayer -vo caca 文件名。

   ![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/836a6aee1c324b18a674594253a72633498448ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

6. 

   在播放时，p 或 Space－暂停/继续播放。 q 或 Esc－退出 MPlayer。

   ![在Linux的纯命令行模式观看视频](https://exp-picture.cdn.bcebos.com/cca2552c56ee7b7f8657a9c66ef4fcf5ef0d41ec.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   END

## 注意事项

- 不同Linux系统，进入纯命令行模式方法可能不同。
- 笔者为了使图片更清晰而截取虚拟机中的图片，暂时还没找到直接在实体系统上在纯命令行截图的方法。在虚拟机中，变为纯命令行模式，窗口与分辨率会自动变小，效果没有在实体电脑上的好。

# 在Linux终端窗口中也能看视频？[多图]

| [日期：2009-02-24] | 来源：Linux公社 作者：Linux | [字体：[大](javascript:ContentSize(16)) [中](javascript:ContentSize(0)) [小](javascript:ContentSize(12))] |
| ------------------ | --------------------------- | ------------------------------------------------------------ |
|                    |                             |                                                              |

在Linux的终端窗口中也看视频？Linux终端的全字符界面怎么可能可以用来看视频呢?这可能吗？在Linux中没有做不到，只有想不到。

现在我们请出ASCII了,要知道ASCII字符可以组成各种各样的图形,虽然精细度不够,但也能看个大概,接下来就让大家用ASCII来欣赏一下吧.

Watch Movies in ASCII

当然您还需要先安装一个mplayer:

sudo apt-get install mplayer

然后执行mplayer,用caca参数调出色泽字体,并组成ASCII字符的图形以打开视频:

![在Linux终端窗口中也能看视频？[多图]](https://www.linuxidc.com/upload/2009_02/09022412399484.jpg)

mplayer -vo caca MovieName.avi

OK，在播放什么风格的大片就看各位自己想象能力了,当然,最好离远点看,要不轮廓依然是不清楚的.

![在Linux终端窗口中也能看视频？[多图]](https://www.linuxidc.com/upload/2009_02/09022412393497.jpg)

![在Linux终端窗口中也能看视频？[多图]](https://www.linuxidc.com/upload/2009_02/09022412393998.jpg)