![PlatformIO IDE(VSCode) 基本使用 - 新建项目](https://pic4.zhimg.com/v2-35664bc621389c176ef2941c3f6aefac_1440w.jpg?source=172ae18b)

# PlatformIO IDE(VSCode) 基本使用 - 新建项目

[![十里](https://pic1.zhimg.com/v2-8669cb4c5ad6f02e511061b82dfb63f6_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/smslit)

[十里](https://www.zhihu.com/people/smslit)[](https://www.zhihu.com/question/48510028)

中国石油大学（华东） 控制工程硕士

28 人赞同了该文章

PlatformIO IDE (VSCode) 可以帮助我们更好地使用 PlatforIO，一个 MCU 项目的开始那就是新建，本文就讲解一下如果使用 PlatformIO IDE 新建一个 MCU 的项目。

## 1. 基本概念

在使用 PlatformIO 的过程中经常会遇到一些词，比如 Platform 、 Framworks 以及 Boards，在新建项目之前有必要先说明一下，这些具体都代表了什么！

### 1.1 Platform

直译的话就是 **平台**，具体就是指的芯片平台，再详细一点那就是各个公司具体的系列芯片的开发平台了。目前为止 PIO[[1\]](https://zhuanlan.zhihu.com/p/78722930#ref_1) 针对支持的平台都有以下功能支撑：

- 支持指定框架的基于脚本的编译构建系统
- 针对各公司常规开发板的预配置
- 提供多架构的构建工具及相关工具链的支持

PIO 目前支持的平台分为嵌入式和桌面两大类。

- 嵌入式平台

- - [Aceinna IMU](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/aceinna_imu.html)
  - [Atmel AVR](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/atmelavr.html)
  - [Atmel SAM](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/atmelsam.html)
  - [Espressif 32](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/espressif32.html)
  - [Espressif 8266](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/espressif8266.html)
  - [Freescale Kinetis](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/freescalekinetis.html)
  - [Infineon XMC](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/infineonxmc.html)
  - [Intel ARC32](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/intel_arc32.html)
  - [Intel MCS-51 (8051)](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/intel_mcs51.html)
  - [Kendryte K210](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/kendryte210.html)
  - [Lattice iCE40](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/lattice_ice40.html)
  - [Maxim 32](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/maxim32.html)
  - [Microchip PIC32](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/microchippic32.html)
  - [Nordic nRF51](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/nordicnrf51.html)
  - [Nordic nRF52](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/nordicnrf52.html)
  - [NXP LPC](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/nxplpc.html)
  - [RISC-V GAP](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/riscv_gap.html)
  - [Samsung ARTIK](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/samsung_artik.html)
  - [SiFive](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/sifive.html)
  - [Silicon Labs EFM32](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/siliconlabsefm32.html)
  - [ST STM32](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/ststm32.html)
  - [ST STM8](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/ststm8.html)
  - [Teensy](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/teensy.html)
  - [TI MSP430](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/timsp430.html)
  - [TI TIVA](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/titiva.html)
  - [WIZNet W7500](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/wiznet7500.html)

- 桌面平台

- - [Native](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/native.html)
  - [Linux ARM](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/linux_arm.html)
  - [Linux i686](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/linux_i686.html)
  - [Linux x86_64](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/linux_x86_64.html)
  - [Windows x86](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/platforms/windows_x86.html)

上面也有前面文章中使用到的 ST STM32，Atmel AVR 一般指的就是 Arduino 系列开发板使用的芯片，说到 Arduino ，它其实就是一个完整的生态，提供开源的硬件开发板的设计以及 Arduino 统一的软件开发包就是所谓的 Frameworks。

### 1.2 Frameworks

上面已经提到 Frameworks 其实就是类似于 SDK 的一个东西，全世界最有名的 Arduino 有自家的一套 SDK，那就是 Arduino，框架基本特征就是提供一整套一致的 API 的集合，本质是一个官方或第三方提供的软件库。

因为 Arduino 极具影响力，所以很多芯片平台也都有了自己的 Arduino 框架，现在 Arduino 框架平台支持的平台有很多：Atmel AVR、Atmel SAM、Espressif 32、Espressif 8266、Infineon XMC、Intel ARC32、Kendryte K210、Microchip PIC32、Nordic nRF51、Nordic nRF52、T STM32、ST STM8 、Teensy、TI MSP430 、TI TIVA [[2\]](https://zhuanlan.zhihu.com/p/78722930#ref_2)。

反过来讲，一个平台有可能支持多个不同开发框架，比如 **ST STM32** 支持的开发框架有：Arduino、CMSIS、libOpenCM3、mbed、SPL、STM32Cube[[3\]](https://zhuanlan.zhihu.com/p/78722930#ref_3)。

PIO 支持的框架也是有很多，总有适合你的：

- Arduino
- ARTIK SDK
- CMSIS
- ESP8266 Non-OS SDK
- ESP8266 RTOS SDK
- ESP-IDF
- Freedom E SDK
- Kendryte FreeRTOS SDK
- Kendryte Standalone SDK
- libOpenCM3
- mbed
- PULP OS
- Pumbaa
- Simba
- SPL
- STM32Cube
- Tizen RT
- WiringPi

详见：[https://docs.platformio.org/en/latest/frameworks/index.html](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/frameworks/index.html)

### 1.3 Boards

PIO 支持绝大部分流行的开发板，比如 Arduino 的全系开发板、STM32 的 Nucleo 和 Discovery 系列评估板。有太多太多了，这里就没必要一一罗列了，可以查看下面的链接了解更多关于开发板的支持列表：

[https://docs.platformio.org/en/latest/boards/index.html](https://link.zhihu.com/?target=https%3A//docs.platformio.org/en/latest/boards/index.html)

PIO 针对支持的开发板都提供完整的项目生成脚本，新建项目从未如此快捷和简单！

## 2. 新建项目

这里我们以新建一个 **Arduino Leonardo** 的项目为例。

- 打开 PIO Home：打开新的 VSCode 的窗口，点击左下角状态栏的第三个小房子按钮，就能打开 PIO Home 页面了：

![img](https://pic3.zhimg.com/v2-6918dd74d5f8235bf2331de249633312_r.jpg)

- 点击项目操作按钮的 **+ New Project**，在弹窗中分别填入或选择 Name、Board、Framework 点击 Finish：

![img](https://pic2.zhimg.com/v2-fd8c07edeedd57679083ca6650b2c245_r.jpg)

- 稍作等待，PIO 会自动根据选择的 Board 和 Framework 配置工程并且下载需要用到的编译工具，需要的编译依赖什么的 PIO 通通帮我们搞定，一段时间过后项目工程就新建完成了，打开 `src` 文件夹下的 `main.cpp` 如下：

![img](https://pic1.zhimg.com/v2-822a481af09b463296bf6c63a7f65534_r.jpg)

## 3. 项目文件结构

项目文件结构要了解一下，方便后期自己手动管理项目。

- **.pio**，存放工程编译产生的文件
- **.vscode**, 存放针对工程定制化的 vscode 配置文件
- **include**，存放统一管理的 h 头文件
- **lib**，存放自己编写的库文件
- **src**，存放工程项目的 C/C++ 源文件
- **test**，存放工程项目的测试文件，一般用不到
- **.gitignore**，git 仓库的忽略文件，方便 git 进行工程项目的版本控制
- **travis.yml**，持续集成的配置文件，一般用不到
- **platformio.ini**，项目的核心配置文件，这个会经常用到，所以得了解其中可用的配置项[[4\]](https://zhuanlan.zhihu.com/p/78722930#ref_4)

## 4. 编译和上传

新建了项目工程之后，就是进行开发了，必然要用到编译代码，要将编译生成的二进制文件上传到开发板的芯片中。

为了看到效果，我们编写一段让板载 LED 闪动的实现：

```cpp
#include <Arduino.h>

void setup() {
  // put your setup code here, to run once:
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

在这之前有必要了解一下 PIO 的工具栏按钮：

![img](https://pic3.zhimg.com/v2-fd15f6ef5c36a9e9dd20ff782426ee52_r.jpg)

**Tip:**

如果使用 Arduino 框架代码中，一定要包含头文件 `Arduino.h`。

### 4.1 编译项目工程

将上面的代码录入 `src` 目录下的 `main.cpp` 文件中，看文件名就知道使用的是 c++ 编程语言了。多种方式可以触发编译，比如笔者经常用的两种方式：

- 点击上面截图底部中工具栏的第二个对号图标
- 按下组合键 `CTRL` + `ALT` + `B`

还有两种方式可以触发编译任务：

- 按下组合键 `CTRL` + `SHIFT` + `P` (macOS 下是 `COMMAND` + `SHIFT` + `P`)，然后输入关键字 **platformio**，选择 **Build**
- 点击窗口左边栏的蚂蚁头的图标会打开 PlatformIO 的工具栏，点击其中的 **Build**

顺利的话，触发了编译，很快就会在终端窗口提示编译完成：

```bash
> Executing task: platformio run <

Processing leonardo (platform: atmelavr; board: leonardo; framework: arduino)
------------------------------------------------------------------------------------
Verbose mode can be enabled via `-v, --verbose` option
CONFIGURATION: https://docs.platformio.org/page/boards/atmelavr/leonardo.html
PLATFORM: Atmel AVR 1.15.0 > Arduino Leonardo
HARDWARE: ATMEGA32U4 16MHz, 2.50KB RAM, 28KB Flash
PACKAGES: toolchain-atmelavr 1.50400.190710 (5.4.0), framework-arduinoavr 4.1.1
LDF: Library Dependency Finder -> http://bit.ly/configure-pio-ldf
LDF Modes: Finder ~ chain, Compatibility ~ soft
Found 7 compatible libraries
Scanning dependencies...
No dependencies
Checking size .pio/build/leonardo/firmware.elf
Memory Usage -> http://bit.ly/pio-memory-usage
DATA:    [=         ]   5.8% (used 149 bytes from 2560 bytes)
PROGRAM: [=         ]  14.4% (used 4130 bytes from 28672 bytes)
============================ [SUCCESS] Took 0.66 seconds ============================
```

### 4.2 上传

先把手头的 Arduino Leonardo 开发板与电脑连接，直接触发上传任务即可，甚至不用自己去选择接口，PlatformIO 会自动查找与电脑连接的端口进行判断然后上传程序，笔者经常会用到的触发方式：

- 组合键 `CTRL` + `ALT` + `U`
- 点击窗口状态栏中 PIO 工具栏的第三个按钮**→**

第一次上传程序的时候，PIO 往往会先根据板子芯片对应的平台选择合适的上传工具包，所以第一次上传可能需要等一会儿，顺利的话也会在终端窗口看到 **Sucess** 的消息，同时会看到 Leonardo 板载 LED 开始闪烁：

<iframe frameborder="0" allowfullscreen="" src="https://www.zhihu.com/video/1146566471055507456?autoplay=false&amp;useMSE=" style="border: none; display: block; width: 688.008px; height: 387px;"></iframe>

Blink Here

## 总结

PIO 让新建芯片开发的项目工程变得异常简单，只需几小步就可以完成，另外本文也简单说了一下程序的编译和上传操作，同样简单方便！希望本文能够帮助想要体会 PlatformIO 魅力的朋友！

------

**博客原文：**

[PlatformIO IDE(VSCode) 基本使用 - 新建项目www.smslit.top![图标](https://pic2.zhimg.com/v2-3087a6b044514cf05dec9bea15077529_180x120.jpg)](https://link.zhihu.com/?target=https%3A//www.smslit.top/2019/08/18/platformio-newproject/)



## 参考

1. [^](https://zhuanlan.zhihu.com/p/78722930#ref_1_0)PIO 是 PlatformIO 的简称，后面系列文章会经常使用这个简称
2. [^](https://zhuanlan.zhihu.com/p/78722930#ref_2_0)更多关于 Arduino 框架的信息参考：https://docs.platformio.org/en/latest/frameworks/arduino.html
3. [^](https://zhuanlan.zhihu.com/p/78722930#ref_3_0)更多关于 stm32 单片机开发平台的信息参考：https://docs.platformio.org/en/latest/platforms/ststm32.html
4. [^](https://zhuanlan.zhihu.com/p/78722930#ref_4_0)PIO 是 PlatformIO 的简称，后面系列文章会经常使用这个简称

发布于 2019-08-18

[Arduino](https://www.zhihu.com/topic/19581430)

[MCU程序设计](https://www.zhihu.com/topic/19654662)