更改dns或者使用以前备份的配置文件然后上传相应的内核文件即可



参考：http://www.openwrt.org.cn/bbs/thread-1639-1-1.html



我在openwrt的web界面修改的wan口dns服务器为8.8.8.8。但是通过ssh查看/etc/resolv.conf文件发现总是被重置为了：

root@Wrv54g:~# cat /etc/resolv.conf 
search lan
nameserver 127.0.0.1
复制代码
据我观察在web刚改完之后有几秒保持了我修改的dns，但之后马上会被重置，请问是什么原因？
root@Wrv54g:~# cat /etc/resolv.conf 
nameserver 127.0.0.1
nameserver 8.8.8.8
nameserver 8.8.4.4
root@Wrv54g:~# cat /etc/resolv.conf 
nameserver 127.0.0.1
nameserver 8.8.8.8
nameserver 8.8.4.4
root@Wrv54g:~# cat /etc/resolv.conf 
search lan
nameserver 127.0.0.1
root@Wrv54g:~# cat /etc/resolv.conf 
search lan
nameserver 127.0.0.1
root@Wrv54g:~# cat /etc/resolv.conf 
search lan
nameserver 127.0.0.1
root@Wrv54g:~#
复制代码
dnsmasq重置了！实际使用的是/tmp/resolv.conf.auto


修改/etc/config/network 文件
config 'interface' 'lan'            
        option 'type' 'bridge'      
        option 'ifname' 'eth0.0'    
        option 'proto' 'static'     
        option 'netmask' '255.255.255.0'
        option 'dns' '208.67.222.222'   
        option 'gateway' '192.168.3.1'  
        option 'ipaddr' '192.168.3.250'

root@Raspberry:/#  /etc/init.d/dnsmasq restart
————————————————
版权声明：本文为CSDN博主「zjqlovell」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/zjqlovell/article/details/78598959

