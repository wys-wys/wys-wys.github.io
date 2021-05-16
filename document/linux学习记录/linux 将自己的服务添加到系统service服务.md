# [linux 将自己的服务添加到系统service服务](https://www.cnblogs.com/shuiche/p/9327809.html)

## 前言[#](https://www.cnblogs.com/shuiche/p/9327809.html#前言)

我们在linux上要启动一个程序得时候, 往往都是要写一堆路径, 找到要启动得服务程序, 再用 ./*** 启动服务. 那么我们有没有快速启动方法吗, 答案是肯定得

## service 介绍[#](https://www.cnblogs.com/shuiche/p/9327809.html#service-介绍)

官方介绍(英文): https://linux.die.net/man/8/service

简单说一下service运行过程. 以iptables为例: service iptables start

- 首先，sevice 会去/etc/init.d下寻找iptables脚本, start是iptables脚本里的一个参数(你可以去查看networking这个脚本支持的参数）
- 然后告诉系统运行iptables这个脚本，剩下的事情就交给iptables脚本去坐了，事实就是这么简单。

至此，你们应该知道如何添加一个service命令了吧

> 编写一个脚本，然后把它放在/etc/init.d这个目录下，再用service + 脚本名字 运行即可。如果是要开机自动启动那就得用chkconfig命令了

注意：
A、service这个命令往往是即时生效，不用开关机，但是重启后服务会回到默认状态。

B、在init.d里面得脚本是没有后缀名的

 

## 设置开机自动启动[#](https://www.cnblogs.com/shuiche/p/9327809.html#设置开机自动启动)

```
chkconfig --add test 
chkconfig test on/off    //重启后永久生效
```

上面的不生效:则使用下面得方法

**通过update-rc.d 命名设置开机自启动**

```
cd /etc/init.d
sudo update-rc.d test defaults 95
```

注：其中数字95是脚本启动的顺序号，按照自己的需要相应修改即可。在你有多个启动脚本，而它们之间又有先后启动的依赖关系时你就知道这个数字的具体作用了。该命令的输出信息参考如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
update-rc.d: warning: /etc/init.d/test missing LSB information
update-rc.d: see &lt;http://wiki.debian.org/LSBInitScripts&gt;
Adding system startup for /etc/init.d/test ...
/etc/rc0.d/K95test -&gt; ../init.d/test
/etc/rc1.d/K95test -&gt; ../init.d/test
/etc/rc6.d/K95test -&gt; ../init.d/test
/etc/rc2.d/S95test -&gt; ../init.d/test
/etc/rc3.d/S95test -&gt; ../init.d/test
/etc/rc4.d/S95test -&gt; ../init.d/test
/etc/rc5.d/S95test -&gt; ../init.d/test
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**卸载启动脚本的方法：**

```
cd /etc/init.d
sudo update-rc.d -f test remove
```

**命令输出的信息参考如下：**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
Removing any system startup links for /etc/init.d/test ...
/etc/rc0.d/K95test
/etc/rc1.d/K95test
/etc/rc2.d/S95test
/etc/rc3.d/S95test
/etc/rc4.d/S95test
/etc/rc5.d/S95test
/etc/rc6.d/K95test
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

## 常见错误:[#](https://www.cnblogs.com/shuiche/p/9327809.html#常见错误:)

\1. **service启动任务时提示: \*program-service: unrecognized service\***

　　这是因为我们还没有更改 执行脚本得 的权限为可执行。`chmod +x /etc/init.d/**serviceName**` 后重新执行上一个命令

\2. **添加到开机启动任务时提示: \*service \**\* does not support chkconfig\***

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
[root@redis01 test]# chkconfig --add test
service test does not support chkconfig
解决方法：(在/etc/init.d/test添加两行注释)
#!/bin/sh
#添加的两行注释内容如下：
# chkconfig:   2345 90 10
# description:  test is a persistent key-value database
# 注释的意思是，test服务必须在运行级2，3，4，5下被启动或关闭，启动的优先级是90，关闭的优先级是10
[root@redis01 test]# chkconfig --add test
[root@redis01 test]# echo $?
0
[root@redis01 test]# chkconfig --list | grep test
test          0:off1:off2:on3:on4:on5:on6:off
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　在编辑其它类似服务时，也可能出现这种情况，解决方法基本类似

 

 参考:

[解决“service XXX does not support chkconfig”的问题](http://blog.51cto.com/professor/1579791)



作者：水车

出处：https://www.cnblogs.com/shuiche/p/9327809.html

版权：本作品采用「[署名-非商业性使用-相同方式共享 4.0 国际](https://creativecommons.org/licenses/by-nc-sa/4.0/)」许可协议进行许可。

本博文版权归本博主所有,未经授权不得转载

 分类: [水车的分类--操作系统](https://www.cnblogs.com/shuiche/category/893055.html)