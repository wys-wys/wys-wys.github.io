# linux下解压tar.xz方法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Locutus](https://blog.csdn.net/yjk13703623757) 2018-04-08 10:53:16 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 63580 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 21

分类专栏： [Linux](https://blog.csdn.net/yjk13703623757/category_6497734.html)

版权

### 1. 解压tar.xz安装包

今天去Ubuntu上安装nodejs，下载的文件是node-v8.11.1-linux-x64.tar.xz，这是两层压缩，外面是xz压缩，里层是tar压缩，所以分两步实现解压。

```
# xz -d node-v8.11.1-linux-x64.tar.xz

# tar -xvf node-v8.11.1-linux-x64.tar.xz123
```

也可以直接解压

```
# tar -xvJf node-v8.11.1-linux-x64.tar.xz1
```

tar.xz格式的压缩包大小比.tar要小，但是压缩解压缩时间比较长
![这里写图片描述](https://img-blog.csdn.net/20180408103718920?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lqazEzNzAzNjIzNzU3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 2. 创建tar.xz压缩文件

- 先创建xxx.tar文件

```
# tar -cvf xxx.tar xxx1
```

- 再创建xxx.tar.xz文件

```
# xz -z xxx.tar1
```

如果要保留被压缩的文件，需要加上参数-k