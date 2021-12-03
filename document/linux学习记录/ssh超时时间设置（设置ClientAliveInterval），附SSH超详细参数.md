# [ssh超时时间设置（设置ClientAliveInterval），附SSH超详细参数](https://www.cnblogs.com/findumars/p/6272224.html)

```
作者: daodaoliang
版本: V 0.0.1
日期: 2016年12月29日
```

------

#### 0x00 OpenSSH 简介

[OpenSSH](http://www.openssh.com/)是采用SSH协议实现的重要的远程连接工具，它对所有的数据进行加密以防止被中途窃听，[OpenSSH](http://www.openssh.com/)提供了大量的安全通道的组件，比如：

1. 远程操作用[ssh](http://man.openbsd.org/?query=ssh&sektion=1)、[scp](http://man.openbsd.org/?query=scp&sektion=1)、[sftp](http://man.openbsd.org/?query=sftp&sektion=1);
2. 秘钥管理用[ssh-add](http://man.openbsd.org/?query=ssh-add&sektion=1)、[ssh-keysign](http://man.openbsd.org/?query=ssh-keysign&sektion=8)、[ssh-keyscan](http://man.openbsd.org/?query=ssh-keyscan&sektion=1)、[ssh-keygen](http://man.openbsd.org/?query=ssh-keygen&sektion=1);
3. 服务端包含[sshd](http://man.openbsd.org/?query=sshd&sektion=8)、[sftp-server](http://man.openbsd.org/?query=sftp-server&sektion=8)、[ssh-agent](http://man.openbsd.org/?query=ssh-agent&sektion=1);

#### 0x01 方案一

上面的所有信息可以自行去对应官网链接进行进一步的学习，在下面只讨论对于sshd的超时连接的问题。

1. 修改server端的配置文件`/etc/ssh/sshd_config`

```
# server每隔60秒给客户端发送一次保活信息包给客户端
ClientAliveInterval 60

# server端发出的请求客户端没有回应的次数达到86400次的时候就断开连接，正常情况下客户端都会相应
ClientAliveCountMax 86400
```

1. 修改client端的配置文件`/etc/ssh/ssh_config`

```
# client 每隔60秒给客户端发送一次保活信息包给客户端
ServerAliveInterval 60

# client 端发出的请求服务端没有回应的次数达到86400次的时候就断开连接，正常情况下服务端都会相应
ServerAliveCountMax 86400
```

#### 0x02 方案二

在命令参数里

```
 ssh -o ServerAliveInterval=60 
 
```

这样子只会在需要的连接中保持持久连接，具体的参数请[参考这里](http://man.openbsd.org/sshd_config.5)。

http://daodaoliang.com/blog/2016/12/29/ssh%E8%B6%85%E6%97%B6%E6%97%B6%E9%97%B4%E8%AE%BE%E7%BD%AE.html