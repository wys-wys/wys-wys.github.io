



###  服务端

直接使用docker  pull registry 然后 使用 docker   run  -d -p   5000：5000  registry

### 客户端

1. 修改配置文件，vim /etc/docker/daemon.json 

   {
  "insecure-registries": ["39.106.185.202:5000"]
   }

insecure-registries 不安全的注册 ，走的http协议，而非https

2. 然后 随便 拉取一个镜像 ，docker  pull busybox  ，
3. 打上标签  docker  tag busybox:lates  39.106.185.202:5000/busybox:latest
4. 推送 镜像，docker push   39.106.185.202:5000/busybox:latest    完成