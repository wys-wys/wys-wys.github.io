# 【arduino】【u8g2库】OLED屏-U8glib库 增强版 U8G2库

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[动手党](https://blog.csdn.net/g1fdgfgdf2_) 2017-12-14 13:05:22 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 31776 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 105

分类专栏： [arduino](https://blog.csdn.net/g1fdgfgdf2_/category_7307092.html)

转载请注明: 冬菇不败  及出处 ：http://www.arduino.cn/thread-41193-1-1.html
以下的函数描述是源自原文： https://github.com/olikraus/u8g2/wiki/u8g2reference#begin
自己再通过测试后才发布，采用一个更新方式（精力有限，学习为主），客官觉得不错，就打赏一下呗~
U8G2是U8GLIB的增强版，相对旧版更加好用，强大，兼容板子多。U8G2有两种模式：U8g2是增强版模式，U8X8是简便模式省内存，在setup（）里必须设定模式.
函数开始前，先讲一个东西。arduino 和OLED连接的方法（示例NANO和128X64 API OLED）
![img](http://www.arduino.cn/data/attachment/forum/201701/09/153401q4czcfp44rf6kv1a.jpg)
颜色对颜色线连接。
nano的板子上的D4567脚可以修改。不修改也行。

SCL=S&COLCK //时钟   SDA=S&DATA //数据     RES/RST = Reset //复位    D/C = DC
API连接这4条交互线就行了，和另外供电。 那么在代码中一开始必须定义好脚： （D3号脚可以不接）

U8G2_SSD1306_128X64_NONAME_1_4W_SW_SPI u8g2 (U8G2_R0, /* clock=*/ 4, /* data=*/ 5, /* cs=*/ 3, /* dc=*/ 6, /* reset=*/ 7);  //这个定义脚代码细心看就懂了。

//U8G2支持的OLED控制芯片： https://github.com/olikraus/u8g2/wiki/gallery
//不同芯片的不同脚定义代码： https://github.com/olikraus/u8g2/wiki/u8g2setupcpp
例子：

1. 
2. \#include <Arduino.h>
3. \#include <SPI.h>
4. \#include <U8g2lib.h>
5. 
6. U8G2_SSD1306_128X64_NONAME_1_4W_SW_SPI u8g2(U8G2_R0, /* clock=*/ 4, /* data=*/ 5, /* cs=*/ 3, /* dc=*/ 6, /* reset=*/ 7);
7. 
8. void setup(void) {
9.  u8g2.begin();  //选择U8G2模式，或者U8X8模式
10. }
11. 
12. void loop(void) {
13.  u8g2.firstPage();
14.  do {
15.   u8g2.setFont(u8g2_font_ncenB14_tr);
16.   u8g2.drawStr(0,15,"Hello World!");
17.  } while ( u8g2.nextPage() );
18.  delay(1000);
19. }
20. 

复制代码

U8G2_R0 是一个参数： 指定大局显示的基本布局:

| 布局        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| U8G2_R0     | 正常显示                                                     |
| U8G2_R1     | 90度顺时针旋转                                               |
| U8G2_R2     | 180度顺时针旋转                                              |
| U8G2_R3     | 270度顺时针旋转                                              |
| U8G2_MIRROR | 正常显示镜像内容（v2.6.x版本以上使用)      注意:U8G2_MIRROR需要与setFlipMode（）配搭使用. |

![img](http://www.arduino.cn/data/attachment/forum/201701/09/160002s72c22zdl77a3390.png)





------------------------------------------------- 屏幕基本函数 -------------------------------------------
**u8g2.begin( )**   //开始构造U8G2, 在setup()内使用。   特别说明： 初始化在 Arduino的环境。 配置OLED的显示模式initDiplay或者省电模式setPowerSave,或者重置（清屏）clearDisplay 。同时检测六个按钮程序（比如前进、后退、确认、上一级...）。如果没有，可以在里定义按钮事件的引脚，用GetMenuEvent函数来定义，来进入到用户想要的界面，详情就看 userInterfaceMessage 和 GetMenuEvent 函数。无返回值。
 关联使用函数：initDispaly 、setPowersave、clearDisplay、

**u8g2.clear()**  // 清除缓冲区"Buffer"内的所有像素点
  关联使用函数：print、home、clearBuffer


**u8g2.clearBuffer()**  //清除内存中的所有缓冲区内的像素，而后可以用sendBuffer函数来把缓冲区“Buffer”在屏幕上显示出来，以便清屏。因这个过程是在微处理器中RAM里的副本"Buffer"中进行，标志“F”，所以 sendBuffer也就是直接操作副本“Buffer”。
   关联使用函数：sendBuffer 例子：

1. 
2. void loop(void) {
3. u8g2.clearBuffer();  //清除当前Buffer内的像素
4. ​                  // 在Buffer内一些操作 
5. u8g2.sendBuffer();  //发送Buffer内容到屏上
6. delay(1000);
7. 

复制代码



**u8g2.clearDisplay()**  //清除显示中所有像素。此过程在begin()中调用。在程序中一般用不上，也是通过sendBuffer和clearBuffer函数显示出来，一样的处理方式。
关联使用函数：begin
**
****u8g2.disableUTF8Print()** //禁用 UTF8字集 （万国语字库），默认是开启的。 关联使用函数：print 、enableUTF8Print 

**u8g2.enableUTF8Print ()**   //启用 UTF8字集，许可UniCode向print发送字符串。这个函数通常在begin（）后调用。
关联使用函数：print、disableUTF8Print
例子：

1. 
2. void setup(void) {
3.  u8g2.begin();
4.  u8g2.enableUTF8Print();    // 使print支持UTF8字集
5. }
6. 

复制代码


**u8g2.Print()**   //在入当前光标位置用当前设置的字体，来打印出（内容）。光标位置可以用setCursor函数 。字体可以用setFont函数。
关联使用函数：print(U8x8)、enableUTF8Print、setFont、setCursor、
例子：

1. u8g2.setFont(u8g2_font_ncenB14_tr); //设置字体
2. u8g2.setCursor(0, 15);  //设置光标处
3. u8g2.print("Hello World!"); //输出内容
4. 

复制代码

U8x8： 一个自带字库，详情见setFont函数

------------------------------------------------- 绘图显示函数 -------------------------------------------
**u8g2.** **drawBitMap()**  //在指定的x / y位置（位图左上角）绘制位图.。位图的部分可能位于显示边界之外。位图由数组位图指定。清除位意味着：不绘制像素。数组内的一个置位意味着：用当前颜色索引写像素。对于单色显示器，颜色索引0通常会清除一个像素，并且颜色索引1将设置一个像素。 因为复杂耗内存，此函数在U8G2中被停用！ 格式：u8g2.drawBitMap (x，y，cnt，h)
参数：  x是水平线位置
       y是垂直线位置
       cnt是点阵图字节数，宽是1字节*8（这个字节数必须控制好，否则点阵图会出现扭曲）
       h是点阵图高度

**u8g2.drawBox()**   //画个实心方形
格式：u8g2.drawBitMap (x，y，w，h)
参数：  x是水平线起始位置
       y是垂直线 起始 位置
       w是方形的宽
       h是 方形的 高
例子：

1. 
2. \#include <Arduino.h>
3. \#include <SPI.h>
4. \#include <U8g2lib.h>
5. 
6. U8G2_SSD1306_128X64_NONAME_1_4W_SW_SPI u8g2(U8G2_R0, /* clock=*/ 4, /* data=*/ 5, /* cs=*/ 3, /* dc=*/ 6, /* reset=*/ 7);
7. 
8. void setup(void) {
9.  u8g2.begin();
10. }
11. 
12. void loop(void) {
13. u8g2.firstPage();
14. do {
15. u8g2.drawBox(48,20,25,15); //（起始X，起始Y，方形的宽W，方形的高H）
16. } while ( u8g2.nextPage() );
17. delay(1000);
18. }
19. 

复制代码

![img](http://www.arduino.cn/data/attachment/forum/201701/09/182732yacjgxou5w26ayxz.jpg)


**u8g2.drawCircle()**    //画个空心圆，可选四个方向的半圆
类似与关联函数：drawDisc 、setDrawColor格式：u8g2.drawCircle(x， y ，rad，opt); // X,YS是绘图起始位置（圆的中心点），rad是圆的四分之一弧度。 opt是选项：

U8G2_DRAW_UPPER_RIGHT   //左上角弧度

U8G2_DRAW_UPPER_LEFT   //右上角弧度

U8G2_DRAW_LOWER_LEFT  //左下角幅度

U8G2_DRAW_LOWER_RIGHT   //右下角幅度

U8G2_DRAW_ALL    //全圆

例子：

1. 
2. void loop(void) {
3. u8g2.firstPage();
4. do {
5. u8g2.drawCircle(48, 30, 10, U8G2_DRAW_LOWER_LEFT);
6. } while ( u8g2.nextPage() );
7. delay(1000);
8. }
9. 

复制代码

![img](http://www.arduino.cn/data/attachment/forum/201701/09/184203nwxia0z003p00hui.jpg) ![img](http://www.arduino.cn/data/attachment/forum/201701/09/184203rwunvvn4zm92wvzv.png)


u8g2.drawDisc()   //画个实心圆，使用法跟drawCircle 一个饼样。多普达手机不好使，图片将就看。
![img](http://www.arduino.cn/data/attachment/forum/201701/09/184818lrrc4ecdhbji4ecb.png)

**U8G2.drawEllipse()**    //画一个空心椭圆形，实际上，和画圆是非常相似的用法。格式：u8g2.drawEllipse(X，Y, RX, RY, OPT);

参数： X，Y是椭圆形中心坐标

​      RX是椭圆形水平线的RAD，RY是垂直线的RAD

​       opt是选项：

U8G2_DRAW_UPPER_RIGHT   //左上角弧度

U8G2_DRAW_UPPER_LEFT   //右上角弧度

U8G2_DRAW_LOWER_LEFT  //左下角幅度

U8G2_DRAW_LOWER_RIGHT   //右下角幅度

U8G2_DRAW_ALL    //全圆

例子：

void loop(void) {

u8g2.firstPage();

do {

u8g2.drawEllipse(48, 30, 15, 10, U8G2_DRAW_ALL);

} while ( u8g2.nextPage() );

delay(1000);

}

、 ![img](http://www.arduino.cn/data/attachment/forum/201701/09/215756tnzvzf1chguznm0v.png) ![img](http://www.arduino.cn/data/attachment/forum/201701/09/215536q95ovsd5f9smc8ns.png)


**
u8g2.drawFilledEllipse()**   //画一个实心椭圆形，与u8g2.drawEllipse用法也是一个饼样
![img](http://www.arduino.cn/data/attachment/forum/201701/09/220740lmt3pv5ivnmuppnn.png)


**u8g2.DrawFrame**   //画一个空心方框格式：
u8g2.drawFrame(X，Y，W，H);  // X，Y是方框的左上角坐标，W,H是宽和高，注意，如果方框比屏大，则多出部分不绘画，也就是说不耗内存和出现错图。
例子：
void loop(void) {
u8g2.firstPage();
do {
u8g2.drawFrame(48,30,25,15);
} while ( u8g2.nextPage() );
delay(1000);
}



![img](http://www.arduino.cn/data/attachment/forum/201701/09/221505qh7llea5762q2f58.png) ![img](http://www.arduino.cn/data/attachment/forum/201701/09/221504crc80zxrdd8xrcr6.png)





**u8g2.drawGlyph()**  //绘制字集里的符号，这个功能很帅。

格式：u8g2.drawGlyph(X, Y, 字集代码);  // XY依然是坐标，字集需要先设置字体，然后参考示图选择符号输出，如下图

例子：

void loop(void) {

u8g2.firstPage();

do {

u8g2.setFont(u8g2_font_unifont_t_symbols);  //先设置字体字集

u8g2.drawGlyph(48, 40, 0x2603);               //输出代码

} while ( u8g2.nextPage() );

delay(1000);

}



![img](http://www.arduino.cn/data/attachment/forum/201701/09/222242wts4sximxshs2xun.png) ![img](http://www.arduino.cn/data/attachment/forum/201701/09/222241jmmv8v6mvemm2m8l.png) ![img](http://www.arduino.cn/data/attachment/forum/201701/09/222501z8tqay9dls48hb9w.png)



**u8g.drawLine()**   //画一条平面直线
格式：u8g.drawLine(x0, y0, x1, y1);  //x0,y0是直线起始位置， x1，y1是直线终止位置。例子：
u8g.drawLine(20, 5, 5, 32);
![img](http://www.arduino.cn/data/attachment/forum/201701/10/155521kz8i6ww69gwmv14q.png)
**drawPixel()**   //画一个点，一个点的像素。
格式：drawPixel(x，y)    //x,y是画点的位置。（宽，高）


**u8g2.drawRFrame()**   //画一个圆角空心方形 
**u8g2.drawRBox()**  //画一个圆角实心方形
特别说明：关于这两个代码，综合一下U8G2里面关于画四边形的函数：drawBox（实心），drawFrame（空心）这两个是直角四边形。然而 drawRBox（实心），drawRFrame（空心） 这两个带R的是圆角四边形的。Box是实心，Frame是空心，带R的都是圆角。
参数：两个函数的参数排放一样： （X起始位，Y 起始位 ，W宽度，H高度，R圆角的半径（至少R<XY）） 
例子：

1. 
2. void loop() { 
3.  u8g2.firstPage();
4.  do { 
5.  u8g2.drawRFrame(20,17,30,22,7);
6.  u8g2.drawRBox(80,25,20,25,5);
7.  } while( u8g2.nextPage());
8.  }  
9. 

复制代码


![img](http://www.arduino.cn/data/attachment/forum/201701/10/161936l55rlsqjbr518b5b.png)
  ps:任何一个形状如果XY初始位置放不好（至少没有位置能全部绘制出W*H），就会出现一下图。多出的图形不会绘制，也就是说不会浪费内存。

![img](http://www.arduino.cn/data/attachment/forum/201701/10/162503lzt9ug91t553sgzt.png)

u8g2.drawStr()  //绘制字符串，可以想象字符串是一串符号，它能输出什么“字符串”在屏上。取决于它的setFont被设置的字体集。
说明：一般都配搭着setFont函数使用，当然，如果不需要其它的字体集，在一开始begin（）后设置，全局。字体集详情看setFont函数。一下是三个实例图。
格式：u8g2.drawStr(X, Y, S );  //S记得加“”。
![img](http://www.arduino.cn/data/attachment/forum/201701/10/164832qy95xrb9ropomeyx.png) 
特别注意，它的初始点XY是在左下角： ![img](http://www.arduino.cn/data/attachment/forum/201701/10/165310olc0d7clslmdo42u.png)

**u8g.drawTriangle()** //绘制实体三角形
格式：u8g.drawTriangle(X0,Y0, X1,Y1, X2,Y2);

X0,Y0 ：第一个角位置

X1,Y1 ：第二个角位置

X2,Y2 ：第三个脚位置

例子：

u8g.drawTriangle(20,5, 27,50, 5,32); //至于如何控制显示要预想的位置，看多几次图片就明白了，很简单。

![img](http://www.arduino.cn/data/attachment/forum/201701/10/165939xn8zk4nauuovsx8a.png)



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞22
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论2](https://blog.csdn.net/g1fdgfgdf2_/article/details/78801454#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏105](javascript:;)
- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarReport.png)举报
- [关注](javascript:;)
- 一键三连