# [linux服务开机自启动&注册系统服务](https://www.cnblogs.com/xulan0922/p/9213578.html)

首先先看下linux系统开机启动顺序，如下图

 ![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622144027181-617243447.png)

 

对，要解决Linux CentOS 和 Red Hat Linux 系统中设置服务自启动有两种方式，就是从图中圈出的两个步骤下手。

 

## 一、修改 /etc/rc.local 文件，添加启动服务的命令

先写好启动脚本或者启动命令，事先保证启动脚本或命令能正常启动服务，然后将脚本路径或启动命令添加至/etc/rc.local文件中，这个方法适合比较简单的shell脚本，比较方便，具体看最后的本次解决方案。

 

## 二、把可执行程序注册为系统服务，并设定级别的自启动

### 1、 注册系统服务

我想使用"service xxxx start"这样的简短命令来管理，就必须注册成为系统服务，那就是在目录 /etc/init.d/ 下，新建一个以服务名为文件名的文件。

如果我们打开目录 /etc/init.d/，看到的文件其实都是服务程序文件，每个文件的内容都大同小异，我们会看到，这里的文件在文件结构上几乎是一样的。几乎每个文件都有 start、stop、restart和status这样的标志，对，我们新建的这个文件也必须具有相同的结构，即可以接受start和stop参数并完成相应的操作。可以这么理解：

service httpd 等价 /etc/rc.d/init.d/httpd

service httpd start 等价 /etc/rc.d/init.d/httpd start

service httpd stop 等价 /etc/rc.d/init.d/httpd stop

所以/etc/init.d/下的这个脚本一般都会有start、stop等方法。这里可以参考mysql公司提供的写好的mysqld，所以我们装mysql的时候一般都会cp mysql.server /etc/init.d/mysql。

### 2、 设定级别的自启动（这里又有两种方式：ln -s软连接和chkconfig）

- **ln -s软连接：**

　　在 Linux 中有 7 种运行级别（可在 /etc/inittab 文件设置），每种运行级别分别对应着 /etc/rc[0~6].d 这 7个目录。这 7个目录中，每个目录分别存放着对应运行级别加载时需要关闭或启动的服务，如下图 rc3.d 目录所示，其实每个脚本文件都对应着 /etc/init.d/ 目录下具体的服务，K 开头的脚本文件代表运行级别加载时需要关闭的，S 开头的代表需要执行启动的。

　　![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622144320265-725498811.png)

　　格式：ln -s 目标文件名 连接文件名

　　例子：cd /etc/rc3.d/

　　ln -s ../init.d/hdz_service ./S99hdz_service

　　连接文件名采用“SXX目标文件名”的格式，其中XX一般是一个从1到100的整数，它表示启动优先级，数字越大，优先级越低，比如：服务A的运行要依赖服务B，那A的XX数字就应该大于B的。后跟“目标文件名”是为了一目了然，一看就知道是哪个文件的符号连接。
　　目录 /etc/rc3.d/ 是系统启动时自动搜索的目录，该目录下的符号连接文件的目标文件，都将被运行，这就是在这个目录建立符号连接的原因——为了开机就运行。

- **Chkconfig命令添加管理服务:**

　　Ps: **服务管理，centos是chkconfig，ubuntu是update-rc.d**

　　1.查看是否已经注册为服务，查看命令：chkconfig --list mysqld*(*以 mysqld 为例*)*

　　*![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622144740788-1326434038.png)*

　　通过命令没有查看到，说明还没有添加到启动服务，通过命令 chkconfig --add mysqld 添加即可。

　　2.给服务可执行的权限：

　　# chmod 755 mysqld 

　　3.如果需要自启动某些服务，只需使用命令*chkconfig <**服务名>* on 即可，若想关闭，将 on 改为 off。

　　# chkconfig mysqld on

　　在默认情况下，chkconfig 会自启动 2345 这四个级别，如果想自定义启动级别可以加上 --leve l选项，后边跟指定的启动级别。

　　**示例：**先将 mysqld 服务的所有启动级别关闭，然后使用 --level选项启动自定义级别。

　　chkconfig --level 2345 mysqld off  #关闭2345级别启动。

 　![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622144828990-858209199.png)

