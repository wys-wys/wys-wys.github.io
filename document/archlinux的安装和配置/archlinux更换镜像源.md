**我们这里使用的是清华源，清华源的好处上面我说了有一些国内常用的中文软件这些，我们换成清华cnarch linux源的好处就是Arch Linux 中文社区驱动的非官方用户仓库。包含中文用户常用软件、工具、字体/美化包等。**

具体操作方法：

```
# sudo gedit /etc/pacman.conf
```

文件末尾添加以下两行：

```
[archlinuxcn]``Server = https:``//mirrors``.tuna.tsinghua.edu.cn``/archlinuxcn/``$arch
```

 

```
然后很多教程在这里配置就结束了，就遇到一些问题，比如我们安装某些软件的时候会提示gpg签名错误损坏等这些，这个是因为没有导入key的原因，我们需要导入一下GPG KEY，具体操作就是
安装archlinuxcn-keyring 包导入 GPG key。
# sudo pacman -S archlinuxcn-keyring
```

 我们再更新一下源：

```
 
# sudo pacman -Sy
```