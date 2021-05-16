python3安装后没有pip解决

必须使用python3 或者pip3作为命令

Yfw&武 2020-03-08 13:32:45  10126  收藏 6
分类专栏： ❤ Python
版权
apt安装
sudo apt install python3-pip
1
手动下载安装pip
下载最新版pip，下载地址https://pypi.org/project/pip/#modal-close

1、安装python-setuptools

apt install python-setuptools

3、解压进入pip-20.0.2目录下，执行
python setup.py install

# python3安装后没有pip解决

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Yfw&武](https://blog.csdn.net/u012577474) 2020-03-08 13:32:45 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10126 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

分类专栏： [❤ Python](https://blog.csdn.net/u012577474/category_9334592.html)

版权

## apt安装

```bash
sudo apt install python3-pip
1
```

## 手动下载安装pip

下载最新版pip，下载地址https://pypi.org/project/pip/#modal-close

1、安装python-setuptools

```
apt install python-setuptools
```

3、解压进入pip-20.0.2目录下，执行
`python setup.py install`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200308133220707.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTI1Nzc0NzQ=,size_16,color_FFFFFF,t_70)



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞3
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论](https://blog.csdn.net/u012577474/article/details/104731459/#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏6](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReward.png)打赏
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连

[*python**3*.8与*pip**3**安装*](https://blog.csdn.net/weixin_42101177/article/details/102971339)

[weixin_42101177的博客](https://blog.csdn.net/weixin_42101177)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 2万+

[*python**安装* 很简单，直接从官网找一个自己喜欢的版本下载即可 官网传送门 接下来就是配置全局变量，网上有很多我就不多说了，具体可以参考这个 这里 之后呢就是在cmd里输入*python*测试一下，如果出现的是*python*的版本号，则表示*安装*成功了。 == 这些呢都还好，重点是有可能你下的*python**3*之前的版本*安装*时没勾选*pip*，导致*pip**没有*一起下下来 ，或者一些其他未知原因，导致*pip*无法使用...](https://blog.csdn.net/weixin_42101177/article/details/102971339)

[*python**3* *没有* *pip**3**解决*方法](https://blog.csdn.net/ab15169196385/article/details/101147935)

[ab15169196385的博客](https://blog.csdn.net/ab15169196385)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 3113

[问题现象：在linux环境下，*安装*完*python**3*.6.2后，发现并*没有**pip**3*功能。 *解决*方](https://blog.csdn.net/ab15169196385/article/details/101147935)


点赞
3

评论

分享

收藏
6

打赏

举报
关注
一键三连

python3.8与pip3安装
weixin_42101177的博客
 2万+
python安装 很简单，直接从官网找一个自己喜欢的版本下载即可 官网传送门 接下来就是配置全局变量，网上有很多我就不多说了，具体可以参考这个 这里 之后呢就是在cmd里输入python测试一下，如果出现的是python的版本号，则表示安装成功了。 == 这些呢都还好，重点是有可能你下的python3之前的版本安装时没勾选pip，导致pip没有一起下下来 ，或者一些其他未知原因，导致pip无法使用...
python3 没有 pip3解决方法
ab15169196385的博客
 3113
问题现象：在linux环境下，安装完python3.6.2后，发现并没有pip3功能。 解决方