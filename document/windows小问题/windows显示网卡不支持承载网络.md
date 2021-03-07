更换旧版无线网卡

![image-20201222154901752](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20201222154901752.png)

![image-20201222154921209](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20201222154921209.png)

netsh wlan show driver

netsh wlan set hostednetwork mode=allow ssid=wys-wys key=wys123456789..

netsh wlan start hostednetwork

开热点连接密码错误，更换驱动

# 网卡不支持承载网络（无法启动wifi热点）--解决办法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[iteye_12373](https://blog.csdn.net/iteye_12373) 2016-03-08 15:38:14 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 12802 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 4

分类专栏： [杂谈](https://blog.csdn.net/iteye_12373/category_8046969.html) 文章标签： [c/c++](https://so.csdn.net/so/search/s.do?q=c/c++&t=blog&o=vip&s=&l=&f=&viparticle=) [操作系统](https://www.csdn.net/tags/MtTacg0sNTgzNi1ibG9n.html)

版权

试过网上很多方法：

[b]更新网卡驱动；[/b]

[b]微软的Intel my wifi；[/b]
参见[url]http://support1.lenovo.com.cn/lenovo/wsi/htmls/detail_12608722252655160.html[/url]

[b]启动【Microsoft 托管网络虚拟适配器】；[/b]
参见[url]http://support1.lenovo.com.cn/lenovo/wsi/htmls/detail_20150914120000377.html[/url]

[b]netsh wlan set hostednetwork mode=allow ssid=livdran2012 key=10010010；[/b]
参见[url]http://www.udaxia.com/wtjd/3592.html[/url]

这几种方案均无法均无法解决。

这种方案试试看，我的网卡驱动是Wireless-N 7265

如果你的网卡支持承载网络，就试试以上的方法。

管理员运行“命令提示符”，输入“netsh wlan show drivers”

[img]http://dl2.iteye.com/upload/attachment/0115/6207/976bb35e-ffa5-38b9-a706-d4c48ac22561.png[/img]
如上图，不支持

接着我们打开设备管理器，右击“此电脑”，选“属性”，左侧点击“设备管理器”，展开“网络适配器”树形菜单，找到显卡驱动，一般名字里面带Wireless、bgn、/b/g/g、802.11、无线 这些关键字的就是无线网卡

[img]http://dl2.iteye.com/upload/attachment/0115/6209/f7d39954-cb3c-3e97-ba51-09eeee07d990.png[/img]
右键，选择“更新驱动程序软件”

[img]http://dl2.iteye.com/upload/attachment/0115/6214/cb2ad27c-51aa-33e7-90fa-5fa00c319681.png[/img]

选择“浏览计算机以查找驱动程序软件”

[img]http://dl2.iteye.com/upload/attachment/0115/6216/86c734ff-924c-38f5-8c48-f75aac6284de.png[/img]
点击 从列表中选取

[img]http://dl2.iteye.com/upload/attachment/0115/6218/3e2cfd4d-cb62-3e24-b732-17a432ec2d1c.png[/img]
选择一个较老版本的驱动，点“下一步”进行安装

安装成功后，重新启动以管理员身份运行的“命令提示符”，记住，必须重启

[img]http://dl2.iteye.com/upload/attachment/0115/6220/327d8dca-15a8-3d76-9108-47769f6f780d.png[/img]

成功！重新启动计算机再尝试常规的wifi共享软件都可以了。

如果不成功，再次选择其他驱动进行安装来尝试。

如果都不行，那应该就是你的硬件不支持了，和售后服务联系看看是否支持承载网络。

祝君成功！