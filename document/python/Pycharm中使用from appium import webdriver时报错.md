- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/HuangXiaoJuan/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/夏诗)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/HuangXiaoJuan/rss/)

# [Pycharm中使用from appium import webdriver时报错：ModuleNotFoundError: No module named 'appium'](https://www.cnblogs.com/HuangXiaoJuan/p/9548409.html)

此时先检查一下有没有安装`Appium-Python-Client，如果没有安装``Appium-Python-Client就在控制台输入``pip install Appium-Python-Client进行Appium-Python-Client的安装，安装完后在Pycharm中导入appium模块时还会出现ModuleNotFoundError: No module named 'appium'的错误，那就是没有在Pycharm中配置Project Interpreter。`

打开Pycharm，PyCharm->Preferences->Project Interpreter

![img](https://images2018.cnblogs.com/blog/1212127/201808/1212127-20180828150941170-1874055285.png)

点击左下角的+号进入Available Packages在输入框中输入Appium-Python-Client,再点击左下角的下载将Appium-Python-Client下载下来，

![img](https://images2018.cnblogs.com/blog/1212127/201808/1212127-20180828151213225-256552844.png)

下载成功之后回到Preferences界面，发现已经多了Appium-Python-Client，此时已经配置成功，回到Pycharm再导入appium就不会报错了。

![img](https://images2018.cnblogs.com/blog/1212127/201808/1212127-20180828151224065-2097311180.png)

 