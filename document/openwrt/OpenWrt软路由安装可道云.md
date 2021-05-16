# OpenWrt软路由安装可道云

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[无人区修炼者](https://blog.csdn.net/weixin_36662706) 2020-04-02 13:12:03 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10190 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

分类专栏： [技术](https://blog.csdn.net/weixin_36662706/category_7799081.html)

版权

前一阵买了个新3刷了OPenWrt固件，使用了一周体验了下真香。

### **什么是软路由？**

答：传统路由器只能进行简单的上网设置内存小不支持定制，但是软路由有大内存可以在里面安装各种各样的软件来进行自定义操作，不仅仅可以拥有传统路由器的上网功能也可以拥有，类似于在路由器里面装一个虚拟机比如Centos或者安装一个NAS以及各种黑科技的操作，所以我为啥不花一个传统路由器的钱来购买一个很舒服的软路由呢？

因为贫穷，我购买的新三1.2版本到手130

![微信图片_20200402120336.jpg](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9qcGVnLzEwMzExMjQvMTU4NTgwMDIyNTI3Ni00Y2Y4MWMzMy04YjJkLTRjNDktYmVlYy04YWU2ZWNlNjU5NzMuanBlZw?x-oss-process=image/format,png)

安装好是这个样子，买来插好线，接线步骤是和普通路由器一样的

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAwMzY3MzEyLTI4NGI3YzY0LTBlNTgtNGY0NS05OGRmLWI3YmFlZTZkNWEyNy5wbmc?x-oss-process=image/format,png)

### 路由器拨号设置

光猫连接的是WAN口其他设备要想链接只能链接LAN口，其实在软路由中我们可以把任意一个口定义成WAN口和LAN口，我这块没有做特殊的定义所以就用传统的WAN、LAN口进行设置。

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAwOTg5NjM3LWQxMzE1OGQ3LWQzZmMtNGNhOS05OTBkLWU5OWY4NzZmMTExOC5wbmc?x-oss-process=image/format,png)

我们在网络这设置拨号

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxMDQzNTQ5LWVlNWE1NzU5LTY0MzAtNDgwZS1hMTE0LTZlOGJmOWZmZGNjYy5wbmc?x-oss-process=image/format,png)

点击这进行修改

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxMDg1MTE3LTQ2MDBjOGI5LTU1YjMtNGJmZi04M2MyLTBiODE4NDAwZTQ1ZS5wbmc?x-oss-process=image/format,png)

设置协议为PPPoE然后点击切换协议

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxMTIwNDE4LTM1MjQyOWFlLTYwZDMtNDIyZS05NWIxLTRmYzM1ZGI1MjI0YS5wbmc?x-oss-process=image/format,png)

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxMTY1MTcwLWNlMjY5ODBiLTFhZjktNGFkYS05YjkzLTcxMTA5OWVmZjc1My5wbmc?x-oss-process=image/format,png)

输入你的用户名密码，然后点击保存应用就完成了你的网络的基础设定拨号完成，可以上网了。

### 插件

因为插件功能有很多所以这块就不一一讲解，选择了一个大家可能都会用到可道云插件进行讲解

openwrt搭建可道云

可道云：http://kodcloud.com/

1.我们去官网进行可道云软件的下载

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxMzk4Nzc3LWQyY2E3NDVjLTY5MmUtNGVhMi1hMzc5LTQ5Y2M4OTMzZjkzNi5wbmc?x-oss-process=image/format,png)

2.下载出来是一个压缩文件，我们新建一个文件夹名称为kodexplorer

3.把压缩文件解压到该文件夹中，后面会用到

4.解压完成后我们使用计算机链接到我们的软路由wifi中

5.使用FTP工具，我这里用的是xftp,把软路由当作一个服务器进行链接

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxNTg5OTI0LTVlNTE1OGI4LTI2YTctNDEwZi04MGNlLThhMjdkYjQwNzgzOS5wbmc?x-oss-process=image/format,png)

 

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxNjU3MzA1LWEzZmFhZjRkLWZhNjctNDJjYi05NTU4LWI2NmU5Y2IyNTBmZi5wbmc?x-oss-process=image/format,png)

链接完成后你需要把你的U盘插到软路由后面的USB当作一个服务器存储的盘

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxNzMwMjU2LWQxNzExZDAyLWQ4MDMtNDJjYS1iZTk3LWQxMDNmYzFiNGYxNC5wbmc?x-oss-process=image/format,png)

插入后他会自己建立目录，你可以在系统挂载点看到他建立目录路径

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxNzg1MTkxLTUxMTIwMmQxLTRiZDEtNGQxNi1iNzUxLWQ5MDA5YjFkMmZhMy5wbmc?x-oss-process=image/format,png)

6.进入目录后把你的解压内容上传到你的软路由挂载点位置中

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAxOTYzNzI0LTU5ZTRjZGRmLTZkYjYtNDA5Zi1iYTAzLTViMGYwNmU1NTI5Zi5wbmc?x-oss-process=image/format,png)

进入路由器设置界面 网络存储->可道云->设置好的你的挂载点目录以及你的，可道云程序存放路径，勾选启用，然后点击保存应用，因为他是一个私有云盘，你可设置最大上传文件大小我这里设置的是1G，还有访问端口号。

应用完成后我就可以通过：192.168.1.1:8080访问我的可道云私有网盘

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAyMC9wbmcvMTAzMTEyNC8xNTg1ODAyNDg4ODc1LTdhNmU3ZGMzLWMwZTYtNDNhZC05Mjk0LTM0ZDFlMGFkNjkwZC5wbmc?x-oss-process=image/format,png)

然后你就可以上传文件当作一个私有网盘使用，里面有内置播放器微信等功能用起来还算很舒服。

当然还有openWrt还有很多插件，比如一线多拨插件，可以让你网速跑满，比如广告屏蔽，多线多拨可以让多台计算机网速不受影响等，需要你自己去挖掘。