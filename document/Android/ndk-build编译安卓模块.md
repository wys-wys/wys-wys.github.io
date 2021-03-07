### 2、ndk-build编译

首先，我们先将ndk-build命令加入环境变量，该命令一般位于ndk安装目录下，我安在F:\android下，因此我的ndk-build命令路径为F:\android\android-ndk-r11b，参考gcc编译方式中的adb环境变量设置，将此路径加入到android变量中即可，注意用分号隔开。

使用ndk-build工具，必须先有一个Android工程。我们可以使用sdk开发包中的tools目录下的android脚本来生成。首先我们列出Android SDK中所有已经按照的SDK平台版本。在sdk\toos目录下执行以下命令：

```cpp
android list
```

执行这条命令后，会列出很多个SDK版本，在这里选择其中一个版本作为我们建立项目的版本号，记住该版本的id

接下来创建Android工程，执行以下命令：

```apache
android create project -n hello2 -p hello2 -t 9 -k com.droider.hello2 -a MyActivity
```

命令行说明：-n 指定工程名称，-t 指定平台版本号，这里可以输入刚才选择版本号的id，-k 指定工程包名，-a 指定默认Actitivy名称。

执行完以上命令后，会看到tools目录下生成了hello2的工程。

下一步，进入工程根目录，新建jni文件夹，并将我们最开始编写的hello.c文件复制进去。接着编写ndk-build所需要的脚本文件，主要是Android.mk与Application.mk两个脚本，Application.mk可选，我们暂时不使用，这里我们只使用Android.mk文件，该文件是工程的编译脚本，描述了编译原生程序所需的编译选项，头文件，源文件及依赖库等。

新建Android.mk，文件内容如下：

```makefile
LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS)
LOCAL_ARM_MODE := arm
LOCAL_MODULE := hello
LOCAL_SRC_FILES := hello.c
include $(BUILD_EXECUTABLE)
```

Android.mk文件说明：

1、LOCAL_PATH：定义本地源码路径

2、CLEAR_VARS：让编译系统清除掉一些已经定义过的宏

3、LOCAL_ARM_MODE：指定生成的原生程序使勇的ARM指定模式

4、LOCAL_MODULE：指定模块名称，即原生程序生成后的文件名

5、LOCAL_SRC_FILES：指定C或C++源列表。示例中使用的只有一个hello.c文件。

6、BUILD_EXECUTABLE：指定生成可执行文件。
Android.mk文件编写完后，将它与hello.c一同放在jni目录下，然后进入命令行切换到hello2根目录，执行ndk-build命令，执行效果如下：

