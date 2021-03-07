# Centos下安装mysql时出现Delta RPMs disabled because /usr/bin/applydeltarpm not installed解决办法

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[WaldeinCheng](https://blog.csdn.net/qq_34691713) 2018-11-09 12:01:01 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 32717 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 19

分类专栏： [Bugs](https://blog.csdn.net/qq_34691713/category_8974894.html) 文章标签： [Centos](https://www.csdn.net/tags/MtTaEg0sMzk5NjctYmxvZwO0O0OO0O0O.html) [Mysql](https://www.csdn.net/tags/MtTaEg5sOTYwNC1ibG9n.html)

版权

**不得不说，如果网络环境没有搭建好的话，在Centos上安装mysql真的是挺复杂的，中间有很多问题出现，大部分都是网络的问题。今天在安装Centos上安装mysql的时候，出现**

```
Delta RPMs disabled because /usr/bin/applydeltarpm not installed
1
```

之后就安装net-tools失败导致安装mysql失败
字面翻译就是deltarpm没有安装，接下来我们安装就是了
执行两条命令

```
yum provides '*/applydeltarpm'    #查看依赖包的位置
yum -y  install deltarpm             #安装命令
12
```

之后完美解决，成功安装mysql.

[原创](https://blog.51cto.com/m51cto?s=4)

# /usr/bin/applydeltarpm not installed问题解决

[![img](https://s2.51cto.com//wyfs02/M02/03/D0/wKiom1mg7MWiVqavAAAhhto7X3g273_middle.jpg)](https://blog.51cto.com/m51cto)

[喵来个鱼](https://blog.51cto.com/m51cto)关注0人评论[27956人阅读](javascript:;)[2018-11-18 23:19:30](javascript:;)

#### yum update遇到问题：

```
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
```

#### 解决办法

此问题安装Deltarpm包（增量 RPM 套件）即可解决，当然您也可以先使用一下命令，查看是哪个包提供applydeltarpm

```
yum provides '*/applydeltarpm'  
yum install deltarpm -y
yum provides '*/applydeltarpm'
Loaded plugins: axelget, fastestmirror
No metadata available for base
No metadata available for epel
No metadata available for extras
No metadata available for updates
Loading mirror speeds from cached hostfile
 * epel: mirrors.aliyun.com
base/7/x86_64/filelists_db                                                  | 6.9 MB  00:00:00     
epel/x86_64/filelists                                                       |  10 MB  00:00:00     
extras/7/x86_64/filelists_db                                                | 603 kB  00:00:00     
updates/7/x86_64/filelists_db                                               | 3.4 MB  00:00:00     
deltarpm-3.6-3.el7.x86_64 : Create deltas between rpms
Repo        : base
Matched from:
Filename    : /usr/bin/applydeltarpm
```

然后安装deltarpm

```
# yum install deltarpm -y

...
Installed size: 209 k
Downloading packages:
deltarpm-3.6-3.el7.x86_64.rpm                                               |  82 kB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : deltarpm-3.6-3.el7.x86_64                                                       1/1 
  Verifying  : deltarpm-3.6-3.el7.x86_64                                                       1/1 

Installed:
  deltarpm.x86_64 0:3.6-3.el7                                                                      

Complete!
```

继续yum updagate即可

©著作权归作者所有：来自51CTO博客作者喵来个鱼的原创作品，如需转载，请注明出处，否则将追究法律责任

[yum](https://blog.51cto.com/search/result?q=yum)[applydeltarpm](https://blog.51cto.com/search/result?q=applydeltarpm)[系统](https://blog.51cto.com/m51cto/category1.html)

2

分享

收藏

[上一篇：pip升级常见故障解决心得](https://blog.51cto.com/m51cto/2162793)[下一篇：centos7停止无效源](https://blog.51cto.com/m51cto/2318595)

[![img](https://s2.51cto.com//wyfs02/M02/03/D0/wKiom1mg7MWiVqavAAAhhto7X3g273_middle.jpg)](https://blog.51cto.com/m51cto)

[喵来个鱼](https://blog.51cto.com/m51cto)

### 146篇文章，197W+人气，45粉丝

关注

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/m51cto)

Ctrl+Enter 发布

发布

取消

2

**0**



分享

关注TA解锁更多精彩文章

关注

[喵来个鱼](https://blog.51cto.com/m51cto)

[![img](https://s2.51cto.com//wyfs02/M02/03/D0/wKiom1mg7MWiVqavAAAhhto7X3g273_middle.jpg)](https://blog.51cto.com/m51cto)

- 相关文章

  [centos7下sudo漏洞自动化批量修复](https://blog.51cto.com/m51cto/2610330)

  [使用Python生成自己的WiFi二维码](https://blog.51cto.com/m51cto/2609384)

  [CentOS7编译安装nginx](https://blog.51cto.com/10632839/2631760)

  [Linux内核 | 进程调度](https://blog.51cto.com/13277700/2631759)

  [监控ADLDAP](https://blog.51cto.com/lishengxian/2631131)

  [Linux内核 | 进程管理](https://blog.51cto.com/13277700/2630977)

  [proxysql-基础](https://blog.51cto.com/laodou/2630933)

  [被 “ 困 ” 京城的时间里，我的CMDB的项目完成了雏形](https://blog.51cto.com/11293981/2630756)

  [Docker快速搭建Clickhouse集群(3分片3副本)](https://blog.51cto.com/14900374/2629096)

  [RocketMQ:设置broker的对外IP](https://blog.51cto.com/14900374/2625587)

  [notepad++设置自动刷新文本（中文版/英文版）](https://blog.51cto.com/13687405/2623763)

  [k8s 存储方式， emptyDir hostpath nfs](https://blog.51cto.com/keep11/2622798)

  [Linux 文件搜索神器 find 实战详解，建议收藏！](https://blog.51cto.com/liwei0526vip/2622100)

  [搭建harbor2.2.0版本](https://blog.51cto.com/13555423/2621233)

  [sed+awk 实现单个文件多行字符合并成单行](https://blog.51cto.com/wujianwei/2621172)

  [jenkins pipeline 发布应用](https://blog.51cto.com/keep11/2621015)

  [docker 搭建zrlog 博客](https://blog.51cto.com/12606610/2620737)

  [Pulsar-admin 常用命令](https://blog.51cto.com/536410/2620346)

  [TCP协议（可靠传输），滑动窗口机制，拥塞机制，避免丢包机制，快速重传机制，回退n步协议等等](https://blog.51cto.com/14632688/2619963)

  [华为鲲鹏认证openeuler系统忘记root密码时如何破解root密码](https://blog.51cto.com/zzzhbr/2619956)

## 推荐专栏[更多](https://blog.51cto.com/cloumn/index?utm_source=p)

[![img](https://s1.51cto.com/images/blog/201804/27/dc6736c5fd50474b5df8b76b040e3d03.jpg)](https://blog.51cto.com/cloumn/detail/5)

[带你玩转高可用](https://blog.51cto.com/cloumn/detail/5)

### 前百度高级工程师的架构高可用实战

#### 共15章 | [曹林华](https://blog.51cto.com/13527416)

##### ￥51.00 523人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/5)

[![img](https://s1.51cto.com/images/blog/201811/28/629650e188ddde78b213e564c2e9ebff.jpg)](https://blog.51cto.com/cloumn/detail/6)

[负载均衡高手炼成记](https://blog.51cto.com/cloumn/detail/6)

### 高并发架构之路

#### 共15章 | [sery](https://blog.51cto.com/sery)

##### ￥51.00 603人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/6)

[![img](https://s1.51cto.com/images/blog/201808/03/a940c66317ecbe58436a2ad3831c2d7d.png)](https://blog.51cto.com/cloumn/detail/13)

[基于Python的DevOps实战](https://blog.51cto.com/cloumn/detail/13)

### 自动化运维开发新概念

#### 共20章 | [抚琴煮酒](https://blog.51cto.com/yuhongchun)

##### ￥51.00 574人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/13)

[![img](https://s1.51cto.com/images/blog/201808/20/45862f289339dc922ffda669fd74ad9b.jpg)](https://blog.51cto.com/cloumn/detail/18)

[网工2.0晋级攻略 ——零基础入门Python/Ansible](https://blog.51cto.com/cloumn/detail/18)

### 网络工程师2.0进阶指南

#### 共30章 | [姜汁啤酒](https://blog.51cto.com/gingerbeer)

##### ￥51.00 2062人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/18)

[![img](https://s1.51cto.com/images/blog/201811/06/5353379fc95da1d7d34fd243b9ace17f.jpg)](https://blog.51cto.com/cloumn/detail/30)

[全局视角看大型园区网](https://blog.51cto.com/cloumn/detail/30)

### 路由交换+安全+无线+优化+运维

#### 共40章 | [51CTOsummer](https://blog.51cto.com/weilan2222)

##### ￥51.00 2620人订阅

[订  阅](https://blog.51cto.com/cloumn/detail/30)

## 好课推荐[更多](https://edu.51cto.com/center/course/index/search?q=yum&qd=bkwz)

- ![搭建企业级 yum 仓库实战指导](https://s1.51ctocdn.cn/images/202007/02/b0cf479242a8d34de78d1cc78c24e35b.jpg)

  [搭建企业级 yum 仓库实战指导145人学习免费试看](http://edu.51cto.com/course/24119.html?qd=bloghktj)

- ![企业级Linux软件包管理(RPM、YUM)实战](https://s1.51ctocdn.cn/images/202101/26/dd548709dda390635fd8ff9a4aa07531.png)

  [企业级Linux软件包管理(RPM、YUM)实战42人学习免费试看](http://edu.51cto.com/course/26569.html?qd=bloghktj)

- ![Linux软件安装rpm与yum_MySQL数据库学习入门视频课程16](https://s1.51ctocdn.cn/images/202007/11/e70cab39922d60916310fff9cf5d4161.png)

  [Linux软件安装rpm与yum_MySQL数据库学习入门视频课程161234人学习免费试看](http://edu.51cto.com/course/13982.html?qd=bloghktj)

- ![分布式云存储、定制rpm包和自建yum库<集群架构 1.> ](https://s1.51ctocdn.cn/images/202011/08/b12a5286879ae6eac55469c583fdc904.png)

  [分布式云存储、定制rpm包和自建yum库<集群架构 1.>275人学习免费试看](http://edu.51cto.com/topic/4203.html?qd=bloghktj)

![img](https://s4.51cto.com/images/blog/202003/17/f84902630cd49eab16f7895cd73e3092.png)

[![img](https://s2.51cto.com/oss/202007/03/f0b9c87765babdf27462fb0b759a2e89.gif)](https://edu.51cto.com/center/activity/member-activity?qd=bokexiaotu)

Copyright © 2005-2020 51CTO.COM 版权所有 京ICP证060544号

<iframe id="redeviation-bs-sidebar" class="notranslate" aria-hidden="true" data-theme="default" __idm_frm__="1485" data-pos="right" style="font-family: -apple-system, &quot;Helvetica Neue&quot;, Helvetica, Arial, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;WenQuanYi Micro Hei&quot;, &quot;Microsoft Yahei&quot;, sans-serif; -webkit-font-smoothing: antialiased; margin: 0px; padding: 0px; opacity: 0; pointer-events: none; position: fixed; top: 0px; left: auto; width: 350px; max-width: none; height: 0px; z-index: 2147483646; speak: none; border: none; transform: translate3d(350px, 0px, 0px); transition: width 0s ease 0.3s, height 0s ease 0.3s, opacity 0.3s ease 0s, transform 0.3s ease 0s; background-color: rgba(255, 255, 255, 0.8) !important; display: block !important; right: 0px; color: rgb(51, 51, 51); font-size: 14px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

# /usr/bin/applydeltarpm not installed问题解决

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[weixin_34348805](https://blog.csdn.net/weixin_34348805) 2018-11-18 23:19:30 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 2719 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

文章标签： [运维](https://www.csdn.net/tags/MtTaEg0sMDQyNTMtYmxvZwO0O0OO0O0O.html)

版权

#### yum update遇到问题：

```
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
```

#### 解决办法

此问题安装Deltarpm包（增量 RPM 套件）即可解决，当然您也可以先使用一下命令，查看是哪个包提供applydeltarpm

```
yum provides '*/applydeltarpm'  



yum install deltarpm -y
yum provides '*/applydeltarpm'



Loaded plugins: axelget, fastestmirror



No metadata available for base



No metadata available for epel



No metadata available for extras



No metadata available for updates



Loading mirror speeds from cached hostfile



 * epel: mirrors.aliyun.com



base/7/x86_64/filelists_db                                                  | 6.9 MB  00:00:00     



epel/x86_64/filelists                                                       |  10 MB  00:00:00     



extras/7/x86_64/filelists_db                                                | 603 kB  00:00:00     



updates/7/x86_64/filelists_db                                               | 3.4 MB  00:00:00     



deltarpm-3.6-3.el7.x86_64 : Create deltas between rpms



Repo        : base



Matched from:



Filename    : /usr/bin/applydeltarpm
```

然后安装deltarpm

```
# yum install deltarpm -y



 



...



Installed size: 209 k



Downloading packages:



deltarpm-3.6-3.el7.x86_64.rpm                                               |  82 kB  00:00:00     



Running transaction check



Running transaction test



Transaction test succeeded



Running transaction



  Installing : deltarpm-3.6-3.el7.x86_64                                                       1/1 



  Verifying  : deltarpm-3.6-3.el7.x86_64                                                       1/1 



 



Installed:



  deltarpm.x86_64 0:3.6-3.el7                                                                      



 



Complete!
```

继续yum updagate即可

转载于:https://blog.51cto.com/m51cto/2318594