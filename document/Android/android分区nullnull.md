# Android系统(HTC的机子)中所提到的HBOOT和recovery有什么区别？ *5*

下面说的，一些内容，和刚才你所说的有点不同，
主要是SPL的解释方面。
为什么HBOOT,recovery,SPL都有版本号呢？
就是这3个东西是不同的吧？经过你的解说，HBOOT和recovery我都能理解了。
但是SPL还是理解不了。。。

------------------下面是技术贴的内容，麻烦解释-------------------
分区解释:
system:系统分区.我们刷机器一般就是刷的这个分区.
userdata:数据分区.
cache:缓存分区
recovery:Recovery分区.
boot:存放内核和ramdisk的分区.
hboot:这个是SPL所在的分区.很重要哦.也是fastboot所在的分区.刷错就真的变砖了.
splash1:这个就是开机第一屏幕了.
radio:这个是无线所在的分区.
misc:其他分区.放的是htc的一些东西.

比如你的机器是G3.那么您的机器需要具备的条件是:SPL版本1.76.2007 S-OFF
现在您需要刷recovery.那么您需要找对recovery版本.
之前的问题以及回答：
________________________________________________

看了大量的资料，觉得HBOOT是比recovery更底层的一个界面，
其实两个界面都和电脑的BOIS设置差不多，只不过recoverry是建立在HBOOT上面的。

另外还想确认一点，HTC的手机中，
SPL(英文全称是SecondProgramLoader)=HBOOT是这样理解吧？
期待高手解答。

-------回答 共1条-------
hboot是最底层的，相当于电脑的bios，负责电脑的POST过程一样。
recovery相当于建立在hboot与android系统间的一个中间层，如名字一般，主要用于系统调试和恢复。你可以理解成类似于PC里windowsPE这种作用的系统。
SPL相当于hboot+recovery吧。比如G1刷机的时候，就相当于先降级SPL获取漏洞，然后通过替换签名的recovery获取刷机的权限。