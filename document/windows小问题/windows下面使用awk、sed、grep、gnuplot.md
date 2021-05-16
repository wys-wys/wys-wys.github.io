# [好久不见](https://www.cnblogs.com/onelikeone/)

## 不滞于物，草木竹石均可为剑。自此精修，渐进于无剑胜有剑之境

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/onelikeone/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/行走的思想)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/onelikeone/rss/)

随笔- 888 文章- 140 评论- 26 阅读- 135万 

# [原来windows下也可以用awk](https://www.cnblogs.com/onelikeone/p/9116629.html)

https://sourceforge.net/projects/gnuwin32/files/gawk/3.1.6-1/gawk-3.1.6-1-bin.zip/download

 

 

# [windows下面使用awk、sed、grep、gnuplot](http://blog.sciencenet.cn/home.php?mod=space&uid=858128&do=blog&quickforward=1&id=994394)

分类: [Android ADB命令](https://www.cnblogs.com/onelikeone/category/1184994.html)

# windows下面使用awk、sed、grep、gnuplot

已有 25739 次阅读 2016-8-4 08:36 |个人分类:[powershell](http://blog.sciencenet.cn/home.php?mod=space&uid=858128&do=blog&classid=171522&view=me)|系统分类:[科研笔记](http://blog.sciencenet.cn/home.php?mod=space&do=blog&view=all&uid=858128&catid=1)

下载windows版本的awk软件：

http://sourceforge.net/projects/gnuwin32/files/gawk/3.1.6-1/gawk-3.1.6-1-bin.zip/download

然后解压，bin文件夹下面就有gawk.exe，这是可以直接在powershell下面运行的程序。接下来添加别名：

1）Set-ExecutionPolicy RemoteSigned

2）Set-Alias awk "D:Program Filesgawk-3.1.6-1-binbin./gawk.exe"

然后就可以体验awk的神奇了。

下载windows版本的sed软件：

https://sourceforge.net/projects/gnuwin32/files/sed/4.2.1/

安装软件，我选择的目录是：D:Program FilesGnuWin32

然后同上，powershell下面运行的程序。接下来添加别名：

1）Set-ExecutionPolicy RemoteSigned

2）Set-Alias sed "D:Program FilesGnuWin32bin./sed.exe"

然后就可以体验sed的神奇了。

下载windows版本的grep软件：

https://sourceforge.net/projects/gnuwin32/files/grep/2.5.4/grep-2.5.4-setup.exe/download

安装软件，我选择的目录是：D:Program FilesGnuWin32

然后同上，powershell下面运行的程序。接下来添加别名：

1）Set-ExecutionPolicy RemoteSigned

2）Set-Alias grep "D:Program FilesGnuWin32bin./grep.exe"

然后就可以体验grep的神奇了。

下载windows版gnuplot：

https://sourceforge.net/projects/gnuplot/files/gnuplot/5.0.4/

操作如上；

说明：删除别名的方法

del Alias:grep
特别注意，上面的方法存在下面问题：

你创建的别名只在当前的会话(session)有效. 要在不同的会话中使用别名, 你必须把别名的定义写入你的Windows PowerShell配置文件, 或者使用Export-Alias将别名存储到文件里。

具体参看《powershell使用vim》







转载本文请联系原作者获取授权，同时请注明本文来自陈超科学网博客。
链接地址：

http://blog.sciencenet.cn/blog-858128-994394.html

上一篇：[DLL显式调用与TCP传输结构体](http://blog.sciencenet.cn/blog-858128-992990.html)
下一篇：[powershell中使用的小命令汇总](http://blog.sciencenet.cn/blog-858128-994407.html)