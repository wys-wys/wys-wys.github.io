# Telegram 图文详解--创建机器人 BOT

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[沙赞](https://blog.csdn.net/weixin_42776979) 2019-03-06 16:49:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 26006 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 8

分类专栏： [telegram](https://blog.csdn.net/weixin_42776979/category_8728852.html) 文章标签： [telegram](https://www.csdn.net/gather_25/MtjaUg3sMTI3MDctYmxvZwO0O0OO0O0O.html) [bot](https://so.csdn.net/so/search/s.do?q=bot&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

今天看到一个电报群里说 利用BOT来签到，很好奇就想学学，来吧 ！

创建一个BOT！！！

1、先搜索BotFather 

我这里搜索到好几个没有一个可用的，输入/help 返回俄文错误信息。

后来在官网找到了 https://telegram.me/BotFather 直接点击不用搜索，靠谱，管用。

![img](https://img-blog.csdnimg.cn/2019030615521413.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

用带官网小图标的靠谱

![img](https://img-blog.csdnimg.cn/20190306155954934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

2、使用 newbot创建

使用newbot 创建，然后提示名称后面加入Bot或者_bot
如果回复 sorry 说明 没有创建成功，否则ok！
最常见的是名称已存在！

 

![img](https://img-blog.csdnimg.cn/20190306155816644.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/2019030616030495.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

TOKEN 一定要保护好！以后接口访问都要用到！

3、使用mybots查看你自己的机器人，我这里就一个。

![img](https://img-blog.csdnimg.cn/20190306160436202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

4、点机按钮，先后有设置选项

![img](https://img-blog.csdnimg.cn/20190306160617839.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

5、API Token 可以从新生成 token和查看token

![img](https://img-blog.csdnimg.cn/20190306160735249.png)

6、 Edit Bot 可以编辑 名称、描述、关于、图片（头像）、命令

名称：不说了，不重复随便改。

描述：这个描述是聊天的时候，在头部显示的。

![img](https://img-blog.csdnimg.cn/20190306161030564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

关于：在个人信息页面显示，发送分享链接的时候显示。

图片：直接复制，或者拖进来，那个附件图标点击都可以！！

![img](https://img-blog.csdnimg.cn/20190306161419586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

 

添加命令：格式 xxx-xxxxx 前命令-后描述。 这个命令因为没有代码，所以没有响应，以后详解。

![img](https://img-blog.csdnimg.cn/20190306161819491.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20190306162114177.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3Njk3OQ==,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20190306162447308.png)

7、Bot settings 设置-- 这组默认就行 

![img](https://img-blog.csdnimg.cn/20190306162621268.png)

inline Mode 内联模式 默认是关闭，启用以后就可以在任何聊天区域 跟机器人互动。

详见 https://core.telegram.org/bots/inline

Allow Groups 允许添加到组 默认是开启的，没啥可说的。

Group Privacy 组策略，默认是开启的， 这样机器人不需要接受所有人发的消息，不需要回复所有人发的消息，只需要/开头的。

可以配合 设置机器人为管理员来实现。

Payments 关于支付，没搞过不多说。

Domain 域名空间，用默认就行，想研究的 https://core.telegram.org/widgets/login

8、Delete Bot 和 Payments 不做介绍了。

 

注：创建一个机器人，7步 8 步可以用默认。 

最主要的是命令的响应，命令要想有响应就需要有服务支持。一般使用谷歌js开发服务，创建脚本服务，返回需要的内容，还可以使用数据库等。另外，还可以用java等语言编写。以后慢慢介绍。