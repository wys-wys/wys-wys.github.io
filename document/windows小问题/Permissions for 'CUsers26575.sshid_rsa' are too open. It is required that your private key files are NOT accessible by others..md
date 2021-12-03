Permissions for 'C:\\Users\\26575\\.ssh\\id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "C:\\Users\\26575\\.ssh\\id_rsa": bad permissions

解决windows10中ssh（OpenSSH_for_Windows）远程登录时报Permissions for "xxx" are too open错误

肖豪拉奥达 2020-04-10 15:17:40  3606  收藏 3
版权
ssh -i.\x.pem root@键式
@
警告：未保护的私人钥匙文件！
@@@@@pem的
权限太开放了。
需要其他人访问您的私人密钥文件。
此私钥将被忽略。
加载密钥
"。\xxx.pem"：root@权限差：拒绝权限（公共键、格萨皮键、格萨皮与麦克风）。

解决：

xxx.pem文件->属性->安全->高级->所有者改成当前操作用户->权限条目删除所有并添加当前操作用户

参考：

https://www.jianshu.com/p/629bf7a09a3d

https://www.jianshu.com/p/0bd91d523750


————————————————
版权声明：本文为CSDN博主「xiaohaolaoda」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/xiaohaolaoda/article/details/105434315