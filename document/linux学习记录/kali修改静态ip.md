# 如何给给kali linux配置静态IP地址？听语音

- 原创
- |
- 浏览：26071
- |
- 更新：2019-05-07 13:37

- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/3201a8f39187031c766f96496a86242fa972ec04.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=1)1
- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/6061b9cd0c6efbf203034c62127bbbf4db58da04.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=2)2
- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/50a010f85856d53db994e15c47d2bb665059ca04.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=3)3
- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/ed792abb19efa25f2ea4fbce59828689a0463b05.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=4)4
- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/3d002dbad341037dd187f0c3a9bc7dc5ce672d05.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=5)5
- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/b442d6d246fe474efc330a0ab0ef354f51b81f05.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=6)6
- [![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/fb738d9c2cf7dfb296a9f799d01b1edef5dc1305.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1)](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html?picindex=7)7

[分步阅读](http://jingyan.baidu.com/album/14bd256eb6ac84bb6d261294.html)

这篇经验来介绍一下怎么给kali linux配置静态IP地址。

## 工具/原料

- kali

## 方法/步骤

1. 

   打开kali的终端。

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/3201a8f39187031c766f96496a86242fa972ec04.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

2. 

   进入root用户。

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/6061b9cd0c6efbf203034c62127bbbf4db58da04.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

3. 

   打开网卡的配置文件，路径是/etc/network/interfaces。

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/50a010f85856d53db994e15c47d2bb665059ca04.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

4. 

   对网卡做出如下配置。

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/ed792abb19efa25f2ea4fbce59828689a0463b05.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

5. 

   配置DNS相关信息。

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/3d002dbad341037dd187f0c3a9bc7dc5ce672d05.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/b442d6d246fe474efc330a0ab0ef354f51b81f05.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

6. 6

   最后一定要重启网卡。

   ![如何给给kali linux配置静态IP地址？](https://exp-picture.cdn.bcebos.com/fb738d9c2cf7dfb296a9f799d01b1edef5dc1305.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1)

   