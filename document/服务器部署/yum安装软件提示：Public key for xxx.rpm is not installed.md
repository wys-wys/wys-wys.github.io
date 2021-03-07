

# yum安装软件提示：Public key for xxx.rpm is not installed

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[陌小铠](https://blog.csdn.net/cy309173854) 2017-04-05 17:20:13 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 16959 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 5

分类专栏： [Linux](https://blog.csdn.net/cy309173854/category_6429619.html) [Linux](https://blog.csdn.net/cy309173854/category_9270033.html) 文章标签： [yum](https://www.csdn.net/tags/MtTaEg0sNDk5NzYtYmxvZwO0O0OO0O0O.html) [NOKEY](https://so.csdn.net/so/search/s.do?q=NOKEY&t=blog&o=vip&s=&l=&f=&viparticle=) [Public-key](https://so.csdn.net/so/search/s.do?q=Public-key&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

yum安装软件提示：Public key for xxx.rpm is not installed:

> warning: rpmts_HdrFromFdno: Header V3 RSA/SHA256 Signature, key ID 0608b895: NOKEY
>
> Public key for fail2ban-0.9.6-1.el6.1.noarch.rpm is not installed

![Public key is not installed](https://img-blog.csdn.net/20170405171347580?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3kzMDkxNzM4NTQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

错误：RPM安装或升级时签名效验错误
原因：在安装或升级软件包时会检查软件包的签名，若系统没有导入或使用了旧版本的GPG keys，那么需要导入或获取最新的GPG keys才能安装。
查看是否安装GPG keys：

```
# rpm -qa gpg*1
```

查看安装GPG keys 详细信息

```
# rpm -qi gpg-pubkey-c105b9de-4e0fd3a31
# rpm -q gpg-pubkey --qf '%{name}-%{version}-%{release} --> %{summary}\n'1
```

![GPG keys 详细信息](https://img-blog.csdn.net/20170405171425714?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3kzMDkxNzM4NTQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 解决方法：

总结以下三种：

### 1. 导入GPG keys：

```
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-*1
```

### 2. 修改yum源文件，跳过gpgcheck(不推荐)

把 repo文件设置为gpgcheck=0
使用yum install 时加上参数–nogpgcheck

### 3. 下载最新签名(推荐)：

```
# cd /etc/pki/rpm-gpg
# wget http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-6 
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6123
```

问题解决：
![问题解决](https://img-blog.csdn.net/20170405171652191?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3kzMDkxNzM4NTQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

# yum 安装报 关于Public key for *.rpm is not installed 的解决方法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[sxfcct](https://blog.csdn.net/sxfcct) 2013-08-12 11:17:43 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3548 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [php](https://blog.csdn.net/sxfcct/category_1260165.html) [linux](https://blog.csdn.net/sxfcct/category_1318693.html)

**此时要导入rpm的签名信息即可**

**以root登录，执行下面命令
\# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
**

**
**

**根据我的Linux版本是CentOS 5.4**

**于是我执行下面命令
\*#rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5\*

问题终于得到解决！**

# Public key for docker-ce-19.03.12-3.el7.x86_64.rpm is not installed

![img](https://www.tnblog.net/img/article/xas.png)1343人阅读2020/9/3 14:35总访问：553011[评论:](https://www.tnblog.net/aojiancc2/article/details/5004#)0[手机](https://www.tnblog.net/aojiancc2/article/details/5004#)[收藏](javascript:;)

![img](https://www.tnblog.net/img/article/atype.png) 分类: docker

centos安装docker报错：Public key for docker-ce-19.03.12-3.el7.x86_64.rpm is not installed
![img](https://img.tnblog.net/arcimg/aojiancc2/80089b095d1846339eb56dbc2e1ee438.png)
错误原因是公钥未安装

解决方法，退出安装docker然后执行两个命令后在安装即可
先执行：

```
wget https://get.docker.com/gpg
```

在执行：

```
rpmkeys --import ./gpg
```

在命令行执行的效果如下：
![img](https://img.tnblog.net/arcimg/aojiancc2/4163f0c2014b4713a5e065f5859ce0b5.png)