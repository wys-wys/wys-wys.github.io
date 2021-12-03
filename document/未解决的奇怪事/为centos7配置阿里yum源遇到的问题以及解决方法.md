[为centos7配置阿里yum源遇到的问题以及解决方法](https://www.cnblogs.com/xuelisheng/p/11452926.html)

## 【问题背景】

卸载安装的Ambari，之前都是因为卸载不干净。这次重写安装，卸载完之后，发现httpd无法启动，所以想卸载httpd进行重新安装，但是执行命令yum list | grep httpd报错。

## 【遇到的问题】

配置过程很简单，去https://opsx.alibaba.com/mirror 获得执行命令：

![img](https://img2018.cnblogs.com/blog/1427627/201909/1427627-20190903142741336-83866376.png)

 

 但是我在执行yum makecache时报错，报错信息如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
Loaded plugins: fastestmirror, langpacks, priorities
Repository epel is listed more than once in the configuration
Cleaning repos: base epel extras updates
Cleaning up everything
Maybe you want: rm -rf /var/cache/yum, to also free up space taken by orphaned data from disabled or removed repos
Cleaning up list of fastest mirrors
[root@hadoop01 yum.repos.d]# yum makecache  
Loaded plugins: fastestmirror, langpacks, priorities
Repository epel is listed more than once in the configuration
Determining fastest mirrors
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
http://mirrors.aliyun.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 14] HTTP Error 404 - Not Found
Trying other mirror.
To address this issue please refer to the below wiki article 

https://wiki.centos.org/yum-errors

If above article doesn't help to resolve this issue please use https://bugs.centos.org/.

http://mirrors.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyuncs.com/centos/$releasever/os/x86_64/repodata/repomd.xml: (28, 'Connection timed out after 30000 milliseconds')
Trying other mirror.
http://mirrors.cloud.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 14] curl#6 - "Could not resolve host: mirrors.cloud.aliyuncs.com; Unknown error"
Trying other mirror.
http://mirrors.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyuncs.com/centos/$releasever/os/x86_64/repodata/repomd.xml: (28, 'Connection timed out after 30001 milliseconds')
Trying other mirror.
http://mirrors.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyuncs.com/centos/$releasever/os/x86_64/repodata/repomd.xml: (28, 'Connection timed out after 30001 milliseconds')
Trying other mirror.
http://mirrors.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyuncs.com/centos/$releasever/os/x86_64/repodata/repomd.xml: (28, 'Connection timed out after 30001 milliseconds')
Trying other mirror.
http://mirrors.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyuncs.com/centos/$releasever/os/x86_64/repodata/repomd.xml: (28, 'Connection timed out after 30001 milliseconds')
Trying other mirror.
http://mirrors.aliyuncs.com/centos/%24releasever/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyuncs.com/centos/$releasever/os/x86_64/repodata/repomd.xml: (28, 'Connection timed out after 30001 milliseconds')
Trying other mirror.
...
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 【解决方法】

在网上找了好多帖子，都没能解决我的问题，后来看到是HTTP请求失败，尝试本地访问之前wget下来的 CentOS-Base.repo 发现其中的：

http://mirrors.aliyun.com/centos/$releasever/os/$basearch/

等URL通过http的形式根本无法访问，此时将变量$releasever改为7（我的系统是centos 7），发现可以访问了，顺便将所有的变量$releasever都改为7。感觉这个变量$releasever根本就没起作用呀。

改完之后，执行yum clean all 以及 yum makecache 成功。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
oaded plugins: fastestmirror, langpacks
Determining fastest mirrors
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
base                                                                                                                 | 3.6 kB  00:00:00     
extras                                                                                                               | 3.4 kB  00:00:00     
updates                                                                                                              | 3.4 kB  00:00:00     
(1/12): base/x86_64/group_gz                                                                                         | 166 kB  00:00:00     
(2/12): base/x86_64/primary_db                                                                                       | 6.0 MB  00:00:00     
(3/12): base/x86_64/filelists_db                                                                                     | 7.1 MB  00:00:00     
(4/12): base/x86_64/other_db                                                                                         | 2.6 MB  00:00:00     
(5/12): extras/x86_64/prestodelta                                                                                    |  73 kB  00:00:00     
(6/12): extras/x86_64/primary_db                                                                                     | 215 kB  00:00:00     
(7/12): extras/x86_64/other_db                                                                                       | 131 kB  00:00:00     
(8/12): extras/x86_64/filelists_db                                                                                   | 249 kB  00:00:00     
(9/12): updates/x86_64/prestodelta                                                                                   | 945 kB  00:00:00     
(10/12): updates/x86_64/filelists_db                                                                                 | 5.2 MB  00:00:00     
(11/12): updates/x86_64/other_db                                                                                     | 764 kB  00:00:00     
(12/12): updates/x86_64/primary_db                                                                                   | 7.4 MB  00:00:00     
Metadata Cache Created
```