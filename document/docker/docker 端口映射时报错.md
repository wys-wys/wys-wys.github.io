# docker: Error response from daemon: driver failed programming external connectivity on endpoint lamp

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

置顶 [米粥粥](https://blog.csdn.net/qq_41545647) 2019-10-22 11:38:53 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 21509 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 22

分类专栏： [无穷报错](https://blog.csdn.net/qq_41545647/category_9443428.html) [虚拟化](https://blog.csdn.net/qq_41545647/category_9368812.html) 文章标签： [Docker报错](https://www.csdn.net/tags/NtTaYgxsODA1My1ibG9n.html) [端口映射](https://www.csdn.net/tags/MtTaEg0sMTIwODMtYmxvZwO0O0OO0O0O.html) [docker容器](https://www.csdn.net/tags/NtTaYgzsMjA4OS1ibG9n.html)

版权

**Docker容器做端口映射报错**
docker: Error response from daemon: driver failed programming external connectivity on endpoint lamp3 (46b7917c940f7358948e55ec2df69a4dec2c6c7071b002bd374e8dbf0d40022c): (iptables failed: iptables --wait -t nat -A DOCKER -p tcp -d 0/0 --dport 86 -j DNAT --to-destination 172.17.0.2:80 ! -i docker0: iptables: No chain/target/match by that name.
**解决方法**
docker服务启动时定义的自定义链DOCKER被清除
重启即可`systemctl restart docker`