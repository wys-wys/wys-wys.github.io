# linux设置开机自启动脚本的最佳方式

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[yinnnnnnn](https://yinnn.blog.csdn.net/) 2018-05-28 21:32:25 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 70476 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 64

分类专栏： [工具](https://blog.csdn.net/qq_35440678/category_6532692.html)

版权

公司的开发机经常因为断电被重启，服务都得手动一个一个启动，专门研究了下如何设置开机自动重启脚本。

## 设置开机启动方式一

最简单粗暴的方式直接在脚本`/etc/rc.d/rc.local`(和`/etc/rc.local`是同一个文件，软链)末尾添加自己的**脚本**
然后，增加脚本执行权限

> chmod +x /etc/rc.d/rc.local

## 设置开机启动方式二

第二种方式是在crontab中设置

> crontab -e
> @reboot /home/user/test.sh

## 每次登录自动执行

也可以设置每次登录自动执行脚本，在`/etc/profile.d/`目录下新建sh脚本，
`/etc/profile`会遍历`/etc/profile.d/*.sh`

另外，几个脚本的区别：
（1） /etc/profile： 此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行. 并从/etc/profile.d目录的配置文件中搜集shell的设置。

（2） /etc/bashrc: 为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取（即每次新开一个终端，都会执行bashrc）。

（3） ~/.bash_profile: 每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次。默认情况下,设置一些环境变量,执行用户的.bashrc文件。

（4） ~/.bashrc: 该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该该文件被读取。

（5） ~/.bash_logout: 当每次退出系统(退出bash shell)时,执行该文件. 另外,/etc/profile中设定的变量(全局)的可以作用于任何用户,而~/.bashrc等中设定的变量(局部)只能继承 /etc/profile中的变量,他们是”父子”关系。

（6） ~/.bash_profile: 是交互式、login 方式进入 bash 运行的~/.bashrc 是交互式 non-login 方式进入 bash 运行的通常二者设置大致相同，所以通常前者会调用后者。



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞11
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论7](https://blog.csdn.net/qq_35440678/article/details/80489102#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏64](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReward.png)打赏
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[*linux* *开机*自动启动*脚本*方法.doc](https://download.csdn.net/download/ztz0223/2435793)

06-07

[*linux**开机*自动启动*脚本*方法，之类给出基本的 原理，具体的也可以在网上搜索一下。](https://download.csdn.net/download/ztz0223/2435793)





[![img](https://profile.csdnimg.cn/0/5/1/3_weixin_45710390)](https://blog.csdn.net/weixin_45710390)

![表情包](https://csdnimg.cn/release/blogv2/dist/pc/img/emoticon.png)



- [![weixin_42179076](https://profile.csdnimg.cn/E/5/2/3_weixin_42179076)](https://blog.csdn.net/weixin_42179076)

  [菜鸟０００００１](https://blog.csdn.net/weixin_42179076)**:**/etc/profile 第一种方法如果添加的脚本执行时候需要权限，会造成循环在登录界面，一直进不了系统。进入单用户模式把添加的脚本删除重启电脑就好了`#!/bin/bash                                                                     ntfsfix /dev/nvme0n1p4ntfsfix /dev/nvme0n1p6ntfsfix /dev/sda1ntfsfix /dev/sda2ntfsfix /dev/sda3`2 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)4

- - [![birdlearn](https://profile.csdnimg.cn/3/4/C/3_birdlearn)](https://blog.csdn.net/birdlearn)

    [the bear](https://blog.csdn.net/birdlearn)回复muzhe1024**:**最后用这种方法实现开机打开了吗10 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

  - [![qq_46394490](https://profile.csdnimg.cn/7/6/F/3_qq_46394490)](https://blog.csdn.net/qq_46394490)

    [码哥![码哥](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[努力的小白z](https://blog.csdn.net/qq_46394490)回复muzhe1024**:**为啥我进入时提示无法打开.sh文件，我已经把他权限改成777了1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

  - [![muzhe1024](https://profile.csdnimg.cn/7/8/A/3_muzhe1024)](https://blog.csdn.net/muzhe1024)

    [muzhe1024](https://blog.csdn.net/muzhe1024)回复**:**发现了，刚才进不去系统，我用启动盘进来把脚本删掉了^_^1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

    ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![TiffanyXYf](https://profile.csdnimg.cn/3/D/E/3_tiffanyxyf)](https://blog.csdn.net/TiffanyXYf)

  [码哥![码哥](https://csdnimg.cn/release/blogv2/dist/components/img/commentTagArrowWhite.png)](https://blog.csdn.net/blogdevteam/article/details/103478461)[VeraWin](https://blog.csdn.net/TiffanyXYf)**:**请问博主有没有遇到过Ubuntu系统桌面启动不了的情况4 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![weixin_41694118](https://profile.csdnimg.cn/F/7/1/3_weixin_41694118)](https://blog.csdn.net/weixin_41694118)

  [君任知命](https://blog.csdn.net/weixin_41694118)**:**通过在/etc/profile添加脚本每次用户登录时才能被执行，在嵌入式linux当中这种解决方法并不是很好。而且假如我的某个脚本要执行开机10s后才在/tmp目录下生成一个文件这样就会导致用终端软件登录时会卡住。希望我的经历能给大家排个雷5 月前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

- [![david0624](https://profile.csdnimg.cn/E/5/1/3_david0624)](https://blog.csdn.net/david0624)

  [david0624](https://blog.csdn.net/david0624)**:**学习了1 年前回复![img](https://csdnimg.cn/release/blogv2/dist/pc/img/commentMore.png)

  ![点赞](https://csdnimg.cn/release/blogv2/dist/pc/img/commentUnHeart.png)

相关推荐