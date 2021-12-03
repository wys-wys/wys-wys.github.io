- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/alog9/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/凌空a)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/alog9/rss/)

随笔- 122 文章- 0 评论- 0 阅读- 51271 

# [CentOS7安装epel的方式](https://www.cnblogs.com/alog9/p/12097471.html)

 

epel是社区强烈打造的免费开源发行软件包版本库。

EPEL，即Extra Packages for Enterprise Linux的简称，是为企业级Linux提供的一组高质量的额外软件包，包括但不限于Red Hat Enterprise Linux (RHEL), CentOS and Scientific Linux (SL), Oracle Enterprise Linux (OEL)。(关于 : EPEL)

方法一：yum命令安装

```
1 yum install epel-release -y
```

 

方法二：手动安装

 

针对系统架构选择相应的类型：http://dl.fedoraproject.org/pub/epel/7/。我们使用的x86_64，就要进入该目录下寻找相应包，安装方法如下：

```
1 # rpm -ivh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

如果报冲突,可以把冲突的包删除

```
1 yum remove epel-release
```

或者：

```
1 # wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm
2 # rpm -vih epel-release-7-2.noarch.rpm
```

 

查看源：

```
1 ll /etc/yum.repos.d/
```

两个epel的repo文件:

```
1 epel.repo
2 
3 epel-testing.repo
```

接下来就更新源：

```
1 yum clean all && yum makecache
```

更新成功之后就可以使用EPEL安装应用了。

安装Howto
安装CentOS SCLo RH存储库：
yum install centos-release-scl-rh

epel是社区强烈打造的免费开源发行软件包版本库。

EPEL，即Extra Packages for Enterprise Linux的简称，是为企业级Linux提供的一组高质量的额外软件包，包括但不限于Red Hat Enterprise Linux (RHEL), CentOS and Scientific Linux (SL), Oracle Enterprise Linux (OEL)。(关于 : EPEL)

方法一：yum命令安装



```undefined
yum install epel-release -y
```

方法二：手动安装

针对系统架构选择相应的类型：http://dl.fedoraproject.org/pub/epel/7/。我们使用的x86_64，就要进入该目录下寻找相应包，安装方法如下：



```cpp
# rpm -ivh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

如果报冲突,可以把冲突的包删除



```csharp
yum remove epel-release
```

或者：



```cpp
# wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm
# rpm -vih epel-release-7-2.noarch.rpm
```

更新数据



```undefined
yum clean all && yum makecache
```

查看仓库多了下面一行，有一万多个包。



```csharp
<pre class="brush:bash;toolbar:false" style="font-family: Arial, Helvetica, sans-serif; padding: 5px; max-width: 680px !important; background-color: rgb(246, 246, 246); border: 1px dotted rgb(170, 170, 170); white-space: pre-wrap; word-wrap: break-word;">*epel/x86_64          Extra Packages for Enterprise Linux 7 - x86_64      11,018</pre>

<pre class="brush:bash;toolbar:false" style="font-family: Arial, Helvetica, sans-serif; padding: 5px; max-width: 680px !important; background-color: rgb(246, 246, 246); border: 1px dotted rgb(170, 170, 170); white-space: pre-wrap; word-wrap: break-word;">[root@hddcluster2 ~]# yum repolist
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.cn99.com
 * epel: mirror01.idc.hinet.net
 * extras: mirrors.aliyun.com
 * updates: mirrors.cn99.com
repo id               repo name                                           status
base/7/x86_64         CentOS-7 - Base                                      9,363
*epel/x86_64          Extra Packages for Enterprise Linux 7 - x86_64      11,018
extras/7/x86_64       CentOS-7 - Extras                                      435
updates/7/x86_64      CentOS-7 - Updates                                     418
repolist: 21,234

[root@hddcluster2 ~]#
```

 

安装完epel，clang库搜索结果：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
1 [root@localhost yum.repos.d]# yum list |grep clang 
2 clang.x86_64                            3.4.2-9.el7                    epel     
3 clang-analyzer.noarch                   3.4.2-9.el7                    epel     
4 clang-devel.x86_64                      3.4.2-9.el7                    epel     
5 csmock-plugin-clang.noarch              2.3.0-1.el7                    epel     
6 [root@localhost yum.repos.d]# 
7 [root@localhost yum.repos.d]# 
8 [root@localhost yum.repos.d]# 
9 [root@localhost yum.repos.d]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

 

 

 

 

安装CentOS SCLo RH存储库：

```
1 yum install centos-release-scl-rh
```

 

安装CentOS SCLo RH存储库后，clang安装源搜索结果：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 [root@localhost yum.repos.d]# yum list |grep clang             
 2 clang.x86_64                               3.4.2-9.el7            epel          
 3 clang-analyzer.noarch                      3.4.2-9.el7            epel          
 4 clang-devel.x86_64                         3.4.2-9.el7            epel          
 5 csmock-plugin-clang.noarch                 2.3.0-1.el7            epel          
 6 llvm-toolset-7-clang.x86_64                5.0.1-4.el7            centos-sclo-rh
 7 llvm-toolset-7-clang-analyzer.noarch       5.0.1-4.el7            centos-sclo-rh
 8 llvm-toolset-7-clang-devel.x86_64          5.0.1-4.el7            centos-sclo-rh
 9 llvm-toolset-7-clang-libs.x86_64           5.0.1-4.el7            centos-sclo-rh
10 llvm-toolset-7-clang-tools-extra.x86_64    5.0.1-4.el7            centos-sclo-rh
11 llvm-toolset-7-git-clang-format.x86_64     5.0.1-4.el7            centos-sclo-rh
12 llvm-toolset-7.0-clang.x86_64              7.0.1-1.el7            centos-sclo-rh
13 llvm-toolset-7.0-clang-analyzer.noarch     7.0.1-1.el7            centos-sclo-rh
14 llvm-toolset-7.0-clang-devel.x86_64        7.0.1-1.el7            centos-sclo-rh
15 llvm-toolset-7.0-clang-libs.x86_64         7.0.1-1.el7            centos-sclo-rh
16 llvm-toolset-7.0-clang-tools-extra.x86_64  7.0.1-1.el7            centos-sclo-rh
17 llvm-toolset-7.0-git-clang-format.x86_64   7.0.1-1.el7            centos-sclo-rh
18 [root@localhost yum.repos.d]# 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

 

分类: [Centos7](https://www.cnblogs.com/alog9/category/1601212.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/sample_face.gif)](https://home.cnblogs.com/u/alog9/)

[凌空a](https://home.cnblogs.com/u/alog9/)
[关注 - 0](https://home.cnblogs.com/u/alog9/followees/)
[粉丝 - 1](https://home.cnblogs.com/u/alog9/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/alog9/p/12073105.html)上一篇： [Linux系统帮助信息查看工具汇总](https://www.cnblogs.com/alog9/p/12073105.html)
[» ](https://www.cnblogs.com/alog9/p/12097724.html)下一篇： [采用yum源安装clang & llvm编译器的参考文档](https://www.cnblogs.com/alog9/p/12097724.html)

posted @ 2019-12-25 16:34 [凌空a](https://www.cnblogs.com/alog9/) 阅读(3690) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=12097471) [收藏](javascript:void(0))





[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/alog9/p/12097471.html#)[返回顶部](https://www.cnblogs.com/alog9/p/12097471.html#top)

发表评论



编辑预览