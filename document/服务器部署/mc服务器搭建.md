## **|准备工作**

准备好对应着你要开的服的版本的官方服务器核心

一个映射软件

核心和映射软件下载↓↓↓

[Minecraft_Server (官服)minecraft-server-jar.7xiu.fun![图标](https://pic2.zhimg.com/v2-6cbf218051d50fdc62234d76c424aa09_120x160.jpg)](https://link.zhihu.com/?target=https%3A//minecraft-server-jar.7xiu.fun/zh-cn/5.html)[https://mcmirror.io/mcmirror.io](https://link.zhihu.com/?target=https%3A//mcmirror.io/)[https://www.natfrp.com/www.natfrp.com](https://link.zhihu.com/?target=https%3A//www.natfrp.com/)[NetPlus 端口映射 - 免费白嫖netplus.idc25.cn![图标](https://pic1.zhimg.com/v2-dd5309889ce8ec15794c610c9eda033c_180x120.jpg)](https://link.zhihu.com/?target=http%3A//netplus.idc25.cn/)

sakura和netplus这两个映射软件自行选择一个即可，如果你已经有映射软件也可以。

## 第一步骤，配置服务端文件

首先，将你的服务器核心放入一个独立的文件夹里（里面最好最好不要有其他文件）
然后，双击运行核心，就会发现文件夹里多了一些文件

![img](https://pic3.zhimg.com/v2-0ad30c1e470f81ff8b491026f6f84832_r.jpg)(｀・ω・´)

点击打开eula.txt文件，修改其中的eula=false为true

![img](https://pic3.zhimg.com/v2-8a4a6439db378ed9a47db4c460e37306_r.jpg)

![img](https://pic3.zhimg.com/v2-750bd7743cb2a7044be2528d08d877b2_r.jpg)把false改为true，然后保存即可

保存，关闭eula.txt文本

协议同意了之后，就可以配置服务器了。

![img](https://pic2.zhimg.com/80/v2-d3df6548f19bb1dc947e66e5ce409725_720w.png)这个就是服务器配置文件了

server.properties就是服务器的配置文件
配置的时候需要用txt格式打开，打开方式很多

①改后缀为txt，修改完后再改回properties后缀
②右键-打开方式-txt
③打开一个空白txt，将properties文件拖入txt文件里就可以快速使用txt打开

emmm，好萌新向喔~(不过我的教程就是为了萌新准备的(｀・ω・´)

打开之后就可以自行更改服务器设置啦，修改方式为更改等号后面的false或true或者是数值文本，如果看不懂建议自备一个谷歌翻译。以下是推荐配置

**enable-command-block=false→true |开启命令方块，如果玩地图就一定要开启啦**
max-players=20→适合的数值 |最大在线人数，如果开的服人比较多久调高点咯
view-distance=10→适合的数值 |服务器视距，如果是性能很弱的服务器建议调小
white-list=false→true |开启白名单，如果是私人服可以考虑开下
**online-mode=true→false |非正版玩家只有关闭这个选项才能游玩**
motd=A Minecraft Server→你想要的的文本 |服务器描述

好多啊(｀・ω・´)

保存，退出，就配置完服务器的基本设置了

## 第二步骤，启动服务器

再次双击server.jar文件，会自动生成服务器文件并启动服务器

![img](https://pic4.zhimg.com/v2-5086e9e6e558b7c704069023ebf44547_r.jpg)

当你看到

[13:40:08 INFO]: Time elapsed: 16294 ms

[13:40:08 INFO]: Done	"27.804s)! For help, type "help"

这就说明，你的服务器开好了！

云服务器端做到这一步就已经完成了，别人只要输入你的服务器IP即可加入

而本地电脑服目前只能通过自己的电脑用127.0.0.1加入，若想要其他人也能加入的话，就需要进入下一步，端口映射

## 第三步骤，映射服务器到公网上！

这一步骤，如果你阅读过我往期教程的话，其实映射方式几乎完全一样，只需要将端口改为服务器默认的端口25565就好了，不过当然了这里还是需要再重新讲一遍啦...

[FinDream：MC如何联机zhuanlan.zhihu.com![图标](https://pic1.zhimg.com/v2-fb9ba6a3f948627458b2a2d6e4863094_180x120.jpg)](https://zhuanlan.zhihu.com/p/132603593)

↑↑↑之前的联机教程↑↑↑

首先，打开你的映射软件，这里就只展示NetPlus啦，

![img](https://pic3.zhimg.com/80/v2-bbc3054de963104b79509a7f480f0f2a_720w.jpg)随便选一个空着的

![img](https://pic4.zhimg.com/80/v2-462650e46f11e40a4a343e5fa18390b3_720w.jpg)因为这个图是从我的联机教程里复制过来的，有点不清晰，没辦法，哦对了，其中内网端口要改为25565，其他都一样

内网端口要改成25565!←←←

然后保存设置，启动映射，复制地址发给要和你一起玩的小朋友就好了~

![img](https://pic2.zhimg.com/v2-136fcdb175c582c8ab8d39a8ac1a46b9_r.jpg)

![img](https://pic4.zhimg.com/v2-34d9cc02e5b858ed705b3fb258e1ac8b_r.jpg)

![img](https://pic1.zhimg.com/v2-6a9760f7619bca39c5dbd8d79b8c2510_r.jpg)

## 第四步骤，加入服务器！

输入映射的IP，就可以加入服务器啦！

![img](https://pic1.zhimg.com/v2-6a9760f7619bca39c5dbd8d79b8c2510_r.jpg)

![img](https://pic1.zhimg.com/v2-49ac7179d40e6d23a5cc6ed73abb2ed0_r.jpg)

## |常用指令

/op ID 给某人OP，获得使用高级命令的权限
/ban ID ban掉某人的ID，使他永远无法加入你的服务器

## 后记

emmm，这个教程还有需要地方需要完善，等我有空了大概会出mod端联机开服的教程，敬请期待~

![img](https://pic4.zhimg.com/v2-1f8efdb8dadbafa7bb54068ae91259b7_r.jpg)

关注我的专栏，获得更多mc的教程！

[Minecraft教程zhuanlan.zhihu.com![图标](https://pic1.zhimg.com/v2-8bdf6edff105c0041800f98a68776364_ipico.jpg)](https://zhuanlan.zhihu.com/c_1234517495362920448)

教程只是辅助，更多的需要你自己的摸索和尝试。如果有实在不懂的地方，可以在评论区询问，我会尽力提供帮助。希望这个教程能帮到你(〃'▽'〃)

编辑于 2

Minecraft开服教程
二.选择服务端
官方jar
不支持安装插件，建议好友之间进行联机，稳定性较好，适合首次开服的服主进行测试。
Bukkit水桶
支持使用插件，是一个很老而又很经典的服务端，目前至1.8官方已停止发布。1.8以后的版本都是非官方续写的，开服建议使用1.7.x或更低版本。
Spigot水龙头
支持插件，新出现的服务端，各个参数都在Bukkit的基础上优化，推荐使用该服务端。
※PaperSpigot是Spigot的升级版本，仍然建议使用。
mcpc+
mod服务端，支持插件和模组，稳定性不佳，不是模组服务器建议不要选择，若使用mod仍是个不错的选择。
客户端
仅支持好友之间联机，服主必须在线玩家才能加入游戏，不支持使用插件及24小时开服。Minecraft开服教程
二.选择服务端
官方jar
不支持安装插件，建议好友之间进行联机，稳定性较好，适合首次开服的服主进行测试。
Bukkit水桶
支持使用插件，是一个很老而又很经典的服务端，目前至1.8官方已停止发布。1.8以后的版本都是非官方续写的，开服建议使用1.7.x或更低版本。
Spigot水龙头
支持插件，新出现的服务端，各个参数都在Bukkit的基础上优化，推荐使用该服务端。
※PaperSpigot是Spigot的升级版本，仍然建议使用。
mcpc+
mod服务端，支持插件和模组，稳定性不佳，不是模组服务器建议不要选择，若使用mod仍是个不错的选择。
客户端
仅支持好友之间联机，服主必须在线玩家才能加入游戏，不支持使用插件及24小时开服。

Minecraft开服教程
三.开服.bat编写
服务端需要.bat文件运行，在桌面上右键，选择「新建文本文档」，输入
[@echo](https://tieba.baidu.com/home/main?un=echo&fr=pb&ie=utf-8) off
java <服务端名称>.jar
pause
保存为 启动服务器.bat，放置于服务端同一目录，双击运行 启动服务器.bat，会生成许多文件，弹出后台（黑色的窗口），最后done完成表示开服成功。
※1.8及以上版本需要同意eula，在生成的eula.txt中设置eula=true。
例(1)：Simon的.bat
title 服务器后台
java bukkit1.7.2.jar
pause
※title参数，显示标题
例(2)：Doodle的.bat
title Doodle的开服器
java -Xms512M -Xmx2G spigot1.9.4.jar
※-Xms定义最小内存，如-Xms256M
※-Xmx定义最大内存，如-Xmx1GMinecraft开服教程
三.开服.bat编写
服务端需要.bat文件运行，在桌面上右键，选择「新建文本文档」，输入
[@echo](https://tieba.baidu.com/home/main?un=echo&fr=pb&ie=utf-8) off
java <服务端名称>.jar
pause
保存为 启动服务器.bat，放置于服务端同一目录，双击运行 启动服务器.bat，会生成许多文件，弹出后台（黑色的窗口），最后done完成表示开服成功。
※1.8及以上版本需要同意eula，在生成的eula.txt中设置eula=true。
例(1)：Simon的.bat
title 服务器后台
java bukkit1.7.2.jar
pause
※title参数，显示标题
例(2)：Doodle的.bat
title Doodle的开服器
java -Xms512M -Xmx2G spigot1.9.4.jar
※-Xms定义最小内存，如-Xms256M
※-Xmx定义最大内存，如-Xmx1GMinecraft开服教程
三.开服.bat编写
服务端需要.bat文件运行，在桌面上右键，选择「新建文本文档」，输入
[@echo](https://tieba.baidu.com/home/main?un=echo&fr=pb&ie=utf-8) off
java <服务端名称>.jar
pause
保存为 启动服务器.bat，放置于服务端同一目录，双击运行 启动服务器.bat，会生成许多文件，弹出后台（黑色的窗口），最后done完成表示开服成功。
※1.8及以上版本需要同意eula，在生成的eula.txt中设置eula=true。
例(1)：Simon的.bat
title 服务器后台
java bukkit1.7.2.jar
pause
※title参数，显示标题
例(2)：Doodle的.bat
title Doodle的开服器
java -Xms512M -Xmx2G spigot1.9.4.jar
※-Xms定义最小内存，如-Xms256M
※-Xmx定义最大内存，如-Xmx1G我的世界服务器server.properties配置教程听语音

- 原创
- |
- 浏览：38894
- |
- 更新：2017-12-13 13:34
- |
- 标签：[服务器](https://jingyan.baidu.com/tag?tagName=服务器) 

- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/6bbfdd14f1c595eedfc8eb9227530688902c9aa2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=1)1
- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/994f412043715fdb9a29e58f468920c5270f8ca2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=2)2
- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/89402670d5413a8c1f01f9ba1ffc508c9ace81a2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=3)3
- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/8b3643dd884ce54aec2ebb5aa3066b0193ddf7a2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=4)4
- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/90c61d1c99c0affc2f8f789a2372941fbfe4eaa2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=5)5
- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/7830e01d96d81819bb29fb78876efbf203b3dea2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=6)6
- [![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/7496877bbbf4da5891d382fcea0f8b56ac04d7a2.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html?picindex=7)7

[分步阅读](http://jingyan.baidu.com/album/8ebacdf074bc0049f75cd550.html)

你想要在我的世界服务器里调整一些自己想要的简单功能？服务器的目录下的server.properties可以给你更多的选项和玩法哦~~~

## 工具/原料

- 我的世界启动器
- 我的世界服务器端

## 方法/步骤

1. 

   首先：

   在我的世界服务器端路径内有一个server.properties

   打开它(可以用notpad++)

   我一个一个讲解下

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/6bbfdd14f1c595eedfc8eb9227530688902c9aa2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/994f412043715fdb9a29e58f468920c5270f8ca2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

2. 

   allow-nether=true   #是否开启地狱

   level-name=world   #默认世界名称（最好不要改）

   enable-query=false  #没有什么大用处

   allow-flight=false    #没有什么大用处

   announce-player-achievements=true  #意义不明

   server-port=25566   #服务器端口（127.0.0.1:25565中的冒号后面是这个server-port的数值）

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/89402670d5413a8c1f01f9ba1ffc508c9ace81a2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

3. 

   enable-rcon=false  #是否开启rcon监听（没有什么用）

   force-gamemode=false  #force游戏模式

   level-seed=      #我的世界地图种子（没有特殊需要就不填）

   server-ip=       #服务器指向IP（默认不要改放空）

   max-build-height=256  #服务器最大建筑高度

   spawn-npcs=true      #是否有主城NPC

   white-list=false        #是否开启白名单（开启后在白名单内的玩家才能进入服务器，否则进入不了。不要随便开）

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/8b3643dd884ce54aec2ebb5aa3066b0193ddf7a2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

4. 

   spawn-animals=true  #主城是否有动物

   snooper-enabled=true  #意义不明

   hardcore=false     #我的世界极限模式是否开启（玩过的都知道）

   online-mode=false  #是否开启正版验证，需用我的世界官方启动器才能进入

   resource-pack=      #服务器资源包：填下载地址（不需要就不填）

   pvp=true         #是否开启服务器PVP

   difficulty=1   #服务器难度： 0和平 1简单 2中等 3困难

   enable-command-block=false  #是否开启命令方块

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/90c61d1c99c0affc2f8f789a2372941fbfe4eaa2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

5. 

   player-idle-timeout=0  #意义不明

   gamemode=0 #玩家默认进入游戏的游戏模式 1创造 0生存 2冒险模式3旁观者

   max-players=20  #服务器最大玩家数（超过后玩家无法进入）

   spawn-monsters=true  #主城是否刷新怪物

   view-distance=10  #意义不明

   generate-structures=true  #意义不明

   spawn-protection=16 #服务器最大保护区（玩家破坏建筑不了）

   motd=A Minecraft Server  MOTD指的是在玩家添加服务器后下面会显示这里面的内容（不能为中文、特殊符号）

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/7830e01d96d81819bb29fb78876efbf203b3dea2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

6. 

   当你都配置好后

   开启服务器

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/7496877bbbf4da5891d382fcea0f8b56ac04d7a2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

7. 

   服务器开启成功提示

   就可以邀请基友一起在服务器玩耍！

   ![我的世界服务器server.properties配置教程](https://exp-picture.cdn.bcebos.com/50a010f85856d53d462d845c47d2bb665059caa2.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)我的世界服务器怎么能让我（我是腐竹）能作弊，别人作弊不了，我是玩创造，别人就是玩生存

   我有minecraft_server，同时求一些服务器好用的mod（使用方法也要）

    我来答 分享 *[举报](javascript:void(0))*

   **2个回答**

   [#热议# 30+的人生活是不是总是忙忙碌碌？](https://zhidao.baidu.com/question/1976385746.html?entry=qb_hotRecommend)

   [**肾心哥哥**](https://zhidao.baidu.com/usercenter?uid=1ca54069236f25705e790f47&role=team)
   推荐于2017-11-26 · TA获得超过4747个赞

   关注

   (=￣ω￣=)您好!很高兴为您解答e69da5e887aa62616964757a686964616f31333335316535有关Minecraft相关的问题

   回答内容如下【您的服务器设置可以参考:http://wenku.baidu.com/view/e8dd8e9cec3a87c24028c4ef.html
   其中有一项就是设置服务器为创造或生存 您设置为生存 然后在服务端输入/op 您的名字 您就可以获得权限了
   另外服务器插件您可以去这里http://www.mcbbs.net/forum-servermod-1.html下载】

   如果回答解决了您的问题,请点击采纳最佳答案!
   如果没有解决或还有其他疑问,请继续追问!(˙ω˙)
   【欢迎提出有关Minecraft的任何问题】
   【我将尽力解决!谢谢您的支持!╮(╯▽╰)╭】

   更多追问追答**

   追问

   为什么会这样

   

   - ![img](https://iknow-pic.cdn.bcebos.com/21a4462309f7905266964fcf0ef3d7ca7acbd5b2)

   追答

   ```
   在服务端输入/op 您的名字   比如我叫sheen 那么我就输入 /op sheen  注意 是在服务端输 不是游戏里
   ```

   