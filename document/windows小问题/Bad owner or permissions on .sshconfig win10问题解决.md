# Bad owner or permissions on .ssh/config win10问题解决

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[ai74583](https://blog.csdn.net/ai74583) 2019-07-15 11:19:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1873 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

文章标签： [运维](https://www.csdn.net/tags/MtTaEg0sMDQyNTMtYmxvZwO0O0OO0O0O.html)

版权

[![img](https://img-operation.csdnimg.cn/csdn/silkroad/img/1625730421900.png)40+行业专场、100+科技成果、300+大咖云集，相约2021 腾讯数字生态大会描绘云、AI、大数据、安全等关键技术的发展蓝图，展示腾讯最新的研究成果、战略规划、技术产品、解决方案！直播通道已开启，马上预约！](https://qdrl.qq.com/J6Ta0CG2)

最近向系统添加了新用户账号后出现了问题，尝试使用私钥登陆服务器，提示了 Bad owner or permissions on .ssh/config 这个报错，就是如题中的问题

![1106918-20190715102859616-1893463244.png](https://img2018.cnblogs.com/blog/1106918/201907/1106918-20190715102859616-1893463244.png)

## 修复

按照Windows 10 GUI中的这些步骤解决权限问题：

1. 找到.ssh文件夹。它通常位于C:\Users，例如C:\Users\Akkuman。
2. 右键单击.ssh文件夹，然后单击“属性”。
3. 找到并点击“安全”标签。
4. 然后单击“高级”。
5. 单击“禁用继承”，单击“确定”。
6. 将出现警告弹出窗口。单击“从此对象中删除所有继承的权限”。
7. 你会注意到所有用户都将被删除。让我们添加所有者。在同一窗口中，单击“编辑”按钮。
8. 接下来，单击“添加”以显示“选择用户或组”窗口。
9. 单击“高级”，然后单击“立即查找”按钮。应显示用户结果列表。
10. 选择您的用户帐户。

![1106918-20190715111754215-1650541499.png](https://img2018.cnblogs.com/blog/1106918/201907/1106918-20190715111754215-1650541499.png)

1. 然后单击“确定”（大约三次）以关闭所有窗口。

完成所有操作后，再次关闭并打开cmder应用程序并尝试连接到远程SSH主机。

现在这个问题应该解决了。

转载于:https://www.cnblogs.com/Akkuman/p/11187776.html

相关资源：[Linux*SSH*工具_linux*ssh*下载,*ssh**.*exe-FTP文档类资源](https://download.csdn.net/download/itnow/1603665?spm=1001.2101.3001.5697)