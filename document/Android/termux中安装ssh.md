# Termux 安装 openssh

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[iknownothingatall](https://blog.csdn.net/iknownothingatall) 2020-05-06 00:06:54 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 421 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [手机](https://blog.csdn.net/iknownothingatall/category_9975562.html) 文章标签： [ssh](https://www.csdn.net/gather_2a/MtTaEg0sNTExMDEtYmxvZwO0O0OO0O0O.html) [linux](https://www.csdn.net/gather_2d/MtjaQg5sMDY0MC1ibG9n.html)

版权



### 文章目录

- [Termux 安装 openssh](https://blog.csdn.net/iknownothingatall/article/details/105941916#Termux__openssh_1)
- - [目标](https://blog.csdn.net/iknownothingatall/article/details/105941916#_3)
  - [预备](https://blog.csdn.net/iknownothingatall/article/details/105941916#_7)
  - [安装](https://blog.csdn.net/iknownothingatall/article/details/105941916#_14)
  - [扩展](https://blog.csdn.net/iknownothingatall/article/details/105941916#_53)



# Termux 安装 openssh

## 目标

- 在 Termux 终端里安装 openssh 并通过Linux终端连接到Termux

## 预备

- Termux
- openssh (Termux下安装)
- Terminator (Linux下终端)
- Linux

## 安装

1. Termux 安装 openssh

```Shell
pkg install openssh -y 
1
```

1. Linux 生成 SSH 验证信息

```Shell
ssh-keygen -t rsa
> Enter
> Enter
123
```

1. Linux 查看 SSH 公钥

```Shell
cat ~/.ssh/id_rsa.pub
1
```

1. 将 Linux SSH 公钥内容复制到 Termux 文件下

```Shell
cat  /data/data/com.termux/files/home/.ssh/authorized_keys
1
```

1. Termux启动 openssh服务

```Shell
sshd
1
```

1. 查看 Termux IP地址

```Shell
ip addr 
1
```

1. Linux 下 Terminator 连接 Termux，默认端口为 8022

```Shell
ssh IP地址 -p 8022
1
```

1. 首次连接输入 yes
2. 连接成功验证

```Shell
ip addr 
1
```

## 扩展

1. 更改 Termux 源及升级

```Shell
# 更改源的清华大学开源软件镜像站源
sed -i 's@^\(deb.*stable main\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24 stable main@' $PREFIX/etc/apt/sources.list
sed -i 's@^\(deb.*games stable\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/game-packages-24 games stable@' $PREFIX/etc/apt/sources.list.d/game.list
sed -i 's@^\(deb.*science stable\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/science-packages-24 science stable@' $PREFIX/etc/apt/sources.list.d/science.list
apt update && apt upgrade -y
```