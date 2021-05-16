## Armbian挂载硬盘（以及自动挂载）

发布时间：2020年09月22日 阅读：771 次

## Armbian挂载硬盘（以及自动挂载）

**（一）**
Filesystem 文件系統
size 文件大小
Used 使用空间
Mounted on 挂载的目录

1. 、查看系统所检测到的磁盘，这里的 sda1检测到的硬盘但是没有被挂载（注意：这里sda1 是’1’ 而不是’L’，有些可能是sdb1。）

```
lsblk							//查看信息1
```

![img](http://wp.jinxiart.com/zb_users/upload/2020/09/20200922143315160075639528470.png)

1. 、在根目录新建一个目录用于挂载硬盘，命令如下：

```
cd /.				//进入根目录mkdir mnts			//新建目录名为‘mnts’ 可用'ls'查看12
```

1. 、挂载新增的磁盘sda1（所有新增硬盘都在/dve/目录下）

```
mount /dev/sda1 /mnts/		//挂载到 mntscd /mnts/					//进入挂载的硬盘 'ls'查看内容12
```

![img](http://wp.jinxiart.com/zb_users/upload/2020/09/20200922143316160075639686936.png)

**（二）开机自动挂载：**

1. 这条命令可以显示硬盘信息，并记下UUID，为下一步做准备，这里以sda1为例

```
blkid /dev/sda11
```

1. 、修改 /etc/fstab 即可。例如我就是在 fstab 最后添加这行：

```
UUID=722059EC2059B835   /mnts      ntfs    defaults        0 01
vi /etc/fstab				//修改fstab1
```

![img](http://wp.jinxiart.com/zb_users/upload/2020/09/20200922143317160075639758165.png)

1. 最后保存并应用， 则成功自定挂载，开机也会自动挂载（注意：这里只对只一个硬盘有效）

```
mount -a					//应用并启动
```