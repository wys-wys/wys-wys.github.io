# Windows10设置某一个程序单独不弹出UAC的方法听语音

- 原创
- |
- 浏览：6626
- |
- 更新：2017-04-20 10:41
- |
- 标签：[操作系统](https://jingyan.baidu.com/tag?tagName=操作系统) [WINDOWS](https://jingyan.baidu.com/tag?tagName=WINDOWS) 

- [![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/560be432939c2cf7f55a84ac452c5b1b1fde127d.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/03b2f78c0de7ee5ea337ae5e.html?picindex=1)1
- [![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/6834ecc4ec9959433ce9104b95425d6b05d1047d.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/03b2f78c0de7ee5ea337ae5e.html?picindex=2)2
- [![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/edafb3bcbe2f477003f0876f6f3b3b860321797d.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/03b2f78c0de7ee5ea337ae5e.html?picindex=3)3
- [![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/65ba880b31210561564b0d5c08aee8d7582a6a7d.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/03b2f78c0de7ee5ea337ae5e.html?picindex=4)4
- [![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/1570c1b6326c5766c4275ae6a4632385e136617d.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/03b2f78c0de7ee5ea337ae5e.html?picindex=5)5

[分步阅读](http://jingyan.baidu.com/album/03b2f78c0de7ee5ea337ae5e.html)

UAC（用户账户控制）在加强了我们使用电脑安全的同时也带了一些不便，在不关闭uac的情况下有些程序我们并不需要弹出uac对话框，但是Windows并没有提供设置单独取消uac，下面我们通过修改注册表可以在不关闭uac情况下单独取消一个程序的uac对话框：

## 方法/步骤

1. 

   打开Cortana，输入regedit，打开注册表编辑器

   ![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/560be432939c2cf7f55a84ac452c5b1b1fde127d.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

2. 

   找到 HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers（windows10创意版1703可以直接在注册表地址栏粘贴导航至该位置）

   ![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/6834ecc4ec9959433ce9104b95425d6b05d1047d.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

3. 

   在右侧空白处右键新建→字符串值；重命名为所要去掉uac对话框程序的路径（如：C:\Drcom\DrUpdateClient\DrMain.exe）

   ![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/edafb3bcbe2f477003f0876f6f3b3b860321797d.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

4. 

   双击打开，将数值数据设为：RunAsInvoker，确定。

   ![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/65ba880b31210561564b0d5c08aee8d7582a6a7d.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

5. 

   到这里全部设置就完了，桌面对应程序的快捷方式也没有盾牌了，以后打开该程序也不会再有uac提示了，如果要恢复，删除刚才新建的注册表即可。

   ![Windows10设置某一个程序单独不弹出UAC的方法](https://exp-picture.cdn.bcebos.com/1570c1b6326c5766c4275ae6a4632385e136617d.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

   END

## 注意事项

- 理论上Windows7，Windows8同样适用，另外建议大家在修改之前备份注册表

经验内容仅供参考，如果您需解决具体问题(尤其法律、医学等领域)，建议您详细咨询相关领域专业人士。

*作者声明：*本篇经验系本人依照真实经历原创，未经许可，谢绝转载。