![img](https://img-blog.csdn.net/20160929195228029)

此时，我们看执行结果的最后一行即我们生成文件的位置。因此，我们进入hello2目录下的libs/armeabi下，将hello文件复制到模拟器或手机中，执行过程参考gcc手动编译。其实主要也就是以下三条命令即可：

```haskell
adb push hello /data/local/tmp
adb shell chmod 755 /data/local/tmp/hello
adb shell /data/local/tmp/hello
```

说明：1、adb需要配置环境变量。

  2、传入的hello必须修改权限为可执行文件

此时，可以看到，控制台命令行输出"Hello ARM!"。

ndk-build 命令详细使用

**ndk-build NDK_PROJECT_PATH=项目根目录    APP_BUILD_SCRIPT=项目根目录/Android.mk   NDK_APPLICATION_MK=项目根目录/Application.mk**

# android开发实践之ndk编译命令简单示例

 更新时间：2017年06月22日 14:18:55  作者：爱因私谈  

这篇文章主要给大家介绍了在android中ndk编译命令使用的相关资料，文中详细介绍了ndk-build命令行参数，并通过简单的示例代码给大家介绍了如何编写 .c 文件，需要的朋友可以参考借鉴，下面来一起看看吧。

**前言**

Android提供了NDK工具，用来编译native代码（c/c++），该工具配置好了相关的交叉编译环境和工具链，只需要你简单地编写几个.mk文件即可将你的c/c++代码编译为Android的java工程/Android手机可以识别、加载和运行的库或者应用程序。

默认情况下，使用NDK编译c/c++代码，需要将该代码放置到任一个Android应用工程的jni目录下，然后编写相应的Android.mk文件，并执行`ndk-build`命令完成编译。其实你也是可以在任意目录下去编译native代码的，只需要在`ndk-build`命令后面添加相应的命令行参数即可，这里给出一些常用的`ndk-build`命令行参数，方便大家灵活地使用NDK编译自己的native代码，具体的示例我将会在后续的文章中给出。

**ndk-build命令行参数**

1、`ndk-build NDK_LOG=1`

用于配置LOG级别，打印ndk编译时的详细输出信息

2、`ndk-build NDK_PROJECT_PATH=.`

指定NDK编译的代码路径为当前目录，如果不配置，则必须把工程代码放到Android工程的jni目录下

3、`ndk-build APP_BUILD_SCRIPT=./Android.mk`

指定NDK编译使用的Android.mk文件

4、`ndk-build NDK_APPLICATION_MK=./Application.mk`

指定NDK编译使用的application.mk文件

5、`ndk-build clean`

清除所有编译出来的临时文件和目标文件

6、`ndk-build -B`

强制重新编译已经编译完成的代码

7、`ndk-build NDK_DEBUG=1`

执行 debug build

8、`ndk-build NDK_DEBUG=0`

执行 release build

9、`ndk-build NDK_OUT=./mydir`

指定编译生成的文件的存放位置

10、`ndk-build -C /opt/myTest/`

到指定目录编译native代码

**例：**

**编写 .c 文件**

假设你在 ~/math 目录下编写了一个 math.c 文件，内容如下：

```
#include <stdio.h>``int` `add( ``int` `a , ``int` `b ) {``return` `a+b;``}
```

编写 Android.mk 文件，内容如下：

```
LOCAL_PATH := $(call my-dir)``include $(CLEAR_VARS)``LOCAL_MODULE := dmath``LOCAL_SRC_FILES := math.c``include $(BUILD_SHARED_LIBRARY)
```

在 ~/math 目录下，执行 `ndk-build` 命令，参数如下：

```
$ ndk-build NDK_PROJECT_PATH=. APP_BUILD_SCRIPT=./Android.mk
```

或：

```
ndk-build NDK_PROJECT_PATH=. APP_BUILD_SCRIPT=./Android.mk NDK_APPLICATION_MK=./Application.mk
```

NDK_PROJECT_PATH 指定了需要编译的代码的工程目录，这里给出的是当前目录，APP_BUILD_SCRIPT给出的是Android makefile文件的路径，当然，如果你还有 Application.mk 文件的话，则可以添加`NDK_APP_APPLICATION_MK=./Application.mk`

执行完`ndk-build`命令后，你会发现当前目录下，生成了 obj 和 libs 文件夹，这样，你的libdmath.so动态库就已经制作完成了，在 libs/armeabi 目录下。

# ndk 命令编译C或c++代码生成android 动态so库和可执行程序

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[xubaipei柏培](https://blog.csdn.net/qq_29333911) 2018-08-21 17:49:26 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1708 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [android-开发](https://blog.csdn.net/qq_29333911/category_6329420.html)

版权

NDK 命令ndk-build 会检查当前执行的目录下Jni 目录有没有Application.mk 和Android.mk 文件所以首先要写好这两个构建脚本

Application.mk

APP_STL := gnustl_static
\#APP_CPPFLAGS := -frtti -fexceptions
APP_CPPFLAGS +=-std=c++11 #允许使用c++11的函数等功能
APP_PLATFORM := android-14
APP_ABI := armeabi-v7a
APP_STL := stlport_static

Android.mk

LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS)

LOCAL_MODULE   := ffmpeg
LOCAL_SRC_FILES := function.c
LOCAL_SRC_FILES := main.c
LOCAL_CPPFLAGS :=--std=c++11 
LOCAL_C_INCLUDES := E:/AndroidDev/android-ndk-r15c/sources/cxx-stl/stlport/stlport
\#include $(BUILD_SHARED_LIBRARY)// 生成so
\#生成可执行
LOCAL_CFLAGS += -pie -fPIE
LOCAL_LDFLAGS += -pie -fPIE
include $(BUILD_EXECUTABLE)

Android.mk 文件教程：https://developer.android.google.cn/ndk/guides/android_mk

Application.mk 文件教程：https://developer.android.google.cn/ndk/guides/application_mk

源码：https://download.csdn.net/download/qq_29333911/10618187