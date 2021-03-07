

# 【原创亲测】win7下pip默认镜像源的配置

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[沈万三爱搬砖](https://blog.csdn.net/yaoqiwaimai) 2017-02-25 17:11:33 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 9334 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 4

分类专栏： [Python](https://blog.csdn.net/yaoqiwaimai/category_6426927.html) 文章标签： [python](https://www.csdn.net/gather_24/MtjaQg4sNDk0LWJsb2cO0O0O.html) [win7](https://www.csdn.net/gather_2f/MtjaMg3sNDIwMDctYmxvZwO0O0OO0O0O.html) [pip](https://www.csdn.net/gather_22/MtTaEg0sMTc0MTQtYmxvZwO0O0OO0O0O.html)

版权

【原创亲测】win7下pip默认镜像源的配置

# 具体实践

1. 用notepad++创建pip.ini文件，保存位置为%USERPROFILE%\pip\pip.ini.
   %USERPROFILE%具体指的是什么目录，可以cmd命令行中输入set，查看所有系统变量，找到*USERPROFILE*,
   我的为C:\Users\qxb-810.

   国内下载源也可以设置成其他的镜像，如中国科学技术大学 PyPi镜像https://mirrors.ustc.edu.cn/pypi/web/simple/.
   **【国内镜像】**

   1. 中国科学技术大学 : https://pypi.mirrors.ustc.edu.cn/simple
   2. 清华：https://pypi.tuna.tsinghua.edu.cn/simple
   3. 豆瓣：http://pypi.douban.com/simple/
   4. 华中理工大学 : http://pypi.hustunique.com/simple
   5. 山东理工大学 : http://pypi.sdutlinux.org/simple

   **截图**

   - pip.ini文件
     ![这里写图片描述](https://img-blog.csdn.net/20170226112451039?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWFvcWl3YWltYWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
   - 在末尾追加这句
   - trusted-host = https://pypi.mirrors.ustc.edu.cn/simple
- 表示新人该软件源
   - 
   - cmd下使用set命令查找USERPROFILE变量
     ![这里写图片描述](https://img-blog.csdn.net/20170226112608883?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWFvcWl3YWltYWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
   
2. 以下载flask为例，下载速度比之前快了很多.
   如果不设置默认镜像源，每次都要手动添加镜像源，
   上面等价于输入: pip install flask -i https://pypi.tuna.tsinghua.edu.cn/simple,
   设置默认的好处是，不要每次都输入-i https://pypi.tuna.tsinghua.edu.cn/simple了.
   **截图**
   ![这里写图片描述](https://img-blog.csdn.net/20170226112645738?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWFvcWl3YWltYWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

# 附录: ubuntu下pip默认镜像源的设置

参考: https://lug.ustc.edu.cn/wiki/mirrors/help/pypi
\1. 切换目录 $ cd ~/.pip, 如果~/.pip/pip.conf不存在，则新建文件

> $ sodu vi pip.conf
> 文件内容如下:
> ![这里写图片描述](https://img-blog.csdn.net/20170226112709473?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWFvcWl3YWltYWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

1. 保存后即可使用新设置的镜像源进行python第三方包的安装

# 参考文章

1. https://bitbucket.org/pypa/pypi/issues/5/pipini-directory-in-windows
2. http://www.pip-installer.org/en/latest/configuration.html#config-file
3. https://ficapy.github.io/2013/12/27/pip_use_china_mirror/
4. [https://lug.ustc.edu.cn/wiki/mirrors/help/pypi](https://lug.ustc.edu.cn/wiki/mirrors/help/pyp)
   - pip.ini directory in windows
     **this should be %USERPROFILE% and not %HOME% at least in windows 7**

pip config set global.index-https://pypi.tuna.tsinghua.edu.cn/simple 在Windows下可以用这条命令直接更改，达到的效果和博主一样

# python3 换源

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[jeikerxiao](https://blog.csdn.net/jeikerxiao) 2017-06-20 14:44:03 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 18573 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

分类专栏： [Python](https://blog.csdn.net/jeikerxiao/category_6545869.html) 文章标签： [python](https://www.csdn.net/tags/MtjaQg4sNDk0LWJsb2cO0O0O.html)

版权

# 1.原因

pip是很强大的模块安装工具，但是由于国外官方pypi经常被墙，导致不可用。

所以我们最好是更换pip源，这样就能解决被墙导致的装不上库的问题。

# 2.可用源

网上有很多可用的源：

豆瓣：http://pypi.douban.com/simple/

清华：https://pypi.tuna.tsinghua.edu.cn/simple

清华大学的pip源，它是官网pypi的镜像，每隔5分钟同步一次，推荐使用。

# 3.使用

## 3.1 临时使用

可以在使用pip的时候加参数`-i https://pypi.tuna.tsinghua.edu.cn/simple`

例如：

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple requests1
```

这样就会从清华这边的镜像去安装requests库。

## 3.2 永久修改

### Linux环境(Mac环境)

```
~/.pip/pip.conf 1
```

没有这个文件就创建一个，修改 index-url 内容如下：

```
[global] index-url = https://pypi.tuna.tsinghua.edu.cn/simple 1
```

### windows环境

直接在user目录中创建一个pip目录:

```
C:\Users\xx\pip\pip.ini1
```

内容如下

```
[global] index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```