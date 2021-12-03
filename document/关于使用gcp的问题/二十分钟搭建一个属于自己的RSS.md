

![image-20211113233702054](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20211113233702054.png)

1. 此部分为数据库部分，rss使用的并非物理机的数据库，而是又开了一个容器作为数据库不要随便改动rss配置里的数据库端端口以及数据库名称只能改动有注释的部分
2. 搭建完成后无法登陆后台，只要一登陆就会跳回登陆界面，应该是https的问题，在宝塔中开启强制https之后清理浏览器后访问成功

![img](https://cdn.jsdelivr.net/gh/RalstonLiu/MdnicePic2/2021-4-3/1617433525650-icon-set-1142000_1280.png)

# 【服务器能干什么】二十分钟搭建一个属于自己的RSS服务

[![img](https://blog.laoda.de/upload/2021/04/Reddit_logo1-c9b43f30f22a410bbc9fa0560abf80d0.png)](https://blog.laoda.de/)[咕咕鸽](https://blog.laoda.de/) ·2020-10-02 ·

1. [【0329更新】](https://blog.laoda.de/archives/tinytinyrss#toc-head-0)
2. [完整视频：](https://blog.laoda.de/archives/tinytinyrss#toc-head-1)
3. 前言
   1. [RSS 服务](https://blog.laoda.de/archives/tinytinyrss#toc-head-3)
4. [准备工作：](https://blog.laoda.de/archives/tinytinyrss#toc-head-4)
5. [1、安装docker](https://blog.laoda.de/archives/tinytinyrss#toc-head-5)
6. [2、安装docker-compose](https://blog.laoda.de/archives/tinytinyrss#toc-head-6)
7. [3、安装Tiny Tiny RSS](https://blog.laoda.de/archives/tinytinyrss#toc-head-7)
8. [4、配置nginx反向代理](https://blog.laoda.de/archives/tinytinyrss#toc-head-8)
9. [5、登陆配置全文阅读与繁简体转换](https://blog.laoda.de/archives/tinytinyrss#toc-head-9)
10. [6、如何在多平台阅读](https://blog.laoda.de/archives/tinytinyrss#toc-head-10)
11. 7、享受自己的信息流
    1. [参考资料](https://blog.laoda.de/archives/tinytinyrss#toc-head-12)

### 【0329更新】

如果大家不想自己捣鼓，只是想尝尝鲜，可以在下面留言，我后台帮大家开几个账号玩一玩。

<iframe src="https://player.bilibili.com/player.html?aid=929944966&amp;bvid=BV1VK4y1m7CH&amp;cid=319310986" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="box-sizing: border-box; border: none; max-width: 100%; position: absolute; width: 780px; height: 468px; left: 0px; top: 0px;"></iframe>

## 完整视频：

[点击观看](https://www.bilibili.com/video/bv1VK4y1m7CH)

## 前言

### RSS 服务

市面上有非常多的 RSS 聚合服务，来帮助我们统一管理、订阅、更新、筛选 RSS 源推送给我们的更新信息，避免我们被海量的文章淹没，也能保证我们多个设备上 RSS 的阅读进度一致。

Feedly、Inoreader 等等都是非常不错的 RSS 服务，但是它们的免费版本都有着一定的限制，有时候无法满足我们的全部功能需求，而动辄一个月数十刀的订阅费用又让人望而却步。

不过，GitHub上有一个开源的 RSS 服务：Tiny Tiny RSS

可以满足我们 RSS 订阅的全部需求！

## 准备工作：

- 一台VPS服务器（以 CentOS 7 为例）
- 安装好宝塔面板配置好LNMP [宝塔安装教程点我](https://yirenliu.cn/archives/666clouds#toc-head-4)

## 1、安装docker

Docker 是非常优秀的虚拟化容器，借助于 Docker 我们可以方便的部署 Tiny Tiny RSS，首先我们在服务器上安装 Docker 本体。在服务器上面执行下面命令来安装 Docker：

```bash
curl -fsSL https://get.docker.com/ | sh
```

然后启动 Docker 服务：

```bash
sudo systemctl start docker
```

然后，我们检查一下 Docker 是否启动成功。我们执行命令 `sudo systemctl status docker`:

[![启动成功](https://img-blog.csdnimg.cn/20201002222919937.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002222919937.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

设置docker自动启动：

```bash
sudo systemctl enable docker
```

## 2、安装docker-compose

接下来我们安装 docker-compose：一个管理和启动多个 Docker 容器的工具。

由于 Tiny Tiny RSS 依赖有 PostgreSQL 的数据库服务以及 mercury_fulltext 的全文抓取服务等等，这些服务我们都借助于 Docker 部署，因此利用 docker-compose 就会大大降低我们的部署难度。

我们继续，在服务器上面执行下面的命令来安装 docker-compose：

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

之后给予安装好的 `docker-compose` 可执行权限：

```bash
chmod +x /usr/local/bin/docker-compose
```

创建链接:

```bash
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

最后我们运行 `docker-compose --version` 来检查安装是否成功。如果有如下输出，说明我们的 `docker-compose` 安装成功：

[![安装成功](https://img-blog.csdnimg.cn/20201002223145515.png#pic_center)](https://img-blog.csdnimg.cn/20201002223145515.png#pic_center)

## 3、安装Tiny Tiny RSS

准备工作已经全部完成，接下来我们下载由 [Awesome-TTRSS](https://ttrss.henry.wang/zh/#关于) 配置的 Tiny Tiny RSS 服务的 `docker-compose` 配置文件：

```bash
# 创建 ttrss 目录并进入
mkdir ttrss && cd ttrss
 
# 利用 curl 下载 ttrss 的 docker-compose 配置文件至服务器
curl -fLo docker-compose.yml https://github.com/HenryQW/Awesome-TTRSS/raw/master/docker-compose.yml
```

**注意**利用 curl 下载 ttrss 的 docker-compose 配置文件至服务器可能会报错，大家可以直接在宝塔面板找到对应的文件夹下，然后新建`docker-compose.yml`文件，复制下面的内容进去：

```yml
version: "3"
services:
  service.rss:
    image: wangqiru/ttrss:latest
    container_name: ttrss
    ports:
      - 181:80
    environment:
      - SELF_URL_PATH=http://localhost:181/ # please change to your own domain
      - DB_PASS=ttrss # use the same password defined in `database.postgres`
      - PUID=1000
      - PGID=1000
    volumes:
      - feed-icons:/var/www/feed-icons/
    networks:
      - public_access
      - service_only
      - database_only
    stdin_open: true
    tty: true
    restart: always
 
  service.mercury: # set Mercury Parser API endpoint to `service.mercury:3000` on TTRSS plugin setting page
    image: wangqiru/mercury-parser-api:latest
    container_name: mercury
    networks:
      - public_access
      - service_only
    restart: always
 
  service.opencc: # set OpenCC API endpoint to `service.opencc:3000` on TTRSS plugin setting page
    image: wangqiru/opencc-api-server:latest
    container_name: opencc
    environment:
      - NODE_ENV=production
    networks:
      - service_only
    restart: always
 
  database.postgres:
    image: postgres:13-alpine
    container_name: postgres
    environment:
      - POSTGRES_PASSWORD=ttrss # feel free to change the password
    volumes:
      - ~/postgres/data/:/var/lib/postgresql/data # persist postgres data to ~/postgres/data/ on the host
    networks:
      - database_only
    restart: always
 
  # utility.watchtower:
  #   container_name: watchtower
  #   image: containrrr/watchtower:latest
  #   volumes:
  #     - /var/run/docker.sock:/var/run/docker.sock
  #   environment:
  #     - WATCHTOWER_CLEANUP=true
  #     - WATCHTOWER_POLL_INTERVAL=86400
  #   restart: always
 
volumes:
  feed-icons:
 
networks:
  public_access: # Provide the access for ttrss UI
  service_only: # Provide the communication network between services only
    internal: true
  database_only: # Provide the communication between ttrss and database only
    internal: true
```

修改 `docker-compose.yml`里面的内容：

- 在配置文件中，将 PostgreSQL 数据库的默认密码进行修改。暴露在公网的数据库使用默认密码非常危险。
- 在配置文件中，将 Tiny Tiny RSS 服务的部署网址修改为我们实际的部署网址。比如我的部署网址是 :`https://rss.yirenliu.cn`
- 注意，如果你的部署 URL 包含端口（默认部署端口为 181 端口），那么这里的 URL 也需要加上端口号，格式为 {网址}:{端口}不过不必担心，如果你这里的 URL 配置不正确，那么访问 Tiny Tiny RSS 的时候，Tiny Tiny RSS 会提醒你修改这里的值为正确的 URL，按照提醒进行配置即可

贴一个我的配置文件给大家参考：

```yml
version: "3"
services:
  database.postgres:
    image: postgres:13-alpine
    container_name: postgres
    environment:
      - POSTGRES_PASSWORD=passwd # please change the password
    volumes:
      - ~/postgres/data/:/var/lib/postgresql/data # persist postgres data to ~/postgres/data/ on the host
    restart: always
 
  service.rss:
    image: wangqiru/ttrss:latest
    container_name: ttrss
    ports:
      - 8002:80
    environment:
      - SELF_URL_PATH=https://rss.yirenliu.cn # please change to your own domain
      - DB_HOST=database.postgres
      - DB_PORT=5432
      - DB_NAME=ttrss
      - DB_USER=postgres
      - DB_PASS=passwd # please change the password
      - ENABLE_PLUGINS=auth_internal,fever # auth_internal is required. Plugins enabled here will be enabled for all users as system plugins
      - FEED_LOG_QUIET=true
    stdin_open: true
    tty: true
    restart: always
    command: sh -c 'sh /wait-for.sh $$DB_HOST:$$DB_PORT -- php /configure-db.php && exec s6-svscan /etc/s6/'
 
  service.mercury: # set Mercury Parser API endpoint to `service.mercury:3000` on TTRSS plugin setting page
    image: wangqiru/mercury-parser-api:latest
    container_name: mercury
    expose:
      - 3000
    restart: always
 
  service.opencc: # set OpenCC API endpoint to `service.opencc:3000` on TTRSS plugin setting page
    image: wangqiru/opencc-api-server:latest
    container_name: opencc
    environment:
      - NODE_ENV=production
    expose:
      - 3000
    restart: always
 
  # utility.watchtower:
  #   container_name: watchtower
  #   image: containrrr/watchtower:latest
  #   volumes:
  #     - /var/run/docker.sock:/var/run/docker.sock
  #   environment:
  #     - WATCHTOWER_CLEANUP=true
  #     - WATCHTOWER_POLL_INTERVAL=86400
  #   restart: always
```

上面是完整的配置结果，我把端口改成了8002，如果是用宝塔面板，记得打开`安全`里面的`端口设置`:

[![开启对应的端口](https://img-blog.csdnimg.cn/20201002223922201.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002223922201.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

我这边是腾讯云轻量应用服务器，还需要在在防火墙打开8002端口：

[![打开相应的端口](https://img-blog.csdnimg.cn/20201002224226853.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002224226853.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

之后，我们保存配置文件，启动 Tiny Tiny RSS 服务。在刚刚的 ttrss 目录下执行：

```bash
docker-compose up -d
```

等待脚本执行完成，如果一切没有问题，那么接下来输入 `docker ps`，我们应该看到类似下面的结果：

[![最后一个是我的博客 - -！](https://img-blog.csdnimg.cn/20201002224348402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002224348402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

上面内容表示我们开启了四个 Docker 容器，分别是：

- Tiny Tiny RSS 本身，监听端口为 0.0.0.0:8002 → 80，同时暴露给外网
- PostgreSQL 数据库服务
- Mercury 全文抓取服务
- OpenCC 简体、繁体中文转换服务

如果发现问题，修改 docker-compose 的配置文件后，需要执行下面的命令重启 Docker 容器们：

**注意**`docker-compose`命令要在`docker-compose.yml`文件下运行!

```bash
 
 
# 关闭 Docker 容器们
docker-compose down
 
# 删除已停止的 Docker 容器
docker-compose rm
 
# ……
# 修改 docker-compose 配置文件
# ……
 
# 再次开启 Docker 服务
docker-compose up -d
 
```

## 4、配置nginx反向代理

事实上，到上一步，如果我访问 {服务器 IP}:8002，应该可以直接看到 Tiny Tiny RSS 的 Web 前端，但是 Tiny Tiny RSS 并不能直接配置 SSL 证书，也就没法添加 HTTPS 支持。

我们可以利用 Nginx 作为反向代理服务器，即可方便的给 Tiny Tiny RSS 单独绑定一个我们希望的域名，并利用[Let's Encrypt](https://letsencrypt.org/) 来部署 HTTPS。

还记得我在之前的`docker-compose.yml`里面，我填好的地址是`https://rss.yirenliu.cn`

这里，我在宝塔面板新建一个站点：

[![不要数据库，不要php，纯静态即可](https://img-blog.csdnimg.cn/2020100222490215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/2020100222490215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

配置好SSL证书：

[![免费证书Let's Encrypt，宝塔会自动续期](https://img-blog.csdnimg.cn/20201002225011367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002225011367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

修改后部分的配置文件：

[![注意观察](https://img-blog.csdnimg.cn/20201002225415603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002225415603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

```nginx
# location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
    # {
    #     expires      30d;
    #     error_log off;
    #     access_log /dev/null;
    # }
    
    # location ~ .*\.(js|css)?$
    # {
    #     expires      12h;
    #     error_log off;
    #     access_log /dev/null; 
    # }
                location / {
    proxy_pass http://127.0.0.1:8002/;
    rewrite ^/(.*)$ /$1 break;
    proxy_redirect off;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Upgrade-Insecure-Requests 1;
    proxy_set_header X-Forwarded-Proto https;
  }
    access_log  /www/wwwlogs/rss.yirenliu.cn.log;
    error_log  /www/wwwlogs/rss.yirenliu.cn.error.log;
}
```

主要是注释了52-64的内容：

```bash
    # location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
    # {
    #     expires      30d;
    #     error_log off;
    #     access_log /dev/null;
    # }
    
    # location ~ .*\.(js|css)?$
    # {
    #     expires      12h;
    #     error_log off;
    #     access_log /dev/null; 
    # }
 
 
```

添加了65-75行的内容，

```bash
 
location / {
    proxy_pass http://127.0.0.1:8002/;
    rewrite ^/(.*)$ /$1 break;
    proxy_redirect off;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Upgrade-Insecure-Requests 1;
    proxy_set_header X-Forwarded-Proto https;
  }
 
```

端口改成你自己在`docker-compose.yml`设置的端口即可。

注意：这个方法可以解决宝塔面板默认只能配置一个反向代理的情况！！！

[![不要用宝塔自带的反向代理设置](https://img-blog.csdnimg.cn/20201002225722149.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002225722149.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

> 用宝塔自带的反向代理设置，会出现只能设置一个网站反向代理的情况，就是说你设置了这个，如果你之后还想用反向代理，再在这边设置，会出错！！！亲测！！！

## 5、登陆配置全文阅读与繁简体转换

接下来就能通过域名正常访问了。

[![登陆界面](https://img-blog.csdnimg.cn/20201002230017186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230017186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

默认账户：`admin`

密码：`password`

第一次登陆，务必修改一下默认的密码:

[![右上角进入偏好设置](https://img-blog.csdnimg.cn/20201002230411676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230411676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

如果上面步骤没有问题的话，我们在服务器上面所部署的 Tiny Tiny RSS 本身就已经包含了：

- Mercury 全文提取服务（默认未开启）
- OpenCC 繁简自动转换服务（默认未开启）
- Fever 格式输出插件（默认已开启，用来和 Reeder 等客户端进行连接）
- 包括 Feedly、RSSHub 在内的多款主题
- 等等……

我们不需要多余的配置，开箱即可使用上面的主题和插件，根本不需要操心其他服务的部署和安装。我们登录自己的 Tiny Tiny RSS，在右上角「设置→ 插件」中即可启用上述插件，在「设置 → 主题」处就可以更改我们部署的 Tiny Tiny RSS 所用的主题。

如果有同学对上面的配置还有问题，请直接参考 Awesome TTRSS 的官方文档：[🐋 Awesome TTRSS | 插件](https://ttrss.henry.wang/zh/#插件)

## 6、如何在多平台阅读

[![启用API](https://img-blog.csdnimg.cn/20201002230458907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230458907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

这个API务必开启，后续我们会在电脑和手机上安装软件来阅读内容，毕竟现在是手机的时代，只在浏览器上看没啥软用。

然后配置一下密码：

[![注意这个地址，后续我们会用到](https://img-blog.csdnimg.cn/20201002231834836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002231834836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)
然后启用一下插件：

[![mercury_fulltext全文阅读插件开启](https://img-blog.csdnimg.cn/20201002230718532.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230718532.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![繁简体转换插件开启](https://img-blog.csdnimg.cn/20201002230800117.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230800117.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

配置全文阅读插件，输入`service.mercury:3000`：

[![在这里插入图片描述](https://img-blog.csdnimg.cn/20201002230856543.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230856543.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)
配置繁简转换插件，同样输入`service.mercury:3000`：

[![在这里插入图片描述](https://img-blog.csdnimg.cn/20201002230926374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002230926374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

## 7、享受自己的信息流

[![添加信息分类](https://img-blog.csdnimg.cn/20201002231042403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002231042403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)
订阅信息源：

[![订阅信息源](https://img-blog.csdnimg.cn/20201002231119131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002231119131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)
这里推荐一个神级项目：[RSSHub](https://docs.rsshub.app/usage.html#sheng-cheng-ding-yue-yuan)

在这里你能找到一切rss源，具体可以自己看一下，这边就不展开了。

[![我们不需要自己编写订阅源，这边点进去自己找](https://img-blog.csdnimg.cn/20201002232933348.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002232933348.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![这个就是RSS的订阅地址](https://img-blog.csdnimg.cn/20201002233025150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002233025150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

一般的话，你在网站的域名最后加上`atom.xml`,有大概率就是对应的rss地址了，比如我的博客域名是`https://yirenliu.cn/`,我的rss地址就是`https://yirenliu.cn/atom.xml`

[![就是这样滴，密密麻麻](https://img-blog.csdnimg.cn/20201002231459392.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002231459392.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

我这边用的是MAC,在appstore上面下载这个：

[![reeder](https://img-blog.csdnimg.cn/20201002233241630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002233241630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![reader](https://img-blog.csdnimg.cn/2020100223164020.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/2020100223164020.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![这个地方填三个东西](https://img-blog.csdnimg.cn/20201002232319605.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002232319605.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

`server`的话填前面我们的那个地址,我的是：`https://rss.yirenliu.cn/plugins/fever/`；

`email` 这边是个坑，我搞了好久，最后其实是填的用户名，我们默认的填`admin`就好；

`password`密码的话就填前面那个API设置过的密码就好。

然后就能成功登陆了。

[![在这里插入图片描述](https://img-blog.csdnimg.cn/20201002232245954.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002232245954.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

IOS上也是这个软件，不过貌似要付钱，我花了好像30块钱买的。

[![就是这个](https://img-blog.csdnimg.cn/20201002232754692.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002232754692.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![我的部分订阅内容](https://img-blog.csdnimg.cn/20201002232842791.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002232842791.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![MAC上的效果](https://img-blog.csdnimg.cn/20201002233133202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002233133202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![网页端效果](https://img-blog.csdnimg.cn/20201002233530202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002233530202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

[![早睡早起，已经快晚上十二点了......](https://img-blog.csdnimg.cn/20201002233707618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20201002233707618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JSaWRkbGU=,size_16,color_FFFFFF,t_70#pic_center)

订阅自己感兴趣的内容，拒绝被所谓的智能算法强行推荐内容，有了这个RSS服务，我们可以把阅读信息的主动权掌握在自己的手中。

#### 参考资料

1.[飞蚊话](https://space.bilibili.com/268630727?spm_id_from=333.788.b_765f7570696e666f.2)

捣鼓视频最初就是看的@[飞蚊话](https://www.bwsl.wang/)的，当时昵称还是“等我稍后补充昵称”，算是我的小入门老师了，当时还在微博要了一个测试rss账号。

2.[RSS 教程](https://www.runoob.com/rss/rss-tutorial.html)
3.[Awesome TTRSS](https://ttrss.henry.wang/)
4.[高效管理你的碎片化知识——RSS订阅大法](https://www.bilibili.com/video/BV17E411L78o?t=154)
5.[Install Docker Compose](https://docs.docker.com/compose/install/)

Q.E.D. 

 [TINYTINYRSS](https://blog.laoda.de/tags/tinytinyrss) [DOCKER](https://blog.laoda.de/tags/docker)

[Java-错误: 类 HelloWorld 是公共的, 应在名为 HelloWorld.java 的文件中声明](https://blog.laoda.de/archives/java-learning-day1)

[宝塔面板绕过强制绑定官网账号的小方法](https://blog.laoda.de/archives/bt-sign-in)

[![咕咕鸽](https://blog.laoda.de/upload/2021/04/Reddit_logo1-c9b43f30f22a410bbc9fa0560abf80d0.png)](https://blog.laoda.de/)

### [咕咕鸽](https://blog.laoda.de/)

------

 鸡起犬眠，豕餐牛作。苏才郭福，姬子彭年。

### 

你是我一生只会遇见一次的惊喜 ...

戳我试试 OωO

![img](https://cn.gravatar.com/avatar?d=mm)

- [提交](javascript:void(0))

- [![热心网友](https://gravatar.loli.net/avatar//c2554e04c10f4bde5bcaad4bc6fc8f5a?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

  #### [热心网友](https://blog.laoda.de/archives/tinytinyrss)

  [REPLY](javascript:void(0);)

  发布于 2021/09/10 15:28( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 93.0.4577.63 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

  

  如果用nginx转发，不用开放端口的。

  

  ------

  - [![咕咕鸽](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://blog.laoda.de/)

    #### [博主 咕咕鸽](https://blog.laoda.de/)

    [REPLY](javascript:void(0);)

    发布于 2021/09/10 15:30( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 93.0.4577.63 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 10.15.7 )

    

    [@热心网友 ](https://blog.laoda.de/archives/tinytinyrss)是的，如果用反向代理就不用开放端口了，当时不知道，谢谢提醒

    

    ------

- [![AHERN](https://gravatar.loli.net/avatar//b7ba91ccb3da4bd9199fc41533532299?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

  #### [AHERN](https://blog.laoda.de/archives/tinytinyrss)

  [REPLY](javascript:void(0);)

  发布于 2021/08/31 22:35( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 91.0.4472.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

  

  tinytinyRSS 怎么在reader上看视频呢？
  我看官方文档上说：

  

  该插件与 Fever API 不能同时作为全局插件启用。如果您同时需要两者：
  1.在环境变量 ENABLE_PLUGINS 中移除 fever 并添加 remove_iframe_sandbox 作为全局插件启用。
  2.在登陆 TTRSS 后，通过设置将 Fever API 作为本地插件启用。

  

  没太看懂，跟着弄了一下还是不行。

  

  ------

  - [![咕咕鸽](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://blog.laoda.de/)

    #### [博主 咕咕鸽](https://blog.laoda.de/)

    [REPLY](javascript:void(0);)

    发布于 2021/09/01 09:24( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 92.0.4515.159 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 10.15.7 )

    

    [@AHERN ](https://blog.laoda.de/archives/tinytinyrss)安装配置好之后好久没登录后台了，有空了试试。

    

    另外，其实我的理解是，RSS主要是为了防止我们被纷繁复杂的各种信息干扰，只订阅我们自己感兴趣的内容，其实完全可以看到了好内容，然后跳转去源站的，比如说留言的需要等等。（IOS的Reeder很方便，你直接在内容页面左滑就到源站了。） 这样也能解决看视频的问题～

    

    ------

    - [![AHERN](https://gravatar.loli.net/avatar//b7ba91ccb3da4bd9199fc41533532299?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

      #### [AHERN](https://blog.laoda.de/archives/tinytinyrss)

      [REPLY](javascript:void(0);)

      发布于 2021/09/01 17:42( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 91.0.4472.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

      

      [@咕咕鸽 ](https://blog.laoda.de/)了解了，感谢

      

      ------

  - [![AHERN](https://gravatar.loli.net/avatar//b7ba91ccb3da4bd9199fc41533532299?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

    #### [AHERN](https://blog.laoda.de/archives/tinytinyrss)

    [REPLY](javascript:void(0);)

    发布于 2021/08/31 23:01( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 91.0.4472.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

    

    [@AHERN ](https://blog.laoda.de/archives/tinytinyrss)打错了 是IOS端的Reeder

    

    ------

- [![.](https://gravatar.loli.net/avatar//a14010dfe48769e80b388c3e0e2935d7?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

  #### [.](https://blog.laoda.de/archives/tinytinyrss)

  [REPLY](javascript:void(0);)

  发布于 2021/05/21 14:25( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 86.0.4240.198 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

  

  哈哈，跟着文字教程和视频教程花了一个多小时终于弄好了

  

  ------

  - [![咕咕鸽](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://blog.laoda.de/)

    #### [博主 咕咕鸽](https://blog.laoda.de/)

    [REPLY](javascript:void(0);)

    发布于 2021/05/23 09:05( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 90.0.4430.212 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 10.15.7 )

    

    [@. ](https://blog.laoda.de/archives/tinytinyrss)玩起来！～

    

    ------

    - [![.](https://gravatar.loli.net/avatar//a14010dfe48769e80b388c3e0e2935d7?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

      #### [.](https://blog.laoda.de/archives/tinytinyrss)

      [REPLY](javascript:void(0);)

      发布于 2021/05/27 13:25( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 86.0.4240.198 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

      

      [@咕咕鸽 ](https://blog.laoda.de/)会了，用正则表达式

      

      ------

    - [![.](https://gravatar.loli.net/avatar//a14010dfe48769e80b388c3e0e2935d7?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

      #### [.](https://blog.laoda.de/archives/tinytinyrss)

      [REPLY](javascript:void(0);)

      发布于 2021/05/27 13:15( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 86.0.4240.198 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

      

      [@咕咕鸽 ](https://blog.laoda.de/)对了，博主，tinytinyrss怎么设置过滤器呢，因为信息太多会导致信息过载，我在过滤器里面设置了但是没反应，能详细教授下吗，谢谢

      

      ------

- [![小囧囧](https://gravatar.loli.net/avatar//f9ef31d7f443b7ffcc5fbf0e6b10b971?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

  #### [小囧囧](https://blog.laoda.de/archives/tinytinyrss)

  [REPLY](javascript:void(0);)

  发布于 2021/04/15 19:05( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 89.0.4389.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

  

  [root@izj6c74blvgoubwuwo74mlz ttrss]# docker-compose up -d
  ERROR:
  Can't find a suitable configuration file in this directory or any
  parent. Are you in the right directory?

  

  ```
      Supported filenames: docker-compose.yml, docker-compose.yaml, compose.yml, compose.yaml
  ```

  

  请问一下 这个什么情况？

  

  ------

  - [![二十五画生](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://yirenliu.cn/)

    #### [博主 二十五画生](https://yirenliu.cn/)

    [REPLY](javascript:void(0);)

    发布于 2021/04/15 19:13( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 89.0.4389.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 11.2.3 )

    

    [@小囧囧 ](https://blog.laoda.de/archives/tinytinyrss)你得到docker-compose.yml这个文件夹下来运行

    

    ------

    - [![小囧囧](https://gravatar.loli.net/avatar//f9ef31d7f443b7ffcc5fbf0e6b10b971?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

      #### [小囧囧](https://blog.laoda.de/archives/tinytinyrss)

      [REPLY](javascript:void(0);)

      发布于 2021/04/15 19:18( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/edge.svg) Edge 89.0.774.76 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/windows_win10.svg) Windows 10 )

      

      [@二十五画生 ](https://yirenliu.cn/)跟你文件夹路径不一样home/admin/ttrss

      

      ------

      - [![二十五画生](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://yirenliu.cn/)

        #### [博主 二十五画生](https://yirenliu.cn/)

        [REPLY](javascript:void(0);)

        发布于 2021/04/18 20:06( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 89.0.4389.128 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 11.2.3 )

        

        [@小囧囧 ](https://blog.laoda.de/archives/tinytinyrss)你先cd到这个目录home/admin/ttrss，然后运行docker-compose up -d

        

        ------

      - [![二十五画生](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://yirenliu.cn/)

        #### [博主 二十五画生](https://yirenliu.cn/)

        [REPLY](javascript:void(0);)

        发布于 2021/04/15 19:27( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 89.0.4389.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 11.2.3 )

        

        [@小囧囧 ](https://blog.laoda.de/archives/tinytinyrss)嗯，跑起来就好

        

        ------

- [![小囧囧](https://gravatar.loli.net/avatar//f9ef31d7f443b7ffcc5fbf0e6b10b971?s=256&d=mm)](https://blog.laoda.de/archives/tinytinyrss)

  #### [小囧囧](https://blog.laoda.de/archives/tinytinyrss)

  [REPLY](javascript:void(0);)

  发布于 2021/04/15 01:11( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/mobile%20safari.svg) Mobile Safari 13.0.1 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/ios.svg) iOS 12.3.1 )

  

  那个域名是之前买好的吗？

  

  ------

  - [![二十五画生](https://gravatar.loli.net/avatar//c2df2341445b2a4a6e56d3729fe7cda7?s=256&d=mm)](https://yirenliu.cn/)

    #### [博主 二十五画生](https://yirenliu.cn/)

    [REPLY](javascript:void(0);)

    发布于 2021/04/15 10:03( ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/chrome.svg) Chrome 89.0.4389.114 ![img](https://cdn.jsdelivr.net/gh/LIlGG/cdn@1.0.0/img/Sakura/images/ua/svg/macos.svg) Mac OS 11.2.3 )

    

    [@小囧囧 ](https://blog.laoda.de/archives/tinytinyrss)是的，相关视频可以看这个：https://www.bilibili.com/video/BV1Sy4y1k7kZ/

    

    ------

- 上一页
- 1
- 2
- 下一页