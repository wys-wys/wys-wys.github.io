此时先检查一下有没有安装`Appium-Python-Client，如果没有安装``Appium-Python-Client就在控制台输入``pip install Appium-Python-Client进行Appium-Python-Client的安装，安装完后在Pycharm中导入appium模块时还会出现ModuleNotFoundError: No module named 'appium'的错误，那就是没有在Pycharm中配置Project Interpreter。`

打开Pycharm，PyCharm->Preferences->Project Interpreter

![img](https://images2018.cnblogs.com/blog/1212127/201808/1212127-20180828150941170-1874055285.png)

点击左下角的+号进入Available Packages在输入框中输入Appium-Python-Client,再点击左下角的下载将Appium-Python-Client下载下来，

![img](https://images2018.cnblogs.com/blog/1212127/201808/1212127-20180828151213225-256552844.png)

下载成功之后回到Preferences界面，发现已经多了Appium-Python-Client，此时已经配置成功，回到Pycharm再导入appium就不会报错了。

![img](https://images2018.cnblogs.com/blog/1212127/201808/1212127-20180828151224065-2097311180.png)

 

标签: [python](https://www.cnblogs.com/HuangXiaoJuan/tag/python/), [UI自动化测试](https://www.cnblogs.com/HuangXiaoJuan/tag/UI自动化测试/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1212127/20181011112724.png)](https://home.cnblogs.com/u/HuangXiaoJuan/)

[夏诗](https://home.cnblogs.com/u/HuangXiaoJuan/)
[关注 - 7](https://home.cnblogs.com/u/HuangXiaoJuan/followees/)
[粉丝 - 3](https://home.cnblogs.com/u/HuangXiaoJuan/followers/)

[+加关注](javascript:void(0);)

0

0

[« ](https://www.cnblogs.com/HuangXiaoJuan/p/9548036.html)上一篇： [如何升级pip3](https://www.cnblogs.com/HuangXiaoJuan/p/9548036.html)
[» ](https://www.cnblogs.com/HuangXiaoJuan/p/9687951.html)下一篇： [appium报错：An unknown server-side error occurred while processing the command. Original error: Could not proxy command to remote server. Original error: Error: read ECONNRESET](https://www.cnblogs.com/HuangXiaoJuan/p/9687951.html)