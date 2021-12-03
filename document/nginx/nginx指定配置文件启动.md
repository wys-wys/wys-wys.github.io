第一步：先关闭nginx， kill掉所有的nginx进程

```
pkill -9 nginx
# 运行命令参看nginx服务是否关闭
netstat -tnulp | grep nginx # 参看端口是否关闭
systemctl status nginx  # 查看服务是否关闭
```

![img](https://img-blog.csdnimg.cn/20201026181626775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpbmExMDA=,size_16,color_FFFFFF,t_70)

第二步： 指定nginx的启动配置文件，要写完整路径

```
nginx -c -t /etc/nginx/nginx.conf # 配置文件路径
# -c </path/to/config> 为 Nginx 指定一个配置文件，来代替缺省的。

# -t 不运行，而仅仅测试配置文件。nginx 将检查配置文件的语法的正确性，并尝试打开配置文件中所引用到的文件
```