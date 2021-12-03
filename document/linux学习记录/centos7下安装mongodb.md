# centos7下安装mongodb

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[chenlongjs](https://blog.csdn.net/chenlongjs) 2020-03-03 20:14:47 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10854 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 16

分类专栏： [个人问题总结](https://blog.csdn.net/chenlongjs/category_7726905.html) [服务器配置](https://blog.csdn.net/chenlongjs/category_8017190.html)

版权

# mongodb介绍

MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。Mongo几乎可以实现类似关系数据库单表查询的绝大部分功能，还支持对数据建立索引。

# 下载解压mongodb

**下载压缩包**
我这里选择的是先在官网下载好，然后复制到服务器下
我下载的是
mongodb-linux-x86_64-rhel70-4.0.10.tgz

1）定位到 usr 目录

```
  cd /usr1
```

2）新建mongodb目录
然后再把下载好的压缩包复制到这里来，我用的是**winSCP**这个软件直接拖拉过来的

```
mkdir -m 777 mongodb12
```

3）解压到 usr/mongodb 目录下，并重命名文件夹

```
tar zxvf mongodb-linux-x86_64-rhel70-4.0.10.tgz1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615131143408.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h5YjA5MjY=,size_16,color_FFFFFF,t_70)
4）重命名文件夹

```
mv mongodb-linux-x86_64-rhel70-4.0.10 mongodb-4.0.101
```

# 配置环境变量和初始化操作

1）配置环境变量

```
vi /etc/profile1
```

按下字母 I 键，开始编辑，
在 export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL 一行的上面添加如下内容:

```
export PATH=/usr/mongodb/mongodb-4.0.10/bin:$PATH1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615132848349.png)

按ESC退出编辑，并输入 :wq 保存退出

2）再通过下面的命令使环境变量生效：

```
source /etc/profile1
```

3）回到mongodb目录下创建数据库目录

```
cd  /usr/mongodb/mongodb-4.0.101
```

4）在该目录下新建配置文件

```
touch mongodb.conf1
```

5）创建数据库目录

```
mkdir db1
```

6）创建日志目录

```
mkdir log1
```

7）设置文件夹权限，方便操作

```
chmod 777 db
chmod 777 log12
```

8）创建日志文件

```
cd log
touch mongodb.log12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615134117766.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h5YjA5MjY=,size_16,color_FFFFFF,t_70)

# 修改配置文件内容

1）在mongodb.conf 中添加以下内容

```
port=27017 #端口
dbpath= /usr/mongodb/mongodb-4.0.10/db #数据库存文件存放目录
logpath= /usr/mongodb/mongodb-4.0.10/log/mongodb.log #日志文件存放路径
logappend=true #使用追加的方式写日志
fork=true #以守护进程的方式运行，创建服务器进程
maxConns=100 #最大同时连接数
noauth=true #不启用验证
journal=true #每次写入会记录一条操作日志（通过journal可以重新构造出写入的数据）。
             #即使宕机，启动时wiredtiger会先将数据恢复到最近一次的checkpoint点，然后重放后续的journal日志来恢复。
storageEngine=wiredTiger  #存储引擎，有mmapv1、wiretiger、mongorocks
bind_ip = 0.0.0.0  #设置成全部ip可以访问，这样就可以在windows中去连虚拟机的MongoDB，也可以设置成某个网段或者某个ip1234567891011
```

# 启动mongodb

```
mongod --config /usr/mongodb/mongodb-4.0.10/mongodb.conf1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615135644269.png)

# 关闭防火墙

CentOS 7.0默认使用的是firewall作为防火墙，如果不关闭的话，访问不到mongodb，如果不想关闭也可以开放某个端口。

第一种：
直接关闭firewall：

```
systemctl stop firewalld.service         #停止firewall
systemctl disable firewalld.service    #禁止firewall开机启动12
```

第二种：
直接编辑/etc/sysconfig/iptables文件
在原有的22的端口上一行加入内容并保存

```
-A INPUT -p tcp -m state --state NEW -m tcp --dport 27017-j ACCEPT1
```

重启服务：

```
  service iptables restart1
```

查看端口是否开放：

```
more /etc/sysconfig/iptables1
```

到这里我们的安装结束，现在我们打开工具去测试连接是否成功~~

# 推荐使用可视化工具

推荐使用工具：  Studio3T
测试连接图片

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061516533192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h5YjA5MjY=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615165353754.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h5YjA5MjY=,size_16,color_FFFFFF,t_70)
连接成功，大功告成！！！

怎么下载和使用该工具，可以看我的另外一篇微博：

配置开启启动
编写启动脚本

vim /etc/init.d/mongodb
添加如下内容

