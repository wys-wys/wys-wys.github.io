# harbor搭建与使用

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[何止七八](https://blog.csdn.net/qq_24095941) 2019-01-09 12:47:31 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 88891 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 84

分类专栏： [docker](https://blog.csdn.net/qq_24095941/category_8591529.html) [k8s](https://blog.csdn.net/qq_24095941/category_8591528.html) 文章标签： [docker](https://www.csdn.net/tags/Ntjakg4sNzAwMC1ibG9n.html) [harbor](https://www.csdn.net/tags/MtjaQgysNTA3NTItYmxvZwO0O0OO0O0O.html)

版权

前两天测试[服务docker化并k8s布署](https://blog.csdn.net/qq_24095941/article/details/85761609)时，出于方便，使用了docker hub。由于我们的代码是要放到镜像里的，通过运行容器，便能获取我们的全部代码，风险很大。所以我们决定进行私有化的镜像部署。

经过调研，决定使用harbor这个开源项目。

## 项目介绍

[harbor git 地址](https://github.com/goharbor/harbor)

优点：

1. 本身自代 docker 私有仓库
2. 支持基于角色的权限管理
3. 支持 LDAP

## 安装

harbor支持k8s的helm安装和本地安装，我这次先择的安装方式是本地安装。

我的运行环境是 Centos7.2。

#### 0. 前置条件

1. 需要安装`docker`并运行

```shell
yum install docker   # 安装docker
...
systemctl start docker   # 运行docker服务
123
```

1. 需要安装`docker-compose`

```shell
yum install docker-compose
1
```

#### 1. 下载安装包

直接选择编译好的包
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019010911514271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI0MDk1OTQx,size_16,color_FFFFFF,t_70)

这里有两个包`Harbor offline installer` 和 `Harbor online installer`，两者的区别的是 `Harbor offline installer` 里就包含的 Harbor 需要使用的镜像文件。

下载成功，并解压

```shell
tar -zxvf harbor-offline-installer-v1.7.1.tgz
1
```

进入解压的目录，并 `ls`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019010911582242.png)

`harbor.v1.7.1.tar.gz` 里就是 Harbor 用到的镜像

#### 2. 编辑配置文件

`harbor.cfg` 是这个项目的配置文件

###### 1. 修改 hostname 先项

将 hostname 改成你本机的网址或IP

```shell
hostname = A.B.C.D  # 写你自己的网址或IP，公网访问要写公网IP
1
```

###### 2. 支持Http 访问

```shell
customize_crt = false
1
```

#### 3. 运行

1. 修改完配置文件后，运行 `./prepare`，它会哪所配置文件修改一文件
2. 运行 `./install.sh`

运行成功，`docker ps` 查看，可以看到服务已经起来了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190109122127147.png)

#### 4. 常用管理命令

- 停止服务： `docker-compose stop`
- 开始服务： `docker-compose start`

## GUIl界面使用

#### 1. 新建项目

新建一个项目，命名为 `ainirobot`，并设置访问级别为公开。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190109122657903.png)

这里的项目就是一私有化的Docker镜像仓库。

## 上传镜像

#### 1. 修改Docker配置

docker 默认是按 https 请求的，由于我搭的私有库是 http 的，所以需要修改 docker 配置，将信任的库的地址写上
修改文件 `/etc/docker/daemon.json`

```json
{
  "insecure-registries": [
    "A.B.C.D"
  ]
}
12345
```

然后重启docker

```shell
systemctl restart docker
1
```

#### 2. 制作镜像

将 mongo 制作成一个私有镜像， mongo 为我之前从 docker hub 上拉取的镜像。

```shell
docker tag mongo A.B.C.D/ainirobot/nebulae_mongo:0.0.1
1
```

#### 3. 上传

###### 1. 先登陆私有库

```shell
docker login A.B.C.D
1
```

###### 2. PUSH

```shell
docker push A.B.C.D/ainirobot/nebulae_mongo:0.0.1
1
```

###### 3. 结果

从后台已经能看到这个镜像了
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190109123759895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI0MDk1OTQx,size_16,color_FFFFFF,t_70)

## 推荐

完成了私有库的搭建后，可以再安装一个k8s集群后台管理系统（[wayne系统介绍](https://blog.csdn.net/qq_24095941/article/details/86519202)）。