[![img](http://pubimage.360doc.com/index7/nlogo.jpg)](http://www.360doc.com/index.html)

[![img](http://pubimage.360doc.com/head/weixin/100.jpg)我的图书馆](http://www.360doc.com/my360doc.aspx)

[留言交流](http://www.360doc.com/advice.html)



[一生一世](http://www.360doc.com/userhome/75049036) / [待分类](http://www.360doc.com/userhome.aspx?userid=75049036&cid=-1000) / [OpenWrt 使用 KodExplorer (可道云) 搭建...](javascript:void(0))

[转word](javascript:void(0))[全屏](javascript:void(0))[修改](javascript:void(0))



![img](http://pubimage.360doc.com/NewArticle/bgcolor.jpg)

![img](http://pubimage.360doc.com/NewArticle/fontSize.jpg)

## OpenWrt 使用 KodExplorer (可道云) 搭建私有云存储

2021-04-29 转自 [KodExplorer](http://www.360doc.com/userhome/45661140) 私有

随着国内网盘一家接一家的倒闭，用户可以放心使用的网盘越来越少了，目前可以放心使用的好像只有百度和腾讯了，不过都存在种种限制。如果你只是想单纯的存储、管理文件，私有云可能是一个不错的解决方案。VPS 搭建私有云成本太高，NAS 方案一般小伙伴也不愿意折腾，随着路由器性能越来越高，在路由器上搭建私有云存储，成为了很多小伙伴的选择。今天教大家在 OpenWrt 路由器使用 KodExplorer 来搭建私有云存储。![KODExplorer](http://imgi101i120.360doc.com/DownloadImg/2017/11/2918/117618962_1_2017112906033896.png?Expires=1619709480&OSSAccessKeyId=LTAIth6fJnBvI6ht&Signature=uHrMuOv1Z%2Fj7SMA%2FSB0wChyNqk0%3D&domain=109)准备工作既然是私有云，肯定需要存储设备，最好用移动硬盘这种大容量设备，分区格式推荐为 ext4，如果你的固件 NTFS 速度快的话，无所谓，ext4 格式化方法可以看《[斐讯 K3 LEDE 安装迅雷远程下载](https://www.mivm.cn/k3-lede-thunder/)》中的步骤。可用空间 8M+ 内存 128M +最后，一颗不怕死的心，因为步骤稍微有点复杂。

# 搭建 Web 环境

首先，搭建 Web 环境，这里我们使用：Nginx + PHP 。上传、修改文件推荐使用 [WinSCP ](https://winscp.net/eng/docs/lang:chs)进行操作，如果你熟练使用 VI 等编辑器，无所谓，还有，SSH 连接好。

## Nginx

软件包搜索 nginx 并安装，安装完成后输入  返回 Nginx 版本号即安装成功。Nginx 和 uhttpd 都是80端口，所以需要改下其中某个服务的端口。Nginx：修改文件：/etc/nginx/nginx.conf，大概第36行， 将 80 改为其他端口 (1 – 65536)。

## uhttpd

：修改文件：/etc/config/uhttpd，第3行和第4行，  将 80 改为其他端口(1 – 65536)。如果改了 uhttpd 端口，输入  重启 uhttpd。不是80端口的服务访问地址需要在路由器IP后面加端口，比如：192.168.1.1:8080输入  创建 Web 目录，路径根据你存储设备挂载路径自行更改。修改文件：/etc/nginx/nginx.conf第1行  改为 大概第44行，将  改为 Web 路径，示例： ，接着修改下一行：。

大概第65行，去掉注释，为 Nginx 配置 PHP。

location ~ \.php$ { root /mnt/sda1/www; # Web 目录路径 

try_files $uri =404; # PHP 文件不存在返回404 

fastcgi_pass unix:/var/run/php7-fpm.sock; # 通过 Unix 套接字执行 PHP 

fastcgi_index index.php; 

fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name; # 修复 Nginx fastcgi 漏洞 

include fastcgi_params; 

}

## PHP

软件包搜索 php7-fpm 并安装，安装完成后输入  返回 PHP 版本号即安装成功。安装所需 PHP 模块，软件包：php7-mod-curl php7-mod-gd php7-mod-iconv php7-mod-json php7-mod-mbstring php7-mod-opcache php7-mod-session php7-mod-zip，比较多，用命令安装吧：

修改文件：/etc/php.ini去掉注释并改为存储设备路径 + :/tmp/:/proc/ 示例： 改为  如果你的设备内存较大的话，可以适当增加。注释  ( 前面加一个分号 ; ) 和  改为  和  该值不能大于 memory_limit 且 upload_max_filesize 不能大于 post_max_size修改文件：/etc/php7-fpm.d/www.conf 改为  去掉注释 去掉注释修改文件：/etc/init.d/php7-fpm 改为 输入 创建 PHP 调试文件， 重启 Nginx 和 PHP-FPM，浏览器访问 Nginx/info.php，比如：192.168.1.1:8080/info.php，输出 PHP 信息即为配置成功。![PHP](http://imgi101i120.360doc.com/DownloadImg/2017/11/2918/117618962_2_20171129060338440.png?Expires=1619709480&OSSAccessKeyId=LTAIth6fJnBvI6ht&Signature=hjhDLEn2JpePmiKm%2B9VwWZefh5E%3D&domain=109)Web 环境配置完成，接下来安装 KodExplorer。KodExplorer前往 [https://kodcloud.com](https://kodcloud.com/) 下载 KodExplorer 并上传路由器，输入  解压，比如： ，如果提示找不到命令：unzip，安装 unzip 软件包即可，也可以解压后再上传。浏览器访问 Nginx 设置 KodExplorer 管理员密码，设置完成后即可登陆。KodExplorer 特色完善的文件管理功能，完美取代 FTP，像使用操作系统一样的体验。在线预览，几乎支持所有格式的在线预览，图片、音乐、视频、文本等等。支持多用户、分组权限管理。强大的代码编辑器，几乎支持所有语言代码的在线编辑，代码高亮、自动补全、多标签、Zend Codeing 支持。![KODExplorer 登录](http://imgi101i120.360doc.com/DownloadImg/2017/11/2918/117618962_3_20171129060338768.jpg?Expires=1619709480&OSSAccessKeyId=LTAIth6fJnBvI6ht&Signature=cOmw0fS3dgUzuCZGQeKQnwlHk6Q%3D&domain=109)![KODExplorer 文件管理](http://imgi101i120.360doc.com/DownloadImg/2017/11/2918/117618962_4_2017112906033918.jpg?Expires=1619709480&OSSAccessKeyId=LTAIth6fJnBvI6ht&Signature=ZuvX46zaJXotgSKmxPBKeUaBkFY%3D&domain=109)![KODExplorer 代码编辑器](http://imgi101i120.360doc.com/DownloadImg/2017/11/2918/117618962_5_20171129060339284.png?Expires=1619709480&OSSAccessKeyId=LTAIth6fJnBvI6ht&Signature=2v5rpGtLCzptbKnePD6S9oDBfp0%3D&domain=109)KodExplorer 我个人觉得还是可以的，虽然不支持文件同步，不过也有很多特色功能，比如代码编辑器、多种文件格式预览，而且不依赖于数据库，对硬件要求较小。KodExplorer 使用中遇到任何问题，可前往[官网](https://kodcloud.com/)或[论坛](https://bbs.kodcloud.com/)寻找答案。最后说几句为什么用 KodExplorer？开始是想搭建 ownCloud，但遇到点问题。opkg 源的 MySQL 版本太旧，ownCloud 最新版本需要 5.5 +，虽然 PostgreSQL 可以用，但是太耗性能，如果使用旧版本 ownCloud 可能不兼容 PHP7，所以选择了 KodExplorer。 