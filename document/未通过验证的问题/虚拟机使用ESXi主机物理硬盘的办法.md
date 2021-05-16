# 虚拟机使用ESXi主机物理硬盘的办法

[![img](https://s3.51cto.com//wyfs02/M02/11/3E/wKioL1LODpihx-BxAAAYVdU4mf0354_middle.jpg)](https://blog.51cto.com/wangchunhai)

[王春海](https://blog.51cto.com/wangchunhai)关注20人评论[118973人阅读](javascript:;)[2018-06-19 15:22:06](javascript:;)

###  

**VMware Workstation****的虚拟机可以使用主机物理硬盘、主机上的USB****或并口、串口设备，作为虚拟机的企业版本VMware ESXi****也可以使用主机USB****或并口、串口设备，但默认情况下，ESXi****并不能使用主机物理硬盘。**

**VMware ESXi****的虚拟机可以主机USB****或并口、串口设备，也可以使用FC****、SAS HBA****接口卡或iSCSI****连接的存储磁盘（裸磁盘分配给虚拟机），但默认情况下并不能直接使用ESXi****主机本地的硬盘，必须得格式化成VMFS****存储才能分配给虚拟机使用。但在有些时候需要使用物理主机硬盘怎么办？本文将介绍解决办法。**



在单台主机的虚拟化环境中需要考虑“备份”。但是备份保存在相同存储是没有意义的，一个合理的方式是将备份保留到“其他位置”，这个其他位置最好网络中的其他主机。但在“单台主机”运营的情况下，将备份保存在主机以外的位置不太现实（如果主机托管到电信机房，并且机房带宽有限的情况下，将备份通过网络传输到外地不现实），此时要为备份提供“相对安全”的位置有如下几种方法：

（1）外置硬盘法。找一个较大容量（例如4TB、6TB、8TB）的USB移动硬盘，将该移动硬盘连接到服务器用做备份。但移动硬盘长期供电并接在服务器上并不是一个好的选择。

（2）非RAID磁盘法。在服务器中剩余的磁盘槽位中，单独插一块较大容量的硬盘（例如4TB），该硬盘不添加到RAID中，也不通过ESXi格式化为VMFS卷，而是分配给ESXi中的虚拟机直接使用（裸机映射的磁盘），这块硬盘将用做备份。例如，某台DELL R730XD的服务器配置了12块硬盘，这12块硬盘中的前10块配置成RAID-50（如图1所示），第11块作为“全局热备磁盘”（ID为10的磁盘，ID从0开始），第12块磁盘设置为“Non-RAID”磁盘（ID为11的磁盘），这第12块磁盘就是用做数据备份的磁盘，如图2所示。

[![clip_image002](https://s4.51cto.com/images/blog/201806/19/b7287f792df44bc50c4b29ce09886954.gif?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/b3bc9069950f58f119af48af6264ea62.gif?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图1 前10块磁盘组成RAID-50划分2个卷

[![clip_image004](https://s4.51cto.com/images/blog/201806/19/2e1ca92e19a3393b7d0af2bc55362d95.gif?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/4e25ca90ce55418c1b666afb62c304fd.gif?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图2 第11块为全局热备磁盘，第12块为Non-RAID磁盘

（3）在该ESXi主机上创建了名为“WS08R2_BE2016_172.20.1.22”的虚拟机，为该虚拟机分配4个vCPU（4个插槽，每插槽1个核心）、8GB内存。

默认情况下，ESXi的虚拟机不能直接使用物理主机硬盘，需要使用ssh登录到ESXi中，将主机硬盘映射才能使用，主要步骤如下。

（1）使用vSphere Client登录到ESXi，在“配置→存储器→设备”中，可以看到当前主机的设备，其中名称以DELL开头的则是用RAID卡划分的两个卷，而以ATA开头的则是在图15中配置为的Non RAID磁盘（相当于HBA直通），右键单击这个设备选择“将标识符复制到剪贴板”，如图7所示。

[![clip_image006](https://s4.51cto.com/images/blog/201806/19/4d882bd07e86bb9073cb47d5997a10e9.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/bc1d26c7e302430b9702e74b354ccf42.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图7 复制标识符

【说明】这个设备没有在ESXi添加为存储。单击“数据存储”可以看到当前添加了3个存储，图7中的4TB磁盘没有被添加为存储，如图8所示。后文的操作将这个4TB的硬盘“挂载”在某个现有分区中，例如图8中的Datastore分区。

[![clip_image008](https://s4.51cto.com/images/blog/201806/19/b6df5566320c50832d8d709bef0101b7.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/8b9da7bcb5f314e666891159181f9645.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图8 查看VMFS数据存储

（2）打开“记事本”，将上一步复制的标识符粘贴到“记事本”中，并保留naa.500等字符，如图9所示，然后再次将这个字符串复制。

[![clip_image010](https://s4.51cto.com/images/blog/201806/19/b38bec530f42be7dcbca70bef8daacef.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/df2679019cbaa3ac48d2d3370388e033.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图9 标识符

（3）使用ssh工具（例如Xshell 5）登录到ESXi主机，执行

ls /vmfs/disks

命令查看当前的设备，可以看到图9中记录的标识符。

[![clip_image012](https://s4.51cto.com/images/blog/201806/19/9bdbefdfd3aed423129d3392bcc0704b.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/e40866d068e50777d9c888a4f1be2da1.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图10 查看磁盘标识符

（4）执行以下命令，将物理磁盘添加到ESXi存储中，标识成一个虚拟磁盘。

vmkfstools -z /vmfs/devices/disks/<硬盘标识符> /vmfs/volumes/datastore1/<目标RDM磁盘名>.vmdk

在本示例中可以为

vmkfstools -z /vmfs/devices/disks/naa.50014ee0042fd6fd /vmfs/volumes/Datastore/WDC4TB.vmdk

注意磁盘标识名与vmfs等命令参数间不能有英文的空格，其中Datastore是VMFS分区名称。其中WDC4TB中的字母为大写，命令及执行过程如图11所示。

[![clip_image014](https://s4.51cto.com/images/blog/201806/19/e4b529ef288617547d799a908954eb73.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/4a38c6140c835bee3cd8abd1f5efb809.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图11 为物理磁盘建立RDM映射

（5）返回到vSphere Client，在“配置→存储器”中右键单击Datastore存储，选择“浏览数据存储”，）在“数据存储浏览器”中可以看到图11映射的磁盘，如图14所示。

[![clip_image016](https://s4.51cto.com/images/blog/201806/19/60e35c726d543584a4964cb612edb0b0.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/eecd6ad96656d51b5a79f036baab9a70.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图14 查看映射的RDM磁盘

（6）修改“WS08R2_BE2016_172.20.1.22”虚拟机的配置，添加硬件设备，在“添加硬件→选择磁盘”中选择“使用现有虚拟硬盘”，在“浏览数据存储”中，浏览Datastore存储根目录选择WDC4TB.vmdk虚拟硬盘，其他选择默认值。

（7）打开虚拟机电源，在“磁盘管理”中将新添加的4TB硬盘分区、格式化，设置盘符为D。

（8）在备份虚拟机中安装Veritas Backup Exec 2016（原Symantec公司的Backup Exec，现己改名）或其他备份软件，将其他虚拟机备份到D盘。图23是备份后的截图。

[![clip_image018](https://s4.51cto.com/images/blog/201806/19/e0259c053f13b1f68aa9263c4f803351.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com/images/blog/201806/19/1d97955aa69f28561cf489af57367baa.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

图23 备份后的截图

关于Veritas Backup Exec的安装、配置本文不做过多介绍，请自行配置。

【说明】将备份保存在单独的4TB的硬盘中，如果ESXi主机及RAID存储出现问题，可以取下4TB的磁盘，并将其挂在其他安装了Veritas Backup Exec 2016软件的计算机中，通过导入备份的方式，恢复虚拟机或数据，这是作为灾难恢复的一种方法。

©著作权归作者所有：来自51CTO博客作者王春海的原创作品，如需转载，请注明出处，否则将追究法律责任

## 如果文章对你有帮助，请赞赏

赞赏

1人进行了赞赏支持

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_13791795)

[云计算](https://blog.51cto.com/search/result?q=云计算)[虚拟化](https://blog.51cto.com/search/result?q=虚拟化)[esxi](https://blog.51cto.com/search/result?q=esxi)

4

分享

收藏

[上一篇：联想3850 X5服务器添加内存...](https://blog.51cto.com/wangchunhai/2107845)[下一篇：VMware vSAN中小企业应...](https://blog.51cto.com/wangchunhai/2149402)

[![img](https://s3.51cto.com//wyfs02/M02/11/3E/wKioL1LODpihx-BxAAAYVdU4mf0354_middle.jpg)](https://blog.51cto.com/wangchunhai)

[王春海](https://blog.51cto.com/wangchunhai) 

### 542篇文章，3109W+人气，3521粉丝

#### 伴随你一生的，唯有知识与能力！

关注

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/wangchunhai)

Ctrl+Enter 发布

发布

取消

20条评论

按时间倒序按时间正序

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_13660422)

[wx5ab0abee87d48](https://blog.51cto.com/u_13660422)

1楼 2018-06-19 15:32:52

不错

[![img](https://s5.51cto.com//oss/202103/08/a3a3295914a5a8cb0ee3bcd2c678efa3.jpg?x-oss-process=image/resize,m_fixed,h_120,w_120)](https://blog.51cto.com/u_89029)

[咖大啡](https://blog.51cto.com/u_89029)

2楼 2018-06-19 16:01:091

赞~

[![img](https://s1.51cto.com//wyfs02/M02/7E/65/wKioL1b-KUSgbZ1qAAApIeQSnSE164_middle.jpg)](https://blog.51cto.com/u_11258494)

[桩子尚品](https://blog.51cto.com/u_11258494)

3楼 2018-06-19 16:57:341

攒

[![img](https://s3.51cto.com//wyfs02/M00/10/DF/wKiom1LODdbAByNgAAAShtGiwRs389_middle.jpg)](https://blog.51cto.com/dynamic)

[CTO_LiuJinFeng](https://blog.51cto.com/dynamic)

4楼 2018-06-19 20:44:221

如果用Hyper-v，这不是很简单就可以用其它任何硬盘，没必要这麻烦?

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@CTO_LiuJinFeng ](https://blog.51cto.com/dynamic)

  使用Hyper-V或VMware ESXi，根据客户的需求、现状来选择的。 VMware Workstation、Hyper-V都可以“直接”使用主机物理硬盘的。 VMware ESXi不能“直接使用本机物理硬盘”，可以直接使用裸机映射的硬盘。

  2018-06-20 07:46:44

  回复

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/andylu0075)

[andylu0075](https://blog.51cto.com/andylu0075)

5楼 2018-06-20 08:57:301

写的很不错，收藏了。解决了独立虚拟机无法远程备份的难题。请教一个问题，EXSI宿主机，里的虚拟机2008R2的系统，如果要安装Workstation。 如何在2008R2 的虚拟机上开启虚拟化支持。EXSI是6.0的版本

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@andylu0075 ](https://blog.51cto.com/andylu0075)

  关闭虚拟机，修改虚拟机配置，在CPU选项中，在“硬件虚拟化”中，选中“向客户机操作系统公开硬件辅助的虚拟机”这一项。使用vSphere Web Client登录vCenter 管理ESXi，或者使用vSphere Host Client登录到ESXi主机。

  2018-06-20 12:22:55

  回复

[![img](https://s1.51cto.com//oss/201807/17/299ad3cbd947fe15e502c234be11ad0a.jpg?x-oss-process=image/resize,m_fixed,h_120,w_120)](https://blog.51cto.com/u_13846508)

[知心大叔](https://blog.51cto.com/u_13846508)

6楼 2018-07-12 18:46:18

我这眼神啊~ 看成王春梅了，哈哈哈。还以为是个大姐。

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_12157226)

[zhengwei9948aqw](https://blog.51cto.com/u_12157226)

7楼 2018-08-12 10:07:4151

REENAS LACP 可以提高带宽吗，比如，我是两张千兆网卡 LACP后，那么就应当是2Gb 如果我的客户端也是两张千兆网卡，那么 它们之间考贝文件，理论应当达到2Gb .是这样吗？？

还想请教一一下，这个LACP 与ESXI上的那个NIC TEAM 有什么区别呀，感觉是不是一样的呀，
期待你的回复

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@zhengwei9948aqw ](https://blog.51cto.com/u_12157226)

  LACP可以提高总的带宽，是所有使用这两张网卡的所有用户总的可用带宽，但任何一个应用，使用的还是其中的一张千兆网卡。所以，客户之间拷贝文件，无论是配置 几块网卡，还是使用其中的一张，所以还是千兆。

  2018-08-12 10:32:27

  回复

- [zhengwei9948aqw](https://blog.51cto.com/u_12157226)[:@王春海 ](https://blog.51cto.com/wangchunhai)

  您好，老师，感谢您的回复， 我现在有如下疑问想请教一下， 现在公司搭了一个FREENAS 服务器，用作共享存储，此服务器是有一个4口的千兆网卡。 由于ISCSI是基于TCP的原因，所以服务器与此共享存储之间的瓶颈就在于这个IP-ISCSI. 现在我的想法是 用两个网口 做 LACP 之 后，通过汇聚交换机 连上服务器， 这样服务器在访问 ISCSI上的数据时，速度会是2Gbps吗？？

  2018-08-12 11:05:45

  回复

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@zhengwei9948aqw ](https://blog.51cto.com/u_12157226)

  还是1G的。你可以这样理解： 你iSCSI服务器A的2个网卡做了LACP，两台服务器B、C同时访问A，各是1G； 如果你不做LACP，C与B两台服务器同时访问A，则各有0.5G。

  2018-08-12 12:02:19

  回复

还有2条回复

[![img](https://s2.51cto.com//oss/201812/13/2e32d5afbcc3dad95577f0d5bd4e5403.jpg?x-oss-process=image/resize,m_fixed,h_120,w_120)](https://blog.51cto.com/u_694642)

[bbq0927](https://blog.51cto.com/u_694642)

8楼 2019-05-13 16:51:231

王老师，请教一下，现在我的一台服务器做了一台VM，DELLR720的四个硬盘，现在空间不够了，需要增加容量，手上有6个硬盘，可以教一下，可以直接插入硬盘，然后在client端的控制台打开可以看到吗？还是要需要注意一些其他问题，或者是不可以这样，谢谢，FYI

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@bbq0927 ](https://blog.51cto.com/u_694642)

  服务器本地硬盘，一般需要使用RAID划分为卷，ESXi中才能看到（其他的Windows操作系统也是这样）。直接插上是不能用的。 重新启动服务器，按Ctrl+R进入RAID配置。添加RAID配置，新新添加的6个硬盘创建为新的卷，再进ESXi中将新添加的卷格式化为VMFS，或者附加到原来VMFS的后面扩展现有VMFS卷。

  2019-05-13 21:14:39

  回复

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_14699029)

[wx5e4cac28e8050](https://blog.51cto.com/u_14699029)

9楼 2020-02-19 11:34:321

王老师，在看了您的文章后想在本地环境试验一下，但是出现了个小问题。esxi6.7版本
执行命令：
vmkfstools -z /vmfs/devices/disks/mpx.vmhba1\:C0\:T1\:L0 /vmfs/volumes/datastore1/backup.vmdk
报错：
Failed to create virtual disk: Invalid argument (1441801).

您知道这个可能是什么原因导致的？

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@wx5e4cac28e8050 ](https://blog.51cto.com/u_14699029)

  你写的磁盘 标识符可能不对，你看一下图10、图11的示例，再重新检查一下 另外这个加载的磁盘 ，应该是没有使用（没有格式化为VMFS文件 系统的），使用的就不能再重新加载。

  2020-02-19 18:06:42

  回复

[![img](https://ucenter.51cto.com/images/noavatar_middle.gif)](https://blog.51cto.com/u_15007633)

[yun_we](https://blog.51cto.com/u_15007633)

10楼 2021-02-04 11:02:211

不错！
那主机里面的多台虚拟机，该怎么备份比较好呢？

- 作者[王春海](https://blog.51cto.com/wangchunhai)[:@yun_we ](https://blog.51cto.com/u_15007633)

  现在我们主要是使用Veeam来备份

  2021-02-04 11:13:20

  回复