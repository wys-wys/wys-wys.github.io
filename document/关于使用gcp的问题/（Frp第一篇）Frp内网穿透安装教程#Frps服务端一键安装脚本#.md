（Frp第一篇）Frp内网穿透安装教程#Frps服务端一键安装脚本#

分类专栏： # Centos7
版权

Centos7
专栏收录该内容
2 篇文章1 订阅
订阅专栏
系统：CentOS7
内存：1G
CPU：单核1G
客户端安装教程：（Frp第二篇）Frp内网穿透安装教程#Frp OpenWrt客户端安装#图形化管理

注意事项：记得给使用的端口开放防火墙，开放防火墙，开放防火墙
Frps服务端一键配置脚本地址：https://github.com/MvsCode/frps-onekey

脚本有两个源，国外VPS可以用Github的源，国内的VPS建议使用Aliyun的源，要不可能很慢。本教程使用的就是Aliyun的源

#下载脚本
wget https://code.aliyun.com/MvsCode/frps-onekey/raw/master/install-frps.sh -O ./install-frps.sh
#设置脚本运行权限
chmod 700 ./install-frps.sh
#执行脚本
./install-frps.sh install
1、选择源，1是Aliyun，2是Github。我们选1



2、选择服务端口。默认是5443。这个端口的作用是在客户端连接服务端时是通过这个端口连接的。可以不用修改



3、设置http连接的端口。默认80，没有被占用就默认



4、设置https连接的端口。默认443，没有被占用就默认



5、设置面板的端口。直接用默认端口6443



6、设置登录面板的用户名和密码,根据个人喜好设置





7、设置token。客户端需要填写的



8、设置域名，如果有就填写，没有就默认IP



其他的配置就默认就好

安装好之后可以通过 frps config 指令修改或者查看配置。所以忘记了不怕

9、启动服务

frps start


最后，在浏览器中输入 http://ip:6443。如果打不开，请看看是不是VPS的防火墙没有开放6443端口。

如果成功就能看到如下的界面



 