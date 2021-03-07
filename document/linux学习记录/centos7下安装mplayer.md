# centos7下安装mplayer

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[天天进步一点点](https://blog.csdn.net/u013196348) 2018-11-01 14:04:33 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1427 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [Linux](https://blog.csdn.net/u013196348/category_8274078.html)

版权

在centos7下本地的一些格式的视频是无法播放的,因此我们需要安装mplayer播放器,能够播放大部分格式的视频:

\1. 安装epel-release,如果不安装,会出现依赖关系错误

​     yum -y install epel-release

\2. rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm

\3. yum makecache

4.依次执行下列命令

  yum search mplayer

  yum install mplayer

  yum install smplayer