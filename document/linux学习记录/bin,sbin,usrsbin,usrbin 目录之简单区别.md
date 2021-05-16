# /bin,/sbin,/usr/sbin,/usr/bin 目录之简单区别

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[IT农夫](https://blog.csdn.net/kkdelta) 2012-07-02 13:18:14 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 77527 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 25

分类专栏： [Unix/Linux](https://blog.csdn.net/kkdelta/category_893780.html) 文章标签： [path](https://www.csdn.net/tags/MtTaEg0sMTg1NzAtYmxvZwO0O0OO0O0O.html) [脚本](https://so.csdn.net/so/search/s.do?q=脚本&t=blog&o=vip&s=&l=&f=&viparticle=) [command](https://www.csdn.net/tags/MtTaEg0sMzkxMjItYmxvZwO0O0OO0O0O.html) [less](https://www.csdn.net/tags/MtzaYgzsOTY5OS1ibG9n.html) [bash](https://www.csdn.net/tags/MtTaEg0sNDEyNDEtYmxvZwO0O0OO0O0O.html) [kill](https://www.csdn.net/tags/MtTaEg0sNTQwMjUtYmxvZwO0O0OO0O0O.html)

##    **/bin,/sbin,/usr/sbin,/usr/bin 目录**

   这些目录都是存放命令的，首先区别下/sbin和/bin：

  从命令功能来看，/sbin 下的命令属于基本的系统命令，如shutdown，reboot，用于启动系统，修复系统，/bin下存放一些普通的基本命令，如ls,chmod等，这些命令在Linux系统里的配置文件脚本里经常用到。

  从用户权限的角度看，/sbin目录下的命令通常只有管理员才可以运行，/bin下的命令管理员和一般的用户都可以使用。

  从可运行时间角度看，/sbin,/bin能够在挂载其他文件系统前就可以使用。

  而/usr/bin,/usr/sbin与/sbin /bin目录的区别在于：

  /bin,/sbin目录是在系统启动后挂载到根文件系统中的，所以/sbin,/bin目录必须和根文件系统在同一分区；

  /usr/bin,usr/sbin可以和根文件系统不在一个分区。

  /usr/sbin存放的一些非必须的系统命令；/usr/bin存放一些用户命令，如led(控制LED灯的)。

  转下一位网友的解读，个人认为诠释得很到位：

  **/bin**是系统的一些指令。bin为binary的简写主要放置一些系统的必备执行档例如:cat、cp、chmod df、dmesg、gzip、kill、ls、mkdir、more、mount、rm、su、tar等。
  **/sbin**一般是指超级用户指令**。**主要放置一些系统管理的必备程式例如:cfdisk、dhcpcd、dump、e2fsck、fdisk、halt、ifconfig、ifup、 ifdown、init、insmod、lilo、lsmod、mke2fs、modprobe、quotacheck、reboot、rmmod、 runlevel、shutdown等。
  **/usr/bin**　是你在后期安装的一些软件的运行脚本。主要放置一些应用软体工具的必备执行档例如c++、g++、gcc、chdrv、diff、dig、du、eject、elm、free、gnome*、 gzip、htpasswd、kfm、ktop、last、less、locale、m4、make、man、mcopy、ncftp、 newaliases、nslookup passwd、quota、smb*、wget等。

  **/usr/sbin**  放置一些用户安装的系统管理的必备程式例如:dhcpd、httpd、imap、in.*d、inetd、lpd、named、netconfig、nmbd、samba、sendmail、squid、swap、tcpd、tcpdump等。
  如果新装的系统，运行一些很正常的诸如：shutdown，fdisk的命令时，悍然提示：bash:command not found。那么
  首先就要考虑root 的$PATH里是否已经包含了这些环境变量。
  可以查看PATH，如果是：PATH=$PATH:$HOME/bin则需要添加成如下：
  PATH=$PATH:$HOME/bin:/sbin:/usr/bin:/usr/sbin



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞21
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论6](https://blog.csdn.net/kkdelta/article/details/7708250#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏25](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[linux /*usr*/*bin* 和/*usr*/local/*bin* *区别*](https://blog.csdn.net/bianb123/article/details/98846901)

[bianb123的博客](https://blog.csdn.net/bianb123)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 8396

[/*usr*/*bin* 系统预装的一些可执行程序，随系统升级会改变 /*usr*/local/*bin* 用户安装的可执行程序，不受系统升级影响，用户编译安装软件时，一般放到/*usr*/local*目录*下 如果两个*目录*含有相同的可执行程序，通过查看PATH，比较优先级 echo $PATH /root/perl5/*bin*:/*usr*/local/*sbin*:/*usr*/local/*bin*:/*usr*/*sbin*...](https://blog.csdn.net/bianb123/article/details/98846901)





[![img](https://profile.csdnimg.cn/0/5/1/3_weixin_45710390)](https://blog.csdn.net/weixin_45710390)

![表情包](https://csdnimg.cn/release/blogv2/dist/pc/img/emoticon.png)



- [![weixin_43378860](https://profile.csdnimg.cn/F/2/A/3_weixin_43378860)](https://blog.csdn.net/weixin_43378860)

  [码哥![码哥](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[æµæµã](https://blog.csdn.net/weixin_43378860)**:**学习了。谢谢。8 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![lRune](https://profile.csdnimg.cn/1/F/A/3_lrune)](https://blog.csdn.net/lRune)

  [lRune](https://blog.csdn.net/lRune)**:**谢谢，学习了1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![langyue919](https://profile.csdnimg.cn/E/D/F/3_langyue919)](https://blog.csdn.net/langyue919)

  [langyue919](https://blog.csdn.net/langyue919)**:**最后一行里的目录的/不能省略3 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![zalebool](https://profile.csdnimg.cn/E/A/1/3_zalebool)](https://blog.csdn.net/zalebool)

  [zalebool](https://blog.csdn.net/zalebool)**:**不错的文章，赞一个？7 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![u011500128](https://profile.csdnimg.cn/1/F/D/3_u011500128)](https://blog.csdn.net/u011500128)

  [xiaoyu2er](https://blog.csdn.net/u011500128)**:**很不错~受教~7 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![numeric010](https://profile.csdnimg.cn/4/A/9/3_numeric010)](https://blog.csdn.net/numeric010)

  [numeric010](https://blog.csdn.net/numeric010)**:**交换老婆,你就可以得到两个...xx8 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)