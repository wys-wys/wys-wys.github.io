# 检测到 #include 错误。请更新 includePath。已为此翻译单元 禁用波形曲线。C/C++ 无法打开 源 文件 "bits/stdc++.h"C/C++

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[虚拟WORLD-er](https://blog.csdn.net/qq_37960007) 2020-02-23 10:35:39 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 26007 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 43

分类专栏： [vscode](https://blog.csdn.net/qq_37960007/category_8904707.html) 文章标签： [c++万能头文件](https://www.csdn.net/tags/MtTaMgwsMTQxLWJsb2cO0O0O.html) [include报错](https://so.csdn.net/so/search/s.do?q=include报错&t=blog&o=vip&s=&l=&f=&viparticle=) [已为此翻译单元 禁用波形曲线](https://so.csdn.net/so/search/s.do?q=已为此翻译单元 禁用波形曲线&t=blog&o=vip&s=&l=&f=&viparticle=) [检测到 #include 错误](https://so.csdn.net/so/search/s.do?q=检测到 #include 错误&t=blog&o=vip&s=&l=&f=&viparticle=) [vscode](https://www.csdn.net/tags/MtzacgxsOTMxNi1ibG9n.html)

版权

换了新vscode，准备c++刷一刷 leetcode，结果万能头文件 include 报错：

![img](https://img-blog.csdnimg.cn/20200223095711479.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3OTYwMDA3,size_16,color_FFFFFF,t_70)

害，又是这个错误，其实官方文档里都说的明明白白了，一直觉得没必要写，但搜索引擎上乍一搜好像又没有很多相似文章，那这里还是记录下吧。

事实上是这样的，如果你电脑装了visual studio，或者wsl（windows下Linux子系统），vscode会优先用前两者的编译器，如果前两个都没检测到，vscode才会使用mingw，下图官方文档说的很清楚（居然还有当年的笔记）

![img](https://img-blog.csdnimg.cn/20200223101047135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3OTYwMDA3,size_16,color_FFFFFF,t_70)

而巧的是，<bits/stdc++.h>万能头文件是mingw里才有的（据我观察是这样，不知道新版的wsl，vs支不支持），所以为了include万能头文件不报错，你要做的就是打开c_cpp_properties.json（首次vscode会提示你打开），把compilerPath

![img](https://img-blog.csdnimg.cn/20200223102103143.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3OTYwMDA3,size_16,color_FFFFFF,t_70)

改成你mingw的路径即可：

![img](https://img-blog.csdnimg.cn/20200223102556279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3OTYwMDA3,size_16,color_FFFFFF,t_70)

然后就没问题了

![img](https://img-blog.csdnimg.cn/2020022310275673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3OTYwMDA3,size_16,color_FFFFFF,t_70)