检查openwrt的dns  /etc/resole.conf

修改dns，docker容器会使openwrt的dns错误

运行时如果提示tun内核无法下载或者更新，可手动到github上下载内核文件上传到相应目录下

https://github.com/vernesong/OpenClash/releases/tag/TUN

设置了clash后发现依然无法翻墙

故通过clash的yacd面板允许局域网，通过局域网代理的方式翻墙