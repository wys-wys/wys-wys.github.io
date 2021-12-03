# 雨轩恋i](https://www.cnblogs.com/yuxuanlian/)

## 

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/yuxuanlian/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/雨轩恋i)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/yuxuanlian/rss/)

随笔- 53 文章- 0 评论- 29 阅读- 93381 

# [Python使用代理的方法](https://www.cnblogs.com/yuxuanlian/p/10139659.html)

我们在做爬虫的过程中经常会遇到这样的情况：最初爬虫正常运行，正常抓取数据，一切看起来都是那么的美好，然而一杯茶的功夫可能就会出现错误，比如403 Forbidden；出现这样的原因往往是网站采取了一些反爬虫的措施，比如，服务器会检测某个IP在单位时间内的请求次数，如果超过了某个阈值，那么服务器会直接拒绝服务，返回一些错误信息。这时候，代理就派上用场了。

国内的免费代理网站：

[西刺代理](https://www.xicidaili.com/)

[快代理免费代理](https://www.kuaidaili.com/free/inha/)

[全网代理ip](http://www.goubanjia.com/)

接下来看如何设置代理：

**urllib代理设置：**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
from urllib.error import URLError
from urllib.request import ProxyHandler,build_opener

proxy='123.58.10.36:8080'  #使用本地代理
#proxy='username:password@123.58.10.36:8080'  #购买代理
proxy_handler=ProxyHandler({
    'http':'http://'+proxy,
    'https':'https://'+proxy
})
opener=build_opener(proxy_handler)
try:
    response=opener.open('http://httpbin.org/get') #测试ip的网址
    print(response.read().decode('utf-8'))
except URLError as e:
    print(e.reason)
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

运行结果如下：

![img](https://img2018.cnblogs.com/blog/1471003/201812/1471003-20181218200044731-924552458.png)

 

**requests代理设置：**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import requests

proxy='123.58.10.36:8080'  #本地代理
#proxy='username:password@123.58.10.36:8080'
proxies={
    'http':'http://'+proxy,
    'https':'https://'+proxy
}
try:
    response=requests.get('http://httpbin.org/get',proxies=proxies)
    print(response.text)
except requests.exceptions.ConnectionError as e:
    print('错误:',e.args)
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

运行结果如下：

![img](https://img2018.cnblogs.com/blog/1471003/201812/1471003-20181218200206306-526102698.png)

 

**Selenium代理设置：**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
from selenium import webdriver


proxy='123.58.10.36:8080'
chrome_options=webdriver.ChromeOptions()
chrome_options.add_argument('--proxy-server=http://'+proxy)
browser=webdriver.Chrome(chrome_options=chrome_options)
browser.get('http://httpbin.org/get')
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

运行结果：

![img](https://img2018.cnblogs.com/blog/1471003/201812/1471003-20181218200256758-1326698509.png)

以上就是代理的一些简单设置、、、

 

雨轩恋拳打南山嘤嘤怪，脚踩北海竹鼠商

分类: [python爬虫](https://www.cnblogs.com/yuxuanlian/category/1310421.html)

标签: [代理](https://www.cnblogs.com/yuxuanlian/tag/代理/)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1471003/20191015171813.png)](https://home.cnblogs.com/u/yuxuanlian/)

[雨轩恋i](https://home.cnblogs.com/u/yuxuanlian/)
[关注 - 72](https://home.cnblogs.com/u/yuxuanlian/followees/)
[粉丝 - 47](https://home.cnblogs.com/u/yuxuanlian/followers/)

[+加关注](javascript:void(0);)

1

0

[« ](https://www.cnblogs.com/yuxuanlian/p/10122702.html)上一篇： [Python安装tesserocr遇到的各种问题及解决办法](https://www.cnblogs.com/yuxuanlian/p/10122702.html)
[» ](https://www.cnblogs.com/yuxuanlian/p/10149831.html)下一篇： [记一次更改了电脑名称后遇到的各种错误反思及感想](https://www.cnblogs.com/yuxuanlian/p/10149831.html)

posted @ 2018-12-18 20:05 [雨轩恋i](https://www.cnblogs.com/yuxuanlian/) 阅读(17534) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=10139659) [收藏](javascript:void(0))

# 在python中设置代理

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[tomatoues](https://blog.csdn.net/weixin_43320017) 2019-02-17 10:18:17 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 388 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [纯代码](https://blog.csdn.net/weixin_43320017/category_8590293.html)

版权

## 使用requests的情况下

```
import requests

proxy = '10.10.1.10:3128'
proxies = {
    'http': 'http://' + proxy,
    'https': 'https://' + proxy,
}
try:
    response = requests.get('http://httpbin.org/get', proxies=proxies)
    print(response.text)
except requests.exceptions.ConnectionError as e:
    print('Error', e.args)
123456789101112
```

## 使用selenium的情况下

```
from selenium import webdriver

proxy = '10.10.1.10:3128'
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument('--proxy-server=http://' + proxy)
browser = webdriver.Chrome(chrome_options=chrome_options)
browser.get('http://httpbin.org/get')
```

# python 使用代理的几种方式

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[whatday](https://blog.csdn.net/whatday) 2021-01-04 10:45:46 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 730 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

版权

**目录**

[HTTP全局代理：环境变量方式](https://blog.csdn.net/whatday/article/details/112169945#t0)

[HTTP全局代理：代码实现方式](https://blog.csdn.net/whatday/article/details/112169945#t1)

[SOCKS全局代理](https://blog.csdn.net/whatday/article/details/112169945#t2)

[针对部分请求设置代理](https://blog.csdn.net/whatday/article/details/112169945#t3)

------

本文介绍几种在Python里使用代理的方式，假定代理运行在本机，HTTP代理端口为1231, SOCKS5代理端口为8080。

### HTTP全局代理：环境变量方式

在命令行里配置如下环境变量，然后执行Python脚本，Python在进行网络请求时就会使用配置的代理。

```bash
export http_proxy="http://127.0.0.1:1231"



export https_proxy="http://127.0.0.1:1231"
```

### HTTP全局代理：代码实现方式

也可以在Python代码里添加如下内容，效果与上面的方式相同：

```python
import os



os.environ["http_proxy"] = "http://10.0.0.100:7890"



os.environ["https_proxy"] = "http://127.0.0.1:1231"
```

### SOCKS全局代理

通过设置环境变量的方式通常只能使用HTTP代理。要使用全局SOCKS代理可以使用tsocks.

安装tsocks后，编辑`/etc/tsocks.conf`，以使用端口为8080的本地SOCKS5代理为例：

```bash
server = 127.0.0.1



server_port = 8080 



server_type = 5
```

配置完成后在原来的脚本执行命令前添加tsocks即可使用，例如:

```bash
tsocks python3 myscript.py
```

### 针对部分请求设置代理

前面的几种方式会为所有的HTTP请求设置代理，如果只想让部分请求使用代理，可以使用requests的proxies参数：

```python
import requests



proxies = {'http': "socks5://127.0.0.1:8080",



           'https': "socks5://127.0.0.1:8080"}



print(requests.get(url, proxies=proxies).content)
```

例如下载图片，可使用：

```python
with requests.get(url, proxies=proxies, stream=True) as r:



    if r.status_code != 200:



        return



    with open(path, 'wb') as f:



        for chunk in r.iter_content(chunk_size=8192): 



            f.write(chunk)
```

 

 



- ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUp.png)点赞1
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarComment.png)评论1](https://blog.csdn.net/whatday/article/details/112169945#commentBox)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarShare.png)分享](javascript:;)
- [![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png)收藏2](javascript:;)
- [关注](javascript:;)
- 一键三连

[*python* 更改 设置*代理*ip](http://download.csdn.net/download/nimabi6666/8891025)

07-11

[*python* 更改 设置*代理*ip 新手刚编写*的* 嘿嘿](http://download.csdn.net/download/nimabi6666/8891025)

[*python*发送请求两种*代理*设置*方式*](https://blog.csdn.net/zaqwescsdn/article/details/47104603)

[zaqwescsdn的博客](https://blog.csdn.net/zaqwescsdn)

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png) 1980

[1*使用*httplib时*的*设置*方式*import httplib,urllib,urllib2; params = urllib.urlencode({ 'param':"55B2A1EDA8B09D13", 'js_sfl':2, 'codetxt':'532832'});](https://blog.csdn.net/zaqwescsdn/article/details/47104603)