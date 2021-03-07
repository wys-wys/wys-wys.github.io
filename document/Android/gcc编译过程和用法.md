[![博客园Logo](https://www.cnblogs.com/images/logo.svg?v=R9M0WmLAIPVydmdzE2keuvnjl-bPR7_35oHqtiBzGsM)](https://www.cnblogs.com/)[首页](https://www.cnblogs.com/)[新闻](https://news.cnblogs.com/)[博问](https://q.cnblogs.com/)[专区](https://brands.cnblogs.com/)[闪存](https://ing.cnblogs.com/)[班级](https://edu.cnblogs.com/)![搜索](https://www.cnblogs.com/images/aggsite/search.svg)[注册](https://account.cnblogs.com/signup/)[登录](javascript:void(0);)

[![返回主页](https://www.cnblogs.com/skins/custom/images/logo.gif)](https://www.cnblogs.com/chaguang/)

# [菜鸟也有高飞的时候](https://www.cnblogs.com/chaguang/)

## 

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/chaguang/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/菜鸟也有高飞的时候)
- [订阅](javascript:void(0))
- [管理](https://i.cnblogs.com/)

# [gcc的基本用法](https://www.cnblogs.com/chaguang/p/8306106.html)

## linux下gcc的基本用法

```
gcc 是 GUN Compiler Collection的缩写，可以支持多种语言编译，比如 C,C++,Java, pascal 等
```

### gcc的编译过程

![img](https://images2017.cnblogs.com/blog/1044665/201801/1044665-20180117212346053-1244954563.png)

- 预处理（pre-processing）E：插入头文件，替换宏
- 编译（Compiling）S：编译成汇编
- 汇编（Assembling） c：编译成目标文件
- 链接 （Linking）：链接到库中，变成可执行文件

gcc -E hello.c -o hello.i

gcc -S hello.i –o hello.s

gcc –c hello.s –o hello.o

gcc hello.s –o hello 链接，生成可执行文件

/hello 运行

也可以一次性完成:

gcc hello.c –o hello

但一般情况下生成.o文件比较好，可以重定位文件，让别人使用

### gcc常用选项

| 选项名 | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| o      | 生成目标                                                     |
| c      | 取消链接步骤，编译源码并最后生成目标文件                     |
| E      | 只运行C预编译器（头文件，宏等展开）                          |
| S      | 生成汇编语言文件后停止编译（.s文件）                         |
| Wall   | 打开编译告警（所有）                                         |
| g      | 嵌入调试信息，方便gdb调试                                    |
| llib   | 链接 lib 库 （这里是小写 L ） 相当于 C++ #pragma comment(lib, “xxx.lib”) |
| Idir   | 增加 include 目录 (这里是大写 i ) 头文件路径                 |
| LDir   | 增加 lib 目录 （编译静态库和动态库）                         |

### 多模块编译

- 一次性编译：

  gcc -Wall fun.c main_fun.c –o main_fun

- 独立编译：

  gcc –Wall –c main_fun.c –o main_fun.o

  gcc –Wall –c fun.c –o fun.o

  gcc –Wall main_fun.o fun.o –o main_fun

多模块编译中如果某一个模块发生了变化，只需要编译更改的模块即可

### 静态库与共享库(动态库)

#### 静态库（.a）

> 程序在编译链接时候把库的代码链接到可执行文件中。程序运行时候，不再需要静态库，生成的可执行文件大，每个可执行文件都会加载一份拷贝到内存

- 静态库生成（libxxx.a）

  首先生成.o文件，然后通过.o文件生成.a文件

  例如：

  gcc –c fun.c

  ar rcs libfun.a fun.o

- 静态库使用

  gcc –Wall main.c libfun.a –o main

  gcc –Wall –L. main.c –o main –lfun

  -L.表示在当前目录搜索 libfun.a

- 静态库搜索路径

  1:编译使用选项 –L 指定的目录(建议)

  2:修改环境变量，搜索指定的目录 设置环境变量 LIBRARY_PATH

  export LIBRARY_PATH=“*库目录*”

  3:lib文件放入系统指定目录，例如/usr/lib/等

#### 共享库（.so或.sa）

> 程序运行时候才去链接共享库代码，多个程序共享使用,使用时候只需要加载一份到内存

直接可以通过.c文件生成.so文件

例如：gcc –shared –fPIC fun.o –o [libFun.so](http://libfun.so/)

shared：生成共享库格式

fPIC： 产生位置无关码，允许在任何地址加载 (否则只能从指定地址加载，无法控制)相对地址

使用： gcc –Wall main.o –o main –L. -lFun

只需要-l+文件名即可

配置方式

1:拷贝到so文件到共享库目录 /usr/lib/

2:更改 LD_LIBRARY_PATH，如果已经有了一个这样的目录，要写成export LD_LIBRARY_PATH=$LD_LIBRARY_PATH：“*库目录*”这样子 如果写在profile配置文件里 export LD_LIBRARY_PA TH="目录:$LD_LIBRARY_PATH"

3:配置 /etc/ld.so.conf; 并使用 ldconfig 命令进行更新

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/sample_face.gif)](https://home.cnblogs.com/u/chaguang/)

[菜鸟也有高飞的时候](https://home.cnblogs.com/u/chaguang/)
[关注 - 0](https://home.cnblogs.com/u/chaguang/followees/)
[粉丝 - 7](https://home.cnblogs.com/u/chaguang/followers/)

[+加关注](javascript:void(0);)

1

0

[« ](https://www.cnblogs.com/chaguang/p/8282326.html)上一篇： [vim的使用](https://www.cnblogs.com/chaguang/p/8282326.html)
[» ](https://www.cnblogs.com/chaguang/p/8333891.html)下一篇： [makefile的基本用法](https://www.cnblogs.com/chaguang/p/8333891.html)

posted @ 2018-01-17 21:25 [菜鸟也有高飞的时候](https://www.cnblogs.com/chaguang/) 阅读(18061) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=8306106) [收藏](javascript:void(0))





[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/chaguang/p/8306106.html#)[返回顶部](https://www.cnblogs.com/chaguang/p/8306106.html#top)

登录后才能发表评论，立即 [登录](javascript:void(0);) 或 [注册](javascript:void(0);)， [访问](https://www.cnblogs.com/) 网站首页

[博客园派送云上免费午餐，AWS注册立享12个月免费套餐](https://brands.cnblogs.com/aws/free?source=blog_under_login_tip)

### 公告

昵称： [菜鸟也有高飞的时候](https://home.cnblogs.com/u/chaguang/)
园龄： [4年1个月](https://home.cnblogs.com/u/chaguang/)
粉丝： [7](https://home.cnblogs.com/u/chaguang/followers/)
关注： [0](https://home.cnblogs.com/u/chaguang/followees/)

[+加关注](javascript:void(0))

| [<](javascript:void(0);)2020年11月[>](javascript:void(0);)   |                                                              |      |      |      |      |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---- | ---- | ---- | ---- | ------------------------------------------------------------ |
| 日                                                           | 一                                                           | 二   | 三   | 四   | 五   | 六                                                           |
| 1                                                            | 2                                                            | 3    | 4    | 5    | 6    | 7                                                            |
| 8                                                            | 9                                                            | 10   | 11   | 12   | 13   | 14                                                           |
| 15                                                           | 16                                                           | 17   | 18   | 19   | 20   | [21](https://www.cnblogs.com/chaguang/archive/2020/11/21.html) |
| [22](https://www.cnblogs.com/chaguang/archive/2020/11/22.html) | [23](https://www.cnblogs.com/chaguang/archive/2020/11/23.html) | 24   | 25   | 26   | 27   | 28                                                           |
| 29                                                           | 30                                                           | 1    | 2    | 3    | 4    | 5                                                            |
| 6                                                            | 7                                                            | 8    | 9    | 10   | 11   | 12                                                           |

### 搜索

 

 

### 常用链接

- [我的随笔](https://www.cnblogs.com/chaguang/p/)
- [我的评论](https://www.cnblogs.com/chaguang/MyComments.html)
- [我的参与](https://www.cnblogs.com/chaguang/OtherPosts.html)
- [最新评论](https://www.cnblogs.com/chaguang/RecentComments.html)
- [我的标签](https://www.cnblogs.com/chaguang/tag/)

### 随笔档案

- [2020年11月(3)](https://www.cnblogs.com/chaguang/archive/2020/11.html)
- [2018年6月(1)](https://www.cnblogs.com/chaguang/archive/2018/06.html)
- [2018年5月(1)](https://www.cnblogs.com/chaguang/archive/2018/05.html)
- [2018年4月(1)](https://www.cnblogs.com/chaguang/archive/2018/04.html)
- [2018年3月(12)](https://www.cnblogs.com/chaguang/archive/2018/03.html)
- [2018年2月(5)](https://www.cnblogs.com/chaguang/archive/2018/02.html)
- [2018年1月(6)](https://www.cnblogs.com/chaguang/archive/2018/01.html)
- [2017年12月(9)](https://www.cnblogs.com/chaguang/archive/2017/12.html)
- [2017年11月(5)](https://www.cnblogs.com/chaguang/archive/2017/11.html)
- [2017年10月(7)](https://www.cnblogs.com/chaguang/archive/2017/10.html)
- [2017年7月(6)](https://www.cnblogs.com/chaguang/archive/2017/07.html)
- [2017年6月(1)](https://www.cnblogs.com/chaguang/archive/2017/06.html)
- [2017年4月(1)](https://www.cnblogs.com/chaguang/archive/2017/04.html)
- [2017年3月(6)](https://www.cnblogs.com/chaguang/archive/2017/03.html)
- [2017年2月(2)](https://www.cnblogs.com/chaguang/archive/2017/02.html)

### 最新评论

- [1. Re:PPP协议](https://www.cnblogs.com/chaguang/p/8097967.html)
- 写的很好
- --站在浪潮之巅

### 阅读排行榜

- [1. gcc的基本用法(18060)](https://www.cnblogs.com/chaguang/p/8306106.html)
- [2. 图书管理系统（C++）(15194)](https://www.cnblogs.com/chaguang/p/6368633.html)
- [3. PPP协议(7601)](https://www.cnblogs.com/chaguang/p/8097967.html)
- [4. python中XML模块(6080)](https://www.cnblogs.com/chaguang/p/8510165.html)
- [5. VS2015 中错误 C4996(2659)](https://www.cnblogs.com/chaguang/p/6542390.html)

### 评论排行榜

- [1. PPP协议(1)](https://www.cnblogs.com/chaguang/p/8097967.html)

### 推荐排行榜

- [1. PPP协议(2)](https://www.cnblogs.com/chaguang/p/8097967.html)
- [2. gcc的基本用法(1)](https://www.cnblogs.com/chaguang/p/8306106.html)
- [3. VS2015 中错误 C4996(1)](https://www.cnblogs.com/chaguang/p/6542390.html)
- [4. 图书管理系统（C++）(1)](https://www.cnblogs.com/chaguang/p/6368633.html)

Copyright © 2020 菜鸟也有高飞的时候
Powered by .NET 5.0.0 on Kubernetes

<iframe id="blockbyte-bs-sidebar" class="notranslate" aria-hidden="true" __idm_frm__="231" data-pos="right" style="margin: 0px; padding: 0px; opacity: 0; pointer-events: none; position: fixed; top: 0px; left: auto; width: 350px; max-width: none; height: 0px; z-index: 2147483646; speak: none; border: none; transform: translate3d(350px, 0px, 0px); transition: width 0s ease 0.3s, height 0s ease 0.3s, opacity 0.3s ease 0s, transform 0.3s ease 0s; background-color: rgba(255, 255, 255, 0.8) !important; display: block !important; right: 0px; color: rgb(0, 0, 0); font-family: &quot;PingFang SC&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, &quot;Microsoft Yahei&quot;, sans-serif; font-size: 12px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"></iframe>