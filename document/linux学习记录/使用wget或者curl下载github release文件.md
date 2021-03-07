# 使用wget或者curl下载github release文件

[TestOps风铃](https://blog.csdn.net/weixin_38389124) 2020-05-27 16:50:31 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1226 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 1

分类专栏： [Linux](https://blog.csdn.net/weixin_38389124/category_8808617.html)

版权

转载地址：wget --no-check-certificate --content-disposition

有时候需要在服务器下载GitHub上的release资源，这时候我们可以使用wget或者curl进行处理，这里拿携程开源的配置中心Apollo为例，下载他的release版本

### wget

> wget --no-check-certificate --content-disposition https://github.com/ctripcorp/apollo/releases/download/v1.5.1/apollo-adminservice-1.5.1-github.zip

### curl

> curl -LJO https://github.com/ctripcorp/apollo/releases/download/v1.5.1/apollo-adminservice-1.5.1-github.zip