【摘要】 1、先安装yum-utils[root@izgu3e8gvhx2vgz~]#yuminstallyum-utils2、添加nginx源。创建文件/etc/yum.repos.d/nginx.repo，文件内容如下：[root@izgu3e8gvhx2vgz~]#vim/etc/yum.repos.d/nginx.repo[nginx-stable]name=nginxstabl...

1、先安装 yum-utils

> [root@izgu3e8gvhx2vgz ~]# yum install yum-utils

2、添加nginx源。创建文件/etc/yum.repos.d/nginx.repo，文件内容如下：

> [root@izgu3e8gvhx2vgz ~]# vim /etc/yum.repos.d/nginx.repo
> [nginx-stable]
> name=nginx stable repo
> baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
> gpgcheck=1
> enabled=1
> gpgkey=https://nginx.org/keys/nginx_signing.key
> module_hotfixes=true
>
> [nginx-mainline]
> name=nginx mainline repo
> baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
> gpgcheck=1
> enabled=0
> gpgkey=https://nginx.org/keys/nginx_signing.key
> module_hotfixes=true

3，查看nginx源

> [root@iZ2ze5oztlicgchxp8yrrtZ ]# yum info nginx
> Repository AppStream is listed more than once in the configuration
> Repository extras is listed more than once in the configuration
> Repository PowerTools is listed more than once in the configuration
> Repository centosplus is listed more than once in the configuration
> Last metadata expiration check: 0:15:39 ago on Tue 11 Aug 2020 03:30:35 PM CST.
> Installed Packages
> Name : nginx
> Epoch : 1
> Version : 1.18.0
> Release : 1.el8.ngx
> Architecture : x86_64
> Size : 3.6 M
> Source : nginx-1.18.0-1.el8.ngx.src.rpm
> Repository : @System
> From repo : nginx-stable
> Summary : High performance web server
> URL : http://nginx.org/
> License : 2-clause BSD-like license
> Description : nginx [engine x] is an HTTP and reverse proxy server, as well as
> : a mail proxy server.

4、安装nginx

> [root@izgu3e8gvhx2vgz ~]# yum install nginx

5、验证nginx是否安装成功

> [root@iZ2ze5oztlicgchxp8yrrtZ]# nginx -v
> nginx version: nginx/1.18.0