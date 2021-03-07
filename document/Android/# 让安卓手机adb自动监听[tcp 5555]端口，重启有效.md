# # 让安卓手机adb自动监听[tcp 5555]端口，重启有效（好像没有什么暖用）

[![img](https://upload.jianshu.io/users/upload_avatars/5704150/2c3a9135-d9d2-46cd-ac1f-52334dad7ac6.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/39e3c7800113)

[meStronger](https://www.jianshu.com/u/39e3c7800113)关注

2019.12.07 11:40:14字数 82阅读 1,924

# 让安卓手机adb自动监听[tcp 5555]端口，重启有效

### 1.Root 手机

### 2.用ADB命令解锁system



```shell
# adb root
# adb disable-verity
```

### 3.修改 `/default.prop` 或 `/system/build.prop`文件.



```shell
//添加这一行
service.adb.tcp.port=5555
```

## 4.保存文件时提示：Read-only file system.



```shell
//设置可读写权限
# mount -o rw,remount /system

//恢复只可读
# mount -o ro,remount /system
```

重启手机后仍然有效，提升效率，多留点时间陪陪女朋友吧

# [Android使用adb命令直接修改文件](https://my.oschina.net/lwaif/blog/1570939)

[Domineering](https://my.oschina.net/lwaif)

[工作日志](https://my.oschina.net/lwaif?tab=newest&catalogId=324824)

2017/11/10 11:48

阅读数 1.9W

|      |      |
| ---- | ---- |
|      |      |

以修改hosts文件为例:

由于某些原因，可能需要指定域名对应的IP地址。Android是基于Linux的系统，与Linux类似，通过hosts文件来设置。

在Android下，/etc是link到/system/etc的，我们需要修改/system/etc/hosts来实现。但是这个文件是只读，不能通过shell直接修改。可以通过连接到PC上使用adb来修改。步骤如下：

1、获得root权限：adb root

2、设置/system为可读写：adb remount

3、将hosts文件复制到PC：adb pull /system/etc/hosts <PC机上文件名>

4、修改PC机上文件

5、将PC机上文件复制到手机：adb push <PC机上文件名> /system/etc/hosts

如果要查看是否修改成功，可以在PC上执行adb shell，运行cat /system/etc/hosts；或者在手机上运行cat /system/etc/hosts。

本文转载自网络

举报