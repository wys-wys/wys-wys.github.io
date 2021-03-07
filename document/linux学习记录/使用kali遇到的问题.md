# arpspoof未找到命令解决方法

最后更新时间：2020-06-30 12:34:31
[kali](https://www.perfcode.com/tag/kali) [arpspoof](https://www.perfcode.com/tag/arpspoof) [arp](https://www.perfcode.com/tag/arp)

------

arpspoof 是一款进行arp欺骗的工具，攻击者通过毒化受害者arp缓存，将网关mac替换为攻击者mac，然后攻击者可截获受害者发送和收到的数据包，可获取受害者账户、密码等相关敏感信息。

运行 arpspoof 命令时提示：arpspoof未找到命令

其原因是你还未安装 arpspoof 工具；

arpspoof 是 dsniff 的一个附属工具，所以我们需要安装的是 dsniff ：

```shell
apt-get install dsniff
```