# python自带IDEL简单操作

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[放心去fly](https://me.csdn.net/iorijjw) 2013-05-02 15:31:15 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 2713 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

Python编辑器IDLE傻瓜入门

 

下载python进行安装，默认自带此工具
开始->程序->Python 2.*/3.*-> IDLE (Python GUI)
如此就打开了Python Shell->File->New window(Ctrl+N)
就出现了python编辑器
编写代码比如

Java代码  [![收藏代码](http://www.iteye.com/images/icon_star.png)](http://www.iteye.com/topic/603535)

1. print('Hello World') 

然后保存文件为helloworld.py(注意记得加py扩展名，默认是不会自动加添的)。
在编辑器窗口按F5即可在Python Shell中看到结果。

如何debug
1.设置断点：在Python编辑器中要调试的代码行右击->Set Breakpoint，之后该行底色就变黄了
2.打开debugger：Python Shell->Debug->Debugger
3.编辑窗口按F5
4.debug过程略

- Go表示运行完相当于eclipse的F8，不过按F5后先要Go一下才能往下走，默认是不运行的
- Step表示一步一步相当于eclipse的F5
- Over表示跳过函数方法相当于eclipse的F6
- Out表示跳出本函数相当于eclipse的F7


IDLE编辑器快捷键
自动补全代码     Alt+/（查找编辑器内已经写过的代码来补全)
补全提示        Ctrl+Shift+space(默认与输入法冲突，修改之)
(方法：Options->configure IDLE…->Keys-> force-open-completions
提示的时候只要按空格就出来对于的，否则翻上下键不需要按其他键自动就补全了)

后退           Ctrl+Z

重做           Ctrl+Shift+Z
加缩进         Ctrl+]
减缩进         Ctrl+[
加注释         Alt+3
去注释         Alt+4

Python Shell快捷键

自动补全同上     tab
**上一条命令      Alt+P
下一条命令      Alt+N**