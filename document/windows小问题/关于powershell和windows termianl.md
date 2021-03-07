- [ ] #### 解决：Win10系统下，打开终端，提示 “无法加载文件C:\XXX\WindowsPowerShell\profile.ps1"的问题

**解决办法：**

1.win10左下角点击logo，找到Windows Powershell，右击，然后以管理员身份打开.

2.打开后，输入：

```
get-ExecutionPolicy   # 查看系统执行策略状态



 



set-executionpolicy remotesigned # 修改执行策略状态
```

3.之后，关闭Windows Powershell即可。

4.此外，关闭VScode，然后重新打开VScode，然后在终端就可以正常输入脚本执行操作了。

ns lookup 查看当前提供域名解析的dns服务器

