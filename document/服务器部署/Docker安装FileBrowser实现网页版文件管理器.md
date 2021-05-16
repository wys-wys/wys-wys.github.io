# [Docker安装FileBrowser实现网页版文件管理器](https://www.azimiao.com/5858.html)

📅 2020-3-01 /🏸 [梓喵·技术](https://www.azimiao.com/category/tec) /📌 野兔位置：[首页](https://www.azimiao.com/) » [梓喵·技术](https://www.azimiao.com/category/tec) » [本页](https://www.azimiao.com/5858.html)

![img](https://pic-cdn.azimiao.com/wp-content/uploads/2019/06/dockerlogo-s.jpg)

FileBrowser是一款基于现代浏览器技术的WEB版多用户文件管理器，它可以与我们的`Aria2`、`qBittorrent`等软件相结合，构建一个完整的离线下载与文件管理私有云。

### 预览图

![img](https://pic-cdn.azimiao.com/wp-content/uploads/2020/03/535ad2fa5669f9e3d18092e3c119fe4b.png)

### 安装

1. 拉取镜像

   ```bash
   docker pull filebrowser/filebrowser
   ```

   Bash

2. 创建所需文件夹

   ```bash
   #日志与数据库
   mkdir ~/filebrowser_data
   ```

   Bash

3. 运行容器

   ```bash
   docker run \
   -v /path/to/root:/srv \
   -v home/yetu/filebrowser_data/filebrowser.db:/database.db \
   -v home/yetu/filebrowser_data/.filebrowser.json:/.filebrowser.json \
   -p 80:80 \
   --restart=always \
   filebrowser/filebrowser
   ```

   docker run -d -v /root/filebrowser/sites/root:/srv -v /root/filebrowser/filebrowserconfig.json:/etc/config.json -v /root/filebrowser/database.db:/etc/database.db -p 10000:80 filebrowser/filebrowser
   Bash

   路径与端口含义

   

   - `/path/to/root`：欲挂载的宿主机目录，文件管理将以这个目录作为根目录。
   - `80`：访问端口

4. 开始使用

   访问

   ```
   http://ip:port
   ```

   ，如果得法，会进入登录界面。

   

   初始管理员账户名与密码均为`admin`。

   进入界面后，在`Setting`->`Profile Settings`中修改账户显示语言为简体中文。

   在`用户管理`中可以添加多个用户，并分别设置它们的权限（诸如上传、下载、删除等文件管理权限）。

   ![img](https://pic-cdn.azimiao.com/wp-content/uploads/2020/03/24c795fae94a0d9a2ef4f4ed149e3134.png)

梓喵出没博客(azimiao.com)版权所有，转载请注明链接：https://www.azimiao.com/5858.html
欢迎加入梓喵出没博客交流群：[313732000](https://jq.qq.com/?_wv=1027&k=5VjqiqQ)

[DOCKER](https://www.azimiao.com/tag/docker)[FILEBROWSER](https://www.azimiao.com/tag/filebrowser)[技术](https://www.azimiao.com/tag/technology)[技术·软件](https://www.azimiao.com/tag/technology_software)

[Docker安装Aria2与AriaNg实现离线下载](https://www.azimiao.com/5830.html)

[Steam解谜游戏Seek Girl Ⅲ(三)攻略及完美存档](https://www.azimiao.com/5865.html)

### 你可能也喜欢

 