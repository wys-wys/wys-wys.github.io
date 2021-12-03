# npm WARN saveError ENOENT: no such file or directory, open ‘ /root/package. json ‘

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[Code_Zevin_J](https://blog.csdn.net/JZevin) 2020-08-07 16:40:11 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1198 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [linux](https://blog.csdn.net/jzevin/category_10226336.html) 文章标签： [npm](https://www.csdn.net/tags/MtzaYg3sODAxMi1ibG9n.html) [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [ubuntu](https://www.csdn.net/tags/MtTaEg0sNTA1ODktYmxvZwO0O0OO0O0O.html)

版权

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200807162812591.png)

## 报错分析🔍

先来翻译一下报错信息：**我们缺少一个文件名为`package.json`的系统文件**
其实最主要的是这应该是你第一次使用npm安装模块，并没有进行npm的初始化操作。初始化一下就好了：

```javascript
npm init -y
1
```

之后你使用安装命令会发现刚才的警告还剩最后两个：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080716325217.png)
是因为系统在给你配置package.json文件的时候并没有帮你设置`description`字段和存储库字段，需要我们自己手动设置。直接用vim打开这个文件编辑：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200807163453649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0paZXZpbg==,size_16,color_FFFFFF,t_70)
如图设置：`description`字段的内容无所谓，不为空即可；第二个权限设置成私有的即可。接下来就可以正常使用npm安装命令了。

------

完整的npm安装模块的操作请看我另一篇：

[**【linux系统（ubuntu16.04）】Node.js中使用npm命令安装readline-sync模块实现用户键盘输入**](https://blog.csdn.net/JZevin/article/details/107849422)