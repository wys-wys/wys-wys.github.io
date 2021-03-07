# [Linux nohup命令详解](https://www.cnblogs.com/zq-inlook/p/3577003.html)

**nohup命令及其输出文件**                                                                                             

　　今天在linux上部署wdt程序，在SSH客户端执行./start-dishi.sh,启动成功,在关闭SSH客户端后，运行的程序也同时终止了，怎样才能保证在推出SSH客户端后程序能一直执行呢？通过网上查找资料，发现需要使用nohup命令。

完美解决方案：nohup ./start-dishi.sh >output 2>&1 &

**现对上面的命令进行下解释**

用途：不挂断地运行命令。
语法：nohup Command [ Arg ... ] [　& ]
描述：nohup 命令运行由 Command 参数和任何相关的 Arg 参数指定的命令，忽略所有挂断（SIGHUP）信号。在注销后使用 nohup 命令运行后台中的程序。要运行后台中的 nohup 命令，添加 & （ 表示“and”的符号）到命令的尾部。

操作系统中有三个常用的流：
　　0：标准输入流 stdin
　　1：标准输出流 stdout
　　2：标准错误流 stderr

　　一般当我们用 > console.txt，实际是 1>console.txt的省略用法；< console.txt ，实际是 0 < console.txt的省略用法。

 

 

**下面步入正题：**

\>nohup ./start-dishi.sh >output 2>&1 &

解释：
 \1. 带&的命令行，即使terminal（终端）关闭，或者电脑死机程序依然运行（前提是你把程序递交到服务器上)； 

 \2. 2>&1的意思 

　　这个意思是把标准错误（2）重定向到标准输出中（1），而标准输出又导入文件output里面，所以结果是标准错误和标准输出都导入文件output里面了。 至于为什么需要将标准错误重定向到标准输出的原因，那就归结为标准错误没有缓冲区，而stdout有。这就会导致 >output 2>output 文件output被两次打开，而stdout和stderr将会竞争覆盖，这肯定不是我门想要的. 

　　这就是为什么有人会写成： nohup ./command.sh >output 2>output出错的原因了 

==================================================================================

最后谈一下/dev/null文件的作用，这是一个无底洞，任何东西都可以定向到这里，但是却无法打开。 所以一般很大的stdou和stderr当你不关心的时候可以利用stdout和stderr定向到这里>./command.sh >/dev/null 2>&1 

It’s not too late to change.

# [nohup和&后台运行，进程查看及终止](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html)





# 阅读目录



- nohup和&后台运行，进程查看及终止
  - [1.nohup](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_0)
  - [2.&](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_1)
  - [3.nohup和&的区别  ](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_2)
  - [&：是指在后台运行，当用户退出（挂起）的时候，命令自动跟着结束](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_3)
  - [nohup：不挂断的运行，注意并没有后台运行的功能，就是指用nohup运行命令可以使命令永久的执行下去，和用户终端没有关系，例如我们断开SSH连接都不会影响他的运行，注意了nohup没有后台运行的意思；&才是后台运行因此将nohup和&结合使用，就可以实现使命令永久地在后台执行的功能](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_4)
  - [4.举例](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_5)
  - [1 sh test.sh &](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_6)
  - [2 nohup sh test.sh](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_7)
  - [3 nohup sh test.sh &](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_8)
  - [输出重定向](https://www.cnblogs.com/yunwangjun-python-520/p/10713564.html#_label0_9)

 

**正文**

# nohup和&后台运行，进程查看及终止



## 1.nohup

用途：不挂断地运行命令。我们在使用Xshell等工具执行Linux脚本时，有时候会由于网络问题，导致失去连接，终端断开，程序运行一半就意外结束了。这种时候，就可以用nohup指令来运行指令，使程序可以忽略挂起信号继续运行。

语法：nohup Command [ Arg … ] [　& ]

　　无论是否将 nohup 命令的输出重定向到终端，输出都将附加到当前目录的 nohup.out 文件中。

　　如果当前目录的 nohup.out 文件不可写，输出重定向到 $HOME/nohup.out 文件中。

　　如果没有文件能创建或打开以用于追加，那么 Command 参数指定的命令不可调用。

退出状态：该命令返回下列出口值： 　

　　126 可以查找但不能调用 Command 参数指定的命令。 　

　　127 nohup 命令发生错误或不能查找由 Command 参数指定的命令。 　

　　否则，nohup 命令的退出状态是 Command 参数指定命令的退出状态。

 



## 2.&

用途：在后台运行

一般两个一起用

nohup command &



## 3.nohup和&的区别  



## &：是指在后台运行，当用户退出（挂起）的时候，命令自动跟着结束



##  nohup：不挂断的运行，注意并没有后台运行的功能，就是指用nohup运行命令可以使命令永久的执行下去，和用户终端没有关系，例如我们断开SSH连接都不会影响他的运行，注意了nohup没有后台运行的意思；&才是后台运行  因此将nohup和&结合使用，就可以实现使命令永久地在后台执行的功能



## 4.举例



## 1 sh test.sh &

```
将sh test.sh任务放到后台 ，关闭xshell，对应的任务也跟着停止
```

 



##  2 nohup sh test.sh

```
将sh test.sh任务放到后台，关闭标准输入，终端不再能够接收任何输入（标准输入），重定向标准输出和标准错误到当前目录下的nohup.out文件，
即使关闭xshell退出当前session依然继续运行
```

 



##  3 nohup sh test.sh &

```
将sh test.sh任务放到后台，但是依然可以使用标准输入，终端能够接收任何输入，重定向标准输出和标准错误到当前目录下的nohup.out文件，
即使关闭xshell退出当前session依然继续运行
```

 



## 输出重定向

　　

```
作业在后台运行的时候，可以把输出重定向到某个文件中，相当于一个日志文件，记录运行过程中的输出。使用方法：nohup command > out.file 2>&1 &
command>out.file是将command的输出重定向到out.file文件，即输出内容不打印到屏幕上，而是输出到out.file文件中。
在上面的例子中，0 – stdin (standard input)，1 – stdout (standard output)，2 – stderr (standard error) ；
2>&1是将标准错误（2）重定向到标准输出（&1），标准输出（&1）再被重定向输入到out.file文件中。
```

 

 





举个例子，我们需要保持 test.py 程序的持续运行（用于长时间训练神经网络），并且将控制台输出重定向到日志文件中，那么如下命令可以轻松办到：

```
nohup python test.py > log.txt &
```

在使用 nohup 后台运行命令之后，需要使用 exit 正常退出当前账户，这样才能更好地保证命令一直在后台运行。

上述进程保持持续运行一段时间后，若想停止运行，即杀掉该进程，有如下操作：

```
kill -9  进程id
```

 

```
 
```

eg:

```
nohup /usr/local/node/bin/node /www/im/chat.js >> /usr/local/node/output.log 2>&1 &
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320150831908-545166421.png)

进程号7585

查看运行的后台进程

（1）jobs -l

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320150912955-1772662776.png)

jobs命令只看当前终端生效的，关闭终端后，在另一个终端jobs已经无法看到后台跑得程序了，此时利用ps（进程查看命令）

（2）ps -ef 

```
ps -aux|grep chat.js
 a:显示所有程序 
 u:以用户为主的格式来显示 
 x:显示所有程序，不以终端机来区分
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320153334877-1168175476.png)

