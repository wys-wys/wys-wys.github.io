## 需求简介

基于nginx搭建了一个https访问的虚拟主机，监听的域名是test.com，但是很多用户不清楚https和http的区别，会很容易敲成http://test.com，这时会报出404错误，所以我需要做**基于test.com域名的http向https的强制跳转**

我总结了三种方式，跟大家共享一下

 

 

## nginx的rewrite方法

 

### 思路

这应该是大家最容易想到的方法，将所有的http请求通过rewrite重写到https上即可

 

### 配置

 

1. server { 
2.   listen 192.168.1.111:80; 
3.   server_name test.com; 
4.    
5.   rewrite ^(.*)$ https://$host$1 permanent; 
6. } 


搭建此虚拟主机完成后，就可以将http://test.com的请求全部重写到https://test.com上了

原文：http://blog.csdn.net/wzy_1988/article/details/8549290

 

## 需求简介

基于nginx搭建了一个https访问的虚拟主机，监听的域名是test.com，但是很多用户不清楚https和http的区别，会很容易敲成http://test.com，这时会报出404错误，所以我需要做**基于test.com域名的http向https的强制跳转**

我总结了三种方式，跟大家共享一下

 

 

## nginx的rewrite方法

 

### 思路

这应该是大家最容易想到的方法，将所有的http请求通过rewrite重写到https上即可

 

### 配置

1. server { 
2.   listen 192.168.1.111:80; 
3.   server_name test.com; 
4.    
5.   rewrite ^(.*)$ https://$host$1 permanent; 
6. } 


搭建此虚拟主机完成后，就可以将http://test.com的请求全部重写到https://test.com上了

 

 

## nginx的497状态码

 

### error code 497

1. 497 - normal request was sent to HTTPS 


解释：当此虚拟站点只允许https访问时，当用http访问时nginx会报出497错误码

 

### 思路

利用error_page命令将497状态码的链接重定向到https://test.com这个域名上

 

### 配置

1. server { 
2.   listen    192.168.1.11:443; #ssl端口 
3.   listen    192.168.1.11:80;  #用户习惯用http访问，加上80，后面通过497状态码让它自动跳到443端口 
4.   server_name test.com; 
5.   \#为一个server{......}开启ssl支持 
6.   ssl         on; 
7.   \#指定PEM格式的证书文件  
8.   ssl_certificate   /etc/nginx/test.pem;  
9.   \#指定PEM格式的私钥文件 
10.   ssl_certificate_key /etc/nginx/test.key; 
11.    
12.   \#让http请求重定向到https请求  
13.   error_page 497 https://$host$uri?$args; 
14. } 

 



## index.html刷新网页

 

### 思路

上述两种方法均会耗费服务器的资源，我们用curl访问baidu.com试一下，看百度的公司是如何实现baidu.com向www.baidu.com的跳转

 

![image-20210830191651834](C:\Users\26575\AppData\Roaming\Typora\typora-user-images\image-20210830191651834.png)

可以看到百度很巧妙的利用meta的刷新作用，将baidu.com跳转到www.baidu.com.因此我们可以基于http://test.com的虚拟主机路径下也写一个index.html，内容就是http向https的跳转

 

### index.html

1. <html> 
2. <meta http-equiv="refresh" content="0;url=https://test.com/"> 
3. </html> 



### nginx虚拟主机配置

1. server { 
2.   listen 192.168.1.11:80; 
3.   server_name test.com; 
4.    
5.   location / { 
6. ​        \#index.html放在虚拟主机监听的根目录下 
7. ​    root /srv/www/http.test.com/; 
8.   } 
9. ​    \#将404的页面重定向到https的首页 
10.   error_page 404 https://test.com/; 
11. } 