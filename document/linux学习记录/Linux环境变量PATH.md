# Linux环境变量PATH

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[鹏鹏俊玲](https://blog.csdn.net/qq_29837161) 2018-12-26 09:30:35 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 7112 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 17

分类专栏： [Linux](https://blog.csdn.net/qq_29837161/category_7967845.html) 文章标签： [linux](https://www.csdn.net/tags/MtjaQg5sMDY0MC1ibG9n.html) [PATH](https://www.csdn.net/tags/MtTaEg0sMTg1NzAtYmxvZwO0O0OO0O0O.html)

版权

### 一、PATH 是什么

当你在shell命令行界面中输入一个外部命令时(非 shell 内部命令)， shell必须搜索系统来找到对应的程序。 PATH环境变量定义了用于进行命令和程序查找的目录。
PATH中的目录使用冒号分隔。
在 shell 中输入 " echo $PATH " 可以查看PATH 中的值。
如果命令或者程序的位置没有包括在PATH变量中，那么如果不使用绝对路径的话， shell是没法找到的。如果想要在虚拟目录结构中的任何位置执行某个程序，办法是把这个程序所在的目录添加到 PATH 环境变量中，或者把这个程序放在 / 链接(ln)到已经存在PATH中的目录下。

### 二、添加目录到 PATH 中

**1、临时有效**

在 shell 中输入：   PATH=$PATH:directory你要添加的目录
上面的命令对PATH变量的修改只能持续到退出或重启系统。

**2、永久有效**

启动bash shell有3种方式：登录时作为默认登录shell；作为非登录shell的交互式shell；作为运行脚本的非交互shell。
不同的启动方式，bash 会在不同的启动文件或环境文件中查找命令。

① 登录 shell

当你登录Linux系统时， bash shell会作为登录shell启动。登录shell会从5个不同的启动文件里读取命令：
/etc/profile   主启动文件，系统上的每个用户登录时都会执行这个启动文件。
$HOME/.bash_profile    HOME下的都是针对某个用户的，不同的发行版本，不一定都有这4个文件。
$HOME/.bashrc
$HOME/.bash_login
$HOME/.profile

$HOME表示的是某个用户的主目录。它和波浪号（ ~）的作用一样。

⑴ /etc/profile
在不同的发行版本中，/etc/profile 文件中内容是不一样的，但都迭代 /etc/profile.d 目录下的所有文件。 /etc/profile.d 目录为Linux系统提供了一个放置特定应用程序启动文件的地方，当用户登录时， shell会执行这些文件。大部分应用都会创建两个启动文件：一个供bash shell使用（使用.sh扩展名），一个供c shell使用（使用.csh扩展名）。

⑵ $HOME目录下的启动文件
shell会按照按照下列顺序，运行第一个被找到的文件，余下的则被忽略：
$HOME/.bash_profile
$HOME/.bash_login
$HOME/.profile
$HOME/.bashrc 通常通过其它3个文件运行的。

②交互式 shell 进程

比如是在命令行提示符下敲入bash时启动，那么你启动的shell叫作交互式shell。不会访问/etc/profile文件，只会检查用户HOME目录中的.bashrc文件，即$HOME/.bashrc。
.bashrc文件有两个作用：一是查看/etc目录下通用的bashrc文件，二是为用户提供一个定制自己的命令别名和私有脚本函数的地方。

③非交互式 shell

系统执行shell脚本时用的就是这种shell。不同的地方在于它没有命令行提示符。但是当你在系统上运行脚本时，也许希望能够运行一些特定启动的命令。
脚本能以不同的方式执行。只有其中的某一些方式能够启动子shell。
当shell启动一个非交互式shell进程时，它会检查BASH_ENV环境变量来查看要执行的启动文件。如果有指定的文件， shell会执行该文件里的命令，这通常包括shell脚本变量设置。在一些linux发行版本中，变量BASH_ENV没有被设置，shell脚本通过子shell继承父shell导出过的变量。对于那些不启动子shell的脚本，变量已经存在于当前shell中了。

### 三、总结

①对全局环境变量来说（ Linux系统中所有用户都需要使用的变量），可能更倾向于将新的或修改过的变量设置放在/etc/profile文件中，但是有问题。如果你升级了所用的发行版，这个文件也会跟着更新，那你所有定制过的变量设置可就都没有了。
最好是在/etc/profile.d目录中创建一个以.sh结尾的文件。把所有新的或修改过的全局环境变量设置放在这个文件中。
  操作方法(需要管理员权限，/etc/profile对普通用户来说是只读的)：
    打开/etc/profile的编辑页面： vim /etc/profile
    在文件的最后添加语句：  export PATH=$PATH:directory你要添加的目录
    系统重启之后，就生效了。
  注：添加的语句中的等号(=)前后不要有空格。
      修改 /etc/environment 文件能达到一样的效果，只不过是在PATH="  ... "中直接添加 ":directory你要添加的目录"。系统重启生效。

②在大多数发行版中，存储个人用户永久性bash shell变量的地方是$HOME/.bashrc文件。这一点适用于所有类型的shell进程。
  操作方法：
    打开~/.bashrc文件：  vim ~/.bashrc
    在文件的最后添加语句： export PATH=$PATH:directory你要添加的目录
  生效方法：
    关闭当前终端窗口，重新打开一个新终端窗口就能生效
    在shell中输入“source ~/.bashrc”命令，立即生效

