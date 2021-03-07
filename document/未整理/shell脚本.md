在当前shell中执行脚本

> . /脚本

> source /脚本 

在子shell中执行脚本

> ./脚本
>
> bash /脚本

rpm -qc bash 

>  查看bash配置文件

vim /etc/passwd

设置指令别名

> alias yang='sl'

永久设置命令别名

> vim ~/.bashrc 然后将 alias yang='sl' 添加到文件中

| 系统级                          | 用户级                                                       |
| ------------------------------- | ------------------------------------------------------------ |
| (/etc/profile )  (/etc/bashrc ) | (~/.bash_priofile )   (~/.bashrc)  (~/.bash_logout)  (~/.bash_history) |

| login shell                                                  | nologin shell               |
| ------------------------------------------------------------ | --------------------------- |
| (/etc/profile)  (/etc/bashrc)  (~/.bash_priofile) (~/.bashrc) | （/etc/bashrc）（~/.bashrc) |

ctrl + d 结束前台进程

ctrl + r 搜索历史命令

crtl+ a 移动到此行最前面

ctrl + d 移动到此行最后边

ctrl + u 删除光标前面的所有内容

ctrl + k 删除光标后边的所有内容

echo $? 返回上一条执行命令的值 0为真1为假

&& 表示前一个命令返回值为真时执行后边的命令。 || 表示前一条命令为假时执行后一条命令

$1 $2 等是位置变量

显示所有的环境变量

> env

uname -a查看内核版本号

uname -r查看内核详细信息

halt 关机pwd查看当前路径  



![IMG_8461](F:\qq下载的文件\MobileFile\IMG_8461.PNG)

![IMG_8460](F:\qq下载的文件\MobileFile\IMG_8460.PNG)

![IMG_8459](F:\qq下载的文件\MobileFile\IMG_8459.PNG)

![IMG_8458](F:\qq下载的文件\MobileFile\IMG_8458.PNG)

 ps -l  列出与本次登录有关的进程信息；
  ps -aux  查询内存中进程信息；
  ps -aux | grep ***  查询***进程的详细信息；
  top  查看内存中进程的动态信息；
  kill -9 pid  杀死进程。

USER ：进程的所属用户，
PID ：进程的进程ID号， 
%CPU ：进程占用的 CPU资源 百分比，
%MEM ：进程占用的 物理内存 百分比， 
VSZ ：进程使用掉的虚拟内存量 (Kbytes) ，
RSS ：进程占用的固定的内存量 (Kbytes) ，
TTY ：与进程相关联的终端（tty),? 代表无关,tty1-tty6是本机上面的登入者程序 ,pts/0表示为由网络连接进主机的程序。
STAT ：进程的状态，具体见2.1列出来的部分 ，
START ：进程开始创建的时间 ，
TIME ：进程使用的总cpu时间，
COMMAND : 进程对应的实际程序。

查看端口占用情况及与外界连接情况 netstat -nap

id+用户名    查看是否存在此用户

df -Th :查看磁盘使用状况

echo “hello alice" |mail -s "hello1" alice 发送邮件

free -m 查看内存使用情况

crontab -e  ： 计划任务  */5****  每五分钟执行一次

字符串变量用双引号引起来

$%{var}显示字符串变量的长度

^[0 - 9]+$ ^开头+ 前面字符又一到多个 $ 结尾