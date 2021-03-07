# [git 设置和取消代理](https://qyi.io/archives/634.html)

[ 小技巧](https://qyi.io/archives/category/tips) [admin](https://qyi.io/archives/author/admin) 1年前 (2019-11-30) 1415次浏览 [0个评论](https://qyi.io/archives/634.html#respond)

```
设置代理:
http方式:
git config --global https.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
Socket5方式:
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
建议使用socket5
取消代理：
git config --global --unset http.proxy
git config --global --unset https.proxy
```