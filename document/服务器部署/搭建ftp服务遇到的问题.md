# fFilezilla-----服务器发回了不可路由的地址,使用服务器地址代替-------解决办法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[iastro](https://blog.csdn.net/iastro) 2014-06-17 08:59:07 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 57971 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [Filezilla](https://blog.csdn.net/iastro/category_2338157.html) 文章标签： [ftp](https://www.csdn.net/tags/MtTaEg0sNTU3NzgtYmxvZwO0O0OO0O0O.html) [Filezilla](https://www.csdn.net/tags/MtjaEg3sNjIwMzctYmxvZwO0O0OO0O0O.html)

版权

命令: PASV
响应: 227 Entering Passive Mode 
状态: 服务器发回了不可路由的地址。使用服务器地址代替。
命令: LIST
错误: 连接超时

错误: 读取目录列表失败

解决方法：更改Filezilla设置，编辑-设置-连接-FTP-被动模式，将“使用服务器的外部ip地址来代替”改为“回到主动模式”即可。

# FTP连接报错530 Permission denied解决方法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[GoRustNeverStop](https://feeman.blog.csdn.net/) 2016-04-30 11:00:38 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 88941 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 8

分类专栏： [linux/unix](https://blog.csdn.net/weiyuefei/category_1799911.html)

版权

虚拟机装好RedHat后，准备使用filezilla连接,输入IP地址，root用户，密码，快速连接，报错：

530 Permission denied。

故障排除：

**1.首先检查系统是否开启了vsftp服务，如果没有开启，先开启该服务。**

**2.查看配置**

vsftpd的配置，配置文件中限定了vsftpd用户连接控制配置。
vsftpd.ftpusers：位于/etc/vsftpd目录下。它指定了哪些用户账户不能访问FTP服务器，例如root等。
vsftpd.user_list：位于/etc/vsftpd目录下。该文件里的用户账户在默认情况下也不能访问FTP服务器，仅当vsftpd .conf配置文件里启用userlist_enable=NO选项时才允许访问。
vsftpd.conf：位于/etc/vsftpd目录下。来自定义用户登录控制、用户权限控制、超时设置、服务器功能选项、服务器性能选项、服务器响应消息等FTP服务器的配置。

**3.配置修改完成后，执行service vsftpd restart重启vsftpd服务。**

# FileZilla无法连接到服务器，不安全的服务器，不支持 FTP over TLS的解决方案

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[高欣的博客](https://blog.csdn.net/gaoxin_gx) 2019-04-24 12:43:24 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3681 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [其他](https://blog.csdn.net/gaoxin_gx/category_8818132.html)

版权

今天用FileZilla传输文件的时候总是出现“FileZilla无法连接到服务器，不安全的服务器，不支持 FTP over TLS的解决方案”
这样的字样，换了Flashfxp也是一样，检查服务器的配置，反复修改，一样是这样的问题，终于选择了百度，按照百度的解决方法，依然没有解决

最后只能用：一顿操作猛如虎，管他是否二百五

呼…解决了!

我的配置之中就只有搭建了vsftp，apache，其余的是没有进行搭建的。
解决方法：

协议改为SFTP-SSH就可以了
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019042412395223.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dhb3hpbl9neA==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190424123958980.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dhb3hpbl9neA==,size_16,color_FFFFFF,t_70)
flashfxp亦是如此