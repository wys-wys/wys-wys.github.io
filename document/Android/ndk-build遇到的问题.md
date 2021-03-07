# Android NDK: APP_PLATFORM not set. Defaulting to minimum supported version android-14.

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[牛八少爷](https://niubashaoye.blog.csdn.net/) 2019-07-19 17:21:37 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 6082 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [NDK开发错误](https://blog.csdn.net/niuba123456/category_7786544.html) 文章标签： [NDK](https://www.csdn.net/gather_2d/MtTaEg0sMjA0NzYtYmxvZwO0O0OO0O0O.html)

版权

# 1.错误描述

Android NDK: APP_PLATFORM not set. Defaulting to minimum supported version android-14.
D:/ProgramFiles/Android/ndk15/build//../build/core/build-binary.mk:688: Android NDK: Module yuv depends on undefined modules: jpeg
D:/ProgramFiles/Android/ndk15/build//../build/core/build-binary.mk:701: *** Android NDK: Aborting (set APP_ALLOW_MISSING_DEPS=true to allow missing dependencies)   .  Stop.

![img](https://img-blog.csdnimg.cn/20190719171556231.png)

# 2.错误原因

Application.mk设置的ndk版本与使用的ndk版本不一致；

# 3.解决方案

在Application.mk中添加或修改：

```
APP_PLATFORM := android-15



APP_ALLOW_MISSING_DEPS=true
```

 