# [frantzz](https://www.cnblogs.com/frantz/)

## ☀☀

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/frantz/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/frantzz)
- [订阅](javascript:void(0))
- [管理](https://i.cnblogs.com/)

随笔 - 85 文章 - 0 评论 - 1 阅读 - 29573

# [docker安装可视化portainer](https://www.cnblogs.com/frantz/p/12693618.html)

portainer是比较好用的可视化docker页面，也提供了回调（curl请求）用于自动触发运行容器。

1.docker pull portainer

2.docker run -dit -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name portainer {image_id}

3.![img](https://img2020.cnblogs.com/blog/1756619/202004/1756619-20200413200457355-2087045773.png)

 

分类: [docker](https://www.cnblogs.com/frantz/category/1534866.html)

# Docker 安装Portainer

[![img](https://upload.jianshu.io/users/upload_avatars/12099606/94226189-87e7-49e2-8675-f9fee5891362?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/ab72584780d8)

[一二先生](https://www.jianshu.com/u/ab72584780d8)关注

0.262019.09.30 14:03:23字数 225阅读 11,629

- 搜索相关Portainer镜像，以免错过更好的第三方镜像

  

  ```undefined
  docker search portainer
  ```

- 下载选定的Portainer镜像，这里我们选择下载量最多的官方镜像，如果未指定版本则默认为最新版本，`latest`版本

  

  ```undefined
  docker pull portainer/portainer
  ```

- 运行镜像

  - 本机模式

    

    ```csharp
    docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always --name prtainer portainer/portainer
    ```

  - 远程模式

    

    ```undefined
    docker run -d -p 9000:9000 --restart=always --name prtainer portainer/portainer
    ```

- 访问Portainer容器：`http://IP:9000`

  - 首次登录需要设置`admin`的密码
  - 选择docker连接
    - 选择`Local`，代表本地模式，portainer仅管理本机的docker容器
    - 选择`Remote`，代表远程模式，名称随意，在`Endpoint URL`中填写`docker节点的地址:docker远程端口`（docker安装教程中的设置的`-H 0.0.0.0:2375`中的`2375`）



3人点赞



[配置安装](https://www.jianshu.com/nb/39745464)