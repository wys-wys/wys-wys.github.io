**如何使用pgrep[命令](https://www.linuxcool.com/)**

语法：

```
pgrep [options] pattern
```

当在没有任何选项的情况下调用时，pgrep将显示与给定名称匹配的所有正在运行的程序的pid。例如，要找到SSH服务器的PID，可以运行以下命令:

```
[root@localhost ~]# pgrep ssh
853
1063
1589
```

如果想要结束ssh进程，可以使用pkill命令

```
[root@localhost ~]# pkill ssh
```

pgrep在换行中打印每个匹配的进程ID。-d选项允许指定不同的分隔符。例如，如果想使用空格作为分隔符，运行下面的命令:

```
[root@localhost ~]# pgrep ssh -l -d ' ‘
1654 sssd_ssh1664 sshd1666 sshd
```

使用-l选项可以列出PID和进程名称：

```
[root@localhost ~]# pgrep -l ssh
1654 sssd_ssh
1664 sshd
1666 sshd
```

如果想完全匹配，可以使用:

```
[root@localhost ~]# pgrep '^sshd$' -l
1664 sshd
1666 sshd
```

使用-u选项告诉pgrep显示给定用户正在运行的进程：

```
[root@localhost ~]# pgrep -u root -l
1 systemd
2 kthreadd
…
…
520 xfsaild/dm-0
521 kworker/0:1H
600 systemd-journal
622 lvmetad
628 systemd-udevd
632 rpciod
634 xprtiod
659 xfs-buf/sda1
```

若要显示与给定条件不匹配的进程，请使用 -v选项。下面的命令将打印所有不是由用户“root”运行的进程:

```
[root@localhost ~]# pgrep -v -u root -l
801 dbus-daemon
802 rpcbind
810 avahi-daemon
812 polkitd
817 avahi-daemon
820 chronyd
1282 pickup
1283 qmgr
```

-c选项告诉pgrep只打印匹配进程的数量

```

[root@localhost ~]# pgrep -v -u root -l -c
8
```