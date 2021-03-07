

Docker 服务端私有部署 - 收藏服务设置说明

2019/10/16

为知笔记 Docker 服务端新增网页收藏能力，支持将微信公众号文章和微博收藏，网页剪辑器，以及转发邮件保存。

### 如何将外网内容保存至私有部署服务

用户在为知笔记官方服务上，通过绑定微信、微博，转发保存文章，或网页剪辑器中保存的内容，通过接下来步骤中设置的服务地址，被自动保存至私有部署服务对应的账号中。

> - 收藏的内容在官方服务账号与私有服务账号中均会保存

### 收藏服务地址设置

1. 登录私有部署个人账号，在设置 - 私有服务中，复制地址 ![img](https://cdn2.wiz.cn/wp-content/new-uploads/75e65590-effb-11e9-ae73-4770c178a8b4.png)

```
如果文本框为空，请联系管理员购买许可后开通收藏服务
```

1. 登录为知笔记官方服务账号，在设置 - 私有服务中，粘贴第 1 步获取的地址，点击保存 ![img](https://cdn2.wiz.cn/wp-content/new-uploads/8662ea50-effb-11e9-ae73-4770c178a8b4.png)

完成以上步骤后，即可通过公有云官方服务，使用微信、微博收藏，网页剪辑器，以及邮件转发保存功能。具体方法：

- [保存微信到为知笔记](https://www.wiz.cn/wiz-wechat.html)
- [保存微博到为知笔记](https://www.wiz.cn/zh-cn/ios-weibo-collection.html)
- [保存网页内容到为知笔记](https://www.wiz.cn/zh-cn/downloads-webclipper.html)
- [保存邮件到为知笔记](https://www.wiz.cn/zh-cn/wiz-mywiz.html)

### 管理后台设置

```
该步骤为管理员在服务后台操作设置
```

登录 Docker 服务端管理后台，设置服务端地址 添加私有部署服务外网地址后，点击更新。注意该地址需要能够被为知笔记在线服务访问。如果私有部署的地址变更，需要管理员通知所有用户重新执行绑定公有云账号的操作。 ![img](https://cdn2.wiz.cn/wp-content/new-uploads/646aee70-effb-11e9-ae73-4770c178a8b4.png)

## 获取 Docker 服务端

[为知笔记服务端docker镜像使用说明](https://www.wiz.cn/docker)