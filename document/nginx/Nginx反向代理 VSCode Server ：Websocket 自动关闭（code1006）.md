Nginx反向代理 VSCode Server ：Websocket 自动关闭（code:1006）

分类专栏： Debugger 文章标签： nginx linux
版权

Debugger
专栏收录该内容
1 篇文章0 订阅
订阅专栏
NGINX 反向代理 VSCode Server 出现错误 ：Websocket 自动关闭（code:1006）

实际上是Nginx 缺少 WebSocket 代理的原因

 

解决方案 ： HTTP的Upgrade协议头机制用于将连接从HTTP连接升级到WebSocket连接，Upgrade机制使用了Upgrade协议头和Connection协议头

示例 vscode.conf 完整配置如下：

upstream vscode  {
    server 127.0.0.1:9000; #VSCode Server
}

#VSCode Server Err:1006 解决方案： https://www.cnblogs.com/qianxunman/p/13656874.html
#Nginx WebDSocket 代理 ： https://blog.csdn.net/chszs/article/details/26369257
map $http_upgrade $connection_upgrade {  
    default upgrade;  
    '' close;  
}

# another virtual host using mix of IP-, name-, and port-based configuration
server {
    listen       19000;

    location / {
        proxy_pass  http://vscode;
        #proxy_pass http://192.168.1.154:8080;
     
        #Proxy Settings https://www.cnblogs.com/wangzhisdu/p/7771069.html
        #Timeout Setting https://www.cnblogs.com/lianhaifeng/p/13525844.html
        proxy_http_version 1.1;  
        proxy_redirect     off;
        proxy_set_header   Host             $host;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header   Upgrade          $http_upgrade;  
        proxy_set_header   Connection       "Upgrade"; 
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_max_temp_file_size   0;
        proxy_connect_timeout      60;     #nginx与upstream server的连接超时时间(单位：s)
        proxy_send_timeout         90;     #nginx发送数据至 upstream server超时, 默认60s, 如果连续的60s内没有发送1个字节, 连接关闭
        proxy_read_timeout         90;    #nginx接收 upstream server数据超时, 默认60s, 如果连续的60s内没有收到1个字节, 连接关闭
        proxy_buffer_size          4k;       #代理请求缓存区_这个缓存区间会保存用户的头信息以供Nginx进行规则处理_一般只要能保存下头信息即可 
        proxy_buffers              4 32k;    #同上 告诉Nginx保存单个用的几个Buffer最大用多大空间
        proxy_busy_buffers_size    64k;      #如果系统很忙的时候可以申请更大的proxy_buffers 官方推荐*2
        proxy_temp_file_write_size 64k;   #proxy缓存临时文件的大小
        #proxy_temp_path  /usr/local/nginx/temp; #用于指定本地目录来缓冲较大的代理请求
    }
     
    location ~.*\.(js|css|html|png|jpg)$ {
        expires    3d;
    }
}