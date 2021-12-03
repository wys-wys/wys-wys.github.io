# python UIAutomator2使用超详细教程

 更新时间：2021年02月19日 14:29:58  作者：Jepson2017  

这篇文章主要介绍了python UIAutomator2使用超详细教程,本文给大家介绍的非常详细，对大家的学习或工作具有一定的参考借鉴价值，需要的朋友可以参考下

##### 目录

- [一、环境要求
  ](https://www.jb51.net/article/205942.htm#_label0)
- [二、介绍
  ](https://www.jb51.net/article/205942.htm#_label1)
- [三、库地址
  ](https://www.jb51.net/article/205942.htm#_label2)
- [四、安装](https://www.jb51.net/article/205942.htm#_label3)
- [五、应用及操作](https://www.jb51.net/article/205942.htm#_label4)



## 一、环境要求 

python 3.6+
android 4.4+



## 二、介绍 

uiautomator2 是一个可以使用Python对Android设备进行UI自动化的库。其底层基于Google uiautomator，Google提供的uiautomator库可以获取屏幕上任意一个APP的任意一个控件属性，并对其进行任意操作。



## 三、库地址 

GitHub地址：
https://github.com/openatx/uiautomator2

https://github.com/openatx/uiautomator2/blob/master/README.md



## 四、安装

1、安装uiautomator2

```
pip install ``-``-``pre uiautomator2 ``pip install pillow （如果需要截图，可安装这个库）
```

2、设备安装atx-agent

> 首先设备连接到PC，并能够adb devices发现该设备。
> 执行下面的命令会自动安装本库所需要的设备端程序：uiautomator-server，atx-agent，openstf / minicap，openstf / minitouch

```
# init就是所有USB连接电脑的手机上都安装uiautomator2``python ``-``m uiautomator2 init`` ` `# 指定手机安装uiautomator2， 用 --mirror``python ``-``m uiautomator2 init ``-``-``mirror ``-``-``serial $SERIAL` `# 嫌弃慢的话，可以用国内的镜像``python ``-``m uiautomator2 init ``-``-``mirror
```

最后提示success，代表atx-agent初始化成功。

3、安装weditor
有了这个，方便我们快速的识别手机上的元素，方便写代码

```
pip install ``-``U weditor
```

安装好之后，就可以在命令行运行 **weditor --help** 确认是否安装成功了。

Windows系统可以使用命令在桌面创建一个快捷方式:

```
weditor ``-``-``shortcut
```

在windows cmd中执行上述命令后，会在桌面上创建一个快捷方式，如下图：

![在这里插入图片描述](https://img.jbzj.com/file_images/article/202102/20210219142126115.png)

启动方法：

> 方法1.命令行直接输入 **weditor** 会自动打开浏览器，输入设备的ip或者序列号，点击Connect即可;
> 方法2.桌面上双击WEditor快捷方式即可;
> 方法3.命令行中执行 **python -m weditor**

启动后如下图：

![在这里插入图片描述](https://img.jbzj.com/file_images/article/202102/20210219142126116.jpg)



## 五、应用及操作

**调用uiautomator2的过程**

> 配置手机设备参数，设置具体操作的是哪一台手机
> 抓取手机上应用的控件，制定对应的控件来进行操作
> 对抓取到的控件进行操作，比如点击、填写参数等。

**设备连接方法，有两种**：

> python-uiautomator2连接手机的方式有两种，一种是通过WIFI，另外一种是通过USB。两种方法各有优缺点。
> WIFI最便利的地方要数可以不用连接数据线，USB则可以用在PC和手机网络不在一个网段用不了的情况。

（1）通过WiFi，假设设备IP 192.168.0.107和您的PC在同一网络中

```
import` `uiautomator2 as u2``d ``=` `u2.connect(``'192.168.0.107'``)
```

（2）通过USB， 假设设备序列是123456789F

```
import` `uiautomator2 as u2``d ``=` `u2.connect(``'123456789F'``) ``# USB链接设备。或者u2.connect_usb('123456f')``#d = u2.connect_usb() 或者 d = u2.connect() ，当前只有一个设备时可以用这个
```

在没有参数的情况下调用u2.connect()， uiautomator2将从环境变量ANDROID_DEVICE_IP获取设备IP。如果这个环境变量是空的，uiautomator将返回connect_usb，您需要确保只有一个设备连接到计算机。

**检查并维持设备端守护进程处于运行状态：**

```
d.healthcheck()
```

**打开调试开关：**

```
d.debug ``=` `True``d.info
```

**安装应用，只能从URL安装：**

```
d.app_install(``'http://some-domain.com/some.apk'``) ``#引号内为下载apk地址
```

**启动应用：**

```
d.app_start(``'com.eg.android.AlipayGphone'``) ``#引号内为包名称，这里为支付宝
```

**停止应用：**

```
#相当于'am force-stop'强制停止应用``d.app_stop(``'com.eg.android.AlipayGphone'``) ` `#相当于'pm clear' 清空App数据``d.app_clear(``'com.eg.android.AlipayGphone'``)
```

**停止所有正在运行的应用程序：**

```
# 停止所有``d.app_stop_all()` `# 停止所有应用程序，除了com.examples.demo``d.app_stop_all(excludes``=``[``'com.examples.demo'``])
```

**跳过弹窗，禁止弹窗：**

```
d.disable_popups() ``# 自动跳过弹出窗口 ``d.disable_popups(``False``) ``# 禁用自动跳过弹出窗
```

**获取设备信息：**

```
# 获取基本信息``d.info` `# 获取窗口大小``print``(d.window_size())``# 设备垂直输出示例: (1080, 1920)``# 设备水平输出示例: (1920, 1080)` `# 获取当前应用程序信息。对于某些android设备，输出可以为空``print``(d.current_app())` `#获取设备序列号``print``(d.serial)` `#获取WIFI IP``print``(d.wlan_ip)` `#获取详细的设备信息``print``(d.device_info)
```

**获取应用信息：**

```
d.app_info(``"com.eg.android.AlipayGphone"``)``# 会输出``'''``{`` ``"packageName": "com.eg.android.AlipayGphone", `` ``"mainActivity": "com.eg.android.AlipayGphone.AlipayLogin", `` ``"label": "支付寶", `` ``"versionName": "10.2.13.9020", `` ``"versionCode": 360, `` ``"size": 108306104``}``'''``# 保存应用程序图标``img ``=` `d.app_icon(``"com.eg.android.AlipayGphone"``)``img.save(``"icon.png"``)
```

**推拉文件：**
（1）将文件推送到设备

```
# push文件夹``d.push(``"foo.txt"``, ``"/sdcard/"``)``# push和重命名``d.push(``"foo.txt"``, ``"/sdcard/bar.txt"``)``# push fileobj``with ``open``(``"foo.txt"``, ``'rb'``) as f:`` ``d.push(f, ``"/sdcard/"``)``# 推动和更改文件访问模式``d.push(``"foo.sh"``, ``"/data/local/tmp/"``, mode``=``0o755``)
```

（2）从设备中拉出一个文件

```
d.pull(``"/sdcard/tmp.txt"``, ``"tmp.txt"``)` `# 如果在设备上找不到文件，FileNotFoundError将引发``d.pull(``"/sdcard/some-file-not-exists.txt"``, ``"tmp.txt"``)
```

**关键事件：**
（1）打开/关闭屏幕

```
d.screen_on()＃打开屏幕 ``d.screen_off() ＃关闭屏幕
```

（2）获取当前屏幕状态

```
d.info.get(``'screenOn'``) ``# 需要 Android> = 4.4
```

（3）硬键盘和软键盘操作

```
d.press(``"home"``) ``# 点击home键``d.press(``"back"``) ``# 点击back键``d.press(``"left"``) ``# 点击左键``d.press(``"right"``) ``# 点击右键``d.press(``"up"``) ``# 点击上键``d.press(``"down"``) ``# 点击下键``d.press(``"center"``) ``# 点击选中``d.press(``"menu"``) ``# 点击menu按键``d.press(``"search"``) ``# 点击搜索按键``d.press(``"enter"``) ``# 点击enter键``d.press(``"delete"``) ``# 点击删除按键``d.press(``"recent"``) ``# 点击近期活动按键``d.press(``"volume_up"``) ``# 音量+``d.press(``"volume_down"``) ``# 音量-``d.press(``"volume_mute"``) ``# 静音``d.press(``"camera"``) ``# 相机``d.press(``"power"``) ``#电源键
```

（4）解锁屏幕

```
d.unlock()``# 相当于``# 1. 发射活动:com.github.uiautomator.ACTION_IDENTIFY``# 2. 按home键
```

**手势与设备的交互：**

```
# 单击屏幕``d.click(x,y) ``# x,y为点击坐标` `# 双击屏幕``d.double_click(x,y)``d.double_click(x,y,``0.1``) ``# 默认两个单击之间间隔时间为0.1秒` `# 长按``d.long_click(x,y)``d.long_click(x,y,``0.5``) ``# 长按0.5秒（默认）` `# 滑动``d.swipe(sx, sy, ex, ey)``d.swipe(sx, sy, ex, ey, ``0.5``) ``#滑动0.5s(default)` `#拖动``d.drag(sx, sy, ex, ey)``d.drag(sx, sy, ex, ey, ``0.5``)``#拖动0.5s(default)``# 滑动点 多用于九宫格解锁，提前获取到每个点的相对坐标（这里支持百分比）` `# 从点(x0, y0)滑到点(x1, y1)再滑到点(x2, y2)``# 两点之间的滑动速度是0.2秒``d.swipe((x0, y0), (x1, y1), (x2, y2), ``0.2``)``# 注意：单击，滑动，拖动操作支持百分比位置值。例：``d.long_click(``0.5``, ``0.5``) 表示长按屏幕中心
```

**XPath：**

```
# 检索方向``d.orientation``# 检索方向。输出可以是 "natural" or "left" or "right" or "upsidedown"` `# 设置方向``d.set_orientation(``"l"``) ``# or "left"``d.set_orientation(``"r"``) ``# or "right"``d.set_orientation(``"n"``) ``# or "natural"` `#冻结/ 开启旋转``d.freeze_rotation() ``# 冻结旋转``d.freeze_rotation(``False``) ``# 开启旋转` `########## 截图 ############``# 截图并保存到电脑上的一个文件中，需要Android>=4.2。``d.screenshot(``"home.jpg"``)`` ` `# 得到PIL.Image格式的图像. 但你必须先安装pillow``image ``=` `d.screenshot() ``# default format="pillow"``image.save(``"home.jpg"``) ``# 或'home.png'，目前只支持png 和 jpg格式的图像`` ` `# 得到OpenCV的格式图像。当然，你需要numpy和cv2安装第一个``import` `cv2``image ``=` `d.screenshot(``format``=``'opencv'``)``cv2.imwrite(``'home.jpg'``, image)`` ` `# 获取原始JPEG数据``imagebin ``=` `d.screenshot(``format``=``'raw'``)``open``(``"some.jpg"``, ``"wb"``).write(imagebin)` `#############################` `# 转储UI层次结构``# get the UI hierarchy dump content (unicoded).（获取UI层次结构转储内容）``d.dump_hierarchy()` `# 打开通知或快速设置``d.open_notification() ``#下拉打开通知栏``d.open_quick_settings() ``#下拉打开快速设置栏` `# 检查特定的UI对象是否存在``d(text``=``"Settings"``).exists ``# 返回布尔值，如果存在则为True，否则为False``d.exists(text``=``"Settings"``) ``# 另一种写法``# 高级用法``d(text``=``"Settings"``).exists(timeout``=``3``) ``# 等待'Settings'在3秒钟出现` `# 获取特定UI对象的信息``d(text``=``"Settings"``).info` `# 获取/设置/清除可编辑字段的文本(例如EditText小部件)``d(text``=``"Settings"``).get_text() ``#得到文本小部件``d(text``=``"Settings"``).set_text(``"My text..."``) ``#设置文本``d(text``=``"Settings"``).clear_text() ``#清除文本` `# 获取Widget中心点``d(text``=``"Settings"``).center()``#d(text="Settings").center(offset=(0, 0)) # 基准位置左前
```

**UI对象有五种定位方式：**

```
# text、resourceId、description、className、xpath、坐标` `# 执行单击UI对象``#text定位单击``d(text``=``"Settings"``).click()``d(text``=``"Settings"``, className``=``"android.widget.TextView"``).click()` `#resourceId定位单击``d(resourceId``=``"com.ruguoapp.jike:id/tv_title"``, className``=``"android.widget.TextView"``).click() ` `#description定位单击``d(description``=``"设置"``).click()``d(description``=``"设置"``, className``=``"android.widget.TextView"``).click()` `#className定位单击``d(className``=``"android.widget.TextView"``).click()` `#xpath定位单击``d.xpath(``"//android.widget.FrameLayout[@index='0']/android.widget.LinearLayout[@index='0']"``).click()` `#坐标单击``d.click(``182``, ``1264``)` `# 等待元素出现(最多10秒），出现后单击 ``d(text``=``"Settings"``).click(timeout``=``10``)``# 在10秒时点击，默认的超时0``d(text``=``'Skip'``).click_exists(timeout``=``10.0``)``# 单击直到元素消失，返回布尔``d(text``=``"Skip"``).click_gone(maxretry``=``10``, interval``=``1.0``) ``# maxretry默认值10,interval默认值1.0``# 点击基准位置偏移``d(text``=``"Settings"``).click(offset``=``(``0.5``, ``0.5``)) ``# 点击中心位置，同d(text="Settings").click()``d(text``=``"Settings"``).click(offset``=``(``0``, ``0``)) ``# 点击左前位置``d(text``=``"Settings"``).click(offset``=``(``1``, ``1``)) ``# 点击右下` `# 执行双击UI对象``d(text``=``"设置"``).double_click() ``# 双击特定ui对象的中心``d.double_click(x, y, ``0.1``) ``# 两次单击之间的默认持续时间为0.1秒` `#执行长按UI对象``# 长按特定UI对象的中心``d(text``=``"Settings"``).long_click()``d.long_click(x, y, ``0.5``) ``# 长按坐标位置0.5s默认` `# 将UI对象拖向另一个点或另一个UI对象``# Android<4.3不能使用drag.``# 在0.5秒内将UI对象拖到屏幕点(x, y)``d(text``=``"Settings"``).drag_to(x, y, duration``=``0.5``)` `# 将UI对象拖到另一个UI对象的中心位置，时间为0.25秒``d(text``=``"Settings"``).drag_to(text``=``"Clock"``, duration``=``0.25``)
```

**常见用法：**

```
# 等待10s``d.xpath(``"//android.widget.TextView"``).wait(``10.0``)` `# 找到并单击``d.xpath(``"//*[@content-desc='分享']"``).click()` `# 检查是否存在``if` `d.xpath(``"//android.widget.TextView[contains(@text, 'Se')]"``).exists:`` ``print``(``"exists"``)`` ` `# 获取所有文本视图文本、属性和中心点``for` `elem ``in` `d.xpath(``"//android.widget.TextView"``).``all``():`` ``print``(``"Text:"``, elem.text)`` ` `#获取视图文本``for` `elem ``in` `d.xpath(``"//android.widget.TextView"``).``all``():`` ``print``(``"Attrib:"``, elem.attrib)`` ` `#获取属性和中心点``#返回: (100, 200)``for` `elem ``in` `d.xpath(``"//android.widget.TextView"``).``all``():`` ``print``(``"Position:"``, elem.center())` `# xpath常见用法：``# 所有元素``/``/``*` `# resource-id包含login字符``/``/``*``[contains(@resource``-``id``, ``'login'``)]` `# 按钮包含账号或帐号``/``/``android.widget.Button[contains(@text, ``'账号'``) ``or` `contains(@text, ``'帐号'``)]` `# 所有ImageView中的第二个``(``/``/``android.widget.ImageView)[``2``]` `# 所有ImageView中的最后一个``(``/``/``android.widget.ImageView)[last()]` `# className包含ImageView``/``/``*``[contains(name(), ``"ImageView"``)]
```

文章参考：[https://vic.kim/2019/05/20/UIAutomator2%E7%9A%84%E4%BD%BF%E7%94%A8/](https://vic.kim/2019/05/20/UIAutomator2的使用/)

到此这篇关于python UIAutomator2使用超详细教程的文章就介绍到这了,更多相关python UIAutomator2使用内容请搜索脚本之家以前的文章或继续浏览下面的相关文章希望大家以后多多支持脚本之家！

**您可能感兴趣的文章:**

- [python 使用uiautomator2连接手机设备的实现](https://www.jb51.net/article/211150.htm)
- [Python+uiautomator2实现自动刷抖音视频功能](https://www.jb51.net/article/211073.htm)
- [详解python uiautomator2 watcher的使用方法](https://www.jb51.net/article/169659.htm)
- [利用Python批量提取Win10锁屏壁纸实战教程](https://www.jb51.net/article/137233.htm)
- [Python中Selenium模拟JQuery滑动解锁实例](https://www.jb51.net/article/119603.htm)
- [Python+uiautomator2实现手机锁屏解锁功能](https://www.jb51.net/article/211162.htm)



- [python](http://common.jb51.net/tag/python/1.htm)
- [UIAutomator2](http://common.jb51.net/tag/UIAutomator2/1.htm)
- [使用](http://common.jb51.net/tag/使用/1.htm)

## 相关文章

- 

- [![解决tensorboard多个events文件显示紊乱的问题](https://img.jbzj.com/images/xgimg/bcimg0.png)](https://www.jb51.net/article/180506.htm)

  [解决tensorboard多个events文件显示紊乱的问题](https://www.jb51.net/article/180506.htm)

  今天小编就为大家分享一篇解决tensorboard多个events文件显示紊乱的问题，具有很好的参考价值，希望对大家有所帮助。一起跟随小编过来看看吧

  2020-02-02

- [![Python使用itchat模块实现简单的微信控制电脑功能示例](https://img.jbzj.com/images/xgimg/bcimg1.png)](https://www.jb51.net/article/168430.htm)

  [Python使用itchat模块实现简单的微信控制电脑功能示例](https://www.jb51.net/article/168430.htm)

  这篇文章主要介绍了Python使用itchat模块实现简单的微信控制电脑功能,结合实例形式分析了Python基于itchat模块控制电脑实现运行程序、截图等相关操作技巧,需要的朋友可以参考下

  2019-08-08

- [![python添加菜单图文讲解](https://img.jbzj.com/images/xgimg/bcimg2.png)](https://www.jb51.net/article/162503.htm)

  [python添加菜单图文讲解](https://www.jb51.net/article/162503.htm)

  在本篇文章中小编给大家整理的是关于python添加菜单图文讲解以及步骤分析，需要的朋友们学习下吧。

  2019-06-06

- [![JAVA SWT事件四种写法实例解析](https://img.jbzj.com/images/xgimg/bcimg3.png)](https://www.jb51.net/article/188137.htm)

  [JAVA SWT事件四种写法实例解析](https://www.jb51.net/article/188137.htm)

  这篇文章主要介绍了JAVA SWT事件四种写法实例解析,文中通过示例代码介绍的非常详细，对大家的学习或者工作具有一定的参考学习价值,需要的朋友可以参考下

  2020-06-06

- [![基于python实现名片管理系统](https://img.jbzj.com/images/xgimg/bcimg4.png)](https://www.jb51.net/article/151711.htm)

  [基于python实现名片管理系统](https://www.jb51.net/article/151711.htm)

  这篇文章主要为大家详细介绍了基于python实现名片管理系统，具有一定的参考价值，感兴趣的小伙伴们可以参考一下

  2018-11-11

- [![python requests抓取one推送文字和图片代码实例](https://img.jbzj.com/images/xgimg/bcimg5.png)](https://www.jb51.net/article/173467.htm)

  [python requests抓取one推送文字和图片代码实例](https://www.jb51.net/article/173467.htm)

  这篇文章主要介绍了python requests抓取one推送文字和图片代码实例,文中通过示例代码介绍的非常详细，对大家的学习或者工作具有一定的参考学习价值,需要的朋友可以参考下

  2019-11-11

- [![python实现对一个完整url进行分割的方法](https://img.jbzj.com/images/xgimg/bcimg6.png)](https://www.jb51.net/article/65169.htm)

  [python实现对一个完整url进行分割的方法](https://www.jb51.net/article/65169.htm)

  这篇文章主要介绍了python实现对一个完整url进行分割的方法,涉及Python操作URL的相关技巧,非常具有实用价值,需要的朋友可以参考下

  2015-04-04

- [![Python3学习笔记之列表方法示例详解](https://img.jbzj.com/images/xgimg/bcimg7.png)](https://www.jb51.net/article/125142.htm)

  [Python3学习笔记之列表方法示例详解](https://www.jb51.net/article/125142.htm)

  Python3 列表 序列是Python中最基本的数据结构，下面这篇文章主要给大家介绍了关于Python3学习笔记之列表方法的相关资料，文中通过示例代码介绍的非常详细，对大家的学习或者工作具有一定的参考学习价值，需要的朋友可以参考下。

  2017-10-10

- [![详解python3 GUI刷屏器(附源码)](https://img.jbzj.com/images/xgimg/bcimg8.png)](https://www.jb51.net/article/205847.htm)

  [详解python3 GUI刷屏器(附源码)](https://www.jb51.net/article/205847.htm)

  这篇文章主要介绍了详解python3 GUI刷屏器(附源码),本文给大家介绍的非常详细，对大家的学习或工作具有一定的参考借鉴价值，需要的朋友可以参考下

  2021-02-02

- [![python字符串格式化方式解析](https://img.jbzj.com/images/xgimg/bcimg9.png)](https://www.jb51.net/article/172325.htm)

  [python字符串格式化方式解析](https://www.jb51.net/article/172325.htm)

  这篇文章主要介绍了python字符串格式化方式解析,文中通过示例代码介绍的非常详细，对大家的学习或者工作具有一定的参考学习价值,需要的朋友可以参考下

  2019-10-10



## 最新评论

#### 大家感兴趣的内容

- *1*[Python入门教程 超详细1小时学会](https://www.jb51.net/article/926.htm)
- *2*[Pycharm 2020最新永久激活码（附](https://www.jb51.net/article/178076.htm)
- *3*[Python 列表(List)操作方法详解](https://www.jb51.net/article/47978.htm)
- *4*[Python 元组(Tuple)操作详解](https://www.jb51.net/article/47986.htm)
- *5*[Python 字典(Dictionary)操作详解](https://www.jb51.net/article/47990.htm)
- *6*[Pycharm 2020年最新激活码（亲测](https://www.jb51.net/article/178050.htm)
- *7*[python strip()函数 介绍](https://www.jb51.net/article/37287.htm)
- *8*[pycharm 使用心得（一）安装和首](https://www.jb51.net/article/50689.htm)
- *9*[python中使用xlrd、xlwt操作exce](https://www.jb51.net/article/60510.htm)
- *10*[python 中文乱码问题深入分析](https://www.jb51.net/article/26543.htm)

#### 最近更新的内容

- [python实现简单的socket server实例](https://www.jb51.net/article/65173.htm)
- [python如何求圆的面积](https://www.jb51.net/article/189881.htm)
- [Python 命令行非阻塞输入的小例子](https://www.jb51.net/article/41743.htm)
- [Python列表操作方法详解](https://www.jb51.net/article/179898.htm)
- [Python原始字符串(raw strings)用法实例](https://www.jb51.net/article/56154.htm)
- [Java多线程编程中ThreadLocal类的用法及深](https://www.jb51.net/article/87077.htm)
- [pymysql 开启调试模式的实现](https://www.jb51.net/article/170671.htm)
- [python numpy 常用随机数的产生方法的实现](https://www.jb51.net/article/168088.htm)
- [利用python打开摄像头及颜色检测方法](https://www.jb51.net/article/144975.htm)
- [解决tensorflow测试模型时NotFoundError错](https://www.jb51.net/article/144603.htm)

#### 常用在线小工具



微信[投稿](http://tougao.jb51.net/)[脚本任务](https://task.jb51.net/)[在线工具](http://tools.jb51.net/)



目录

- 一、环境要求
- 二、介绍
- 三、库地址
- 四、安装
- 五、应用及操作

[关](https://www.jb51.net/about.htm)