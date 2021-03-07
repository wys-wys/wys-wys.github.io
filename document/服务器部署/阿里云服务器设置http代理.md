# [用阿里云搭建Http代理服务器](https://www.cnblogs.com/jinhengyu/p/10257846.html)

先说下我的运行环境:

Ubuntu16.04+python3.5，用的是阿里云ECS乞丐版。

 

**搭建步骤:**

 

**[python]** [view plain](http://blog.csdn.net/u014563989/article/details/77984998?locationNum=1&fps=1#) [copy](http://blog.csdn.net/u014563989/article/details/77984998?locationNum=1&fps=1#)



1. \0. 直接用xshell或putty远程到云服务器 
2.  
3. \1. pip3 install shadowsocks 
4.  
5. \2. ssserver -p 443 -k password -m rc4-md5 --user nobody -d start 
6.  
7. \3. apt-get install privoxy 
8.  
9. \4. vi /etc/privoxy/config 
10. 修改属性: 
11. listen-address :8118 
12. enable-remote-toggle 1 
13.  
14. 文件末尾添加: 
15. forward-socks5 / 127.0.0.1:443 
16.  
17. \5. service privoxy restart 
18.  
19. \6. 此时配置+启动都已经全部完成, 接下来测试一下就行, 随便找个网易云音乐设置下http代理, 端口填8118, 点测试, 显示成功就证明OK 
20.  
21. \7. 停掉代理: service privoxy stop 