# PS | 安装插件提示未正确签署 not properly signed

[![img](https://upload.jianshu.io/users/upload_avatars/16873033/63d6e2e2-6d28-4cc2-92fc-713ac86d122a.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/9a2ca0f33c8d)

[雪碧是我啊](https://www.jianshu.com/u/9a2ca0f33c8d)关注

0.0932020.08.17 10:23:45字数 311阅读 273

![img](https://upload-images.jianshu.io/upload_images/16873033-f0c1098070663abc.jpeg)

## Mac版本

1.选择系统顶部-菜单-前往-实用工具-终端

![img](https://upload-images.jianshu.io/upload_images/16873033-5fe21024c00d6442.jpeg)

2.输入命令行：defaults write com.adobe.CSXS.7 PlayerDebugMode 1

3.输入完成后，回车确认即可！！重新启动PhotoShop即可使用ps扩展面板！

![img](https://upload-images.jianshu.io/upload_images/16873033-21ca044d0b492cfa.jpeg)

温馨提示:其它版本PhotoShop请自行替换输入命令行

例如：

PS CC 2015：defaults write com.adobe.CSXS.6 PlayerDebugMode 1

PS CC 2015.5：defaults write com.adobe.CSXS.7 PlayerDebugMode 1

PS CC 2017：defaults write com.adobe.CSXS.7 PlayerDebugMode 1

PS CC 2018：defaults write com.adobe.CSXS.8 PlayerDebugMode 1

PS CC 2019/2020：defaults write com.adobe.CSXS.9 PlayerDebugMode 1

## Windows版本

PSCC2017为例:

1.打开-注册表（运行 regedit）

2.打开-HKEY_CURRENT_USER\Software\Adobe\CSXS.7

![img](https://upload-images.jianshu.io/upload_images/16873033-a088040987951b4a.jpeg)

3.鼠标右键-新建-字符串值-确定

![img](https://upload-images.jianshu.io/upload_images/16873033-aa2ea63cc024959a.jpeg)

4.选中刚新建的字符串值注册表-鼠标右键-修改-数值名称：PlayerDebugMode 数值数据：1

温馨提示:其它版本PhotoShop以CSXS.X数值最大的目录下新建字符串值注册表

![img](https://upload-images.jianshu.io/upload_images/16873033-5d720868358cb4ca.jpeg)

例如：

CC 2015：HKEY_CURRENT_USER\Software\Adobe\CSXS.6

CC 2015.5：HKEY_CURRENT_USER\Software\Adobe\CSXS.7

CC 2017：HKEY_CURRENT_USER\Software\Adobe\CSXS.7

CC 2018：HKEY_CURRENT_USER\Software\Adobe\CSXS.8

CC 2019：HKEY_CURRENT_USER\Software\Adobe\CSXS.9



1人点赞



[各种疑难杂症的处方](https://www.jianshu.com/nb/45507963)



更多精彩内容，就在简书APP

"能帮到你很开心！"

赞赏支持还没有人赞赏，支持一下

[![  ](https://upload.jianshu.io/users/upload_avatars/16873033/63d6e2e2-6d28-4cc2-92fc-713ac86d122a.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/100/h/100/format/webp)](https://www.jianshu.com/u/9a2ca0f33c8d)

[雪碧是我啊](https://www.jianshu.com/u/9a2ca0f33c8d)

总资产0.737共写了1129字获得10个赞共0个粉丝