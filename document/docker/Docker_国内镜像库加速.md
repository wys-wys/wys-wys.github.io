# Docker 国内镜像库加速

[![img](https://upload.jianshu.io/users/upload_avatars/1179595/41167ecaa805.png?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/e6e4f22e14d2)

[木猫尾巴](https://www.jianshu.com/u/e6e4f22e14d2)关注

0.9612017.05.31 15:47:25字数 961阅读 54,058

[TOC]

# 说明

官方镜像访问缓慢，国内建议使用镜像，本文中使用阿里的镜像

官方 - [https://registry.docker-cn.com](https://links.jianshu.com/go?to=https%3A%2F%2Fregistry.docker-cn.com)
163 - [http://hub-mirror.c.163.com](https://links.jianshu.com/go?to=http%3A%2F%2Fhub-mirror.c.163.com)

> 一般 `阿里 >官方 > 网易 > 不加速` 建议测试

## 阿里云加速

官方镜像访问缓慢，国内建议使用镜像，本文中使用阿里的镜像

阿里的镜像搜索官方地址是 [http://dev.aliyun.com/search.html](https://links.jianshu.com/go?to=http%3A%2F%2Fdev.aliyun.com%2Fsearch.html)

开发者需要开通阿里开发者帐户，再使用阿里的加速服务
登录后阿里开发者帐户后，[https://cr.console.aliyun.com/undefined/instances/mirrors](https://links.jianshu.com/go?to=https%3A%2F%2Fcr.console.aliyun.com%2Fundefined%2Finstances%2Fmirrors) 中查看你的您的专属加速器地址

[https://yourcode.mirror.aliyuncs.com](https://links.jianshu.com/go?to=https%3A%2F%2Fyourcode.mirror.aliyuncs.com)

> `yourcode` 是您自己帐户的加速前缀，后文中请自行替换

请安装1.9.0以上版本的Docker
阿里云的镜像仓库下载： mirrors.aliyun.com/help/docker-engine



```sh
curl -sSL http://acs-public-mirror.oss-cn-hangzhou.aliyuncs.com/docker-engine/internet | sh -
```

> 加速服务不只是提供镜像加速，还有 docker 在各种操作系统的安装文档和加速，详细见 `镜像加速器 -> 操作文档`

## ubuntu

- Docker客户端版本大于1.10的用户

通过修改daemon配置文件/etc/docker/daemon.json来使用加速器



```sh
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://yourcode.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

- 如果您的系统是 Ubuntu 15.04 16.04，Docker 1.9 以上



```sh
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo tee /etc/systemd/system/docker.service.d/mirror.conf <<-'EOF'
[Service]
ExecStart=
ExecStart=/usr/bin/docker daemon -H fd:// --registry-mirror=https://yourcode.mirror.aliyuncs.com
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

如果您的系统是 Ubuntu 12.04 14.04，Docker 1.9 以下



```sh
echo "DOCKER_OPTS=\"\$DOCKER_OPTS --registry-mirror=https://yourcode.mirror.aliyuncs.com\"" | sudo tee -a /etc/default/docker sudo service docker restart
```

> 修改镜像 `sudo vim /etc/systemd/system/docker.service.d/mirror.conf`

### ubuntu 更新docker

- 因为docker 更新需要关闭镜像配置不然报错



```rust
  Drop-In: /etc/systemd/system/docker.service.d
           └─mirror.conf
   Active: inactive (dead) (Result: exit-code) since 五 2017-09-15 13:25:28 CST; 7min ago
     Docs: https://docs.docker.com
 Main PID: 21151 (code=exited, status=1/FAILURE)
```

方法是



```undefined
sudo rm -rf /etc/systemd/system/docker.service.d
```

更新后，重新配置加速镜像即可

## centos

- 系统要求CentOS 7以上Docker客户端版本大于1.10.0



```sh
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://yourcode.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

- 系统要求CentOS 7以上、Docker1.9以上
  使用如下的脚本将mirror的配置添加到docker daemon的启动参数中



```sh
sudo cp -n /lib/systemd/system/docker.service /etc/systemd/system/docker.service
sudo sed -i "s|ExecStart=/usr/bin/docker daemon|ExecStart=/usr/bin/docker daemon --registry-mirror=https://yourcode.mirror.aliyuncs.com|g" /etc/systemd/system/docker.service
sudo systemctl daemon-reload
sudo service docker restart
```

- 系统要求 CentOS 7 以上，Docker 1.9 以上

将mirror的配置添加到docker daemon的启动参数中



```sh
sudo cp -n /lib/systemd/system/docker.service /etc/systemd/system/docker.service
sudo sed -i "s|ExecStart=/usr/bin/docker daemon|ExecStart=/usr/bin/docker daemon --registry-mirror=https://yourcode.mirror.aliyuncs.com|g" /etc/systemd/system/docker.service
sudo systemctl daemon-reload
sudo service docker restart
```

## macOS

### docker-for-mac



```sh
brew cask info docker
brew cask install docker
```

> 用阿里的二进制镜像
> [http://mirrors.aliyun.com/docker-toolbox/mac/docker-for-mac/](https://links.jianshu.com/go?to=http%3A%2F%2Fmirrors.aliyun.com%2Fdocker-toolbox%2Fmac%2Fdocker-for-mac%2F)

右键点击桌面顶栏的 docker 图标，选择 Preferences

- 在 Daemon 标签（Docker 17.03 之前版本为 Advanced 标签）下的 Registry mirrors 列表中
- 将你的加速镜像地址添加加到"registry-mirrors"的数组里(加速顺序按下表计算)
- 点击 `Apply & Restart` 按钮

### Docker Toolbox

安装或升级Docker 1.9+
安装 kitermatic [https://kitematic.com/](https://links.jianshu.com/go?to=https%3A%2F%2Fkitematic.com%2F)

[https://github.com/docker/kitematic/releases](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fdocker%2Fkitematic%2Freleases)

Docker Toolbox
Toolbox的介绍和帮助： [http://mirrors.aliyun.com/help/docker-toolbox](https://links.jianshu.com/go?to=http%3A%2F%2Fmirrors.aliyun.com%2Fhelp%2Fdocker-toolbox)
Mac系统的安装文件路径： [http://mirrors.aliyun.com/docker-toolbox/mac](https://links.jianshu.com/go?to=http%3A%2F%2Fmirrors.aliyun.com%2Fdocker-toolbox%2Fmac)



```sh
# 查看机器的环境配置，并配置到本地。然后通过Docker客户端访问Docker服务
docker-machine env default
eval "$(docker-machine env default)"
docker info

# 如果没有一台安装有Docker环境的Linux虚拟机，创建虚拟机并指定机器名称为default，同时配置Docker加速器地址
docker-machine create --engine-registry-mirror=https://yourcode.mirror.aliyuncs.com -d virtualbox default
```

如果已经有虚拟机了（比如使用kitmatic安装，启动kitmatic后就会初始化虚拟机），将如下的脚本将mirror的配置添加到docker daemon的启动参数中



```sh
➜  ~ docker-machine ssh default "echo 'EXTRA_ARGS=\"--registry-mirror=https://yourcode.mirror.aliyuncs.com\"' | sudo tee -a /var/lib/boot2docker/profile"
EXTRA_ARGS="--registry-mirror=https://yourcode.mirror.aliyuncs.com"
➜  ~ docker-machine restart default
```

重启后可能获得新的IP地址，你需要执行，`不执行这一步将导致代理配置失效`



```sh
docker-machine env default
eval $(docker-machine env default)
```

## windows

安装或升级Docker 1.9+
安装 kitermatic [https://kitematic.com/](https://links.jianshu.com/go?to=https%3A%2F%2Fkitematic.com%2F)

[https://github.com/docker/kitematic/releases](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fdocker%2Fkitematic%2Freleases)

也叫 Docker Toolbox

Toolbox的介绍和帮助： [http://mirrors.aliyun.com/help/docker-toolbox](https://links.jianshu.com/go?to=http%3A%2F%2Fmirrors.aliyun.com%2Fhelp%2Fdocker-toolbox)
Windows系统的安装文件路径： [http://mirrors.aliyun.com/docker-toolbox/windows](https://links.jianshu.com/go?to=http%3A%2F%2Fmirrors.aliyun.com%2Fdocker-toolbox%2Fwindows)



```sh
# 创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。
docker-machine create --engine-registry-mirror=https://yourcode.mirror.aliyuncs.com -d virtualbox default
# 查看机器的环境配置，并配置到本地。然后通过Docker客户端访问Docker服务。
docker-machine env default
eval "$(docker-machine env default)"
docker info
```

如果已经有虚拟机了，将如下的脚本将mirror的配置添加到docker daemon的启动参数中



```sh
➜  ~ docker-machine ssh default "echo 'EXTRA_ARGS=\"--registry-mirror=https://yourcode.mirror.aliyuncs.com\"' | sudo tee -a /var/lib/boot2docker/profile"
EXTRA_ARGS="--registry-mirror=https://xxx.mirror.aliyuncs.com"
➜  ~ docker-machine restart default
```

重启后可能获得新的IP地址，你需要执行，`不执行这一步将导致代理配置失效`



```sh
docker-machine env default
eval $(docker-machine env default)
```

# 使用daocloud镜像库加速

注册daocloud帐号
[http://www.daocloud.io/](https://links.jianshu.com/go?to=http%3A%2F%2Fwww.daocloud.io%2F)

> 需要CentOS7及以上版本

daocloud提供两种方式

## 加速器2.0配置方法

安装Docker官方的最新发行版



```sh
curl -sSL https://get.daocloud.io/docker | sh
sudo chkconfig docker on
sudo systemctl start docker
sudo systemctl status docker
```

安装主机监控程序



```sh
curl -sSL https://get.daocloud.io/daomonit/install.sh | sh -s cddd20f6b891c6d7d8fd3adf91b9585d22718c17
```

## 加速器1.0配置方法

登陆后取得专属加速器地址，类似这样[http://xxxxxx.m.daocloud.io](https://links.jianshu.com/go?to=http%3A%2F%2Fxxxxxx.m.daocloud.io)

Docker 1.3.2版本以上支持加速器

### CentOS 7



```sh
sudo cp -n /lib/systemd/system/docker.service /etc/systemd/system/docker.service
sudo sed -i 'N;s|\[Service\]\n|\[Service\]\nEnvironmentFile=-/etc/sysconfig/docker\n|g' /etc/systemd/system/docker.service
sudo sed -i 's|fd://|fd:// $other_args |g' /etc/systemd/system/docker.service
# 实测的时候`/etc/sysconfig/docker`文件是不存的,用以下命令新建并配置
echo 'other_args="--registry-mirror=http://xxxxxx.m.daocloud.io"'> /etc/sysconfig/docker
sudo systemctl daemon-reload
sudo service docker restart
```



11人点赞



[docker](https://www.jianshu.com/nb/13036750)



