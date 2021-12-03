# 服务器开启强制HTTPS访问后提示重定向次数过多

- 博主： [站在风中的胖子](https://www.bu7.com/author/1/)
-  

- 发布时间：2019 年 07 月 10 日
-  

- 3231次浏览
-  

- [1 条评论](https://www.bu7.com/archives/13/#comments)
-  

- 588字数
-  

- 分类： [Linux](https://www.bu7.com/category/linux/)

1. [首页](https://www.bu7.com/)
2. 正文 
3. 分享到： 

博客到今天搭建了有十来天了，突然想起来还没开HTTPS访问，于是乎打开宝塔面板一键申请了Let's Encrypt证书，并愉快的开启强制HTTPS访问

[![强制HTTPS.PNG](https://bu7.com/usr/uploads/2019/07/1149162071.png)](https://bu7.com/usr/uploads/2019/07/1149162071.png)

[强制HTTPS.PNG](https://bu7.com/usr/uploads/2019/07/1149162071.png)



但是问题来了，访问提示重定向次数过多。经过没日没夜的检查，发现是因为用了cloudflare，里面的SSL模式要改!

[![域名管理.png](https://bu7.com/usr/uploads/2019/07/2193130408.png)](https://bu7.com/usr/uploads/2019/07/2193130408.png)

[域名管理.png](https://bu7.com/usr/uploads/2019/07/2193130408.png)



[![改为Full.png](https://bu7.com/usr/uploads/2019/07/2420610211.png)](https://bu7.com/usr/uploads/2019/07/2420610211.png)

[改为Full.png](https://bu7.com/usr/uploads/2019/07/2420610211.png)



这里说一下，如果你开了cloudflare的CDN，是有两种方式开启强制HTTPS的，第一种就是上面的方式

第二种呢就是直接在cloudflare里面开启强制HTTPS

[![改为ON.png](https://bu7.com/usr/uploads/2019/07/2540696115.png)](https://bu7.com/usr/uploads/2019/07/2540696115.png)

[改为ON.png](https://bu7.com/usr/uploads/2019/07/2540696115.png)



使用这种方法就不用像上面一样把SSL模式改为FULL，直接用默认的Flexible

 最后修改：2019 年 07 月 10 日 09 : 43 PM

© 允许规范转载

 赞赏

如果觉得我的文章对你有用，请随意赞赏

[下一篇](https://www.bu7.com/archives/8/)[上一篇](https://www.bu7.com/archives/14/)

#### 1 条评论

1. ![img](https://secure.gravatar.com/avatar/7129bd1bafc3daef6fed744fd06cc594?s=65&r=G&d=)

   **Mr.H**

   July 9th, 2020 at 03:51 pm

   感谢，这个问题已经困扰我很久了

   [回复](https://www.bu7.com/archives/13/?replyTo=2#respond-post-13)



#### 发表评论 

评论 *