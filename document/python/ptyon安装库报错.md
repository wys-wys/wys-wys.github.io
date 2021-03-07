# Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple WARNING: Retrying (Retry(total=4, conne

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[wangcc342425](https://blog.csdn.net/weixin_44239195) 2020-06-01 09:22:27 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3476 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 2

分类专栏： [pycharm](https://blog.csdn.net/weixin_44239195/category_9421802.html) [python](https://blog.csdn.net/weixin_44239195/category_9468861.html) 文章标签： [python](https://www.csdn.net/tags/MtjaQg4sNDk0LWJsb2cO0O0O.html) [pip](https://www.csdn.net/tags/MtzaIg0sMjA2NzMtYmxvZwO0O0OO0O0O.html)

版权

# 错误描述

在用anaconda prompt安装python第三方包时出现错误
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by ‘ReadTimeoutError(“HTTPSConnectionPool(host=‘pypi.tuna.tsinghua.edu.cn’, port=443): Read timed out. (read timeout=15)”)’: /simple/pyqt5/

## 用尽一切办法也没有解决，最终寻找各种资料得以解决，利用以下语句安装成功

```python
c
1
```

其中pip install **PyQt5** -i http://pypi.douban.com/simple --trusted-host pypi.douban.com 中加粗部分为需要安装的包

