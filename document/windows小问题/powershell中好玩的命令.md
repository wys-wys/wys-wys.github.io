tracert +目标ip路由追踪

ftp 服务端口 20，21； dns服务端口 ：53  ；dhcp服务端口：67，68 ；tftp服务端口：69；https：443；smb：445；mysql：3306；sqlserver：1433；oracle： 1521；telnet：23；smtp：25；pop3:110;  

ipconfig /release 释放清空ip

ipdonfig /renew 重新获取ip

systeminfo 获取系统详细信息

arp -a查看局域网ip

net view 查看局域网中主机名

shutdown -s -t 180 -c “哈哈哈” 命令关机

shutdown -a 取消关机命令

msg 将消息发送给指定用户

start  www.baidu.com 打开

copy拷贝 del删除 md 创建文件夹rd删除文件夹 copy con 133.txt创建文件

type 命令行中查看文件内容 ren 重名名 tree 查看树形文件结构

telnet “windows下的远程终端”、



我们输入net user demo /add 添加一个账户。

然后我们输入net localgroup 来显示计算机的本地组用户，它是根据权限来划分的。

在命令行下输入net localgroup Administrators demo /add。把用户加入某个组

我们使用net user demo来看一下账户信息。

删除这个账户，输入net user demo /del这个命令

net user administrator /active:yes 激活管理员用户

net use k: \\192.168.0.51\c$ 映射磁盘驱动器命令

net start 查看已启动的服务

net start + 服务 启动服务stop是停止

netstat -an 查看服务监听的端口

netstat -n 查看建立的会话

netstat -nb 查看建立会话的进程

netstat -a查看开启了哪些端口常用 netstat -an

netstat -a查看端口的网络连接情况常用netstat -an

telnet +ip +端口 测试端口是否开放

net 设置无线网络

> netsh wlan set hostednetwork mkode=allow ssid=cc key=010715
>
> 启动无线网络： netsh wlan start hosted

netsh wlan show drivers 查看无线网卡驱动信息

schtasks 创建定时任务

attrib 查看文件名或者目录名的属性

ipconfig /release 释放当前ip地址

ipconfig /renew 重新申请一个ip

win + r 输入ncpa.cpl 打开网络适配器

