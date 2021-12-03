# [wswind](https://www.cnblogs.com/wswind/)

- [首页](https://www.cnblogs.com/wswind/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/wswind)
- [订阅](javascript:void(0))
- [管理](https://i.cnblogs.com/)

# [centos 8 如何重启网络 service network restart / systemctl restart network 失效的解决办法](https://www.cnblogs.com/wswind/p/11729892.html)

systemctl restart network centos8失效了
重启网络可使用以下命令

```bash
#重启整个网络
nmcli n off && nmcli n on 
#重启指定网卡
nmcli c down eth0 && nmcli c up eth0 
ifdown eth0 && ifup eth0
```

注意一定要使用&&一起执行，否则关闭网络后，会无法远程连接到服务器
ifdown / ifup本质为调用nmcli的脚本

ps:
你可以通过图形化工具来设置网络

```
nmtui
```

参考：
https://www.centos.org/forums/viewtopic.php?p=302319
https://access.redhat.com/discussions/3791081
https://www.osetc.com/en/how-to-start-stop-restart-network-service-on-centos-8-or-rhel-8.html
https://www.tecmint.com/set-static-ip-address-in-rhel-8/
https://www.tecmint.com/configure-network-connections-using-nmcli-tool-in-linux/
https://www.certdepot.net/rhel7-configure-ipv4-addresses/

作者：wswind

出处：https://www.cnblogs.com/wswind/p/11729892.html

版权：本作品采用「[署名-非商业性使用-相同方式共享 4.0 国际](https://creativecommons.org/licenses/by-nc-sa/4.0/)」许可协议进行许可。



 标签: [CentOS](https://www.cnblogs.com/wswind/tag/CentOS/)

 1

 0

[« ](https://www.cnblogs.com/wswind/p/11709064.html)上一篇： [HTTP Error 502.5 - ANCM Out-Of-Process Asp.Net Core发布到IIS失败](https://www.cnblogs.com/wswind/p/11709064.html)
[» ](https://www.cnblogs.com/wswind/p/11751829.html)下一篇： [CentOS 8 / CentOS Stream 换源，设置dnf / yum镜像](https://www.cnblogs.com/wswind/p/11751829.html)

posted @ 2019-10-24 00:02 [wswind](https://www.cnblogs.com/wswind/) 阅读(10181) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=11729892) [收藏](javascript:void(0))





发表评论



编辑预览