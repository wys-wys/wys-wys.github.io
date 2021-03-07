## de为何客户端软件可以而浏览器则不能连接FTP服务器

2013年05月13日 ⁄ 综合 ⁄ 共 1891字 ⁄ 字号 [小](javascript:doZoom(12)) [中](javascript:doZoom(13)) [大](javascript:doZoom(18)) ⁄ 评论关闭

为了便于工作，在REHL5上面使用vsftp快速配置了FTP服务器，并在/etc/sysconfig/iptables中开启了20, 21端口。

在我的电脑上打开IE浏览器，发现无法匿名访问，但是通过命令行方式可以访问，同时通过FTP客户端软件也可以正常访问。

这就奇怪了？根据以上分析应该服务器设置是正确的，且网络也是没有问题的。那是为什么呢？

通过查询资料，发现FTP服务存在主动(Active Mode)与被动(Passive Mode)两种模式的服务。

检查/etc/vsftpd/vsftpd.conf文件，发现没有设置被动模式，而我的IE浏览器的工具-》Internet-》高级中，IE浏览器设置为使用被动FTP模式。

因此我修改vsftpd.conf文件，设置FTP服务器为被动模式。修改方式如下：

pasv_enable=YES
pasv_min_port=3000
pasv_max_port=4000

同时修改/etc/sysconfig/iptables打开端口3000到4000，具体可查阅相关资料。

为何被动模式需要设置最小、最大端口呢？

这就需要了解一下主动模式与被动模式FTP服务的机制：

FTP是基于TCP协议的，而不是基于UDP的，FTP与其他协议不同，使用两个控制命令(command port)与数据(data port)两个端口。

通常使用21作为命令端口，20作为数据端口。

一、主动模式

1、客户端随机从一大于1023的端口（比如1030）基于FTP协议向服务器端的21端口发起连接。

2、服务器端从21端口向客户端确认连接

3、服务器端从20数据端口**主动**连接客户端的1031（1030+1）端口

4、客户端从1031端口向20端口确认连接

这样形成了控制命令与数据传输两条连接，21-1030 20-1031

但是主动模式有一个要注意的地方就是，由于服务器端会主动向客户端发出连接请求，在客户端防火墙处可能会认为此为网络入侵，若不放开规则，可能会被客户端拒绝。

二、被动模式

1、客户端随机从一大于1023的端口（比如1030）基于FTP协议向服务器端的21端口发起连接。

2、服务器端从21端口向客户端确认连接，

3、客户端通过控制命令通道高速服务器端应该在哪一个端口（>1023）监听数据连接，比如2000。

4、客户端从1031端口向约定的2000端口发起连接，建立数据传输通道。

5、服务器端从2000向客户端1031端口确认连接。

这样形成了控制命令与数据传输两条连接，21-1030 2000-1031

但是被动模式有一个要注意的地方就是，服务器端被动在>1023的约定端口监听来自客户端的连接请求，故应该在服务器端防火墙侧打开此端口。

三、总结

**Active FTP :**

**command :** client >1023 -> server 21

**data :** client >1023 <- server 20

**Passive FTP :**

**command :** client >1023 -> server 21

**data :** client >1023 -> server >1023

主动模式对服务器端有利，被动模式对客户端有利。但是服务器端既然要提供FTP服务，应该在服务器端设置防火墙规则，提供被动模式服务，而不能要求所有的客户端都设置防火墙规则以适应主动服务模式。当然服务器端在提供被动模式服务时，出于安全考虑，应该设置客户端可发起数据连接的端口范围，这就是上面配置文件中的

pasv_min_port=3000
pasv_max_port=4000

即告诉客户端可以向3000与4000之间的端口发起数据连接。

摘取国外网站上的一段英文如下：

Active FTP is beneficial to the FTP server admin, but detrimental to the client side admin. The FTP server attempts to make connections to random high ports on the client, which would almost certainly be blocked by a firewall on the client side. Passive FTP is beneficial to the client, but detrimental to the FTP server admin. The client will make both connections to the server, but one of them will be to a random high port, which would almost certainly be blocked by a firewall on the server side.为何客户端软件可以而浏览器则不能连接FTP服务器

