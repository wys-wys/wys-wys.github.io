# 极致安卓之—Termux安装完整版Linux

[![myastrotong](https://pic4.zhimg.com/v2-630280f8f6d2060f01810f0a1fc2ea18_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/tang-kong-wen)

[myastrotong](https://www.zhihu.com/people/tang-kong-wen)

空!=无

关注他

127 人赞同了该文章

本文的重点：Termux不是真实的Linux环境，但是Termux可以安装真实的Linux，而且不会损失性能！关键是还不需要root！步骤和遇坑解决措施如下！

在如下两篇中分别介绍了怎么安装Termux和Aid Learning！

[myastrotong：把安卓手机性能发挥到极致之-Termuxzhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/92664273)[myastrotong：把安卓手机性能发挥到极致之-Aid Learningzhuanlan.zhihu.com![图标](https://pic4.zhimg.com/v2-948b998a3e0883478e321df4a558749f_120x160.jpg)](https://zhuanlan.zhihu.com/p/92161002)

这两款比较后发现，Aid Learning性能更好，因为是纯净版Linux，能够安装的东西更多！而Termux只能安装clang、python，其他的重要软件如gcc、g++、gfortran、jdk等等都不能安装！

因此：如果是新款手机我建议按个Aid Learning就算了！别折腾了！最新版的Aid learning还内置了vs code！强大的很！你要不愿意折腾就用这个吧。

[myastrotong：极致安卓—Termux/Aid Learning安装宇宙最强VS Codezhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/106593146)

**有啥不明白的或者特殊需求，就去Aid learning的官方QQ群：\*111245605\*，Aid Learning交流群。大神们等你来！**

但是，重要的是这个但是：

Aid Learning对老旧手机不友好！我的三星Note3无论怎么折腾都安不上Aid Learning。可是我想把老旧手机们串起来组集群啊！没办法了，只能寻求新的解决方法。

如果手机能root就好办了，Linux deploy直接就能安装。可惜折腾了三天，安了无数个流氓root软件，Note3还是无法root。只能退回到Termux上。

上官网发现，从0.73版本之后就不再支持安卓5了。所以三星Note3只能安装0.73版Termux。反正又不是不能用！

[https://f-droid.org/packages/com.termux/f-droid.org](https://link.zhihu.com/?target=https%3A//f-droid.org/packages/com.termux/)

Termux安装完毕以后！

经后台知友提醒，发现有两种方法可以安装完整版Linux。推荐第一种方法，第二种就不用看了。

***写在前面：本文的方法可以在你的Termux上安装任意多个Linux，只要你把相关文件放在不同的文件夹下相互不干扰即可！！！比如，在home文件夹下建立file1和file2，然后就可以分别安装不同的Linux。好处：你可以在每个子Linux安装互不影响的软件，每个子Linux能够管理不同的软件系统。***



**方法1：**

上网站下载AnLinux，当前版本是6.01：

[F-Droid - Free and Open Source Android App Repositoryf-droid.org](https://link.zhihu.com/?target=https%3A//f-droid.org/zh_Hans/packages/exa.lnx.a/)

安装Termux以后，基于AnLinux安装完整版本的Linux。方法如下：

首先在仪表板上选择你想要安装的Linux发行版，这里我选择Debian。

![img](https://pic3.zhimg.com/80/v2-bafe29abef6a05166ea1babeb8afd50a_720w.jpg)

然后第二步，选择复制指令，然后在Termux的终端窗口，粘贴这段指令。



![img](https://pic4.zhimg.com/80/v2-d48191a48a754f7c82f1ca45d385076b_720w.jpg)

等待安装即可！

这一步骤极度依赖网络，我家的破X城宽带，一上外网就抽风。这一步骤我重复了多次。如果你安装不成功，一般都是网络的锅！

安装完毕，就可以进入你安装的Linux了。

按照说明输入如下指令：

```text
 ./start-debian
```

***划重点，坑来了，上面指令是过不去的，千万不要删除了重装浪费时间，千万别忘了后缀.sh，改用如下指令即可（这是我的血泪教训啊！）：***

```text
 ./start-debian.sh
```

进入完整版linux系统，发现进系统后不能访问手机自身的存储文件系统了！修改start-debian.sh文件，发现原来哪行代码被屏蔽掉了，如果你需要，可以把注释符#去掉就有sdcard链接存在了！

就是这一行：

```text
#command+=“ -b /sdcard”
```

![img](https://pic1.zhimg.com/v2-140c7f022197d6c4445ff6ce5a9e54ec_r.jpg)



安装Linux以后，还可以安装桌面。

点击AnLinux左上角，选择“桌面”。

然后进入第一步，选择对应的Linux版本，我上一步是Debian，这里我也选择Debian。

![img](https://pic2.zhimg.com/80/v2-ab5d98ad52910f73b4494eeb3ac92529_720w.jpg)

然后第二步，选择桌面。

手机性能有限，我选择了Xfce4。

![img](https://pic3.zhimg.com/80/v2-a5a217de5e4c036d0ee5a1fbfd7d1b56_720w.jpg)



然后第三步，复制指令，然后把该指令粘贴到Termux的终端。

等待安装。成功与否完全依赖于网络！有错误就请重复本步。而且这一步之前请先输入：

```text
./start-debian
```

也就是先打开Debian系统，然后安装桌面。

![img](https://pic1.zhimg.com/80/v2-73bd642eb68e9c103f0a461211ce30c4_720w.jpg)

安装完成以后，请安装VNC Viewer，就是下图红圈内的这货：

![img](https://pic1.zhimg.com/80/v2-11b802f71fe5de5e0a09b5cb1e0340b4_720w.jpg)

然后在Termux终端开启VNC：

```text
vncserver-start
```

第一次开启时还需要设置密码！

开启完成后如下：

![img](https://pic3.zhimg.com/80/v2-cdecca2f576456865a481f7869f7b26e_720w.jpg)

如果你仔细看上图，会发现我开启了两次，这是因为第一次开机没成功。如果开启不成功，显示如下红圈的错误，则可能是上一次使用没有停止vncserver。

![img](https://pic3.zhimg.com/80/v2-638f0d997024f9b9ac4c4b917e31b7ae_720w.jpg)



请先输入如下指令关闭vncserver：

```text
vncserver-stop
```

可以看到我这里是:localhost:1

表示我的端口是1

开启VNC Viewer，然后设置如下：

![img](https://pic4.zhimg.com/80/v2-eed20a60ab842c80fa2eaa9da9d2f4ef_720w.jpg)

![img](https://pic3.zhimg.com/80/v2-96417ba75fa506765cdd12b75249aa76_720w.jpg)

点击Connect连接，效果如下：

![img](https://pic4.zhimg.com/v2-90a510ea5a2e0fe323620f8031a4fed7_r.jpg)

手机登录Linux的桌面效果还是不好，凑活能看的水平。

使用完毕后，别忘记关闭VNC:

```text
vncserver-stop
```

**方法2：**

以前的操作都属于常规操作，重要的步骤来了，模仿root权限的重要包：

```text
pkg install proot
```

安装完毕以后，执行如下指令，获取root权限：

```text
termux-chroot
```

千万记住了，在Termux上安装或者运行Linux之前一定要执行以上指令，否则安装linux会出错，进入linux后安装包会报错，运行java也会报错，......这些错你都完全无法查出原因！！！

这是我折腾了无数个日夜后得出来的经验！

然后，执行如下指令：

```text
echo "deb [trusted=yes] https://yadominjinta.github.io/files/ termux extras" >> $PREFIX/etc/apt/sources.list
pkg in atilo-cn
```

相关的详细解释见官网

[YadominJinta/atilogithub.com](https://link.zhihu.com/?target=https%3A//github.com/YadominJinta/atilo/blob/master/CN/README_CN.md)

然后执行

```text
atilo list
```

可以查看能够安装的版本，比如Debian, Ubuntu, Arch等等。

执行如下指令安装

```text
atilo install debian
```

执行如下指令卸载

```text
atilo remove debian
```

如果就真的这么简单就能安上，那我也不用写文章了。

重要的通知来了：如果网络环境不好（比如我家的某城宽带），下载没有100%完成，你的安装仍然会继续，后面的步骤任然会走到头，但是你安装的是个阉割版，运行必然出错！此时你执行atilo remove debian。然后重新安装，仍然还是个阉割版！

怎么办呢？官网是没有解释的。查询官网的源码：

[YadominJinta/atilogithub.com![图标](https://pic3.zhimg.com/v2-3f55c69a4dc16c217aefc5cb8226411e_ipico.jpg)](https://link.zhihu.com/?target=https%3A//github.com/YadominJinta/atilo/blob/master/CN/atilo_cn)

![img](https://pic4.zhimg.com/v2-08baee4c8aa2e8dbd120c05fc20dad47_r.jpg)

如图可见，程序是通过比对名称来判断的，如果硬盘里面有了这个文件，不管他是否完整都会跳过下载，所以你每次都是安装的阉割版！！！坑吧！谁叫咱网络不好呢！

找到问题就好解决了，

```text
cd ~/.atilo
ls
```

此时可以看到，目录下有个tmp文件夹！

```text
rm -r tmp
```

没错，下载的安装包就在tmp下，把它删除掉，以上的错误就不再有了！

然后重新执行安装指令就行了：atilo install debian。

如果有错就继续以上步骤！

至此就完成了Termux安装Linux的全部步骤！



我安装的是Debian。在确保获得root权限后（执行termux-chroot），进入系统：

```text
startdebian
```





上述两种方式安装Linux完成以后，以下操作就是相同的了：

```text
apt update
apt upgrade
```

然后执行

```text
apt install gcc
apt install g++
apt install gfortran
apt install cmake
```

然后安装java：

```text
apt search openjdk
```

发现目前的版本是openjdk-11

```text
apt install default-jdk
```

最后是漫长的等待。

然后安装python。

```text
apt install python3
```

pip在Debian里面不一样

```text
apt search pip
```

发现它长这样：

```text
apt install python3-pip
```

然后是python换国内源：

源文件文件在~/.pip/pip.conf

修改内容为：

```text
[global]
index-url =http://pypi.douban.com/simple  
[install]
trusted-host=pypi.douban.com
```

然后安装常用包：

```text
pip3 install numpy
pip3 install pandas
apt install libzmq3-dev
apt install libfreetype6-dev
```

没错，以上两个是matplotlib的依赖包，而且目前debian上是libfreetype6-dev了，不是libfreetype2！（没准你安装的时候又更新了，多用apt search盯着点把！泪目！）

```text
pip3 install matplotlib
pip3 install jupyter
```

安完jupyter以后，参考如下文章，可以设置jupyter的一些便利开发环境，这里就不予赘述了：

[myastrotong：把安卓手机性能发挥到极致之-Termux安装Python及Jupyterzhuanlan.zhihu.com![图标](https://zhstatic.zhihu.com/assets/zhihu/editor/zhihu-card-default.svg)](https://zhuanlan.zhihu.com/p/94203587)

结论：

本文重点是解决在Termux下安装完整版Linux，这样老旧手机（安卓5及以上）就可以安装gcc和java了！

请优先使用第一种方法安装Linux。

第二种方法复杂，且有坑：

其中最大的坑是：一定要执行termux-chroot获得root权限，然后才能顺畅的使用Linux并进行开发！

第二个坑是：安装Linux的过程中如果遇到网络问题，安装程序下载不完全，请记得一定要先删除安装包（tmp文件夹）！



编辑于 02-22