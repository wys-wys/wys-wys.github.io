# [Windows下使用命令实现类似awk命令](https://www.cnblogs.com/minseo/p/13497623.html)

　　Windows默认没有awk命令，下面通过for在windows下实现类似awk功能

　　例如需要获取ftp或者http下文件列表

　　完整的获取命令如下

```
C:\Users\liuym>curl ftp:``//172.16.90.13/``[0x7FFC8CEDD370] ANOMALY: meaningless REX prefix used``-rw-r--r--  1 0    0    50070974 May 29 03:12 magic-box-20200529.zip``-rw-r--r--  1 0    0    43617957 Jun 30 07:32 magic-box-20200630.zip``-rw-r--r--  1 0    0    43617817 Jul 03 06:59 magic-box-20200703.zip``-rw-r--r--  1 0    0    43634705 Jul 06 08:21 magic-box-20200706.zip
```

 　需要获取文件列表

```
for` `/f ``"skip=1 tokens=9 delims= "` `%a ``in` `(``'curl ftp://172.16.90.13/'``) ``do` `@echo %a
```

 　命令解析

```
for` `/f ``"skip=1 tokens=9 delims= "` `%a ``in` `(``'curl ftp://172.16.90.13/'``) ``do` `@echo %a``skip=1 #忽略第一行，默认显示所有行``tokens=9 #显示第9列 类似于awk的 参数$9``delims= #分隔符 本次分隔符为一个空格``curl ftp:``//172.16.90.13/ #循环该命令所有行
```

 　输出如下

```
C:\Users\liuym>``for` `/f ``"skip=1 tokens=9 delims= "` `%a ``in` `(``'curl ftp://172.16.90.13/'``) ``do` `@echo %a`` ``% Total  % Received % Xferd Average Speed  Time  Time   Time Current``                 ``Dload Upload  Total  Spent  Left Speed``100  320  0  320  0   0  320   0 --:--:-- --:--:-- --:--:-- 5161``magic-box-20200630.zip``magic-box-20200703.zip``magic-box-20200706.zip
```

 

分类: [Windows](https://www.cnblogs.com/minseo/category/1218325.html)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/sample_face.gif)](https://home.cnblogs.com/u/minseo/)

[minseo](https://home.cnblogs.com/u/minseo/)
[关注 - 10](https://home.cnblogs.com/u/minseo/followees/)
[粉丝 - 57](https://home.cnblogs.com/u/minseo/followers/)

[+加关注](javascript:void(0);)

1

0

[« ](https://www.cnblogs.com/minseo/p/13451439.html)上一篇： [Ceph对象网关快速入门](https://www.cnblogs.com/minseo/p/13451439.html)
[» ](https://www.cnblogs.com/minseo/p/13516359.html)下一篇： [Ubuntu时间比正常时间多8小时，设置重启以后时间又多8小时解决办法](https://www.cnblogs.com/minseo/p/13516359.html)