2013年05月13日 ⁄ 综合 ⁄ 共 1891字 ⁄ 字号 [小](javascript:doZoom(12)) [中](javascript:doZoom(13)) [大](javascript:doZoom(18)) ⁄ 评论关闭

为了便于工作，在REHL5上面使用vsftp快速配置了FTP服务器，并在/etc/sysconfig/iptables中开启了20, 21端口。

在我的电脑上打开IE浏览器，发现无法匿名访问，但是通过命令行方式可以访问，同时通过FTP客户端软件也可以正常访问。

这就奇怪了？根据以上分析应该服务器设置是正确的，且网络也是没有问题的。那是为什么呢？

通过查询资料，发现FTP服务存在主动(Active Mode)与被动(Passive Mode)两种模式的服务。

检查/etc/vsftpd/vsftpd.conf文件，发现没有设置被动模式，而我的IE浏览器的工具-》Internet-》高级中，IE浏览器设置为使用被动FTP模式。

因此我修改vsftpd.conf文件，设置FTP服务器为被动模式。修改方式如下：

pasv_enable=YES
pasv_min_port=3000
pasv_max_port=4000

同时修改/etc/sysconfig/iptables打开端口3000到4000，具体可查阅相关资料。

为何被动模式需要设置最小、最大端口呢？

这就需要了解一下主动模式与被动模式FTP服务的机制：

FTP是基于TCP协议的，而不是基于UDP的，FTP与其他协议不同，使用两个控制命令(command port)与数据(data port)两个端口。

通常使用21作为命令端口，20作为数据端口。

一、主动模式

1、客户端随机从一大于1023的端口（比如1030）基于FTP协议向服务器端的21端口发起连接。

2、服务器端从21端口向客户端确认连接

3、服务器端从20数据端口**主动**连接客户端的1031（1030+1）端口

4、客户端从1031端口向20端口确认连接

这样形成了控制命令与数据传输两条连接，21-1030 20-1031

但是主动模式有一个要注意的地方就是，由于服务器端会主动向客户端发出连接请求，在客户端防火墙处可能会认为此为网络入侵，若不放开规则，可能会被客户端拒绝。

二、被动模式

1、客户端随机从一大于1023的端口（比如1030）基于FTP协议向服务器端的21端口发起连接。

2、服务器端从21端口向客户端确认连接，

3、客户端通过控制命令通道高速服务器端应该在哪一个端口（>1023）监听数据连接，比如2000。

4、客户端从1031端口向约定的2000端口发起连接，建立数据传输通道。

5、服务器端从2000向客户端1031端口确认连接。

这样形成了控制命令与数据传输两条连接，21-1030 2000-1031

但是被动模式有一个要注意的地方就是，服务器端被动在>1023的约定端口监听来自客户端的连接请求，故应该在服务器端防火墙侧打开此端口。

三、总结

**Active FTP :**

**command :** client >1023 -> server 21

**data :** client >1023 <- server 20

**Passive FTP :**

**command :** client >1023 -> server 21

**data :** client >1023 -> server >1023

主动模式对服务器端有利，被动模式对客户端有利。但是服务器端既然要提供FTP服务，应该在服务器端设置防火墙规则，提供被动模式服务，而不能要求所有的客户端都设置防火墙规则以适应主动服务模式。当然服务器端在提供被动模式服务时，出于安全考虑，应该设置客户端可发起数据连接的端口范围，这就是上面配置文件中的

pasv_min_port=3000
pasv_max_port=4000

即告诉客户端可以向3000与4000之间的端口发起数据连接。

摘取国外网站上的一段英文如下：

Active FTP is beneficial to the FTP server admin, but detrimental to the client side admin. The FTP server attempts to make connections to random high ports on the client, which would almost certainly be blocked by a firewall on the client side. Passive FTP is beneficial to the client, but detrimental to the FTP server admin. The client will make both connections to the server, but one of them will be to a random high port, which would almost certainly be blocked by a firewall on the server side.