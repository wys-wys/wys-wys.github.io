问题：从windows系统上获取linux ftp文件，一直获取不到，但是自己新建文件就可以读到，用户，密码都没问题，别人建的文件也获取不到，查询相关文档发现模式也不对。

解决方案：
把allow_ftpd_full_access off
状态改为allow_ftpd_full_access on即可
具体命令：
查看：sestatus -b | grep ftp
更改：setsebool allow_ftpd_full_access 1

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018110119422046.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI1NjMxNjI3,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181101194333344.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI1NjMxNjI3,size_16,color_FFFFFF,t_70)