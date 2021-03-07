# leanote搭建以及数据迁移

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[涛哥带你学编程](https://blog.csdn.net/hq86937375) 2021-01-27 14:33:44 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 82 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

文章标签： [leanote](https://www.csdn.net/tags/MtzaMg1sMDM2NTgtYmxvZwO0O0OO0O0O.html) [mongodb](https://www.csdn.net/tags/MtzaYg0sNzI3MS1ibG9n.html)

版权

**背景：**

现有的蚂蚁笔记部署在机器xx.x.xxx.135上，之后这台机器不使用了，需要将蚂蚁笔记以及相关数据都迁移到另一台机器xx.x.xxx.55上

------

**思路：**

1. 重新部署搭建新的leanote
2. 从原机器上备份全部的数据，并在新机器上恢复数据

------

**步骤：**

1.安装数据库MongoDB

蚂蚁笔记使用的数据库就是MongoDB

（1）添加yum源

```
vi /etc/yum.repos.d/mongodb-org-4.0.repo
```

添加以下内容：

```
[mongodb-org-4.0]



name = MongoDB Repository



baseurl = https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.0/x86_64/



gpgcheck = 1



enabled = 1



gpgkey = https://www.mongodb.org/static/pgp/server-4.0.asc
```

退出保存

（2）使用yum安装相应版本MongoDB

```
yum install -y mongodb-org-4.0.9 mongodb-org-server-4.0.9 mongodb-org-shell-4.0.9 mongodb-org-mongos-4.0.9 mongodb-org-tools-4.0.9
```

2.下载蚂蚁笔记

从蚂蚁笔记官网下载相应的压缩包

```
leanote-linux-amd64-v2.6.1.bin.tar.gz
```

创建目录developer存放压缩包以及相应数据

```
cd /



#创建一个developer目录用于存放压缩包和数据，当然你也可以选择其他的目录结构



mkdir developer



cd developer



# 上传安装包至该目录下并创建等会需要使用的目录，mongodbdata用于存放数据库，log用于存放日志



mkdir mongodbdata



mkdir log



#解压该压缩包



tar -zxvf leanote-linux-amd64-v2.6.1.bin.tar.gz
```

启动MongoDB数据库，并导入蚂蚁笔记初始化数据，蚂蚁笔记初始化数据存放在**/developer/leanote/mongodb_backup/leanote_install_data**

```
#后台运行，以守护进程的方式运行mongodb数据库，需要--fork #需要设置日志路径和自定义数据库路径--logpath和--dbpath#--fork has to be used with --logpath or --syslog



 



mongod --fork --logpath /developer/log/mongodb.log --dbpath /developer/mongodbdata 



 



#Leanote 初始数据存储在${PATH_TO_LEANOTE}/mongodb_backup/leanote_install_data



# 初始化才运行此行，再次重启时无需运行该行命令



 



mongorestore -h localhost -d leanote --dir /developer/leanote/mongodb_backup/leanote_install_data/
```

3.进入MongoDB数据库，为leanote数据库添加root用户

```
# 进入MongoDB



mongo



 



# 切换到leanote数据库



use leanote;



 



# 添加root用户



db.createUser(



  {



    user: "root",



    pwd: "xxxx",



    roles: [ { role: "dbOwner", db: "leanote" } ]



  }
```

修改蚂蚁笔记相应配置表**/developer/leanote/conf/app.conf**

![img](https://img-blog.csdnimg.cn/2021012710413811.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hxODY5MzczNzU=,size_16,color_FFFFFF,t_70)

4.启动蚂蚁笔记

```
#后台运行脚本，设置日志路径为/developer/log/leanote.log



nohup bash /developer/leanote/bin/run.sh >/developer/log/leanote.log 2>&1 &
```

5.测试与修改管理员admin密码

在地址栏输入http://***${centos ip}\***:8098,即可看到以下页面。

![img](https://img-blog.csdnimg.cn/20210127143009959.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hxODY5MzczNzU=,size_16,color_FFFFFF,t_70)

蚂蚁笔记默认管理员账号和密码为 admin abc123。为了安全，应该第一时间修改管理员密码，具体操作：管理员账号登录后，个人中心直接修改密码

6.数据迁移与恢复

（1）在原机器上备份leanote数据

```
mongodump --port 27017 --db leanote -o /data/leanoteBackUp/
```

（2）使用scp命令将备份数据拷贝到新机器上

```
scp -r leanoteBackUp root@xx.x.xxx.xx:/developer/data
```

（3）回去新机器上，先关闭leanote服务，直接杀进程

![img](https://img-blog.csdnimg.cn/20210127105643700.png)

（4）恢复备份数据

```
mongorestore -h 127.0.0.1:27017 -d leanote /developer/data/leanoteBackUp/leanote -u=root -p=xxxx
```

（5）重新启动leanote服务

```
nohup bash /developer/leanote/bin/run.sh >/developer/log/leanote.log 2>&1 &
```

（6）到此蚂蚁笔记数据迁移恢复完毕，但是在新的机器上登录蚂蚁笔记时，发现有很多图片没有显示，原因在于图片信息存放在leanote下的files目录下，所以还需要将files目录备份。具体操作方法：直接将原机器中的files目录拷贝到新机器中即可。

7.leanote开机自启动设置

（1）切换到以下目录

```
cd  /etc/rc.d/init.d
```

（2）创建 leanote的一个自启动脚本

```
#!/bin/bash



# chkconfig: 2345 80 90



#description:leanote.sh



cd /developer/leanote/bin/



bash run.sh
```

（3）设置脚本权限

```
chmod 754 leanote.sh
```

（4）服务脚本加入到系统启动队列

```
chkconfig --add leanote.sh  



chkconfig leanote.sh on
```

8.设置MongoDB开启启动

在/etc/rc.local添加以下脚本

```
# add mongodb service



mongod --fork --logpath /developer/log/mongodb.log --dbpath /developer/mongodbdata
```

9.定时备份蚂蚁笔记数据，并将备份数据发送到另一台机器存储

编写备份脚本

```
DUMP=/usr/bin/mongodump             # mongodump备份文件执行路径



OUT_DIR=/data/backupLeanoteMongodb    # 临时备份目录



TAR_DIR=/data/backupLeanoteMongodb   # 备份存放路径



DATE=`date -d "today" +"%Y-%m-%d-%H-%M-%S"`         # 获取当前系统时间，作为文件名的一部分



DAYS=7



TAR_BAK="leanote_mongodb_bak_$DATE.tar.gz"                 # 最终保存的数据库备份文件名



cd $OUT_DIR



rm -rf $OUT_DIR/



mkdir -p $OUT_DIR/$DATE



mkdir -p $TAR_DIR/



$DUMP -d leanote -o $OUT_DIR/$DATE                             # 备份leanote数据库



tar -zcvf $TAR_DIR/$TAR_BAK $OUT_DIR/$DATE                      # 压缩为.tar.gz格式



#find $TAR_DIR/ -mtime +$DAYS -delete                # 删除7天前的备份文件



sshpass -p xxxx scp $TAR_DIR/$TAR_BAK  root@xxx.xx.xxx.xx:$TAR_DIR  # 通过 scp 发送至另一台服务器
```

将定时任务执行脚本写入**/var/spool/cron/root**中

```
30 0-23/12  * * * bash /developer/leanote_bak.sh
```

## 使用云服务器搭建个人 Leanote 云笔记本

[我有个疯姑娘](https://yq.aliyun.com/users/khocr3id33ioe) 2019-12-09 17:27:22 浏览2833

- [MongoDB](https://yq.aliyun.com/tags/type_blog-tagid_91/)
-  

- [域名](https://yq.aliyun.com/tags/type_blog-tagid_381/)
-  

- [LOG](https://yq.aliyun.com/tags/type_blog-tagid_471/)
-  

- [云服务器](https://yq.aliyun.com/tags/type_blog-tagid_508/)
-  

- [path](https://yq.aliyun.com/tags/type_blog-tagid_679/)
-  

- [配置](https://yq.aliyun.com/tags/type_blog-tagid_698/)
-  

- [域名解析](https://yq.aliyun.com/tags/type_blog-tagid_746/)
-  

- [域名购买](https://yq.aliyun.com/tags/type_blog-tagid_804/)
-  

- [数据存储](https://yq.aliyun.com/tags/type_blog-tagid_3231/)

**一、下载启动 MongoDB**

`Leanote` 依赖 `MongoDB` 作为数据存储，开始安装 MongoDB：

下载 MongoDB

进入 `/home` 目录，并下载 `MongoDB`：

```
cd /home
wget http://labs-1253675457.cosgz.myqcloud.com/mongodb-linux-x86_64-3.0.1.tgz
```

解压缩源码包：

```
tar -xzvf mongodb-linux-x86_64-3.0.1.tgz
```

创建用于存储的文件夹目录

```
mkdir -p /data/db
```

配置 `MongoDB` 的环境变量：

编辑 `/etc/profile`，在文件末尾追加以下配置：

示例代码：/etc/profile

```
export PATH=$PATH:/home/mongodb-linux-x86_64-3.0.1/bin
```

并执行以下命令，使环境变量生效。

```
source /etc/profile
```

启动 `MongoDB`（启动大概需要 3 ~ 5 分钟）：

```
mongod --bind_ip localhost --port 27017 --dbpath /data/db/ --logpath=/var/log/mongod.log --fork
```

**二、安装 `Leanote`**

`Leanote` 是一款 `Linux` 下开源的软件，开始安装 `Leanote`：

下载 Leanote

先进入 `/home` 目录

```
cd /home
wget http://labs-1253675457.cosgz.myqcloud.com/leanote-linux-amd64-v2.4.bin.tar.gz
```

解开压缩包：

```
tar -zxvf leanote-linux-amd64-v2.4.bin.tar.gz
```

编辑 `Leanote` 配置文件

编辑文件 `/home/leanote/conf/app.conf`，在文件中找到 `app.secret=` 项，并修改为如下内容：

```
app.secret=qcloud666
```

初始化数据库

导入初始化数据：

```
mongorestore -h localhost -d leanote --dir /home/leanote/mongodb_backup/leanote_install_data/
```

启动 `Leanote` 服务

```
nohup /bin/bash /home/leanote/bin/run.sh >> /var/log/leanote.log 2>&1 &
```

**三、准备域名和证书**

如果不需要通过域名访问 `Leanote` 云笔记本则到此就结束了，通过访问 [http:// 地址>:9000 就可以了使用自己的笔记本，初始化账户： admin，初始化密码： abc123](https://yq.aliyun.com/go/articleRenderRedirect?url=)

域名注册

可以在腾讯云或阿里云上进行购买

域名解析

域名购买完成后, 需要将域名解析到云服务器上

域名设置解析后需要过一段时间才会生效，通过 ping 命令检查域名是否生效

如果 ping 命令返回的信息中含有你设置的解析的 IP 地址，说明解析成功。

访问 Leanote 云笔记本

通过 ip 访问笔记本
通过访问 [http://](https://yq.aliyun.com/go/articleRenderRedirect?url=)你的域名:9000 就可以了使用自己的笔记本。

初始化账户： admin
初始化密码： abc123

[云小站](https://www.aliyun.com/minisite/goods?userCode=mrbq2fmx)

本文首发在云栖社区，遵循云栖社区版权声明：本文内容由互联网用户自发贡献，版权归用户作者所有，云栖社区不为本文内容承担相关法律责任。云栖社区已在2020年6月升级到阿里云开发者社区。如果您发现有涉



