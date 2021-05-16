- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/craftor/)
- 
- [联系](https://msg.cnblogs.com/send/Craftor)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/banlieue13/images/xml.gif)](https://www.cnblogs.com/craftor/rss/)

随笔- 71 文章- 0 评论- 89 阅读- 67万 

# [Keil5编译STM32注意事项](https://www.cnblogs.com/craftor/p/3811732.html)

硬件：某STM32开发板，ST-Link/V2

一、硬件相关：

1、引脚连接：

[![image](https://images0.cnblogs.com/blog/156841/201406/271221207893316.png)](https://images0.cnblogs.com/blog/156841/201406/271221195081059.png)

pin7 <—> SWIO

pin9 <—> SWCLK

pin20/pin18 <—> GND

pin19 <—> +3.3V （如果不使用ST-Link给板子供电，不要接）

 

2、Keil中设置：

1）在Debug下，选择ST-Link Debugger

[![image](https://images0.cnblogs.com/blog/156841/201406/271221224452089.png)](https://images0.cnblogs.com/blog/156841/201406/271221217424474.png)

2）选中ST-Link Debugger后，选择Settings。

[![image](https://images0.cnblogs.com/blog/156841/201406/271221236643561.png)](https://images0.cnblogs.com/blog/156841/201406/271221230706446.png)

3）选择Flash Download，然后添加Programming Algroithm。（我这里是STM32F10x的芯片）

[![image](https://images0.cnblogs.com/blog/156841/201406/271221259613462.png)](https://images0.cnblogs.com/blog/156841/201406/271221242267133.png)

 

二、软件相关：

点击这个：

[![image](https://images0.cnblogs.com/blog/156841/201406/271221270088350.png)](https://images0.cnblogs.com/blog/156841/201406/271221264763021.png)

然后看到个：

[![image](https://images0.cnblogs.com/blog/156841/201406/271221297429850.png)](https://images0.cnblogs.com/blog/156841/201406/271221284147878.png)

我这里是一个GPIO的例子，我添加了:CMSIS-Core（必须）、Device->GPIO（GPIO初始化）、Device->Startup（初始代码）、Device->StdPherphDrivers->GPIO（GPIO控制）、Device->StdPherphDrivers->RCC（时钟控制）。

如果编译报错，那肯定是漏了哪个库了。

[![image](https://images0.cnblogs.com/blog/156841/201406/271221313049595.png)](https://images0.cnblogs.com/blog/156841/201406/271221307117779.png)

如果还是编译出错，缺少stm32f10x_conf.h之类的文件，再设置一下这里：

[![image](https://images0.cnblogs.com/blog/156841/201406/271221329456896.png)](https://images0.cnblogs.com/blog/156841/201406/271221320864767.png)

在Define里添加USE_STDPERIPH_DRIVER，在IncludePaths里添加自己工程所在的目录，并把stm32f10x_conf.h复制到工程所在目录下。（stm32f10x_conf.h可以从KeilV5的目录下找到，不要直接指向该文件，因为每个工程可能会根据需要修改）。

如果你的工程还是编译出错，我已经帮不你了，请自己搜索去吧。

分类: [STM32](https://www.cnblogs.com/craftor/category/590854.html)

标签: [Keil](https://www.cnblogs.com/craftor/tag/Keil/), [STM32](https://www.cnblogs.com/craftor/tag/STM32/), [ST-Link](https://www.cnblogs.com/craftor/tag/ST-Link/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)