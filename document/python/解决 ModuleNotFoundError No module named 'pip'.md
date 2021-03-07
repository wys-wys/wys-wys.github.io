# 解决 ModuleNotFoundError: No module named 'pip'

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[王发北](https://blog.csdn.net/wwangfabei1989) 2018-04-27 14:06:47 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 68114 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 63

分类专栏： [python](https://blog.csdn.net/wwangfabei1989/category_7403599.html) 文章标签： [python](https://www.csdn.net/tags/MtjaQg4sNDk0LWJsb2cO0O0O.html) [pip](https://www.csdn.net/tags/MtzaIg0sMjA2NzMtYmxvZwO0O0OO0O0O.html) [ModuleNotFoundError](https://so.csdn.net/so/search/s.do?q=ModuleNotFoundError&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

今天 安装其它python包时，提示说 pip 10.0.1可用，就更新了一下，但是 更新过程中出现了错误，如图所示

![img](https://img-blog.csdn.net/20180427140408254)

因为这个错误导致 pip找不到，

可以首先执行 python -m ensurepip  然后执行 python -m pip install --upgrade pip  即可更新完毕。

如下图所示

 

![img](https://img-blog.csdn.net/20180427140554364)

 

知乎： https://zhuanlan.zhihu.com/albertwang

微信公众号：AI-Research-Studio

![https://img-blog.csdnimg.cn/20190110102516916.png](https://img-blog.csdnimg.cn/20190110102516916.png) 

下面是赞赏码

![img](https://img-blog.csdnimg.cn/20190325093638736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d3YW5nZmFiZWkxOTg5,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20190529101820164.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d3YW5nZmFiZWkxOTg5,size_16,color_FFFFFF,t_70) 