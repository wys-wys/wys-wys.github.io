# windows修改host文件，并且不重启电脑立即生效

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[铁汉柔情li](https://blog.csdn.net/qq_37306041) 2019-05-30 14:21:16 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10162 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 3

分类专栏： [windows](https://blog.csdn.net/qq_37306041/category_8994048.html) 文章标签： [windows](https://www.csdn.net/tags/MtTaEg0sNTAxMTMtYmxvZwO0O0OO0O0O.html)

版权

### 1.host文件的位置：

```
C:\windows\system32\drivers\etc\
```

### 2.修改host文件

### 3.键入以下命令，让修改的内容立即生效

```
ipconfig /flushdns  //刷新DNS
```

 