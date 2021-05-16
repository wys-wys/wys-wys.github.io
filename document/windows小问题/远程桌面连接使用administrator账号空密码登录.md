# 远程桌面连接使用administrator账号空密码登录听语音

- 原创
- |
- 浏览：17677
- |
- 更新：2016-02-27 11:44
- |
- 标签：[桌面](https://jingyan.baidu.com/tag?tagName=桌面) [WINDOWS](https://jingyan.baidu.com/tag?tagName=WINDOWS) [远程](https://jingyan.baidu.com/tag?tagName=远程) [连接](https://jingyan.baidu.com/tag?tagName=连接) [账号](https://jingyan.baidu.com/tag?tagName=账号) 

- [![远程桌面连接使用administrator账号空密码登录](https://exp-picture.cdn.bcebos.com/efb861bd4c7c34b32c3d660f5841037de03731d1.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a1a16631d91192c4c.html?picindex=1)1
- [![远程桌面连接使用administrator账号空密码登录](https://exp-picture.cdn.bcebos.com/e076d77622bc7dc5d71b7eea5e460596b91429d1.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a1a16631d91192c4c.html?picindex=2)2
- [![远程桌面连接使用administrator账号空密码登录](https://exp-picture.cdn.bcebos.com/c99358fe474ec28310c36e5abe4f50b8b53e1cd1.jpg?x-bce-process=image%2Fresize%2Cm_fill%2Cw_92%2Ch_69%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)](http://jingyan.baidu.com/album/380abd0a1a16631d91192c4c.html?picindex=3)3

[分步阅读](http://jingyan.baidu.com/album/380abd0a1a16631d91192c4c.html)

一般情况下远程桌面是不允许administrator账号空密码登录，会弹窗提示：由于账户限制无法登陆

## 方法/步骤

1. 

   首先确保远程计算机的远程桌面功能是打开的如下：

   ![远程桌面连接使用administrator账号空密码登录](https://exp-picture.cdn.bcebos.com/efb861bd4c7c34b32c3d660f5841037de03731d1.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

2. 

   修改windows的安全策略，允许远程桌面连接使用空密码  在远程计算机上启动“组策略编辑器”（开始-运行-GPEDIT.MSC），在“WINDOWS设置-安全设置-本地策略-安全选项”中找到“使用空白密码的本地帐户只允许进行控制台登录”，将其设置为“已停用”。这样就可以使用administrator账号、空密码进行远程桌面连接了。

   ![远程桌面连接使用administrator账号空密码登录](https://exp-picture.cdn.bcebos.com/e076d77622bc7dc5d71b7eea5e460596b91429d1.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   ![远程桌面连接使用administrator账号空密码登录](https://exp-picture.cdn.bcebos.com/c99358fe474ec28310c36e5abe4f50b8b53e1cd1.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   END

经验内容仅供参考，如果您需解决具体问题(尤其法律、医学等领域)，建议您详细咨询相关领域