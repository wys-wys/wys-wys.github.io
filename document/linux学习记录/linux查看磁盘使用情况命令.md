linux查看磁盘使用情况命令

陈袁 2017-11-30 11:34:44  240133  收藏 95
分类专栏： linux 文章标签： linux命令 linux 磁盘
版权
第一：统一磁盘整体情况，包括磁盘大小，已使用，可用
1.查看当前目录
命令

df -h
1![这里写图片描述](https://img-blog.csdn.net/20171130111744654?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWNoZW55dWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
结果：

统一每个目录下磁盘的整体情况

2.查看指定目录
在命令后直接放目录名,比如查看“usr”目录使用情况：

df -h /usr/
1![这里写图片描述](https://img-blog.csdn.net/20171130111928377?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWNoZW55dWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
结果：

统一了指定目录一使用情况，及分配的最大空间

第二：具体查看文件夹的占用情况。
1.查看当前目录每个文件夹的情况。
命令：

du --max-depth=1 -h 
1![这里写图片描述](https://img-blog.csdn.net/20171130112328555?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWNoZW55dWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
结果如下：

最后一行统计整体占用多少磁盘

2.指定目录
只要在命令后直接根目录名，以目录“/usr”为例
命令如下:

du --max-depth=1 -h  /usr/
1![这里写图片描述](https://img-blog.csdn.net/20171130112601005?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWNoZW55dWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
结果如下：

第三：计算文件夹大小
为了快算显示，同时也只是想查看目录整体占用大小。可以直接使用du -sh 命令，如果想查看指定目录，直接在命令后根目录即可。
命令：

du -sh /usr/
1![这里写图片描述](https://img-blog.csdn.net/20171130112848667?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWNoZW55dWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
结果如下：


第四：总结
其中df -h和du -sh使用的比较多，一个统计整体磁盘情况，一个看单独目录点用情况，而命令du --max-depth=1 -h查看了目录下文件夹占用情况，使用比较少，可以用du -sh代替，而且命令较长，当然并不是说它没用。

点赞
21

评论
6

分享

收藏
95

打赏

举报
关注
一键三连