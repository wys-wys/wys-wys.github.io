## pip 安装缓存文件清理

这几天在清理 Windows 电脑 C 盘的时候，发现 `C:\Users\dta05\AppData\pip\Cache` 占用不少空间。本文分析并解决了这个问题。



## 安装包时不缓存

如果 pip 版本在 6.0 以上，我们可以在安装时使用`–no-cache-dir` 参数。举例：

```
pip --no-cache-dir install scipy
```

如果 pip 版本在 6.0 以下，我们可以使用如下命令升级 pip 版本：

```
pip install -U pip
```

## 删除已缓存文件

我们需要根据各自不同的操作系统，**直接删除对应目录的缓存文件即可**。

### Linux and Unix

```
~/.cache/pip
```

### OS X

```
~/Library/Caches/pip
```

### Windows

```
%LocalAppData%\pip\Cache
```

## 参考

- [删除 pip 安装缓存](https://blog.csdn.net/kangkanglou/article/details/78955298)
- [Removing pip’s cache?](https://stackoverflow.com/questions/9510474/removing-pips-cache)

推荐文章

- [Ubuntu 内置的 Python3.5 安装 pip 模块](https://tding.top/archives/399c2726.html)
- [Python 更改 pip 源至国内镜像](https://tding.top/archives/34737cef.html)
- [TMDb 电影数据分析](https://tding.top/archives/7e380af2.html)


----------- 本文结束啦感谢您阅读 -----------