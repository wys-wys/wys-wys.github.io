重启电脑解决

[@veqryn](https://github.com/veqryn) the workaround worked for me, the steps are:

1. Disable hyper-v (which will required a couple of restarts)
   `dism.exe /Online /Disable-Feature:Microsoft-Hyper-V`
2. When you finish all the required restarts, reserve the port you want so hyper-v doesn't reserve it back
   `netsh int ipv4 add excludedportrange protocol=tcp startport=50051 numberofports=1`
3. Re-Enable hyper-V (which will require a couple of restart)
   `dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All`

when your system is back, you will be able to bind to that port successfully.

As [@sbley](https://github.com/sbley) pointed out to [@enashed](https://github.com/enashed)'s solution , you might have side-effects when disabling Hyper-V. I suggest another approach:

As far as I understand, and many have stated, Hyper-V dynamically reserves a port range for itself. You can prohibit specific ports from being dynamically reserved.

First, check, if your required port is reserved, as [@veqryn](https://github.com/veqryn) did:
`$netsh interface ipv4 show excludedportrange protocol=tcp`

If it your port is in one of the ranges, stop winnat:
`$net stop winnat`

Prohibit dynamic reservation for your required port (here for example, 50051, as stated in the original question):
`$netsh int ipv4 add excludedportrange protocol=tcp startport=50051 numberofports=1`

Restart winnat:
`$net start winnat`

使用命令若提示该文件正在被使用，则关闭audiorelay再执行命令

