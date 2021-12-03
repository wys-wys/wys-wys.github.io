CentOS 为 vsftpd 启动 vsftpd：500 OOPS: cannot read config file: /etc/vsftpd/vsftpd.conf

mingyuanchen 2013-09-02 11:18:32  5434  收藏 2
版权
安装vsftp，yum install vsftp*
启动时报如下错误：
为 vsftpd 启动 vsftpd：500 OOPS: cannot read config file: /etc/vsftpd/vsftpd.conf




查看配置
grep -v ^# /etc/vsftpd/vsftpd.conf | grep -v ^$
anonymous_enable=YES
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
xferlog_std_format=YES
listen=YES
pam_service_name=vsftpd
userlist_enable=YES
tcp_wrappers=YES


查看配置文件的权限，都正常
网上搜索，搜索出一大堆乱七八槽的东西，没有任何帮助


突然同事提醒了一句，看看selinux关闭了没有
没关，改为disabled, setenforce 0不重启使之生效
再重新启动vsftpd，OK，正常了
查看SELinux状态：

1、/usr/sbin/sestatus -v ##如果SELinux status参数为enabled即为开启状态

SELinux status: enabled

2、getenforce ##也可以用这个命令检查

关闭SELinux：

1、临时关闭（不用重启机器）：

setenforce 0 ##设置SELinux 成为permissive模式

##setenforce 1 设置SELinux 成为enforcing模式

2、修改配置文件需要重启机器：

修改/etc/selinux/config 文件

将SELINUX=enforcing改为SELINUX=disabled

重启机器即可

参考：http://lynnteng0.blog.51cto.com/2145094/1124889

http://bguncle.blog.51cto.com/3184079/957315


————————————————
版权声明：本文为CSDN博主「mingyuanchen」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u011882565/article/details/10903105