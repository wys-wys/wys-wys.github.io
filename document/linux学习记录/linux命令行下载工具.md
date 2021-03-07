# [Linux 命令行下载工具](https://www.cnblogs.com/duodmi/articles/9768094.html)

## **1.**Wget

　　Wget是一个十分常用命令行下载工具，多数Linux发行版本都默认包含这个工具。如果没有安装可在http://www.gnu.org/software/wget/wget.html下载最新版本进行安装

　　Wget使用格式如下：　　　　

| 下载语法： | wget [选项] [下载地址]                              |              |
| ---------- | --------------------------------------------------- | ------------ |
| 下载示例： | wget https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz | （下载文件） |
| 下载示例： | wget https://www.baidu.com/                         | （下载网页） |

 

##  

##  

##  

## Wget常用参数

　　◆-b：后台下载，Wget默认的是把文件下载到当前目录。

　　◆-O：将文件下载到指定的目录中。

　　◆-P：保存文件之前先创建指定名称的目录。

　　◆-t：尝试连接次数，当Wget无法与服务器建立连接时，尝试连接多少次。

　　◆-c：断点续传，如果下载中断，那么连接恢复时会从上次断点开始下载。

　　◆-r：使用递归下载

 

## 2.Prozilla

　　Prozilla也是一个十分流行的命令行下载工具，支持多线程下载和断点续传功能。可到http://prozilla.genesys.ro/下载最新的1.3.7.4安装包 进行安装使用

Prozilla命令格式如下：

 

| 下载语法： | proz [参数] [下载地址]                              |              |
| ---------- | --------------------------------------------------- | ------------ |
| 下载示例： | proz https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz | （下载文件） |
| 下载示例： | proz https://www.baidu.com/                         | （下载网页） |

 

 

 

 

　　

 

**Prozilla常用的参数**

　　◆-k=n ：设置n个线程下载。不加此参数指定线程数，Prozilla默认为4线程下载。

　　◆-P, --directory-prefix=DIR：指定将下载的文件保存在DIR/目录。

　　◆-r, --resume：继续下载未完成的文件。如果要指定线程数下载可用如下命令： #proz -k=5 https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz 这样便以5线程进行文件的下载，并将文件保存到当前目录。和Wget一样，Prozilla也提供了续传功能，下载中断后，重新输入上述命令，就会出现提示续传，按R键就可继续下载了。

 

## 3.MyGet

MyGet目标设计成一个可扩展的，拥有丰富界面的多线程下载工具，它支持HTTP、FTP、HTTPS、MMS、RTSP等协议。在http://myget.sourceforge.net/release/myget-0.1.0.tar.bz2下载其最新版本0.1.0 安装使用

 

| 下载语法： | mytget [参数] [下载地址]                              |              |
| ---------- | ----------------------------------------------------- | ------------ |
| 下载示例： | mytget https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz | （下载文件） |
| 下载示例： | mytget https://www.baidu.com/                         | （下载网页） |

 

 

 

 

 

 

**MyGet常用的参数**

　　◆-d [目录]：指定下载到的文件在本地存放的位置，默认当前目录。

　　◆-f [文件]：指定下载文件名称。

　　◆-h：帮助选项。

　　◆-n [线程数]：下载线程数量，默认为4个。

　　◆-x [代理服务器地址]：设置代理服务器地址，如“-x http://user:password@host:port”。 MyGet常用的形式如下： #mytget －d /root/ -n 10 https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz

 

## 4.Linuxdown

Linuxdown是一个命令行多线程下载工具，最多可支持30线程的下载。在https://gro.clinux.org/frs/download.php/1015/linuxdown-1.0.0.tar.gz下载最新的1.1.0版本。安装使用

 

linuxdown [下载地址] [选项] [线程数]  需要注意的是下载地址和选项都需要西文引号括起来

| 下载语法： | linuxdown [下载地址] [选项] [线程数]                         |              |
| ---------- | ------------------------------------------------------------ | ------------ |
| 下载示例： | linuxdown “https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz“ 30 | （下载文件） |
| 下载示例： | linuxdown ”https://www.baidu.com/“ 2                         | （下载网页） |

 

 

 

 

 

 

 

## 5.Curl

　　Curl也是Linux下不错的命令行下载工具，小巧、高速，唯一的缺点是不支持多线程下载。在http://curl.haxx.se/download/curl-7.14.0.tar.gz下载最新版本。安装使用


　　Curl使用格式如下： #curl [选项][下载地址]

　　不支持多线程下载

| 下载语法： | curl  [选项][下载地址]                                      |                                                  |
| ---------- | ----------------------------------------------------------- | ------------------------------------------------ |
| 下载示例： | curl -O “https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz“ 30 | （下载文件）使用Curl下载一个文件并保存到当前目录 |
| 下载示例： | curl ”https://www.baidu.com/“ 2                             | （下载网页）                                     |

 

 

 

 

 

 

##  

## 6.Axel

　　Axel是命令行下的多线程下载工具，支持断点续传，速度通常情况下是Wget的几倍。可在http://www.linuxfans.org/nuke/modules.php?name=Site_Downloads&op=mydown&did=1697下载。

　　

　　基本的用法如下： #axel [选项] [下载目录] [下载地址]

 

| 下载语法： | axel   [选项] [下载目录] [下载地址]                          |                                                              |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 下载示例： | axel  -n 10 -o /home/kennycx/ “https://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz“ 30 | （下载文件）用10线程将指定路径的文件下载到/home/kennycx/这个目录下。 |
| 下载示例： | axel  -n 10 -o /home/kennyc2/  ”https://www.baidu.com/“ 2    | （下载网页）用10线程将指定路径的文件下载到/home/kennyc2/这个目录下。 |

 

 

 

 

 

　

 　

本文详细介绍了Linux中常用的下载工具，这些下载工具功能上各有千秋，使用上都比较简单，所以无论是初学者还是Linux高手总有一款适合你。

　　 Linux下用命令行也可以下载HTTP网站的文件。顺便提一下，如果是ftp网站可以用ftp命令然后get XXX。

 

我们感觉困顿的时候，一定不要原地煎熬，一定要支做点什么。