```
#!/bin/sh



#



#chkconfig: 2345 80 90



#description: mongodb



start() {



 /usr/mongodb/mongodb-4.0.10/mongod -f /usr/mongodb/mongodb-4.0.10/mongodb.conf



}



 



stop() {



  /usr/mongodb/mongodb-4.0.10/ -f /usr/mongodb/mongodb-4.0.10/mongodb.conf --shutdown



}



 



case "$1" in



  start)



 start



 ;;



  stop)



 stop



 ;;



  restart)



 stop



 start



 ;;



  *)



 echo $"Usage: $0 {start|stop|restart}"



 exit 1



esac
```

点击Esc，输入 :wq 完成编辑并保存退出

之后执行如下脚本
cd /etc/init.d
chkconfig --add mongodb
chmod +x mongodb
chkconfig mongodb on

重启系统
reboot

停止mongodb服务
service mongodb stop

开启mongodb服务
service mongodb start

# Centos7 安装MongoDB

[![img](https://upload.jianshu.io/users/upload_avatars/7810329/ea24f4ab-c47c-4223-b9bb-a5541b2d2bad.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/89c061b853ad)

[dev_winner](https://www.jianshu.com/u/89c061b853ad)[![  ](https://upload.jianshu.io/user_badge/19c2bea4-c7f7-467f-a032-4fed9acbc55d)](https://www.jianshu.com/mobile/creator)关注

0.5652021.01.10 15:13:59字数 314阅读 639

下载地址：[https://www.mongodb.com/try/download/community](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.mongodb.com%2Ftry%2Fdownload%2Fcommunity)

![img](https://upload-images.jianshu.io/upload_images/7810329-2cdfba4c645c7742.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

- 上传到服务器后解压压缩包并更改目录名为`mongodb`：



```css
tar -zxvf mongodb-linux-x86_64-rhel70-4.4.3.tgz
mv mongodb-linux-x86_64-rhel70-4.4.3 mongodb
```

- 在安装目录下新建3个文件夹，分别用来存储数据、存储日志和存放配置文件：



```kotlin
mkdir -p ./data/db
mkdir ./logs
mkdir ./conf
```

- 在安装目录下的`conf`文件夹中新建一个文件`mongod.conf`。注意：mongodb3.0之后的配置文件采用YAML格式，其内容使用`<key>:<value>`表示，开头使用`空格`作为缩进。若`:`之后有value，则需紧跟一个`空格`；若key只是表示层级，则无需在`:`后增加空格。按照层级，每行`4个空格`缩进，第二级则8个空格，依次类推，顶层则不需要空格缩进。



```bash
 systemLog:
#mongodb发送所有日志输出的目标指定为文件
    destination: file
#mongod或mongos应向其发送所有诊断日志记录信息的日志文件的路径
    path: /opt/mongodb/logs/mongod.log
#当mongos或mongod实例重启时，其会将新条目追加到现有日志文件的末尾。
    logAppend: true
 storage:
#mongod实例存储其数据的目录。storage.dbPath设置仅适用于mongod。
    dbPath: /opt/mongodb/data/db
    journal:
#启用或禁用持久性日志以确保数据文件保持有效和可恢复。
        enabled: true
 processManagement:
#启用在后台运行mongos或mongod进程的守护进程模式。
    fork: true
 net:
#服务实例绑定的IP，默认是localhost，为了外部访问，此处应添加局域网ip而非公网ip
    bindIp: localhost,192.168.211.2
#绑定的端口，默认是27017
    port: 27017
```

- 启动mongodb服务：`./bin/mongod -f ./conf/mongod.conf`

![img](https://upload-images.jianshu.io/upload_images/7810329-d9ab59fc603f0c78.png?imageMogr2/auto-orient/strip|imageView2/2/w/845/format/webp)

mongod服务启动成功

- 停止和关闭mongod服务有两种方式：①快速关闭：`kill -2 mongod进程号`；②标准的关闭方法：通过mongo客户端中的shutdownServer命令来关闭服务：



```bash
#客户端登录服务
#注意，这里是通过localhost登录，若需要远程登录，必须先登录认证才可以进行下一步。
mongo --port 27017
#切换到admin库
use admin
#关闭服务
db.shutdownServer()
```

- 补充：若出现这个错误：`mongoDB ERROr: child process failed, exited with error number 48`，则需进行如下操作：



```bash
#删除 *.lock 文件
rm -f ./data/db/*.lock
#删除所有日志文件并在mongodb安装目录下创建logs文件夹
rm -rf ./logs & mkdir ./logs
#修复数据：
./bin/mongod --repair 
ps -ef | grep mongo
./bin/mongod -f ./conf/mongod.conf
```



3人点赞



[环境搭建及工具使用](https://www.jianshu.com/nb/39395212)