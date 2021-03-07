# Docker容器与主机间的文件传输方法(复制/上传/下载)

时间:2019-04-13

本文章向大家介绍Docker容器与主机间的文件传输方法(复制/上传/下载)，主要包括Docker容器与主机间的文件传输方法(复制/上传/下载)使用实例、应用技巧、基本知识点总结和需要注意事项，具有一定的参考价值，需要的朋友可以参考一下。

1、首先启动容器(以first-mysql容器为例)

```
docker start first-mysql
```

2、查看容器ID

```
root@kobe:/opt/software/temp/test# docker ps
CONTAINER ID    IMAGE        COMMAND         CREATED       STATUS       PORTS                    NAMES
688e83c55129    mysql        "docker-entrypoint.s…"  6 days ago     Up 3 seconds    0.0.0.0:3306->3306/tcp            first-mysql
688e83c55129    这个就是容器的ID了
```

3、新建需要复制的测试文件

示例位置和文件名  ` /opt/software/temp/test/test.txt`

4、复制到容器中

```
docker cp /opt/software/temp/test/test.txt 688e83c55129:/test/
```

5、进入容器查看是否已复制

```
docker exec -it 688e83c55129 bash
```

6、从容器复制文件到主机

先删除主机上的test.txt，然后

```
docker cp 688e83c55129:/test/test.txt /opt/software/temp/test/
```

以上就是主机与容器之间传输文件的方式了，简单易用。

**总结**

以上所述是小编给大家介绍的Docker容器与主机间的文件传输方法(复制/上传/下载)，希望对大家有所帮助，如果大家有任何疑问请给我留言，小编会及时回复大家的。在此也非常感谢大家对脚本之家网站的支持！