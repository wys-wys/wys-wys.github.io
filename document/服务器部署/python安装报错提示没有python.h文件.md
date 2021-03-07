可以看到是缺少Python.h文件，进入/lib/pythonx.x目录查看是否缺少该文件

```
[root@data1 /]# cd /usr/include/python3.6m/
[root@data1 python3.6m]# ls
pyconfig-64.h
```

没有则安装python-devel（Ubuntu应该安装python-dev）

```
[root@data1 /]# yum search python | grep devel
Last metadata expiration check: 0:18:02 ago on Mon 06 Jul 2020 02:23:55 AM UTC
....
python36-devel.x86_64 : Libraries and header files needed for Python development
python38-devel.x86_64 : Libraries and header files needed for Python development
...
[root@data1 /]# yum install python36-devel.x86_64
```

再次安装就可以了

```
[root@data1 /]# pip3 install pyxattr
WARNING: Running pip install with root privileges is generally not a good idea. Try `pip3 install --user` instead.
Collecting pyxattr
  Using cached https://files.pythonhosted.org/packages/cf/b1/7ed931d98b5a91a59b69fcc2860e5b720a22ed1ddb85268415181c9b0986/pyxattr-0.7.1.tar.gz
Installing collected packages: pyxattr
  Running setup.py install for pyxattr ... done
Successfully installed pyxattr-0.7.1
```

psutil/_psutil_common.c:9:20: fatal error: Python.h: No such file or directory compilation termi

candy134834 2020-04-08 15:43:10  1050  收藏
分类专栏： 异常集合
版权
这个导致tensorflow 安装不上以及其他的包 无法安装 

可以 

sudo yum install python-devel
sudo yum install python3-devel 

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/walk1314/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/Mr_Walker)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/walk1314/rss/)

随笔- 49 文章- 0 评论- 1 阅读- 94910 

# [安装psutil时提示缺少python.h头文件(作记录)](https://www.cnblogs.com/walk1314/p/9796500.html)

　　通过pip或者源码安装psutil，都会提示缺少python.h头文件，错误提示如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
...
psutil/_psutil_common.c:9:20: fatal error: Python.h: No such file or directory
 #include <Python.h>
                    ^
compilation terminated.
error: command 'gcc' failed with exit status 1
...
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　出现此错误的原因是没有安装python-devel，python开发包，如果是支持yum的系统，直接yum安装即可：

```
yum -y install python-devel
```