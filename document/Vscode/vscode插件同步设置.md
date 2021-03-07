# [vscode同步设置&扩展插件](https://www.cnblogs.com/ashidamana/p/6761085.html)

首先安装同步插件： [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) 

 

第二步：进入你的github如图：

 **打开设置选项：**

![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425110145709-1197520269.png)

 

**新建一个token：**

![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425110217694-265826573.png)

如图：

![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425110527569-2136789567.png)

 **记住这个token值**

 ![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425110611272-515677998.png)

 

转到vscode

 按shift+alt +u  在弹出窗里输入你的token,然后等下会生成syncSummary.txt文件在窗口中打开这样就算成功了。

![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425111018694-1033070297.png)

syncSummary.txt这个文件里有个gist值或者到用户设置文件中查看gist的值，这个值用来你再另一台电脑上来下载你的设置

![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425111301428-168249381.png)

 

**下载你的设置方法为：打开vscode——按alt+shift+d  在弹出窗里输入你的gist值，等待片刻便同步成功。**

 

 

**如果要重置同步设置：按ctrl+p  输入  '>sync'**  

![img](https://images2015.cnblogs.com/blog/717286/201704/717286-20170425111823147-777456584.png)

 

  **就可以重新配置你的token来同步了**

 