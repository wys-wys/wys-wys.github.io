# 把安卓手机性能发挥到极致之-Termux安装Python及Jupyter

[![myastrotong](https://pic4.zhimg.com/v2-630280f8f6d2060f01810f0a1fc2ea18_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/tang-kong-wen)

[myastrotong](https://www.zhihu.com/people/tang-kong-wen)

空!=无

关注他

9 人赞同了该文章

Termux环境使用Python太难看也不方便，比较好的方式是用网页浏览器使用Jupyter来运行Python。



> 写在前面——利用Jupyter写Java和Python的方法见：

[myastrotong：极致安卓之—Aid Learning基于Jupyter开发Java和Pythonzhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/101147592)[myastrotong：Aid learning/Termux之Jupyter的Java编程高级篇——包管理zhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/103986884)



本文主要介绍方法（本方法无法在Aid Learning下安装Jupyter！缺sqlite3库！）：

首先安装Termux基本环境，方法如下：

[myastrotong：把安卓手机性能发挥到极致之-Termuxzhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/92664273)

装完clang等基本环境后

apt install python

换国内源：

linux的文件在~/.pip/pip.conf，

修改该文件内容为：

[global]

index-url = [http://pypi.douban.com/simple](https://link.zhihu.com/?target=http%3A//pypi.douban.com/simple)

[install]

trusted-host=[http://pypi.douban.com](https://link.zhihu.com/?target=http%3A//pypi.douban.com)

这样在使用pip来安装时，会默认调用该镜像。发现豆瓣的源挺快的！！！！

然后安装如下包：

pip install numpy

pip install pandas

apt install libzmq

pip install jupyter

然后安装matplotlib库用于画图：

首先安装几个库：

apt install freetype libpng pkg-config

然后安装matplotlib ：

pip install matplotlib

然后就输入如下指令可以使用jupyter了：

jupyter notebook

难道使用jupyter notebook进行python开发就这么简单，没有坑吗？

当然不可能，要真的这么简单我就没必要写文章了！

最麻烦的就是上述指令生成以后，使用的网址：

[http://localhost:8888/](https://link.zhihu.com/?target=http%3A//localhost%3A8888/) 后面还跟着一长串的密匙。需要拷贝到网址上，太麻烦！不方便！所以还得改！

如图下所示的两个长串密匙！您要说这能忍也行，反正我是不能忍！

![img](https://pic4.zhimg.com/v2-2c6fa5c6e3589f6bc5f45df6d6793137_r.jpg)

方法如下：

使用下列命令生成配置文件：

jupyter notebook --generate-config

生成如下文件：

/data/data/com.termux/files/home/.jupyter/jupyter_notebook_config.py

然后输入ipython进入Python环境生成密匙：

在 ipython 环境执行下面内容：

from notebook.auth import passwd

passwd()

然后根据提示输入密码（Linux输入的密码是看不见的，别慌！输入吧！）

Enter password:

Verify password:

然后就输出一串类似的数：

'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'

复制该密匙(用你自己生成的数，千万别用我上面的数)，然后修改jupyter_notebook_config.py文件，加入如下内容：

c.NotebookApp.password = 'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'

c.NotebookApp.ip='*' #意思是允许任何ip访问

c.NotebookApp.open_browser = False

c.NotebookApp.port =8888 #可自行指定一个端口, 访问时使用该端口

然后退出。

![img](https://pic1.zhimg.com/v2-1545bdc0f055ca4fc26414bdf2939368_r.jpg)

在命令窗口输入：

jupyter notebook

等待就可以使用网页浏览器测试Python了！

在网页网址部分输入:

http://localhost:8888

或者在同一局域网下，利用ssh在电脑端登录，此时输入手机的局域网IP登录（ifconfig可以查看）：

[http://192.168](https://link.zhihu.com/?target=http%3A//192.168).*.**:8888

登录界面如下：

![img](https://pic4.zhimg.com/v2-ff64c9bffaa2cbbed1b28dfc6db1716f_r.jpg)



点击如图红圈部分New，打开Python环境

![img](https://pic2.zhimg.com/v2-a10651eb1fb83cf0bc64c762a82b6d55_r.jpg)

可见这种方式一劳永逸，可以无需密匙，方便的登录jupyter！



最后，脑子记不住Python指令怎么办？

安装扩展包啊！让Python自己提醒你，方法如下：

apt install libxml2

apt install libxslt

pip3 install jupyter-contrib-nbextensions

前两个不安上，扩展包是安不了的！

以上三个指令安装完毕后。

安装 javascript and css files：

jupyter contrib nbextension install --user

安装configurator：

pip3 install jupyter_nbextensions_configurator



重新打开jupyter，在网页输入网址，界面如下：

![img](https://pic2.zhimg.com/v2-21f272e847431dcbb48844862de06945_r.jpg)

可见Nbextensions已经安装上了！选中Hinterland!

然后点击New，进入Python环境，输入指令，如图，光标下方直接出现了提示符！扩展包生效了！

以上就是Termux下Python环境搭建以及Jupyter开发环境搭建的过程！

从此就可以脱离Termux的黑白界面，在浏览器中开始Python愉快的玩耍了！

![img](https://pic2.zhimg.com/v2-073b5de81dc0a4fc1077dd43b489f179_r.jpg)



值得指出的是，最新版Aid Learning已经自带Jupyter了，Aid爽歪歪啊！de