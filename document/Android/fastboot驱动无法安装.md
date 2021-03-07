# Win10无法安装HiKey970 fastboot驱动的解决方法

[![img](https://cdn2.jianshu.io/assets/default_avatar/15-a7ac401939dd4df837e3bbf82abaa2a8.jpg)](https://www.jianshu.com/u/afeec72890ee)

[随随便便不随便](https://www.jianshu.com/u/afeec72890ee)关注

2019.07.26 20:17:29字数 330阅读 815

HiKey970开发板进入fastboot后，Win10的设备管理器能识别到HiKey970的设备，但无法匹配到驱动。通过设备管理器查看设备可以看到“设备不需要也未加载驱动程序文件”的信息。执行fastboot devices查看不到设备。解决方法如下：

1.下载Google的最新usb驱动



```ruby
 http://smartfire.cn/thread-780-1-1.html
 https://dl-ssl.google.com/android/repository/latest_usb_driver_windows.zip?hl=zh-cn
```

2.解压下载的文件，找到android_winusb.inf，在[Google.NTamd64]后面加上以下内容：



```undefined
;HiKey970
%SingleBootLoaderInterface% = USB_Install, USB\VID_18D1&PID_D00D
%SingleAdbInterface% = USB_Install, USB\VID_18D1&PID_D00D&REV_0100
```

如果电脑是32位的，上述内容加在[Google.NTx86]后面。

3.在设备管理器中安装上述驱动，如果安装不成功，提示找到设备驱动，但“文件的哈希值不在指定的目录文件中。此文件可能已损坏或者被篡改。”此时执行下一步，禁用驱动程序强制签名。

4.在Win10中进入"设置"->"更新和安全"->"恢复"->"立即重新启动"->"疑难解答"->"高级选项"->"启动设置"->"重启"，然后电脑重启，在重启时选择"禁用驱动程序强制签名"，启动到Windows后，继续安装驱动。

5.安装完成后，在cmd中执行fastboot devices检查是否正常。