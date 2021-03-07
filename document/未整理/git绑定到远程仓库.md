绑定远程仓库origin为本地分支名称

 git remote add origin https://github.com/wys-wys/GitHub.git

从远程拉取

git pull https://github.com/wys-wys/GitHub.git/

# Git--建立和解除与远程仓库的关联

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Jinphy](https://blog.csdn.net/Jinphy) 2018-07-25 17:27:38 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 17913 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

分类专栏： [学习](https://blog.csdn.net/jinphy/category_7835292.html) 文章标签： [Git](https://www.csdn.net/tags/MtzaYgwsMzEzMy1ibG9n.html)

版权

**普及：**这里所讲的远程仓库有[Github](http://github.com/)、[Gitee](http://gitee.com/)等，如果看到这篇文章时，你还没有相关网站的账号，赶紧地去注册一个。
但这里时，我就假设你已经有了以上所提及的平台账号了，还记得上一篇文章[Git–入门配置](https://blog.csdn.net/jinphy/article/details/81203891)吗？把生成的公钥添加到以上平台的SSH Key 中

## 关联远程仓库

下面我们就来了解如何建立本地仓库与远程仓库的关联。
***第一、在本地已经有了仓库，需要把它推送到远程仓库去\***

- **以Github平台为例**

- **在github上面创建一个空的仓库**

- **在Git Bash上输入如下命令，将本地仓库与远程仓库关联**

  $git remote add **github** git@github.com:Jinphy/GitTest.git

  **注意：**这里需要注意的是上面命令中的**github** 是远程仓库在本地Git的名称，默认情况下一般命名为**origin**，但是这里为了区分不同平台的远程仓库（例如：Gitee平台的远程仓库在本地可以命名为**gitee**），所以为**github**。另外Jinphy是你自己的账号名，需要改为你自己的，不然你就关联到我的远程仓库了，但是这样对我是没有影响的，因为你是没有权限在我的平台上提交任何代码的

- **查看本地仓库与远程仓库的关联详情**

  $ git remote -v

## 解除远程仓库

删除与远程仓库的关联就比较简单了，直接输入以下命令：
$ git remote rm **github**

**注意：** 以上**github** 是远程仓库在本地Git中的名称。

#### 1. 打开在你的项目文件夹，输入下面的命令

```
git init
```

![img](https://images2015.cnblogs.com/blog/643024/201611/643024-20161117105613529-1331892400.png)

 输完上面的命令，文件夹中会出现一个.git文件夹，如下图所示，其他的的文件也会出现蓝色小问号的标志

 ![img](https://images2015.cnblogs.com/blog/643024/201610/643024-20161020175232498-1872971817.png)

###  2. 添加所有文件

```
git add .
```

注意最后的点是有用的哦

![img](https://images2015.cnblogs.com/blog/643024/201611/643024-20161117105642248-437211863.png)

 输入完成后，文件夹如下所示

![img](https://images2015.cnblogs.com/blog/643024/201610/643024-20161020175721045-34264600.png)

###  3. 提交所有文件

```
git commit -m "这里是备注信息" -a
```

![img](https://images2015.cnblogs.com/blog/643024/201611/643024-20161117105723982-456456864.png)

 完成后，文件夹显示如下

![img](https://images2015.cnblogs.com/blog/643024/201610/643024-20161020180119123-417194644.png)

都会出现绿色的小对勾

###  4. 连接到远程仓库

提前在你的github中新建一个仓库，操作如下

![img](https://images2015.cnblogs.com/blog/643024/201610/643024-20161020180953357-871156867.png)

建好后，取好项目名称，点击create repository按钮，完成仓库的建立

![img](https://images2015.cnblogs.com/blog/643024/201610/643024-20161020180830388-1568291414.png)

![img](https://images2015.cnblogs.com/blog/643024/201610/643024-20161026120125703-263387261.png)

点击红色框出的小按钮，复制链接 

### 5. 连接远程仓库，在本地的命令框中输入下面的命令，即连接到了名为poster的仓库上

```
git remote add origin https://github.com/OliveKong/poster.git 
```

 ![img](https://images2015.cnblogs.com/blog/643024/201611/643024-20161117105800279-1083550297.png)

 

### 6.把本地项目推送到远程仓库

```
git push -u origin master 
```

![img](https://images2015.cnblogs.com/blog/643024/201611/643024-20161117105822107-1011418356.png)

 

 

出现上图的情况就是上传完成了

文章如有bug，请留言！

# github怎样解除绑定的远程仓库



## 最新回答 (2条回答)

![头像](https://cache.soso.com/qlogo/g?b=qq&k=1pDbRicuYxdfgoPNKsUeljw&s=100&t=288)

グ夜、很羙ゝ1级

2016-07-01 回答

```
在创建仓库之前，还需要用已有的帐号创建一个项目，projectname将是这里即将创建的项目名称。在git中，项目被称为仓库(repository)，仓库顾名思义，当然可以包含代码或者非代码。将来我们的网页或者模板实际上都是保存在这个仓库中的。
登录后，访问https://github.com/new，创建仓库。希望可以帮到你
```

9

![头像](https://hhy.sogoucdn.com/deploy/ued/question-njk/pc/dist/img/default-thumb/default-thumb7_d1a7915.png)

匿名用户1级

2014-11-21 回答

```
▶ git remote -h
用法：git remote [-v | --verbose]
   或：git remote add [-t <分支>] [-m <master>] [-f] [--tags|--no-tags] [--mirror=<fetch|push>] <名称> <url>
   或：git remote rename <旧名称> <新名称>
   或：git remote remove <名称>
   或：git remote set-head <名称> (-a | --auto | -d | --delete |<分支>)
   或：git remote [-v | --verbose] show [-n] <名称>
   或：git remote prune [-n | --dry-run] <名称>
   或：git remote [-v | --verbose] update [-p | --prune] [(<组> | <远程>)...]
   或：git remote set-branches [--add] <名称> <分支>...
   或：git remote set-url [--push] <名称> <新的地址> [<旧的地址>]
   或：git remote set-url --add <名称> <新的地址>
   或：git remote set-url --delete <名称> <地址>

    -v, --verbose         冗长输出；必须置于子命令之前
```