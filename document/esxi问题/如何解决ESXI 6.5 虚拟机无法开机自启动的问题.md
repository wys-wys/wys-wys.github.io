# 如何解决ESXI 6.5 虚拟机无法开机自启动的问题

[辣条①号](https://www.wsfnk.com/archives/author/fnk) 2017年11月24日 [ESXI](https://www.wsfnk.com/archives/category/云计算/虚拟化/esxi) 5,793 [0](https://www.wsfnk.com/archives/404.html#respond)

**第一：打开ESXI宿主机的sshd服务**
[![img](https://qiniu.wsfnk.com/esxi-vm1.png=boke)](https://qiniu.wsfnk.com/esxi-vm1.png=boke)

**第二：登录ESXI宿主服务器，启动虚拟机开机自启动功能**

```shell
    /bin/vim-cmd -U root hostsvc/autostartmanager/enable_autostart 1
```

Bash

Copy

**第三：查看自启动顺序里的属性是不是poweron**

```shell
    /bin/vim-cmd -U root hostsvc/autostartmanager/get_autostartseq
```

Bash

Copy

[  ](https://qiniu.wsfnk.com/esxi-vm2.png=boke)