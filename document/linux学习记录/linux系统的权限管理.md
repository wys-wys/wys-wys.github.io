linux系统的权限管理

安然。。 2019-10-09 20:58:18  48  收藏
版权
linux系统的权限管理
文件权限存在的意义
系统中的最底层安全设定方法之一，保证文件可以被可用的用户做相应的操作。

文件权限查看的方法
ls -l file
ls -ld dir
ll file
ll -d dir

文件权限的读取
- |rw-r–r-- | 1 | root | root | 0 | Oct 7 14:48 | file

文件的类型
- ## 空文件或者文本
d ## 目录
l ##软链接
s ##socket 套接字
b ##block 块设备
c ##字符设备

例：软链接与硬链接


文件的权限

rw-|r–| r–
1 2 3
1.[u]文件拥有者对文件能有什么操作
2.[g]文件所有组对文件能有什么的操作
3[o]其他人能对文件做什么

对权限的理解
r
对文件：是否可以查看文件的内容
对目录：是否可以查看目录有什么子文件或者子目录
w
对文件：是否可以改变文件里面记录的字符
对目录：是否可以对目录中的子目录或者子文件的原数据进行更改
x
对文件：是否可以通过文件名称调用文件内的记录的程序
对目录：是否可以进入目录

更改的方式
chmod <u|g|o><+|-> <r|w|x> file| dir
chmod u+x file
chmod g-r file
chmod ug-r file
chmod u-r,g+x file
chmod -r u+x file##递归操作
chmod o=r-x file



例： 改变文件的所有人所有组




umsk
umsk 系统建立文件时默认保留的权力
例：umask 022 ##临时设定系统的预留权限为022
777-022=755(dir)##目录的默认权限 755-111=644(files)##文件的默认权限

永久更改umsk
vim /etc/profile ##系统的配置文件
其中，
60 umask 002 ##普通用户的umask
62 umask 022 ##超级用户的umsk

vim /etc/bashrc ##shell配置文件

source /etc/profile ##让更改立即生效

例： 原始的普通用户和超级用户的umask,永久的更改umask



特殊权限
1.sticky ##粘制位
作用
只针对目录生效，当一个目录上有sticky权限时，在这个目录中的文件只能被文件的所有者删除
设定方式
chmod o+t dir
chmod 1xxx dir
2.sgid ##强制位
作用
对文件：只针对与二进制可执行文件，当文件上有sgid时任何人执行此文件产生的进程都属于此文件的组
对目录：当目录上有sgid权限时任何人在此目录下建立的文件都属于此文件的组
设定的方式
chmod g+s file|dir
chmod 2xxx file|dir
3.suid ##冒险位
作用：只针对与二进制可以执行的文件，当文件上有suid时任何人执行这个文件中记的

acl权限列表
1作用：让特定的用户对特定的文件拥有特定的权限。
2.acl列表查看
例：-rw-rwxr–+ 1 root root 0 jul 21 15:45 file

getfacl file ##查看acl开启的文件的权限, 注： 用ll命令无法查看详细的信息
#file:file ##文件的名称
#owner:root ##文件拥有者
#group:root ##文件拥有组
user:rw- ##文件拥有者的权限
rwx ##指定用户的权限
r–##其他人的权限

3acl列表的管理
setfacl -m u:username:rwx file ##设定username对file有rwx权限
setfacl -m g:group:rwx file ##设定group组成员对file拥有rwx权限
setfacl -x u:username file ##从acl列表中删除username
setfacl -b file ##关闭file上的acl列表

例：指定user1用户对文件可以进行读写操作。

关闭相应的acl权限列表


4mask值
在权限列表中mask表示能生效的权力值
当用chmod减小开启acl的文件权限值时，mask值会发生改变
chmod g-w user1
如果要恢复mask值
setfacl -m m:rw user1
例：改变权限后，mask值发生了改变

5.acl的默认权限设定
acl默认权限只针对目录设定
"acl权限只针对设定完成之后新建立的文件和目录生效，而已经存在的文件是不会继承默认的权限
setfacl -m d:u:student:rwx /mnt/file
setfacl -k /mnt/file
userperm>acluser>aclgroup>groupperm>otherperm

例：设定目录的acl列表后权限的变化



用递归命令后，文件也具备acl默认的权限。