注：

　　用ps -def | grep查找进程很方便，最后一行总是会grep自己

　　用grep -v参数可以将grep命令排除掉

```
ps -aux|grep chat.js| grep -v grep
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320153456502-1139370768.png)

　　再用awk提取一下进程ID　

```
ps -aux|grep chat.js| grep -v grep | awk ``'{print $2}'
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320153606799-967154073.png)

3.如果某个进程起不来，可能是某个端口被占用

查看使用某端口的进程

```
lsof -i:8090
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320154514377-1985478430.png)

```
netstat -ap|grep 8090
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320154600658-246972161.png)

查看到进程id之后，使用netstat命令查看其占用的端口

```
netstat -nap|grep 7779
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320155041815-1272481492.png)

使用kill杀掉进城后再启动

4.终止后台运行的进程

```
kill -9 进程号
```

![img](https://images2015.cnblogs.com/blog/798214/201703/798214-20170320153728049-88100874.png)

 

 

作者：[Mr_Yun](http://www.cnblogs.com/yunwangjun-python-520/)
欢迎任何形式的转载，但请务必注明出处。
限于本人水平，如果文章和代码有表述不当之处，还请不吝赐教。

# 【Linux】nohup后台运行脚本 终止脚本运行

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[凭栏观雨_远](https://blog.csdn.net/plgy_Y) 2019-04-18 16:24:57 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3180 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [Linux](https://blog.csdn.net/plgy_y/category_6434763.html) 文章标签： [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [nohup](https://www.csdn.net/tags/MtTaEg0sMjAwMDMtYmxvZwO0O0OO0O0O.html) [nohup终止](https://so.csdn.net/so/search/s.do?q=nohup终止&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

#### command &和nohup command区别

command & 是后台运行 Ctrl + C后程序**不停止运行**，关闭shell会话后或者其他原因导致shell会话退出 程序**停止运行**

nohup command shell会话退出后，程序不停止运行，Ctrl+C程序停止运行

#### nohup后台运行脚本

nohup command &

#### 终止脚本运行

1. `ps -aux | grep .sh`
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190418162221697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BsZ3lfWQ==,size_16,color_FFFFFF,t_70)
2. `kill -9 PID`
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190418162057191.png)
   终止脚本，此时可能会遇到一些意外情况，比如：脚本中运行hadoop拷贝数据，`hdfs dfs -cp 源目录 目标目录`
   这个命令会启FsShell进程。此时还需要运行`jps`查看正在运行的FsShell进程，`kill -9 PID`，kill掉。