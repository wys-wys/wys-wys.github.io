# windows下MinGW安装

[![img](https://upload.jianshu.io/users/upload_avatars/9565709/737fc504-3a58-4fe0-ab58-32f671150d97.png?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/c6c90d0f734f)

[aaa小菜鸡](https://www.jianshu.com/u/c6c90d0f734f)关注

2018.11.19 15:33:40字数 351阅读 1,420

背景：只是想学习C++，单独测试C++中的各种东西，而VS这种得建个工程，每个工程还只能有一个main，对于我的需求来说很不方便。

解决：使用gcc比较方便，而且有助于理解编译过程
参考：[Windows 下使用 GCC](https://www.cnblogs.com/valor-xh/p/7371710.html)

1. https://sourceforge.net/projects/mingw/files/ 下载
2. 继续到最后不知道该勾选什么，于是按照博客里，先关掉弹出的窗口，将`安装目录\bin`添加到系统环境变量
3. cmd中`mingw-get install gcc`（如果想安装 g++、gdb，则输入命令`mingw-get install g++`和`mingw-get install gdb`）
4. 查看版本：`gcc -v`

使用：
参考：[【C++ 学习笔记】 用G++编译和运行C++程序](https://www.cnblogs.com/xiaoka/archive/2012/07/24/2607408.html)

1. 编译：`g++ -c test.cpp -o test.o`
2. 链接：`g++ test1.o test2.o -o test.exe`
3. 执行：`test.exe`

直接编译成可执行文件：`g++ test.cpp -o test.exe`

还有很多不懂，继续学习再添加

- 哎，运行时各种基本的错误（测试时变量的地址什么的输出的是错的），无法直视，莫名其妙，再装个codeblocks，换成codeblocks\mingw\bin也是同样的错误......不过没问题的话，配好了sublime用还挺方便的...省去了cmd下运行2个命令才能运行