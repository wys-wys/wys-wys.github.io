# [unzip：unzip解压文件到指定目录](https://www.cnblogs.com/yongdaimi/p/9772158.html)

1、把文件解压到当前目录下

```
unzip test.zip
```

2、如果要把文件解压到指定的目录下，需要用到-d参数。

```
unzip -d /temp test.zip
```

3、解压的时候，有时候不想覆盖已经存在的文件，那么可以加上-n参数

```
unzip -n test.zip
unzip -n -d /temp test.zip
```

4、只看一下zip压缩包中包含哪些文件，不进行解压缩

```
unzip -l test.zip
```

5、查看显示的文件列表还包含压缩比率

```
unzip -v test.zip
```

6、检查zip文件是否损坏

```
unzip -t test.zip
```

7、将压缩文件test.zip在指定目录tmp下解压缩，如果已有相同的文件存在，要求unzip命令覆盖原先的文件

```
unzip -o test.zip -d /tmp/
```

 

分类: [Linux-日常使用](https://www.cnblogs.com/yongdaimi/category/1134306.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/653161/20200628173510.png)](https://home.cnblogs.com/u/yongdaimi/)

[夜行过客](https://home.cnblogs.com/u/yongdaimi/)
[关注 - 15](https://home.cnblogs.com/u/yongdaimi/followees/)
[粉丝 - 84](https://home.cnblogs.com/u/yongdaimi/followers/)

[+加关注](javascript:void(0);)

2

0

[« ](https://www.cnblogs.com/yongdaimi/p/9771143.html)上一篇： [GitBash：修改GitBash主题配色和字体](https://www.cnblogs.com/yongdaimi/p/9771143.html)
[» ](https://www.cnblogs.com/yongdaimi/p/9772235.html)下一篇： [FFmpeg编译：jni not found 的问题](https://www.cnblogs.com/yongdaimi/p/9772235.html)

posted @ 2018-10-11 14:18 [夜行过客](https://www.cnblogs.com/yongdaimi/) 阅读(71200) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=9772158) [收藏](javascript:void(0))