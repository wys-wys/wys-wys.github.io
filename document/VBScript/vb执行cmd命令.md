# VBScript：执行命令行（cmd）命令

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[xuejianbest](https://blog.csdn.net/xuejianbest) 2019-01-02 15:01:28 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7786 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 3

分类专栏： [VBScript](https://blog.csdn.net/xuejianbest/category_8577837.html)

版权

连续执行命令用`&&`符号连接，如：

```vbnet
e: && cd e:\abc && dir
1
```

用vbs打开cmd并执行指定指令：

```vbnet
Set obj = createobject("wscript.shell")
obj.run "cmd /k e: && cd E:\aaa && dir"
12
```

打开资源管理器并定位到e:\aaa，若目录不存在则定位到我的文档：

```vbnet
Set obj = createobject("wscript.shell")
obj.run "cmd /c explorer e:\aaa"
12
```

`%cd%`表示当前目录，`explorer %cd%`即打开当前目录

`iexplore`表示ie，`iexplore "www.baidu.com"`打开百度