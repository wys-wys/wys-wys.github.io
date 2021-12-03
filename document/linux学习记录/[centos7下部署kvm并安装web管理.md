- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/zsl-find/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/夜辰雪扬)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/zsl-find/rss/)

随笔- 37 文章- 312 评论- 23 阅读- 14万 

# [centos7下部署kvm并安装web管理客户端](https://www.cnblogs.com/zsl-find/articles/11194999.html)

参考链接

```
https://www.cnblogs.com/root0/p/9356205.html
https://www.cnblogs.com/kcxg/p/11049829.html
https://blog.csdn.net/weixin_43695104/article/details/88554443#31_kvm_60https://www.cnblogs.com/nulige/p/9236191.html
```

 

1.基础环境配置

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
setenforce 0
systemctl stop firewalld
systemctl disable firewalld
sed -i "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config
yum install -y wget
ls /etc/yum.repos.d/
rm -rf /etc/yum.repos.d/*
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum install epel-release -y
yum makecache
vi /etc/resolv.conf 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

2.安装kvm

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
yum makecache #上面没有刷新yum源刷新一下
yum install qemu-kvm libvirt libvirt-python libguestfs-tools virt-install virt-manager #virt-manager为图形管理工具可以选择安装
systemctl enable libvirtd
systemctl start libvirtd
lsmod | grep -i kvm
brctl show #查看网络
virsh net-list #查看网络virsh net-dumpxml default #默认的网络连接方式
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716141300949-264511220.png)

3.桥接设置

3.1vi /etc/sysconfig/network-scripts/ifcfg-ens192 #删除ip的设置并添加红字部分

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="none"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens192"
UUID="fe8d89d2-fe1a-418b-aea2-682643e8661a"
DEVICE="ens192"
ONBOOT="yes"
IPV6_PRIVACY="no"
BRIDGE=br0
NM_CONTROLLED=no
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

3.2 vi /etc/sysconfig/network-scripts/ifcfg-br0 #桥接ip设置

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
TYPE=Bridge
DEVICE=br0
NM_CONTROLLED=no
BOOTPROTO=static
NAME=br0
ONBOOT=yes
IPADDR="192.168.120.54"
PREFIX="24"
GATEWAY="192.168.120.1"
DNS1="223.5.5.5"
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

3.3 重启网卡并测速网络

```
systemctl restart network
ping www.baidu.com
```

3.4下载虚拟机镜像为后面做好准备

```
 cd /var/lib/libvirt/boot/
wget https://mirrors.aliyun.com/centos/7.6.1810/isos/x86_64/CentOS-7-x86_64-Minimal-1810.iso
```

4.安装webvirmgr web管理工具

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
yum -y install git python-pip libvirt-python libxml2-python python-websockify supervisor nginx
yum -y install gcc python-devel
pip install numpy -i https://mirrors.aliyun.com/pypi/simple/ #用阿里源安装numpy组件
cd /server/tools/
mkdir /server/tools/ -pgit clone git://github.com/retspen/webvirtmgr.git #github克隆文件太慢可以下载zip文件解压安装yum install -y unzip zipunzip webvirtmgr-master.zipmv webvirtmgr-master webvirtmgrcd webvirtmgr/pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple #安装所需的pip环境
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

5.设置连接信息并同步配置

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
5.1
./manage.py syncdb #设置登录web登录账号密码 admin可以换成root
You just installed Django's auth system, which means you don't have any superusers defined.
Would you like to create one now? (yes/no): yes
Username (leave blank to use 'root'): admin
Email address: test@163.com
Password: 123456
Password (again): 123456
Superuser created successfully.
Installing custom SQL ...
Installing indexes ...
Installed 6 object(s) from 1 fixture(s)
5.2
./manage.py collectstatic #生成配置文件 输入yes
Type 'yes' to continue, or 'no' to cancel: yes
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

6.配置nginx解析

6.1

```
cd ..
mkdir /var/www
mv webvirtmgr /var/www/
cd /etc/nginx/conf.d/
```

vi /etc/nginx/conf.d/webvirtmgr.conf

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
server {
    listen 80 default_server;

    server_name $hostname;
    #access_log /var/log/nginx/webvirtmgr_access_log;

    location /static/ {
        root /var/www/webvirtmgr/webvirtmgr; # or /srv instead of /var
        expires max;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-for $proxy_add_x_forwarded_for;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_connect_timeout 600;
        proxy_read_timeout 600;
        proxy_send_timeout 600;
        client_max_body_size 1024M; # Set higher depending on your needs
    }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

6.2 关闭默认解析

vi /etc/nginx/nginx.conf #从server行开始注释 只留最后一个大括号

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
#    server {
#        listen       80 default_server;
#        listen       [::]:80 default_server;
#        server_name  _;
#       root         /usr/share/nginx/html;

#       # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;

#       location / {
#        }

#        error_page 404 /404.html;
#            location = /40x.html {
#        }

#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

....
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

 }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

6.3

```
ls /var/www/webvirtmgr/webvirtmgr
chown -R nginx:nginx /var/www/webvirtmgr
service nginx restart #重启nginx生效
```

6.4 设置nginx开机启动

vi /etc/supervisord.d/webvirtmgr.ini

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[program:webvirtmgr]
command=/usr/bin/python /var/www/webvirtmgr/manage.py run_gunicorn -c /var/www/webvirtmgr/conf/gunicorn.conf.py
directory=/var/www/webvirtmgr
autostart=true
autorestart=true
logfile=/var/log/supervisor/webvirtmgr.log
log_stderr=true
user=nginx

[program:webvirtmgr-console]
command=/usr/bin/python /var/www/webvirtmgr/console/webvirtmgr-console
directory=/var/www/webvirtmgr
autostart=true
autorestart=true
stdout_logfile=/var/log/supervisor/webvirtmgr-console.log
redirect_stderr=true
user=nginx
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
service supervisord stop
service supervisord start
```

http://192.168.120.54/

```
admin #上面设置的web登录密码
123456
```

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716144710039-325423156.png)

7 配置宿主机-如果虚拟机比较多，该脚本执行时间会比较长

```
curl http://retspen.github.io/libvirt-bootstrap.sh | sudo sh
```

配置ssh连接

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```javascript
sudo su - nginx -s /bin/bash
-bash-4.2$ ssh-keygen

+-----------------+-bash-4.2$ touch ~/.ssh/config && echo -e "StrictHostKeyChecking=no\nUserKnownHostsFile=/dev/null" >> ~/.ssh/config
-bash-4.2$ chmod 0600 ~/.ssh/config
-bash-4.2$ cat .ssh/id_rsa.pub -bash-4.2$ ssh-copy-id root@192.168.120.54 #拷贝密钥到认证文件夹下
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

然后复制客户端在root下执行

vi /etc/polkit-1/localauthority/50-local.d/50-libvirt-remote-access.pkla

```
[Remote libvirt SSH access]
Identity=unix-user:root
Action=org.libvirt.unix.manage
ResultAny=yes
ResultInactive=yes
ResultActive=yes
chown -R root.root /etc/polkit-1/localauthority/50-local.d/50-libvirt-remote-access.pkla
systemctl restart nginx
systemctl restart libvirtd
```

\8. 然后登录web连接kvm

http://192.168.120.54/login/

admin

123456

1.添加连接

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716145923309-1749460288.png)

 

用root用户 因为上面拷贝密钥用的root用户的

```javascript
-bash-4.2$ ssh-copy-id root@192.168.120.54 #拷贝密钥到认证文件夹下
```

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716145847747-1206908279.png)

 注意 编辑完点击这里其实是54 点击其他地方w无法进入后台 之前添加做了lab ip 后期无法修改

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716150139910-894380835.png)

 

 ![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716150259125-1159116251.png)

 

9.创建虚拟机

9.1创建存储池

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716150639218-672462022.png)

 

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716150726658-1170525442.png)

拷贝之前下载虚拟机iso镜像到默认目录

```
cp /var/lib/libvirt/boot/CentOS-7-x86_64-Minimal-1810.iso /var/lib/libvirt/images/
```

进入存储目录

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716150945702-333689083.png)

可以看到iso文件

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151011529-1692559161.png)

 

9.2 添加系统使用的硬盘

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151140928-266717431.png)

 

 ![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151232493-853582813.png)

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151355515-475245659.png)

 

9.3 网络管理添加桥接网络

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151454684-1266781227.png)

 

网络类型桥接 名称br0 然后创建

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151559254-823984682.png)

 

 

准备工作做完开始创建实例

10.

10.1

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716151857835-652987354.png)

 10.2

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152129981-587600090.png)

10.3设置连接cdrom

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152413126-700288266.png)

设置web 密码 应该是vnc的密码

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152510358-889922187.png)

启动虚拟机 我已经开机 现在只能关闭虚拟机

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152556411-1378701927.png)

web控制台

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152710133-268484928.png)

 

 ![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152736559-461424628.png)

 

特别注意 我是在exsi环境做的测试 开始 无法和外网通信 是网卡需要设置混杂模式 设置后网络正常

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716152941716-1862992227.png)

 

```
virt-manager 管理工具
https://www.cnblogs.com/weilu2/p/kvm_bridge_centos7.html
用云镜像创建虚拟机
https://www.cnblogs.com/kcxg/p/11049829.html
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@localhost centos7-vm1]# ssh-keygen -t ed25519 -C "VM Login ssh key"

[root@localhost centos7-vm1]# virsh net-dhcp-leases default
 2019-07-16 18:32:04  52:54:00:98:46:59  ipv4      192.168.122.53/24         centos7-vm1     -


[root@localhost ~]# cat .ssh/id_ed25519.pub 
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBnkO6rNDbgZbtGsq69NvOfqpLtkEJWIxrC29ymjwTx0 VM Login ssh key

[root@localhost centos7-vm1]# ssh vivek@192.168.122.53

[vivek@centos7-vm1 ~]$ sudo passwd root
123456
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

web界面 可能花屏

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716175327282-1403631332.png)

修改默认的显卡模式为

![img](https://img2018.cnblogs.com/blog/1511243/201907/1511243-20190716175437212-129984445.png)

然后关闭虚拟机 再开机虚拟机就正常了

 虚拟机 压缩和转换

```
qemu-img convert -c -O qcow2 /var/lib/libvirt/images/centos7-vm1/centos7-vm1.qcow2 /var/lib/libvirt/images/centos7-vm1/centos7-new.qcow2

qemu-img convert -c -f raw -O qcow2 /path/old.raw /path/new.qcow2
```

https://www.cnblogs.com/sixloop/p/8515099.html

转换

```
[root@localhost images]# qemu-img info linux66.img #名字是img 实际是qcow2格式

qemu-img convert -c -f raw -O qcow2 /path/old.raw /path/new.qcow2

qemu-img convert -c -O qcow2  /var/lib/libvirt/images/linux66.img /var/lib/libvirt/images/centos7-60.qcow2
```

virtio驱动

```
https://blog.csdn.net/yasyal515/article/details/77649486
https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.141-1/virtio-win-0.1.141.iso
https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/
```

 

满血拉二胡 残血到处浪