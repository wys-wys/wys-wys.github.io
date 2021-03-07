# GitBash设置代理

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[arashethis](https://blog.csdn.net/u010986031) 2018-05-31 17:43:11 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 5913 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

版权

`path/to/install/Git/etc/bash.bashrc`文件添加

```bash
export http_proxy="http://127.0.0.1:1080/pac?auth=**************************************"
export https_proxy="http://127.0.0.1:1080/pac?auth=**************************************"
```

或者在profile配置文件中添加

