# Linux中的虚拟设备/dev/null、/dev/zero、/dev/random和/dev/urandom

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[imyuyufei](https://me.csdn.net/sinat_26058371) 2019-02-02 23:32:13 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7532 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 18

文章标签： [linux](https://www.csdn.net/gather_2d/MtjaQg5sMDY0MC1ibG9n.html)

版权

Unix/Linux将每一个设备都当成一个文件，放在/dev目录下。这些文件有的对应着一个真实存在的物理设备；有的则代表一个虚拟设备，提供一些特定的功能。

下面介绍三个常用的虚拟设备：

**/dev/null**
“空”设备，也有人称它为黑洞。任何输入到这个“设备”的数据都将被直接丢弃。最常用的用法是把不需要的输出重定向到这个文件。例如：

```
$ run.sh 1>/dev/null 2>&1  #将标准输出和错误输出重定向到/dev/null，运行这个脚本不会输出任何信息到终端
```

**/dev/zero**
“零”设备，可以无限的提供空字符（0x00，ASCII代码NUL）。常用来生成一个特定大小的文件。例如：

```
$ dd if=/dev/zero of=./output.txt bs=1024 count=1 #产生一个1k大小的文件output.txt
```

**/dev/random和/dev/urandom**
随机数设备，提供不间断的随机字节流。二者的区别是/dev/random产生随机数据依赖系统中断，当系统中断不足时，/dev/random设备会“挂起”，因而产生数据速度较慢，但随机性好；/dev/urandom不依赖系统中断，数据产生速度快，但随机性较低。
读取这两个文件的输出如下：

```
$ cat /dev/random | od -x
0000000 34fa b5ea 0901 b7e0 27a9 623a 0879 d9eb
0000020 d212 4f6f d928 6637 84a4 8ec5 fc2c 4896
$ cat /dev/urandom | od -x | head -n 5
0000000 8048 4dbd 07c9 2119 02d0 221b 89ba af7f
0000020 3d6f 6a72 3752 4a09 5a47 a3fb dc98 ed9f
0000040 f3e8 e82d 6748 2e14 de80 7554 bb52 f56c
0000060 de73 0e51 262f 5a63 af69 b45c ee49 c1bf
0000100 76b4 6db5 4e5b e438 70fb d207 a28c 04a8
```

在上面的例子中，读取/dev/random文件在输出了两行之后就停住了（系统中断不足），而/dev/urandom产生数据速度很快，没有任何停顿。

下面这个例子，利用/dev/urandom设备产生一个128位的随机字符串：

```
$ str=$(cat /dev/urandom | od -x | tr -d ' ' | head -n 1)
$ echo ${str:7}
17539187d2e8b8e26d49bec90465c14d 
```