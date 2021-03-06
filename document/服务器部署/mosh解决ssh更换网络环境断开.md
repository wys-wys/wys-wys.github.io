# Mosh介绍

APR 5TH, 2013 | [COMMENTS](http://blog.linjunhalida.com/blog/mosh/#disqus_thread)

![image](http://mosh.mit.edu/mosh.png)

这年头做技术没有人不用ssh的吧，然后ssh使用起来还是很不爽的， 远程服务器慢的时候反应慢，ssh有的时候断掉要重新连。。。

[mosh](http://mosh.mit.edu/)是ssh的替代方案，用来解决慢速网络和移动网络的问题，具体上来说：

- 连上一台服务器后，不管你切换什么网络，或者网络断掉，或者机器休眠又醒过来，连接都能够一直保持。
- 缓存输入输出，当连接慢的时候，屏幕上面显示的响应还是很快。

我**强烈**建议大家都去用它。

## 原理

mosh它实现了一套自有的状态同步协议SSP：

- 底层采用UDP，client和网络解耦合，
- 内部client和server都维护到屏幕和输入的状态，根据状态发送diff/patch。
- 再在上层加上一个预测模块，根据用户输入先在本地显示预期的输出结果，收到远程服务器返回的屏幕数据，再更新。

作者同时也提出，现在的应用往往没有针对移动作优化，如果一个用户切换了网络（比如正在移动中）， 那么tcp连接断掉会出现各种问题，在这种场景下，SSP这种解决方案会很有用处。

建议大家可以看看mosh首页的视频，作者介绍得很充分。

## 使用

大家去看[首页的介绍](http://mosh.mit.edu/)就好。这里整理一些我觉得需要提到的：

mosh首先通过ssh连进去，然后开启一个mosh server，端口随机在60000:61000，如果你开了防火墙需要允许这个范围。

指定ssh参数，比如你的ssh端口不是22：



```
mosh $server --ssh='ssh -p 2222' 
```

当你在网络断开的时候，关掉了mosh的进程，远程服务器上面对应的server进程会一直存在， 这个时候重新连上去的时候，就会提示你。这个时候你需要手动kill掉这个进程， 具体见[issue报告](https://github.com/keithw/mosh/issues/403)。

Posted by 机械唯物主义 Apr 5th, 2013