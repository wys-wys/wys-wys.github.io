# Google Drive 里的文件下载的方法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[weixin_30641465](https://blog.csdn.net/weixin_30641465) 2018-11-27 15:40:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 6355 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

文章标签： [matlab](https://www.csdn.net/tags/NtjaIg5sMDYzNC1ibG9n.html) [java](https://www.csdn.net/tags/NtTaIg5sMzYyLWJsb2cO0O0O.html) [移动开发](https://www.csdn.net/tags/MtTaEg0sMTI1NTAtYmxvZwO0O0OO0O0O.html)

版权

```
Google Drive 里并不提供创建直接下载链接的选项，但是可以通过小小的更改链接形式就能把分享的内容保存到本地。例如，一份通过 Google Drive 分享的文件链接形式为：

https://drive.google.com/file/d/FILE_ID/edit?usp=sharing
如果将其改为下面修改版的形式，然后再通过浏览器打开，就会直接下载该文件了：

https://drive.google.com/uc?export=download&id=FILE_ID
所需要做的就是，将红色的 FILE_ID 从原始的地址中，粘贴到修改的地址里。这里有一张图片的链接，通过修改之后，这个链接就是图片的下载地址。

Google 文档下载链接
Google Docs: 分享的文档链接形式为：

https://docs.google.com/document/d/FILE_ID/edit?usp=sharing
将 /edit 用 /export 替换掉，然后添加上文件的格式，例如是文档就添加 doc，是 PDF  就在后面添上 pdf，然后该文件就能被保存了。

https://docs.google.com/document/d/FILE_ID/export?format=doc 

https://docs.google.com/document/d/FILE_ID/export?format=pdf
除了上面的两种文件格式之外，还有’txt’，’html’，’odt’等格式。

Google 演示文稿: 演示文稿的分享链接形式是这样的格式：

https://docs.google.com/presentation/d/FILE_ID/edit?usp=sharing
如果下载 PPT（.pptx）和 PDF 格式的链接如下：

https://docs.google.com/presentation/d/FILE_ID/export/pptx 

https://docs.google.com/presentation/d/FILE_ID/export/pdf
Google 电子表格: 公开的电子表格链接格式为：

https://docs.google.com/spreadsheets/d/FILE_ID/edit?usp=sharing
其下载链接格式为：

https://docs.google.com/spreadsheets/d/FILE_ID/export?format=xlsx 

https://docs.google.com/spreadsheets/d/FILE_ID/export?format=pdf
制作副本
Google 电子表格目前可以将别人分享出来的表格制作一个副本保存在自己的 Google Drive 里，链接形式如下：

分享时的链接:   https://docs.google.com/spreadsheets/d/FILE_ID/edit?usp=sharing 
制作副本的链接: https://docs.google.com/spreadsheet/ccc?key=FILE_ID&newcopy=true
```

 

转载于:https://www.cnblogs.com/kongxiaoshuang/p/10026722.html

相关资源：[改进SEIR模型的matlab代码.zip](https://download.csdn.net/download/weixin_44348260/12412703?spm=1001.2101.3001.5697)

# 一个方便转存 Google Drive 分享文件的方法

[![img](https://upload.jianshu.io/users/upload_avatars/7014661/638924be-6c5f-44b0-b097-715f23d29d4e.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/4a55cf9a2af4)

[烹茶室](https://www.jianshu.com/u/4a55cf9a2af4)关注

2020.01.31 15:14:55字数 782阅读 5,380

用过 Google Drive (以下简称GD) 的朋友们应该都清楚，GD 分享的文件可以一键添加到自己的云盘中，速度很快，一度让我感觉 Google 好牛，但仔细一看会发现这并不是将文件转存到自己的 GD 中，以大神分享的爱情公寓5资源为例：

![img](https://upload-images.jianshu.io/upload_images/7014661-c8847346b05bbb7e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1114/format/webp)

2020-01-30-11-22-39-eb6691c425cbb3e1.png

如上图所示，我已经将该资源通过 GD 提供的一键保存按钮将资源放在我的云盘，我已经可以在我的云盘看到，但是仔细看文件详情，目前我还是以分享的方式查看，文件所有者还是共享者。

## 方法一

为了解决这一问题，有多种方法，最直接的一种就是直接在文件上右键，制作一个拷贝，这样一来， GD 就为我们拷贝一份放在了我们的云盘。

![img](https://upload-images.jianshu.io/upload_images/7014661-7672816ef6f5f8a0.png?imageMogr2/auto-orient/strip|imageView2/2/w/568/format/webp)

2020-01-30-11-26-01-d8d4773485ac2507.png

这一方法很简单直接，但是问题也显而易见，就是对文件夹执行该操作。

除了这一方法，还有一种较为专业，操作起来也较为复杂，但是可以对任何文件进行转存，可以批量处理。

## 方法二

本方法基于 `rclone` ，需准备一台境外大带宽服务器，安装 rclone，绑定云盘，然后使用命令一键转存：

```
rclone copy gdvideo:/Movies/Grab/爱情公寓5 onedrivee5:/Public/Video/ -P
```

这样的方式可以在云盘内或是云盘间转存文件，灵活方便，功能强大，为问题在于门槛较高。

使用 Rclone 还可以 [Linux 下使用 rclone 挂载网盘到本地](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.frytea.com%2Farchives%2F31%2F)

下面来介绍一种最为简单，操作较为方便的方法，基于 Telegram。

## 方法三

前些日子在 Telegram [@NewlearnerChannel](https://links.jianshu.com/go?to=https%3A%2F%2Ft.me%2FNewlearnerChannel) 频道看到这样一则推送：



```css
#Bot #GoogleDrive #telegram

谷歌网盘管理Bot🤖️
@GoogleDriveManagerBot

谷歌网盘挂载观影是很多人喜欢的看剧姿势，但目前转存不便以及文件命名不规范令人心烦，此 Bot 旨在帮助解决这一问题

🪓功能
 ⁃ 谷歌网盘资源转存
 ⁃ 网盘内资源批量重命名

💡提醒
 ⁃ 首次使用需要授权
 ⁃ 普通用户每日有转存上限

✍🏻作者：上官断大

参考内容 (https://softgateon.herokuapp.com/urltodrive/)

本文首发于 @GoogoCC

频道：@NewlearnerChannel
```

本机器人可以实现谷歌网盘资源转存以及网盘内资源批量重命名，普通用户仅可绑定一个 GD 账号，绑定好之后向机器人发送 `/copy`，机器人提示`请输入要拷贝的 Google Drive 资源链接 (可以通过浏览器或 APP 复制):` ，输入您需要转存的资源连接，之后机器人提示 `请输入保存此资源的文件夹链接 (可以通过浏览器或 APP 复制):`，此时输入您需要存入文件夹的 ID（网页访问文件夹，拷贝网址最后一段代码），之后机器人询问是否确认将文件拷贝到某文件夹，**使用键盘** 选择确认即可，之后就可以在 GD 中看到存好的文件了。

![img](https://upload-images.jianshu.io/upload_images/7014661-809871915c5ed46a.png?imageMogr2/auto-orient/strip|imageView2/2/w/489/format/webp)

2020-01-30-11-38-57-2902e6a34b0c69c7.png

## 总结

本文介绍了三种转存 GD 分享文件到自己 GD 的方法，GD 普通用户使用方法三即可，高级用户可使用方法二，普通少文件方法一即可，此外还有其他方法欢迎一起探索！

全文完。

#### 2 个回答

默认排序

[![Taki](https://pic1.zhimg.com/v2-794a50f12e0cc2b69bfc1742fdc2e15d_xs.jpg?source=1940ef5c)](https://www.zhihu.com/people/wu-tai-qiang)

[Taki](https://www.zhihu.com/people/wu-tai-qiang)

有事值乎问我

23 人赞同了该回答创建于: 2020-02-24 14:53:56  编辑于: 2020-09-04 00:34:01创建于: 2020-02-24 14:53:56  编辑于: 2020-09-04 00:34:01创建于: 2020-02-24 14:53:56  编辑于: 2020-09-04 00:34:01

[https://googledrive.moeclub.workers.dev/](https://link.zhihu.com/?target=https%3A//googledrive.moeclub.workers.dev/){yourfileid}------------分割线------------------------------------最近发现不太work，有了一个新的方法：首先你得有一个**软件，网速差或者流量限制都行，推荐蓝色的灯笼，链接可以[http://github.com](https://link.zhihu.com/?target=http%3A//github.com)里面找。然后：[https://www.multcloud.com/#cloudType=oneDrive&tokenId=8VdMWtS2tTCwnzmkKm6c4WHJITavqClUryA002fEDiwouCibCMnLBXYB002fOOKwu8tAKJ&fileId=/](https://link.zhihu.com/?target=https%3A//www.multcloud.com/%23cloudType%3DoneDrive%26tokenId%3D8VdMWtS2tTCwnzmkKm6c4WHJITavqClUryA002fEDiwouCibCMnLBXYB002fOOKwu8tAKJ%26fileId%3D/)里面，注册一个账号，**关联自己的谷歌账号与其他云盘【onedrive/mega/baiduyun等】的账号**，新建一个Transfer任务，将自己的google drive的文件transfer到onedrive/mega【其实也支持直接到百度云，但是慢啊，真的慢，此外需要将google drive文件移到文件夹里面，权限设置为所有人可见】![img](https://pic1.zhimg.com/v2-41fcbe109e0d2fa947faf0bd61803739_r.jpg?source=1940ef5c)接下来有两种方法：1：你可以使用电脑端的onedrive来同步，但是速度很佛系，2：建议在chrome打开onedrive网页版【也需要**】，然后使用迅雷接管chrome下载，![img](https://pic1.zhimg.com/v2-ad4a38c0fe4f60e450001a5683577291_r.jpg?source=1940ef5c)在onedrive网页版逐个下载文件，本来是浏览器自带的下载器下载，迅雷的插件会自动检测，然后使用迅雷下载，下载速度还行。-------------------------分割线2---------------------------------------除了将google drive文件移到onedrive以外，还可以尝试将文件移到MEGA网盘中，mega网盘比较良心，可以尝试。![img](https://pic1.zhimg.com/v2-86a31761115d6d8e522925ed6df53380_r.jpg?source=1940ef5c)有关mega网盘：[网盘可以良心到什么程度? 试试MEGA吧!www.jianshu.com](https://link.zhihu.com/?target=https%3A//www.jianshu.com/p/44741a9e243f)

[编辑于 2020-09-04](https://www.zhihu.com/question/370464588/answer/1035001509)

真诚赞赏，手留余香