　　chkconfig --level 35 mysqld on #指定3、5级别启动。

　　![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622144847095-2033001087.png)

其中2345是默认启动级别，级别有0-6共7个级别。

　　等级0表示：表示关机 　　

　　等级1表示：单用户模式 　　

　　等级2表示：无网络连接的多用户命令行模式 　　

　　等级3表示：有网络连接的多用户命令行模式 　　

　　等级4表示：不可用 　　

　　等级5表示：带图形界面的多用户模式 　　

　　等级6表示：重新启动

　　10是启动优先级，90是停止优先级，优先级范围是0－100，数字越大，优先级越低。

ps：这里另外提一句，关于systemctl 命令，是centos7才有的，6和6之前的版本都没有，systemctl 是系统服务管理器命令,它将 service 和 chkconfig 这两个命令组合到一起，也可以设置开机启动，关于systemctl和chkconfig的区别请参考http://blog.csdn.net/kenhins/article/details/74518978

### ----------------------------------------------小技巧---------------------------------------------

　　已上的步骤比较麻烦，能否把这几个步骤自动化一下？这样在一台新机子上部署就方便了。还记得我们那个记录代码文件之间依赖关系的makefile文件吗？我们在这里要用到它了。
　　在makefile文件中添加一个标志，并在该标志下添加和下面类似的代码：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 install:
 cp ./hdz_pro /usr/sbin/
 cp ./hdz_service /etc/init.d/
 cd /etc/init.d/
 chmod +x hdz_service
 cd /etc/rc3.d/
 ln -sf ../init.d/hdz_service ./S99hdz_service
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　在标志install下的没一句话，前面一定要留空白，这不仅是有利于阅读，更是一个要求，makefile文件要求每一句可执行语句前都要有空白（空格或tab）。

　　上面代码中的 hdz_pro 和 hdz_service 分别是可执行文件名和服务名，这两个名称换成你自己的就行了，操作时用以下命令： make install

​    运行完就一切OK了。

### ----------------------------------------------------------------------------------------------------------

###  本次关于解决阿里云开机启动apicy中间件12301.jar的解决方案（采用第一种方式）

**1.新建一个脚本，如/home/server/middleware.sh，内容如下**

```
#/bin/bash
export JAVA_HOME=/home/dev/jdk/jdk1.8.0_20
export PATH=$PATH:$JAVA_HOME/bin
nohup java -jar /home/server/12301.jar --spring.profiles.active=pressure >> /home/server/nohup.out 2>&1 &
```

　　Ps:这里有两个注意点

- 有一个nohup: failed to run command ‘java’: No such file or directory的错误就是因为没有导入java的环境变量，所以前两行一定需要。　　

　　![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622150119339-1686894743.png)

-  脚本中一定要用绝对路径，之前写的>> ./nohup.out，就是一个坑，因为开机启动的时候根本没有当前路径。

**2.执行如下命令,将该脚本标记为可执行文件(添加可执行的权限)**

```
　　chmod +x /home/server/middleware.sh
```

**3.修改 /etc/rc.local 文件，添加启动服务的命令**

　　#vi /etc/rc.local

 　![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622150542989-611990471.png)

**4.这样, middleware.sh这个脚本在开机的时候就会被执行了,以后再这里面写启动服务的命令就可以了**

 

###  linux使用某非root用户执行开机启动项（由于服务器由唱游提供，没有root用户）

1.  创建shell脚本，/home/devuser/server/middleware.sh

 　![img](https://images2018.cnblogs.com/blog/1403430/201806/1403430-20180622150743967-1978255010.png)

　　2. 用root用户登录，修改/etc/rc.local，在最后一行添加

　　su - devuser -c "/home/devuser/server/middleware.sh"

　　这个地方一定要注意 su - 这个是环境的变量也会做相应的转换；如果环境变量没有改变的话，我们用su  就可以了。

 

### 总结下，修改 /etc/rc.local 文件的方法一般适用于简单的shell脚本，注册为系统服务（/etc/init.d/）的方法适用于官方就有脚本提供（如mysqld，httpd），或实在有自写服务脚本的需要。

 

分类: [linux](https://www.cnblogs.com/xulan0922/category/1240098.html)