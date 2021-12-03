# 安装pywin32即可

python 3.7.4 安装win32gui 报错的解决方法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[原始新人类](https://blog.csdn.net/kdyangj) 2020-07-20 19:16:18 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 4145 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

文章标签： [python](https://www.csdn.net/tags/MtjaQg4sNDk0LWJsb2cO0O0O.html)

版权

我的环境是python 3.7.4 （64位），已经安装了 pywin32-221.win-amd64-py3.7.exe ，但在使用 pip install win32gui 时，总是报错：  ModuleNotFoundError: No module named 'win32.distutils.command'

 

后来发现，其实安装了pywin32后，安装目录下已经有了win32gui

![img](https://img-blog.csdnimg.cn/20200720191133317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tkeWFuZ2o=,size_16,color_FFFFFF,t_70)

 

只需要打开Python编辑器，执行一下 import win32gui 即可

![img](https://img-blog.csdnimg.cn/20200720191147186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tkeWFuZ2o=,size_16,color_FFFFFF,t_70)

# python安装win32gui的相关问题

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[老油条666](https://blog.csdn.net/qq_15054345) 2020-07-09 18:37:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3361 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [python学习](https://blog.csdn.net/qq_15054345/category_8670018.html)

版权

[![img](https://img-blog.csdnimg.cn/20201014180756738.png?x-oss-process=image/resize,m_fixed,h_64,w_64)python学习](https://blog.csdn.net/qq_15054345/category_8670018.html)专栏收录该内容

9 篇文章0 订阅

订阅专栏

问题一：直接pip/pip3 install win32gui报错，报错代码为" ModuleNotFoundError: No module named 'win32.distutils.command'，我的环境是python3.7。网上有大佬说win32gui和python3.7不兼容，但个人感觉是这个模块在python3.7版本里已经整合到了pywin32模块中。有图有真相：

![img](https://img-blog.csdnimg.cn/20200709182947178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE1MDU0MzQ1,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20200709183046263.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE1MDU0MzQ1,size_16,color_FFFFFF,t_70)

问题2：安装了pywin32模块后项目中导入使用，编辑器也报错，运行还是报错（一般来说编辑器报错显示红色下划线基本运行都不会通过，但之前我用过pycharm2019.3.1版本出现过编辑器报错，但是运行成功的情况），这个问题我能给出的一个原因是：可能是我们在创建项目之后，再安装的pywin32库。通过pip或者pip3安装的库一般都会直接安装到python安装路径下，但是我们创建项目时，会把python的安装路径下的虚拟环境做一份拷贝到项目路径下，这就造成了项目下的虚拟环境和python安装路径下的虚拟环境不同步的情况。解决办法就是删除项目路径下的虚拟环境，重新导入python路径下的虚拟环境。pycharm下删除后很容易导入新的。