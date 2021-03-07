# docker run -d  -t -p 81:80 centos:httpd bash

# Docker容器将在“docker run -d”后自动停止

根据我到目前为止阅读的教程，使用“`docker ps -a`”将从图像启动容器，容器将在后台运行。 这就是它的样子，我们可以看到我们已经有了容器ID。

```
root@docker:/home/root# docker run -d centos
605e3928cdddb844526bab691af51d0c9262e0a1fc3d41de3f59be1a58e1bd1d
```

但如果我跑“`docker ps -a`”，则不会返回任何内容。

所以我试过“`docker ps -a`”，我可以看到容器已经退出：

```
root@docker:/home/root# docker ps -a
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS                         PORTS               NAMES
605e3928cddd        centos:latest         "/bin/bash"         31 minutes ago      Exited (0) 31 minutes ago                          kickass_swartz
```

我做错了什么？ 我该如何解决这个问题？

[docker](https://www.itranslater.com/tag/2096467873936966656)

[J John](https://stackoverflow.com/users/4414185/j-john) asked 2019-03-17T08:50:31Z

9个解决方案

321 votes

centos dockerfile有一个默认命令`docker exec`。

这意味着，当在后台运行时（`docker exec`），shell立即退出。

2017年更新

更新版本的docker授权在分离模式和前台模式下运行容器（`docker exec`,`-d`或`-it`）

在这种情况下，您不需要任何其他命令，这就足够了：

```
docker run -t -d centos
```

bash将在后台等待。
这最初是在kalyani-chaudhari的回答中报道的，并在泽西豆的回答中详细说明。

```
vonc@voncvb:~$ d ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4a50fd9e9189        centos              "/bin/bash"         8 seconds ago       Up 2 seconds                            wonderful_wright
```

------

原始答案（2015）

如本文所述：

> 建议使用`-d`而不是运行`docker exec`，因为只需一个命令就可以运行容器，而不需要通过按Ctrl + P + Q来分离容器的终端。
>
> 但是，`docker exec`选项存在问题。 除非命令未在前台运行，否则容器会立即停止。
> Docker要求您的命令继续在前台运行。 否则，它认为您的应用程序停止并关闭容器。
>
> 问题是某些应用程序不在前台运行。 我们怎样才能让它变得更容易？
>
> 在这种情况下，您可以在命令中添加`docker exec`。
> 通过这样做，即使您的主命令在后台运行，您的容器也不会停止，因为尾部在前台继续运行。

这样可行：

```
docker run -d centos tail -f /dev/null
```

A `docker exec`将显示centos容器仍在运行。

从那里，你可以附加它或从它分离（或`docker exec`一些命令）。

[VonC](https://stackoverflow.com/users/6309/vonc) answered 2019-03-17T08:52:47Z

45 votes

根据这个答案，添加`-t`标志将阻止容器在后台运行时退出。 然后，您可以使用`docker exec -i -t <image> /bin/bash`进入shell提示符。

```
docker run -t -d <image> <command>
```

似乎-t选项没有很好地记录，尽管帮助说它“分配了一个伪TTY”。

[cjsimon](https://stackoverflow.com/users/2104168/cjsimon) answered 2019-03-17T08:53:23Z

18 votes

## 背景

Docker容器运行一个使其保持活动状态的进程（“命令”或“入口点”）。 只要命令继续运行，容器将继续运行。

在您的情况下，命令（默认情况下，`-t`，在`-i`上）立即退出（正如bash没有连接到终端并且无法运行时）。

通常，当您以守护进程模式运行容器（使用`-t`）时，容器正在运行某种守护进程（如`-i`）。 在这种情况下，只要httpd守护程序正在运行，容器将保持活动状态。

您似乎要做的是在容器内运行守护程序进程的情况下保持容器的活动状态。 这有点奇怪（因为容器在与它交互之前没有做任何有用的事情，可能是`-t`），但在某些情况下，做这样的事情可能是有意义的。

（你的意思是要在容器内部进行bash提示吗？这很简单！`-t`）

## 解

在容器模式下无限期地保持容器处于活动状态的一种简单方法是运行`-t`作为容器的命令。 这并不依赖于在守护进程模式下分配TTY等奇怪的事情。 虽然它依赖于做一些奇怪的事情，比如使用`-i`作为主要命令。

```
$ docker run -d centos:latest sleep infinity
$ docker ps
CONTAINER ID  IMAGE         COMMAND          CREATED       STATUS       PORTS NAMES
d651c7a9e0ad  centos:latest "sleep infinity" 2 seconds ago Up 2 seconds       nervous_visvesvaraya
```

## 替代方案

如cjsimon所示，`-t`选项分配“伪tty”。 这会让bash继续无限期地运行，因为它认为它连接到交互式TTY（即使你没有通过`-i`也无法与特定的TTY交互）。 无论如何，这应该也可以解决问题：

```
$ docker run -t -d centos:latest
```

不是100％肯定`-t`是否会产生其他奇怪的互动; 如果有，可以在下面留言。

[mkasberg](https://stackoverflow.com/users/1263211/mkasberg) answered 2019-03-17T08:55:06Z

13 votes

您好这个问题是因为如果容器中没有正在运行的应用程序，则docker容器会退出。

```
-d 
```

选项只是以守护进程模式运行容器。

因此，使容器持续运行的技巧是指向docker中的shell文件，它将使您的应用程序保持运行。您可以尝试使用start.sh文件

```
Eg: docker run -d centos sh /yourlocation/start.sh
```

这个start.sh应该指向一个永无止境的应用程序。

如果您不想运行任何应用程序，可以安装`monit`，这将使您的docker容器保持运行。请告知我们这两个案例是否适合您保持容器运行。

祝一切顺利

[Pratik](https://stackoverflow.com/users/3003758/pratik) answered 2019-03-17T08:56:09Z

7 votes

你可以用以下两种方法完成你想要的：

```
docker run -t -d <image-name>
```

要么

```
docker run -i -d <image-name>
```

要么

```
docker run -it -d <image-name>
```

其他答案（即tail -f / dev / null）建议的命令参数是完全可选的，并且不需要让容器在后台运行。

另请注意，Docker文档建议组合-i和-t选项将使其行为类似于shell。

看到：

[https://docs.docker.com/engine/reference/run/#foreground]

[jersey bean](https://stackoverflow.com/users/4143840/jersey-bean) answered 2019-03-17T08:57:16Z

6 votes

执行命令如下：

```
docker run -t -d <image-name>
```

如果要指定port，则命令如下：

```
docker run -t -d -p <port-no> <image-name>
```

使用以下命令验证正在运行的容器：

```
docker ps
```

[kalyani chaudhari](https://stackoverflow.com/users/5887772/kalyani-chaudhari) answered 2019-03-17T08:58:01Z

3 votes

Docker要求您的命令继续在前台运行。 否则，它认为您的应用程序停止并关闭容器。

因此，如果您的docker入口脚本是后台进程，如下所示：

```
/usr/local/bin/confd -interval=30 -backend etcd -node $CONFIG_CENTER &
```

'＆amp;' 如果以后没有触发其他前台进程，则使容器停止并退出。所以解决方案就是删除'＆amp;' 或者在其后运行另一个前景CMD，例如

```
tail -f server.log
```

[Peiming Hu](https://stackoverflow.com/users/5118359/peiming-hu) answered 2019-03-17T08:58:46Z

1 votes

也许只是我，但在CentOS 7.3.1611和Docker 1.12.6上，但我最终不得不使用@VonC＆amp; amp; @Christopher Simon让这个工作可靠。 在此之前我没有做任何事情会阻止容器在成功运行CMD后退出。 我正在启动oracle-xe-11Gr2和sshd。

Dockerfile

```
...
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' && systemctl enable sshd
...
CMD /etc/init.d/oracle-xe start && /sbin/sshd && tail -f /dev/null
```

然后添加-d -t和-i来运行

```
docker run --shm-size=2g --name oracle-db -d -t -i -p 5022:22 -p 5080:8080 -p 1521:1521 centos-oracle:7.3.1611 
```

最后几个小时后，我的头靠在墙上

```
ssh -v root@127.0.0.1 -p 5022
...
root@127.0.0.1's password: 
debug1: Authentication succeeded (password).
```

无论出于何种原因，如果删除尾部-f，或者省略任何-t -d -i选项，则在执行CMD之后上述将退出。

[steven87vt](https://stackoverflow.com/users/2583675/steven87vt) answered 2019-03-17T08:59:42Z

0 votes

我在以下帖子中解释过它有同样的问题。

如何在“退出”后使用docker alpine容器？

[vimal krishna](https://stackoverflow.com/users/2211208/vimal-krishna) answered 2019-03-17T09:00:19Z

translate from [https://stackoverflow.com:/questions/30209776/docker-container-will-automatically-stop-after-docker-run-d](https://stackoverflow.com/questions/30209776/docker-container-will-automatically-stop-after-docker-run-d)