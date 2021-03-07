# windows的powershell7 配置

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[self-confidence](https://blog.csdn.net/u012946588) 2020-09-16 10:43:34 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 288 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [后端](https://blog.csdn.net/u012946588/category_6828859.html) 文章标签： [windows 8](https://so.csdn.net/so/search/s.do?q=windows 8&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

## 下载安装powershell7

下载地址[powershell官网](https://docs.microsoft.com/zh-cn/powershell/)

## 主要操作以及配置文件

1. powershell输入

```
code $profile
1
```

1. 依次操作文件

```
1). windowsPowerShell\Microsoft.PowerShell_profile.ps1

# Clear-Host
Set-Location E:\www\

Import-Module posh-git
Import-Module oh-my-posh
Import-Module PSReadLine
Import-Module posh-docker
Import-Module Get-ChildItemColor


Set-PSReadLineKeyHandler -Key Tab -Function Complete
Set-PSReadLineKeyHandler -Key "Ctrl+d" -Function MenuComplete 
#Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
Set-PSReadLineKeyHandler -Key "Ctrl+f" -Function ForwardWord

Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
Set-PSReadLineOption -HistorySearchCursorMovesToEnd
set-psreadlineoption -predictionsource history

Set-Theme Sorin

#设置别名

function dp([string]$msg) { 
    if($msg -eq "a"){
        echo "🚀🚀🚀🚀  docker ps -a"
        docker ps -a
    }else{
        echo "🚀🚀🚀🚀  docker ps "
        docker ps
    }
}
function sh([string]$msg) { 
   docker exec -it $msg /bin/sh
}
function bash([string]$msg) { 
   docker exec -it $msg /bin/bash
}
function dr([string]$msg) { 
   docker restart $msg
}
# 3. 查看目录 ls & ll
function ListDirectory {
    (Get-ChildItem).Name
    Write-Host("")
}

# 设置ls和ll
$GetChildItemColorTable.File['Directory'] = "Red"
ForEach ($Exe in $GetChildItemColorExtensions.ExecutableList) {
    $GetChildItemColorTable.File[$Exe] = "Green"
}
Set-Alias -Name ls -Value ListDirectory
Set-Alias -Name ll -Value Get-ChildItem
Set-Alias l Get-ChildItem -option AllScope
Set-Alias ls Get-ChildItemColorFormatWide -option AllScope
# 设置代理

function proxy(){
    netsh winhttp set proxy 127.0.0.1:1080
}
function unproxy(){
    netsh winhttp reset proxy
}
function ip(){
    Invoke-WebRequest "http://ifconfig.me/ip"
}


#设置别名
Set-Alias dphp docker_php  
Set-Alias dnginx docker_nginx 
Set-Alias dp docker_ps  

Set-Alias build build_docker  
function docker_php { 
    docker exec -it php /bin/sh
}
function docker_nginx { 
    docker exec -it nginx /bin/sh
}
function docker_ps { 
    docker ps
}
function build_docker([string]$msg) { 
    Set-Location E:\www\docker_env
    docker-compose stop $msg 
    docker-compose build $msg
    docker-compose up -d $msg
}

12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152535455565758596061626364656667686970717273747576777879808182838485868788899091929394
2) PowerShell\Microsoft.PowerShell_profile.ps1

# Clear-Host
Set-Location E:\www\

Import-Module posh-git
Import-Module oh-my-posh
Import-Module PSReadLine
Import-Module posh-docker
Import-Module Get-ChildItemColor


Set-PSReadLineKeyHandler -Key Tab -Function Complete
Set-PSReadLineKeyHandler -Key "Ctrl+d" -Function MenuComplete 
#Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
Set-PSReadLineKeyHandler -Key "Ctrl+f" -Function ForwardWord

Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
Set-PSReadLineOption -HistorySearchCursorMovesToEnd
set-psreadlineoption -predictionsource history

Set-Theme Sorin

#设置别名

function dp([string]$msg) { 
    if($msg -eq "a"){
        echo "🚀🚀🚀🚀  docker ps -a"
        docker ps -a
    }else{
        echo "🚀🚀🚀🚀  docker ps "
        docker ps
    }
}
function sh([string]$msg) { 
   docker exec -it $msg /bin/sh
}
function bash([string]$msg) { 
   docker exec -it $msg /bin/bash
}
function dr([string]$msg) { 
   docker restart $msg
}
# 3. 查看目录 ls & ll
function ListDirectory {
    (Get-ChildItem).Name
    Write-Host("")
}

# 设置ls和ll
$GetChildItemColorTable.File['Directory'] = "Red"
ForEach ($Exe in $GetChildItemColorExtensions.ExecutableList) {
    $GetChildItemColorTable.File[$Exe] = "Green"
}
Set-Alias -Name ls -Value ListDirectory
Set-Alias -Name ll -Value Get-ChildItem
Set-Alias l Get-ChildItem -option AllScope
Set-Alias ls Get-ChildItemColorFormatWide -option AllScope
# 设置代理

function proxy(){
    netsh winhttp set proxy 127.0.0.1:1080
}
function unproxy(){
    netsh winhttp reset proxy
}
function ip(){
    Invoke-WebRequest "http://ifconfig.me/ip"
}


#设置别名
Set-Alias dphp docker_php  
Set-Alias dnginx docker_nginx 


Set-Alias build build_docker  
function docker_php { 
    docker exec -it php /bin/sh
}
function docker_nginx { 
    docker exec -it nginx /bin/sh
}
function build_docker([string]$msg) { 
    Set-Location E:\www\docker_env
    docker-compose stop $msg 
    docker-compose build $msg
    docker-compose up -d $msg
}

12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152535455565758596061626364656667686970717273747576777879808182838485868788899091
3)   settings.json

{
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "profiles": {
        "defaults": {},
        "list": [{
            "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
            "name": "PowerShell",
            "commandline": "C:/Program Files/PowerShell/7/pwsh.exe",
            "hidden": false,
            "fontFace": "Fira Code",
            "fontSize": 12,
            "colorScheme": "Duotone Dark",
            "useAcrylic": true,
            "acrylicOpacity": 0.8,
            "cursorShape": "bar"
        }, {
            "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
            "hidden": true,
            "name": "Azure Cloud Shell",
            "source": "Windows.Terminal.Azure"
        },
 {
     "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
     "hidden": false,
     "name": "PowerShell",
     "source": "Windows.Terminal.PowershellCore"
 }]
    },
    "schemes": [{
        "name": "Gruvbox Dark",
        "black": "#1e1e1e",
        "red": "#be0f17",
        "green": "#868715",
        "yellow": "#cc881a",
        "blue": "#377375",
        "purple": "#a04b73",
        "cyan": "#578e57",
        "white": "#978771",
        "brightBlack": "#7f7061",
        "brightRed": "#f73028",
        "brightGreen": "#aab01e",
        "brightYellow": "#f7b125",
        "brightBlue": "#719586",
        "brightPurple": "#c77089",
        "brightCyan": "#7db669",
        "brightWhite": "#e6d4a3",
        "background": "#1e1e1e",
        "foreground": "#e6d4a3"
    },{
        "name": "Duotone Dark",
        "black": "#1f1d27",
        "red": "#d9393e",
        "green": "#2dcd73",
        "yellow": "#d9b76e",
        "blue": "#ffc284",
        "purple": "#de8d40",
        "cyan": "#2488ff",
        "white": "#b7a1ff",
        "brightBlack": "#353147",
        "brightRed": "#d9393e",
        "brightGreen": "#2dcd73",
        "brightYellow": "#d9b76e",
        "brightBlue": "#ffc284",
        "brightPurple": "#de8d40",
        "brightCyan": "#2488ff",
        "brightWhite": "#eae5ff",
        "background": "#1f1d27",
        "foreground": "#b7a1ff"
    }],
    "keybindings": []
}
1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515253545556575859606162636465666768697071727374
```

## 安装 测试

```
 以管理员权限打开powershell，输入
Install-Module oh-my-posh -Scope CurrentUser
Install-Module psreadline -allowprereleas -Force
Install-Module psreadline -allowprereleas
Install-Module -Name PowerShellGet -Force
 Install-Module ZLocation -Scope CurrentUser
 Install-Module -Scope CurrentUser posh-docker
 Install-Module posh-git -Scope CurrentUser
Install-Module -AllowClobber Get-ChildItemColor
set-psreadlineoption -predictionsource history
 Install-Module psreadline -allowprerelease
##设置权限
 Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
 Set-PSRepository -Name PSGallery -InstallationPolicy Trusted

## 
ls
ll
dp: docker ps
dp a:docker ps -a
进入容器：sh php 或者sh nginx等
重建容器：build php
```