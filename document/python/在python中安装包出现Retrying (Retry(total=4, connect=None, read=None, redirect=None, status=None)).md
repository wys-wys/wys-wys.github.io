# 在python中安装包出现Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None))

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

置顶 [lsf_007](https://blog.csdn.net/lsf_007) 2019-02-26 11:28:20 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 106985 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 493

分类专栏： [python教程](https://blog.csdn.net/lsf_007/category_8668765.html) 文章标签： [python](https://www.csdn.net/tags/MtjaQg4sNDk0LWJsb2cO0O0O.html) [安装包](https://www.csdn.net/tags/MtjaMg1sNTcxNTgtYmxvZwO0O0OO0O0O.html) [Retrying](https://so.csdn.net/so/search/s.do?q=Retrying&t=blog&o=vip&s=&l=&f=&viparticle=) [total=4](https://so.csdn.net/so/search/s.do?q=total=4&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

先向大家展示以下困扰了我好久的问题
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019022611210842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xzZl8wMDc=,size_16,color_FFFFFF,t_70)
死活就是安装不上，总是说出错，其实就是说连接超时，下载不了安装包，我这里也没有科学上网的工具，经过多方百度，找到了办法
通过几次ｐｉｐ的使用，对于默认的pip源的速度实在无法忍受，于是便搜集了一些国内的pip源，如下：

阿里云 http://mirrors.aliyun.com/pypi/simple/

中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/

豆瓣(douban) http://pypi.douban.com/simple/

清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/

中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
但是经过网上给的方法进行安装，还是出现错误
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226112344983.png)
主要意思就是位于pypi.douban.com的存储库不是受信任的或安全的主机，正在被忽略。
要求使用“–trusted host pypi.douban.com”允许此警告。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226112506607.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xzZl8wMDc=,size_16,color_FFFFFF,t_70)
所以最终的

## 解决办法：pip install keras -i http://pypi.douban.com/simple --trusted-host pypi.douban.com（其中的keras是你需要下载的，根据自己需求自行更改）

**如果对大家有帮助，点一下点赞和评论，让更多的人可以看到，减少走的弯路！**

# 安装pip报错：WARNING: Retrying (Retry(total=4,...

[![稻花香](https://pic4.zhimg.com/v2-56577a2b28e7e18343d862ba4aff5ca5_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/dao-hua-xiang-47)

[稻花香](https://www.zhihu.com/people/dao-hua-xiang-47)

关注他

6 人赞同了该文章

安装pip报错：WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProxyError('Cannot connect to proxy.', NewConnect

ionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x0000020A2A9C6F28>: Failed to establish a new connection: [WinError 10061] 由于目标计算

机积极拒绝，无法连接。'))': /simple/pip/

或者：

WARNING: You are using pip version 19.2.3, however version 19.3.1 is available.

You should consider upgrading via the 'python -m pip install --upgrade pip' command.

这时候可以修改pip下载源，可按照如下操作：

**Windows**：

1. 找到系统盘下C:\C:\Users\用户名\AppData\Roaming
2. 查看在Roaming文件夹下有没有一个pip文件夹，如果没有创建一个；
3. 进入pip文件夹，创建一个pip.ini文件；
4. 使用记事本的方式打开pip.ini文件，写入：

[global]

index-url = [http://mirrors.aliyun.com/pypi/simple](https://link.zhihu.com/?target=http%3A//mirrors.aliyun.com/pypi/simple) # 指定下载源

trusted-host = [http://mirrors.aliyun.com](https://link.zhihu.com/?target=http%3A//mirrors.aliyun.com) # 指定域名

然后使用管理员权限打开cmd后运行命令：pip install -i [http://mirrors.aliyun.com/pypi/simple](https://link.zhihu.com/?target=http%3A//mirrors.aliyun.com/pypi/simple) --upgrade pip --user，就会OK了

![img](https://pic4.zhimg.com/v2-61c462b6a170cb6ad0de79fb999eae1b_r.jpg)