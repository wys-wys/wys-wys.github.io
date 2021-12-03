> #### Nginx是一个web服务器也可以用来做负载均衡及反向代理使用，
>
> #### 目前使用最多的就是负载均衡，这篇文章主要介绍了centos8 安装 nginx
>
> #### Nginx是一种开源的高性能HTTP和反向代理服务器，负责处理Internet上一些最大站点的负载。
>
> #### 它可用作HTTP和非HTTP服务器的独立Web服务器，负载平衡器，内容缓存和反向代理。
>
> #### 与Apache相比，Nginx可以处理大量并发连接，并且每个连接的内存占用量较小。

## 一、下载Nginx

**官网**：http://nginx.org/

###### 创建文件夹 `mkdir nginx`

###### 进入创建的文件夹，根据需要下载合适的版本

![img](https://img2020.cnblogs.com/blog/1481359/202003/1481359-20200329215746420-701366744.png)

###### 通过 `wget http://nginx.org/download/nginx-1.17.6.tar.gz` 下载文件

## 二、安装必要插件

```
yum -y install gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel
```

> **这几个插件作用:**
>
> > **gcc** 可以编译 C,C++,Ada,Object C和Java等语言
> >
> > **pcre pcre-devel** pcre是一个perl库，包括perl兼容的正则表达式库，nginx的http模块使用pcre来解析正则表达式，所以需要安装pcre库
> >
> > **zlib zlib-devel** zlib库提供了很多种压缩和解压缩方式nginx使用zlib对http包的内容进行gzip，所以需要安装
> >
> > **openssl openssl-devel** openssl是web安全通信的基石，没有openssl，可以说我们的信息都是在裸奔

## 三、解压下载好的文件

```
tar -zxvf nginx-1.17.6.tar.gz
```

进入到 nginx-1.17.6文件夹下面

开始安装

如果不想指定安装路径直接执行 ./configure 即可



指定安装路径:`./configure --prefix=/software/nginx` 这句话的意思是指定安装路径

`make` 编译

`make install` 安装

进入到安装nginx目录下面的sbin

启动命令 `./nginx`

打开浏览器访问你的IP地址，显示此页面表示Nginx启动成功

![img](https://img2020.cnblogs.com/blog/1481359/202003/1481359-20200329220738238-519465839.png)

## 四、配置

##### 从容停止服务器

> ```
> nginx -s quit
> ```
>
> 这种方法较stop相比就比较温和一些了，需要进程完成当前工作后再停止。

##### 立即停止服务器

> ```
> nginx -s stop
> ```
>
> 这种方法比较强硬，无论进程是否在工作，都直接停止进程。

#### 查询nginx主进程号

> ```
> ps -ef | grep nginx
> ```
>
> 从容停止 kill -QUIT 主进程号
>
> 快速停止 kill -TERM 主进程号
>
> 强制停止 kill -9 nginx