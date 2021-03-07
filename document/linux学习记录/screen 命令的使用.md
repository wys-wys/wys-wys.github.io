# Centos系统里screen命令的使用

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[zhangzhm](https://blog.csdn.net/zhangzhm) 2017-02-07 13:48:35 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 610 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

版权

1.如果在screenCRT中开启窗口，然后运行一个程序，当注销时，程序会自动毁掉。
2.使用nohup可以解决此问题，把程序放到后台运行，查看nohup.out可以查看程序运行的怎样了，但是使用nohup把程序放到后台，就再也无法切换程序到前台了，而screen可以。

**使用方法：**

**1.安装，**centos默认没有安装，安装一下。

**2.进入screen。**

直接输入screen回车即可，此时会进入一个新的终端。可以进行要长时间运行的作业。

**3.返回到主终端（screen仍然在后台运行）**
Ctrl+A 然后按D 屏幕显示[detached]

**4.返回到screen**
screen -ls
There is a screen on:
    18245.pts-1.imobile-sv006-200  (Detached)
1 Socket in /var/run/screen/S-root.
可以看到所有的screen socket，使用screen -r 18245 即可返回。

**5.彻底退出screen
**screen终端输入exit。屏幕显示[screen is terminating]即可

**6.屏幕共享，协同作业**

其中一个用户 screen -S ipcpu 使用命名的socket便于输入
另一个用户 screen -x ipcpu 即可，两人可以协同操作，一方的操作会在另一方屏幕显示。

**screen的其他命令**
Ctrl-a ? 各功能的帮助摘要
Ctrl-a c 创建一个新的 window (终端)
Ctrl-a Ctrl-n 和 Ctrl-a Ctrl-p 切换到下一个或前一个 window
Ctrl-a Ctrl-N N 为 0 到 9 的数字，用来切换到相对应的 window
Ctrl-a ” 获取所有正在运行的 window 的可导航的列表
Ctrl-a a 清楚错误的 Ctrl-a
Ctrl-a Ctrl-d 断开所有会话，会话中所有任务运行于后台
Ctrl-a x 用密码锁柱 screen 终端

===============================

后记

在使用screen过程中，经常会遇到“闪屏”的问题，这是可以关掉的。

**快速关掉**：也就是先输入CTRL + a，再输入CTRL + g。

**永久关闭**：修改*/etc/screenrc 加入* 

**vbell off**

其实这与vi中的visualbell功能很是类似。在vi中关闭闪屏，是使用**:set novisualbell**命令。

# screen使用

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[大大大zzc](https://blog.csdn.net/qq_28832135) 2018-04-06 10:49:39 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10955 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 22

分类专栏： [Linux学习笔记](https://blog.csdn.net/qq_28832135/category_6275431.html) 文章标签： [screen](https://www.csdn.net/tags/MtTaEg0sMTAxNTAtYmxvZwO0O0OO0O0O.html)

**Screen**是一款由GNU计划开发的用于命令行终端切换的自由软件。用户可以通过该软件同时连接多个本地或远程的命令行会话，并在其间自由切换。GNU Screen可以看作是窗口管理器的命令行界面版本。它提供了统一的管理多个会话的界面和相应的功能。

**会话恢复**

只要Screen本身没有终止，在其内部运行的会话都可以恢复。这一点对于远程登录的用户特别有用——即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。只要再次登录到主机上执行screen -r就可以恢复会话的运行。同样在暂时离开的时候，也可以执行分离命令detach，在保证里面的程序正常运行的情况下让Screen挂起（切换到后台）。这一点和图形界面下的VNC很相似。

**多窗口**

在Screen环境下，所有的会话都独立的运行，并拥有各自的编号、输入、输出和窗口缓存。用户可以通过快捷键在不同的窗口下切换，并可以自由的重定向各个窗口的输入和输出。Screen实现了基本的文本操作，如复制粘贴等；还提供了类似滚动条的功能，可以查看窗口状况的历史记录。窗口还可以被分区和命名，还可以监视后台窗口的活动。 会话共享 Screen可以让一个或多个用户从不同终端多次登录一个会话，并共享会话的所有特性（比如可以看到完全相同的输出）。它同时提供了窗口访问权限的机制，可以对窗口进行密码保护。

GNU's Screen 官方站点：http://www.gnu.org/software/screen/

### 语法 

```
# screen [-AmRvx -ls -wipe][-d <作业名称>][-h <行数>][-r <作业名称>][-s ][-S <作业名称>]
```

### 选项 

```
-A 　将所有的视窗都调整为目前终端机的大小。
-d <作业名称> 　将指定的screen作业离线。
-h <行数> 　指定视窗的缓冲区行数。
-m 　即使目前已在作业中的screen作业，仍强制建立新的screen作业。
-r <作业名称> 　恢复离线的screen作业。
-R 　先试图恢复离线的作业。若找不到离线的作业，即建立新的screen作业。
-s 　指定建立新视窗时，所要执行的shell。
-S <作业名称> 　指定screen作业的名称。
-v 　显示版本信息。
-x 　恢复之前离线的screen作业。
-ls或--list 　显示目前所有的screen作业。
-wipe 　检查目前所有的screen作业，并删除已经无法使用的screen作业。
```

### 常用screen参数 

```
screen -S yourname -> 新建一个叫yourname的session
screen -ls -> 列出当前所有的session
screen -r yourname -> 回到yourname这个session
screen -d yourname -> 远程detach某个session
screen -d -r yourname -> 结束当前session并回到yourname这个session
```

在每个screen session 下，所有命令都以 ctrl+a(C-a) 开始。

```
C-a ? -> 显示所有键绑定信息
C-a c -> 创建一个新的运行shell的窗口并切换到该窗口
C-a n -> Next，切换到下一个 window 
C-a p -> Previous，切换到前一个 window 
C-a 0..9 -> 切换到第 0..9 个 window
Ctrl+a [Space] -> 由视窗0循序切换到视窗9
C-a C-a -> 在两个最近使用的 window 间切换 
C-a x -> 锁住当前的 window，需用用户密码解锁
C-a d -> detach，暂时离开当前session，将目前的 screen session (可能含有多个 windows) 丢到后台执行，并会回到还没进 screen 时的状态，此时在 screen session 里，每个 window 内运行的 process (无论是前台/后台)都在继续执行，即使 logout 也不影响。 
C-a z -> 把当前session放到后台执行，用 shell 的 fg 命令则可回去。
C-a w -> 显示所有窗口列表
C-a t -> time，显示当前时间，和系统的 load 
C-a k -> kill window，强行关闭当前的 window
C-a [ -> 进入 copy mode，在 copy mode 下可以回滚、搜索、复制就像用使用 vi 一样
    C-b Backward，PageUp 
    C-f Forward，PageDown 
    H(大写) High，将光标移至左上角 
    L Low，将光标移至左下角 
    0 移到行首 
    $ 行末 
    w forward one word，以字为单位往前移 
    b backward one word，以字为单位往后移 
    Space 第一次按为标记区起点，第二次按为终点 
    Esc 结束 copy mode 
C-a ] -> paste，把刚刚在 copy mode 选定的内容贴上
```

### 使用 screen 

**安装screen**

流行的Linux发行版（例如Red Hat Enterprise Linux）通常会自带screen实用程序，如果没有的话，可以从GNU screen的官方网站下载。

```
[root@TS-DEV ~]# yum install screen
[root@TS-DEV ~]# rpm -qa|grep screen
screen-4.0.3-4.el5
[root@TS-DEV ~]#
```

**创建一个新的窗口**

安装完成后，直接敲命令screen就可以启动它。但是这样启动的screen会话没有名字，实践上推荐为每个screen会话取一个名字，方便分辨：

```
[root@TS-DEV ~]# screen -S david 
```

screen启动后，会创建第一个窗口，也就是窗口No. 0，并在其中打开一个系统默认的shell，一般都会是bash。所以你敲入命令screen之后，会立刻又返回到命令提示符，仿佛什么也没有发生似的，其实你已经进入Screen的世界了。当然，也可以在screen命令之后加入你喜欢的参数，使之直接打开你指定的程序，例如：

```
[root@TS-DEV ~]# screen vi david.txt
```

screen创建一个执行vi david.txt的单窗口会话，退出vi 将退出该窗口/会话。

**查看窗口和窗口名称**

打开多个窗口后，可以使用快捷键C-a w列出当前所有窗口。如果使用文本终端，这个列表会列在屏幕左下角，如果使用X环境下的终端模拟器，这个列表会列在标题栏里。窗口列表的样子一般是这样：

```
0$ bash  1-$ bash  2*$ bash  
```

这个例子中我开启了三个窗口，其中*号表示当前位于窗口2，-号表示上一次切换窗口时位于窗口1。

Screen默认会为窗口命名为编号和窗口中运行程序名的组合，上面的例子中窗口都是默认名字。练习了上面查看窗口的方法，你可能就希望各个窗口可以有不同的名字以方便区分了。可以使用快捷键C-a A来为当前窗口重命名，按下快捷键后，Screen会允许你为当前窗口输入新的名字，回车确认。

**会话分离与恢复**

你可以不中断screen窗口中程序的运行而暂时断开（detach）screen会话，并在随后时间重新连接（attach）该会话，重新控制各窗口中运行的程序。例如，我们打开一个screen窗口编辑/tmp/david.txt文件：

```
[root@TS-DEV ~]# screen vi /tmp/david.txt
```

之后我们想暂时退出做点别的事情，比如出去散散步，那么在screen窗口键入C-a d，Screen会给出detached提示：

暂时中断会话

![img](http://man.linuxde.net/wp-content/uploads/2015/12/105052iyv.jpg)

半个小时之后回来了，找到该screen会话：

```
[root@TS-DEV ~]# screen -ls
```

![img](http://man.linuxde.net/wp-content/uploads/2015/12/1050524wP.jpg)

重新连接会话：

```
[root@TS-DEV ~]# screen -r 12865
```

一切都在。

当然，如果你在另一台机器上没有分离一个Screen会话，就无从恢复会话了。这时可以使用下面命令强制将这个会话从它所在的终端分离，转移到新的终端上来：

![img](http://man.linuxde.net/wp-content/uploads/2015/12/1050528Fl.jpg)

**清除dead 会话**

如果由于某种原因其中一个会话死掉了（例如人为杀掉该会话），这时screen -list会显示该会话为dead状态。使用screen -wipe命令清除该会话：

![img](http://man.linuxde.net/wp-content/uploads/2015/12/105053LNE.jpg)

**关闭或杀死窗口**

正常情况下，当你退出一个窗口中最后一个程序（通常是bash）后，这个窗口就关闭了。另一个关闭窗口的方法是使用C-a k，这个快捷键杀死当前的窗口，同时也将杀死这个窗口中正在运行的进程。

如果一个Screen会话中最后一个窗口被关闭了，那么整个Screen会话也就退出了，screen进程会被终止。

除了依次退出/杀死当前Screen会话中所有窗口这种方法之外，还可以使用快捷键C-a :，然后输入quit命令退出Screen会话。需要注意的是，这样退出会杀死所有窗口并退出其中运行的所有程序。其实C-a :这个快捷键允许用户直接输入的命令有很多，包括分屏可以输入[split](http://man.linuxde.net/split)等，这也是实现Screen功能的一个途径，不过个人认为还是快捷键比较方便些。

### screen 高级应用  

**会话共享**

还有一种比较好玩的会话恢复，可以实现会话共享。假设你在和朋友在不同地点以相同用户登录一台机器，然后你创建一个screen会话，你朋友可以在他的终端上命令：

```
[root@TS-DEV ~]# screen -x
```

这个命令会将你朋友的终端Attach到你的Screen会话上，并且你的终端不会被Detach。这样你就可以和朋友共享同一个会话了，如果你们当前又处于同一个窗口，那就相当于坐在同一个显示器前面，你的操作会同步演示给你朋友，你朋友的操作也会同步演示给你。当然，如果你们切换到这个会话的不同窗口中去，那还是可以分别进行不同的操作的。

**会话锁定与解锁**

Screen允许使用快捷键C-a s锁定会话。锁定以后，再进行任何输入屏幕都不会再有反应了。但是要注意虽然屏幕上看不到反应，但你的输入都会被Screen中的进程接收到。快捷键C-a q可以解锁一个会话。

也可以使用C-a x锁定会话，不同的是这样锁定之后，会话会被Screen所属用户的密码保护，需要输入密码才能继续访问这个会话。

**发送命令到screen会话**

在Screen会话之外，可以通过screen命令操作一个Screen会话，这也为使用Screen作为脚本程序增加了便利。关于Screen在脚本中的应用超出了入门的范围，这里只看一个例子，体会一下在会话之外对Screen的操作：

```
[root@TS-DEV ~]# screen -S sandy -X screen ping www.baidu.com
```

这个命令在一个叫做sandy的screen会话中创建一个新窗口，并在其中运行ping命令。

**屏幕分割**

现在显示器那么大，将一个屏幕分割成不同区域显示不同的Screen窗口显然是个很酷的事情。可以使用快捷键C-a S将显示器水平分割，Screen 4.00.03版本以后，也支持垂直分屏，快捷键是C-a |。分屏以后，可以使用C-a <tab>在各个区块间切换，每一区块上都可以创建窗口并在其中运行进程。

可以用C-a X快捷键关闭当前焦点所在的屏幕区块，也可以用C-a Q关闭除当前区块之外其他的所有区块。关闭的区块中的窗口并不会关闭，还可以通过窗口切换找到它。

![img](http://man.linuxde.net/wp-content/uploads/2015/12/1050538zX.jpg)

**C/P模式和操作**

screen的另一个很强大的功能就是可以在不同窗口之间进行复制粘贴了。使用快捷键C-a <Esc>或者C-a [可以进入copy/paste模式，这个模式下可以像在vi中一样移动光标，并可以使用空格键设置标记。其实在这个模式下有很多类似vi的操作，譬如使用/进行搜索，使用y快速标记一行，使用w快速标记一个单词等。关于C/P模式下的高级操作，其文档的这一部分有比较详细的说明。

一般情况下，可以移动光标到指定位置，按下空格设置一个开头标记，然后移动光标到结尾位置，按下空格设置第二个标记，同时会将两个标记之间的部分储存在copy/paste buffer中，并退出copy/paste模式。在正常模式下，可以使用快捷键C-a ]将储存在buffer中的内容粘贴到当前窗口。

![img](http://man.linuxde.net/wp-content/uploads/2015/12/105054so0.jpg)

# CentOS下screen 命令详解

[![img](https://upload.jianshu.io/users/upload_avatars/14376830/ef2af95d-161b-4278-b5e3-3faf39c2bfff?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/96e1e1bd0b0f)

[半道出了个家](https://www.jianshu.com/u/96e1e1bd0b0f)关注

2018.10.13 18:51:06字数 3,907阅读 167

# CentOS下screen 命令详解

一、背景

系统管理员经常需要SSH 或者telent 远程登录到Linux 服务器，经常运行一些需要很长时间才能完成的任务，比如系统备份、ftp 传输等等。通常情况下我们都是为每一个这样的任务开一个远程终端窗口，因为它们执行的时间太长了。必须等待它们执行完毕，在此期间不能关掉窗口或者断开连接，否则这个任务就会被杀掉，一切半途而废了。

二、简介

GNU Screen是一款由GNU计划开发的用于命令行终端切换的自由软件。用户可以通过该软件同时连接多个本地或远程的命令行会话，并在其间自由切换。

GNU Screen可以看作是窗口管理器的命令行界面版本。它提供了统一的管理多个会话的界面和相应的功能。

会话恢复

<dl>

<dd>只要Screen本身没有终止，在其内部运行的会话都可以恢复。这一点对于远程登录的用户特别有用——即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。只要再次登录到主机上执行screen -r就可以恢复会话的运行。同样在暂时离开的时候，也可以执行分离命令detach，在保证里面的程序正常运行的情况下让Screen挂起（切换到后台）。这一点和图形界面下的VNC很相似。</dd>

</dl>

多窗口

<dl>

<dd>在Screen环境下，所有的会话都独立的运行，并拥有各自的编号、输入、输出和窗口缓存。用户可以通过快捷键在不同的窗口下切换，并可以自由的重定向各个窗口的输入和输出。Screen实现了基本的文本操作，如复制粘贴等；还提供了类似滚动条的功能，可以查看窗口状况的历史记录。窗口还可以被分区和命名，还可以监视后台窗口的活动。</dd>

</dl>

会话共享

<dl>

<dd>Screen可以让一个或多个用户从不同终端多次登录一个会话，并共享会话的所有特性（比如可以看到完全相同的输出）。它同时提供了窗口访问权限的机制，可以对窗口进行密码保护。</dd>

</dl>

GNU's Screen 官方站点：http://www.gnu.org/software/screen/

三、语法

# screen [-AmRvx -ls -wipe][-d <作业名称>][-h <行数>][-r <作业名称>][-s ][-S <作业名称>]

参数说明

-A 　将所有的视窗都调整为目前终端机的大小。
-d <作业名称> 　将指定的screen作业离线。
-h <行数> 　指定视窗的缓冲区行数。
-m 　即使目前已在作业中的screen作业，仍强制建立新的screen作业。
-r <作业名称> 　恢复离线的screen作业。
-R 　先试图恢复离线的作业。若找不到离线的作业，即建立新的screen作业。
-s 　指定建立新视窗时，所要执行的shell。
-S <作业名称> 　指定screen作业的名称。
-v 　显示版本信息。
-x 　恢复之前离线的screen作业。
-ls或--list 　显示目前所有的screen作业。
-wipe 　检查目前所有的screen作业，并删除已经无法使用的screen作业。

四、常用screen参数

screen -S yourname -> 新建一个叫yourname的session
screen -ls -> 列出当前所有的session
screen -r yourname -> 回到yourname这个session
screen -d yourname -> 远程detach某个session
screen -d -r yourname -> 结束当前session并回到yourname这个session

在每个screen session 下，所有命令都以 ctrl+a(C-a) 开始。
C-a ? -> 显示所有键绑定信息
C-a c -> 创建一个新的运行shell的窗口并切换到该窗口
C-a n -> Next，切换到下一个 window
C-a p -> Previous，切换到前一个 window
C-a 0..9 -> 切换到第 0..9 个 window
Ctrl+a [Space] -> 由视窗0循序切换到视窗9
C-a C-a -> 在两个最近使用的 window 间切换
C-a x -> 锁住当前的 window，需用用户密码解锁
C-a d -> detach，暂时离开当前session，将目前的 screen session (可能含有多个 windows) 丢到后台执行，并会回到还没进 screen 时的状态，此时在 screen session 里，每个 window 内运行的 process (无论是前台/后台)都在继续执行，即使 logout 也不影响。
C-a z -> 把当前session放到后台执行，用 shell 的 fg 命令则可回去。
C-a w -> 显示所有窗口列表
C-a t -> Time，显示当前时间，和系统的 load
C-a k -> kill window，强行关闭当前的 window
C-a [ -> 进入 copy mode，在 copy mode 下可以回滚、搜索、复制就像用使用 vi 一样
C-b Backward，PageUp
C-f Forward，PageDown
H(大写) High，将光标移至左上角
L Low，将光标移至左下角
0 移到行首
$ 行末
w forward one word，以字为单位往前移
b backward one word，以字为单位往后移
Space 第一次按为标记区起点，第二次按为终点
Esc 结束 copy mode
C-a ] -> Paste，把刚刚在 copy mode 选定的内容贴上

五、使用 screen

5.1 安装screen

流行的Linux发行版（例如Red Hat Enterprise Linux）通常会自带screen实用程序，如果没有的话，可以从GNU screen的官方网站下载。

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# yum install screen[root@TS-DEV ~]# rpm -qa|grep screenscreen-4.0.3-4.el5[root@TS-DEV ~]#</pre>

5.2 创建一个新的窗口

安装完成后，直接敲命令screen就可以启动它。但是这样启动的screen会话没有名字，实践上推荐为每个screen会话取一个名字，方便分辨：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen -S david </pre>

screen启动后，会创建第一个窗口，也就是窗口No. 0，并在其中打开一个系统默认的shell，一般都会是bash。所以你敲入命令screen之后，会立刻又返回到命令提示符，仿佛什么也没有发生似的，其实你已经进入Screen的世界了。当然，也可以在screen命令之后加入你喜欢的参数，使之直接打开你指定的程序，例如：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen vi david.txt</pre>

screen创建一个执行vi david.txt的单窗口会话，退出vi 将退出该窗口/会话。

5.3 查看窗口和窗口名称

打开多个窗口后，可以使用快捷键C-a w列出当前所有窗口。如果使用文本终端，这个列表会列在屏幕左下角，如果使用X环境下的终端模拟器，这个列表会列在标题栏里。窗口列表的样子一般是这样：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">0 bash 2$ bash </pre>

这个例子中我开启了三个窗口，其中号表示当前位于窗口2，-号表示上一次切换窗口时位于窗口1。

Screen默认会为窗口命名为编号和窗口中运行程序名的组合，上面的例子中窗口都是默认名字。练习了上面查看窗口的方法，你可能就希望各个窗口可以有不同的名字以方便区分了。可以使用快捷键C-a A来为当前窗口重命名，按下快捷键后，Screen会允许你为当前窗口输入新的名字，回车确认。

5.4 会话分离与恢复

你可以不中断screen窗口中程序的运行而暂时断开（detach）screen会话，并在随后时间重新连接（attach）该会话，重新控制各窗口中运行的程序。例如，我们打开一个screen窗口编辑/tmp/david.txt文件：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen vi /tmp/david.txt</pre>

之后我们想暂时退出做点别的事情，比如出去散散步，那么在screen窗口键入`C-a d`，Screen会给出detached提示：

暂时中断会话

[图片上传失败...(image-ae9664-1539427780746)]

半个小时之后回来了，找到该screen会话：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen -ls</pre>

[图片上传失败...(image-621bc0-1539427780746)]

重新连接会话：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen -r 12865</pre>

一切都在。

当然，如果你在另一台机器上没有分离一个Screen会话，就无从恢复会话了。

这时可以使用下面命令强制将这个会话从它所在的终端分离，转移到新的终端上来：

[图片上传失败...(image-86d100-1539427780746)]

5.5 清除dead 会话

如果由于某种原因其中一个会话死掉了（例如人为杀掉该会话），这时screen -list会显示该会话为dead状态。使用screen -wipe命令清除该会话：

[图片上传失败...(image-dc2764-1539427780746)]

5.6 关闭或杀死窗口

正常情况下，当你退出一个窗口中最后一个程序（通常是bash）后，这个窗口就关闭了。另一个关闭窗口的方法是使用C-a k，这个快捷键杀死当前的窗口，同时也将杀死这个窗口中正在运行的进程。

如果一个Screen会话中最后一个窗口被关闭了，那么整个Screen会话也就退出了，screen进程会被终止。

除了依次退出/杀死当前Screen会话中所有窗口这种方法之外，还可以使用快捷键C-a :，然后输入quit命令退出Screen会话。需要注意的是，这样退出会杀死所有窗口并退出其中运行的所有程序。其实C-a :这个快捷键允许用户直接输入的命令有很多，包括分屏可以输入split等，这也是实现Screen功能的一个途径，不过个人认为还是快捷键比较方便些。

六、screen 高级应用

6.1 会话共享

还有一种比较好玩的会话恢复，可以实现会话共享。假设你在和朋友在不同地点以相同用户登录一台机器，然后你创建一个screen会话，你朋友可以在他的终端上命令：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen -x</pre>

这个命令会将你朋友的终端Attach到你的Screen会话上，并且你的终端不会被Detach。这样你就可以和朋友共享同一个会话了，如果你们当前又处于同一个窗口，那就相当于坐在同一个显示器前面，你的操作会同步演示给你朋友，你朋友的操作也会同步演示给你。当然，如果你们切换到这个会话的不同窗口中去，那还是可以分别进行不同的操作的。

6.2 会话锁定与解锁

Screen允许使用快捷键C-a s锁定会话。锁定以后，再进行任何输入屏幕都不会再有反应了。但是要注意虽然屏幕上看不到反应，但你的输入都会被Screen中的进程接收到。快捷键C-a q可以解锁一个会话。

也可以使用C-a x锁定会话，不同的是这样锁定之后，会话会被Screen所属用户的密码保护，需要输入密码才能继续访问这个会话。

6.3 发送命令到screen会话

在Screen会话之外，可以通过screen命令操作一个Screen会话，这也为使用Screen作为脚本程序增加了便利。关于Screen在脚本中的应用超出了入门的范围，这里只看一个例子，体会一下在会话之外对Screen的操作：

<pre style="margin-top: 0px; margin-bottom: 0px; white-space: pre-wrap; overflow-wrap: break-word; font-family: "Courier New" !important; font-size: 12px !important;">[root@TS-DEV ~]# screen -S sandy -X screen ping www.baidu.com</pre>

这个命令在一个叫做sandy的screen会话中创建一个新窗口，并在其中运行ping命令。

6.4 屏幕分割

现在显示器那么大，将一个屏幕分割成不同区域显示不同的Screen窗口显然是个很酷的事情。可以使用快捷键C-a S将显示器水平分割，Screen 4.00.03版本以后，也支持垂直分屏，快捷键是C-a |。分屏以后，可以使用C-a <tab>在各个区块间切换，每一区块上都可以创建窗口并在其中运行进程。

可以用C-a X快捷键关闭当前焦点所在的屏幕区块，也可以用C-a Q关闭除当前区块之外其他的所有区块。关闭的区块中的窗口并不会关闭，还可以通过窗口切换找到它。

[图片上传失败...(image-9009f1-1539427780745)]

6.5 C/P模式和操作

screen的另一个很强大的功能就是可以在不同窗口之间进行复制粘贴了。使用快捷键C-a <Esc>或者C-a [可以进入copy/paste模式，这个模式下可以像在vi中一样移动光标，并可以使用空格键设置标记。其实在这个模式下有很多类似vi的操作，譬如使用/进行搜索，使用y快速标记一行，使用w快速标记一个单词等。关于C/P模式下的高级操作，其文档的这一部分有比较详细的说明。

一般情况下，可以移动光标到指定位置，按下空格设置一个开头标记，然后移动光标到结尾位置，按下空格设置第二个标记，同时会将两个标记之间的部分储存在copy/paste buffer中，并退出copy/paste模式。在正常模式下，可以使用快捷键C-a ]将储存在buffer中的内容粘贴到当前窗口。

[图片上传失败...(image-ad96f2-1539427780745)]

6.6 更多screen功能

同大多数UNIX程序一样，GNU Screen提供了丰富强大的定制功能。你可以在Screen的默认两级配置文件/etc/screenrc和$HOME/.screenrc中指定更多，例如设定screen选项，定制绑定键，设定screen会话自启动窗口，启用多用户模式，定制用户访问权限控制等等。如果你愿意的话，也可以自己指定screen配置文件。

以多用户功能为例，screen默认是以单用户模式运行的，你需要在配置文件中指定multiuser on 来打开多用户模式，通过acl（acladd,acldel,aclchg...）命令，你可以灵活配置其他用户访问你的screen会话。更多配置文件内容请参考screen的man页。



0人点赞



[python](https://www.jianshu.com/nb/30150913)