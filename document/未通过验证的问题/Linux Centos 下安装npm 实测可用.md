# Linux Centos 下安装npm 实测可用

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[B站：阿里武](https://blog.csdn.net/qq874455953) 2018-12-16 13:35:19 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1960 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [解决方案](https://blog.csdn.net/qq874455953/category_7723746.html) 文章标签： [npm](https://www.csdn.net/tags/MtzaYg3sODAxMi1ibG9n.html) [Centos](https://www.csdn.net/tags/MtTaEg0sMzk5NjctYmxvZwO0O0OO0O0O.html)

## 转载地址

## https://blog.csdn.net/u012129607/article/details/60966045

1.root 登录linux

2.没有目录就自己创建一个

```
cd /usr/local/node/
```

3.下载安装包

```
wget https://npm.taobao.org/mirrors/node/v4.4.7/node-v4.4.7-linux-x64.tar.gz
```

4.解压安装包

```
tar -zxvf node-v4.4.7-linux-x64.tar.gz
```

5.移除安装包

```
rm -rf node-v4.4.7-linux-x64.tar.gz
```

6.建立软连接

```
ln -s /usr/local/node/node-v4.4.7-linux-x64/bin/npm /usr/local/bin/npm
ln -s /usr/local/node/node-v4.4.7-linux-x64/bin/node /usr/local/bin/node1
```

7.查看npm版本

```
npm -v
```

8.npm升级，@后面是版本号

```
npm i -g npm@3.3.1
```

安装完成。

转载自https://blog.csdn.net/u012129607/article/details/60966045

# Centos 7无法安装npm

时间 2018-11-10

标签 [centos](http://www.voidcn.com/tag/centos) [node.js](http://www.voidcn.com/tag/node.js) [npm](http://www.voidcn.com/tag/npm) 栏目 [CentOS](http://www.voidcn.com/column/centos)

*原文*  [https://serverfault.com/questions/611791/centos-7-cant-yum-install-npm](javascript:void())

我正在尝试在centos 7上安装nodejs和npm



所以我先做了
  rpm -i [http://dl.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm](javascript:void())
获得epel存储库

然后我尝试了yum install nodejs.哪个有效.
然后我尝试了yum install npm. Yum返回“未找到npm包”

我是否必须手动构建npm？那我该怎么办？

我刚刚重新检查过这个. nodejs和npm以及两者的所有依赖关系都已添加到epel 7.我刚安装在我的CentOS 7盒子上.你应该能够做到：





```
yum -y install nodejs npm
```

-y标志会自动对每个确认问题回答“是”,所以如果你想对某些事情说不,请将其留空.

# [centos用 yum 方式安装 nodejs 和 npm](http://www.dahouduan.com/2014/12/25/centos-yum-install-nodejs-npm/)

[ 全栈](http://www.dahouduan.com/category/fullstack/) [shanhuhai](http://www.dahouduan.com/author/shanhuhai/) 7年前 (2014-12-25) 27543℃

要通过 yum 来安装 nodejs 和 npm 需要先给 yum 添加 epel 源，
添加方法在 [centos 添加epel和remi源](http://www.dahouduan.com/2014/12/25/centos-yum-add-epel-remi/) 中
安装完成后,执行

```
yum -y install nodejs npm --enablerepo=epel
```

转载请注明：[大后端](http://www.dahouduan.com/) » [centos用 yum 方式安装 nodejs 和 npm](http://www.dahouduan.com/2014/12/25/centos-yum-install-nodejs-npm/)