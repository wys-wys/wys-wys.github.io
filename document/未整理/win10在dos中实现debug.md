# win10实现debug

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[neverR-M](https://blog.csdn.net/believe__dream) 2016-04-05 23:16:27 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 10808 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 6

分类专栏： [系统和软件](https://blog.csdn.net/believe__dream/category_2889861.html)

版权

Win10木有debug，首先需要让win10可以运行debug。

1、 安装虚拟机：

在网上下载的VMware Workstation 12 Player虚拟机

![img](https://img-blog.csdn.net/20160405231303107?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

装好虚拟机之后安装了xp系统，但是发现虚拟机安好之后运行debug只是在虚拟机里边可以debug，在win10系统里边并不可以像网上一样进行debug。![img](https://img-blog.csdn.net/20160405231341139?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



所以用了网上说的第二种方法：DOSBox

1、 DOSBox

云心DOSBox之后

![img](https://img-blog.csdn.net/20160405231428764?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



这个时候就可以进行debug了。

输入mount C D:\ 这个指令时将D盘作为debug的C盘(下载的debug.exe文件存在D盘中)，接下来输入C：就是进入debug的C盘最后debug命令之后就可以进行debug了。

网上debug常用命令：http://llhh921.blog.sohu.com/67306527.html

在运行debug时查看基本命令：

![img](https://img-blog.csdn.net/20160405231508092?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



用debug读取debug盘中的a.txt文件——直接输入命令debug a.txt，在之后出现的-后边输入d 100，就可以查看文件了

![img](https://img-blog.csdn.net/20160405231538124?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

这样就完成了在win10下用debug读取文件咯！！

# 常用debug命令http://llhh921.blog.sohu.com/67306527.html

|      |                                                              |
| ---- | ------------------------------------------------------------ |
| 正文 |                                                              |
|      | 汇编语言调试DEBUG命令详解分类：[编程技术](http://llhh921.blog.sohu.com/entry/5261330/)2007-10-15 20:04阅读(4639)[评论(0)](http://llhh921.blog.sohu.com/67306527.html#commentForm) 汇编语言作为一道独特的风景,一直扮演着很重要的角色.我简单介绍下汇编语言调试程序DEBUG命令,要灵活运用还要靠自己不断的实践.1、显示命令D ① D [地址] ② D [范围]如不指定范围，一次显示8行×16个字节。  －D ；默认段寄存器为DS，当前偏移地址  －D DS:100 / －D CS:200  －D 200:100  －D 200；200为偏移地址，默认段寄存器DS  －D DS:100 110/ －D 100 L 102.修改命令E    ① E 地址 ；从指定地址开始，修改（或连续修改）存储单元内容。DEBUG首先显示指定单元内容，如要修改，可输入新数据；空格键显示下一个单元内容并可修改，减号键显示上一个单元内容并可修改；如不修改，可直接按空格键或减号键；回车键结束命令。    ② E 地址 数据表；从指定的地址开始用数据表给定的数据修改存储单元。  －E DS:100 F3 ‘AB’ 8D。3.添充命令F    F 范围 数据表；  将数据表写入指定范围的存储单元；数据个数多，忽略多出的数据，个数少，则重复使用数据表。  －F DS:0 L5 01,02,03,04,05  －F DS:0 L5 01 02 03 04 05（空格分隔）  －F DS:0 L5 FF ；5个字节重复使用FF 4.显示修改寄存器命令R    R；★显示所有寄存器和标志位状态；       ★显示当前CS：IP指向的指令。    显示标志时使用的符号：    标志          标志=1     标志=0    OF           OV        NV    DF           DN        UP    IF            EI         DI    SF           NG        PL    ZF           ZR        NZ    AF           AC        NA    PF           PE         PO    CF           CY        NC5.汇编命令A    A [地址]；从指定的地址开始输入符号指令；如省略地址，则接着上一个A命令的最后一个单元开始；若第一次使用A命令省略地址，则从当前CS:IP开始（通常是CS：100）。    注释:①在DEBUG下编写简单程序即使用A命令。    ②每条指令后要按回车。    ③不输入指令按回车，或按Ctrl+C结束汇编。    ④支持所有8086符号硬指令，伪指令只支持DB、DW，不支持各类符号名。6.反汇编命令U    ① U [地址]；从指定地址开始反汇编32个字节的机器指令；省略地址时,则接着上一个U命令的最后一个单元开始；若第一次使用U命令省略地址，则从当前CS:IP开始（通常是CS：100）。    ② U 范围；对指定范围的单元进行反汇编。  －U  －U100  －U100L107.运行程序命令G    ① G；从CS:IP指向的指令开始执行程序，直到程序结束或遇到INT 3。    ② G=地址；从指定地址开始执行程序，直到程序结束或遇到INT 3。    ③ G 断点1[，断点2，…断点10]；从CS:IP指向的指令开始执行程序，直到遇到断点。    ④G=地址 断点1[，断点2，…断点10]  －G ；从CS:IP指向的指令开始执行程序。  －G=100 ；从指定地址开始执行程序。  －G=100 105 110 1208.跟踪命令（单步执行命令）T    ① T；从当前IP开始执行一条指令。    ② T 数值；从当前IP开始执行多条指令。    ② T =地址；    ③ T =地址 数值；  －T  －T5 / －T=100  59.跟踪执行并跳过子程序命令P    P [=地址] [数值]；类似T命令，但跳过子程序和中断服务程序。10.退出DEBUG命令Q    Q；返回DOS环境。   －Q11.命名命令N    N 文件标示符；指定文件，以便用W命令在磁盘上生成该文件，或者用L命令从磁盘装入该文件。    －N MY_PRO.COM    写盘：在当前盘当前目录生成指定文件。    读盘：在当前盘当前目录读取指定文件。  － N A:\ USER \ MY_PRO.COM12.装入命令L    ① L [地址]；装入N命令指定的文件，默认的内存地址为CS：100。     －N MY_PRO.COM     －L    ② L 地址 驱动器号 扇区号 扇区数；将某驱动器的若干扇区（最多80H个）装入内存；     0=A，1=B，2=C……；默认的段地址为CS。     －L DS:200 2 0 113.写盘命令W    ① W [地址]；将指定地址开始的内存数据写入磁盘，生成N命令指定的文件；默认的内存地址为CS:100；写盘的字节数由BX(高位字)和CX(低位字)决定，可执行程序写盘时，文件扩展名应指定.COM。     －N MY_PRO.COM     －W    ② W 地址 驱动器号 扇区号 扇区数；将内存数据写入磁盘的若干扇区（最多80H）；默认的段地址为CS。   －W DS:0 2 0 1  注释：写磁盘扇区要慎用14.其他命令    （1）比较命令C     C 范围 地址；将指定范围内的内容与以指定地址为起点的内容相比较。    （2）16进制数计算命令H     H 数1，数2（H 数1 数2）；同时计算两个数字的和与差。    （3）查找命令S     S 范围 数据；在指定范围内查找指定数据。    （4）输入命令I     I 端口地址；输入一个字节并显示。    （5）输出命令O     O 端口地址 字节数据；输出到指定的端口。    （6）传送命令M     M 范围 地址；将指定范围的内容传送到以指定地址为起点的存储单元。 最后修改于 2007-10-15 20:06   阅读(4639)[评论(0)](http://llhh921.blog.sohu.com/67306527.html#commentForm) |