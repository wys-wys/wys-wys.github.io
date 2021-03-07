 Bat批处理脚本是一种简化的脚本语言。本文中编写了两个小脚本，其实就是两行命令，一个是开机结束某定位程序进程的，一个用于定时让电脑睡眠避免熬夜。当然，这两个脚本还要配合系统任务计划程序才能实现条件触发后自动执行。那么，怎么隐藏bat批处理文件执行时的命令窗口，静默运行呢？或可参考如下经验。

## 工具/原料

- Win10为例；Bat批处理文件；计算机任务计划程序；屏幕键盘；记事本；Vbs文件。

## 步骤

1. 

   以下图让电脑立刻进入睡眠的脚本为例，演示如何静默执行该脚本；

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/51cd85cec7f88a770a284dff6e4a2f27e6eff848.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

2. 

   首先，“win+r”组合键打开“运行”窗口，输入“osk”可打开屏幕键盘，题外话；

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/e6ae36066b0192dd6cb573401a87031c98c0f048.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

3. 

   在运行窗口中输入“notepad”回车，可以快速打开记事本程序；

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/025d87c0affce18642da6dc11f1fbee435daeb48.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

4. 

   然后，如图在记事本中粘贴或输入“createobject("wscript.shell").run "C:\Users\chaoy\Desktop\SleepPc.bat",0”，其中的 "C:\Users\chaoy\Desktop\SleepPc.bat"更换为自己的脚本所在绝对路径及文件名；

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/4b626771fe1d96d868eca4932ccd0c6efaf2e148.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

5. 

   接着，将文件另存为自定义名称的“.vbs”后缀文件即可，如图；

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/0d2fe5f202b375d7ee8e7e47515872dadf49d848.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

6. 

   保存后可选中该文件，右键“编辑”以查看是否有错误，检查无误后关闭；

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/df087f0f8b56ad04519dd25adae10ef85956d048.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

7. 

   这样，再要执行原来的批处理文件时，只需运行这个vbs文件。当然，如果用到任务计划程序，也要相应地改为运行该vbs文件，即可实现静默执行原bat批处理文件的目的。

   ![bat批处理文件怎么隐藏无窗口静默运行执行](https://exp-picture.cdn.bcebos.com/0fb94656d53da8245e1c0961306651598440cb48.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

   END

## 注意事项

- 让bat批处理文件隐藏无窗口静默运行，如有更好的经验，欢迎不吝投票评论分享。