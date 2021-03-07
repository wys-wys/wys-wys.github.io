# 下载npm依赖包报错 npm ERR! code ERR_TLS_CERT_ALTNAME_INVALID npm ERR! errno ERR_TLS_CERT_ALTNAME_INVALID

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[zhangbinlong](https://blog.csdn.net/zhangbinlong) 2020-07-22 17:43:37 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 3787 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 9

分类专栏： [Java](https://blog.csdn.net/zhangbinlong/category_7265784.html) [npm](https://blog.csdn.net/zhangbinlong/category_10224156.html) 文章标签： [npm](https://www.csdn.net/tags/MtzaYg3sODAxMi1ibG9n.html)

版权

# npm报错 npm ERR! code ERR_TLS_CERT_ALTNAME_INVALID **npm ERR! errno ERR_TLS_CERT_ALTNAME_INVALID**

在下载npm依赖包输入 npm install 命令的时候出错 以下是错误信息

错误信息：

npm ERR! code ERR_TLS_CERT_ALTNAME_INVALID
npm ERR! errno ERR_TLS_CERT_ALTNAME_INVALID
npm ERR! request to https://registry.cnpmjs.org/vue-cli failed, reason: Hostname/IP does not match certificate’s altnames: Host: registry.cnpmjs.org. is not in the cert’s altnames: DNS:r.cnpmjs.org

npm ERR! A complete log of this run can be found in:
npm ERR! C:\Users\yy\AppData\Roaming\npm-cache_logs\2020-06-12T05_41_01_727Z-debug.log

![输入 npm install 出错](https://img-blog.csdnimg.cn/20200722173831965.png)

## 解决方法

输入命令：

1. npm config set strict-ssl false
2. npm install -g supervisor

之后再输入npm install 即可

https://marketing.csdn.net/poster/112?utm_source=1538247462&spm=1000.2116.3001.4180

### 软件简介

CNPM 是中国 npm 镜像的客户端。

安装

```
$ npm install cnpm -g
```

国内安装 [China mirror](https://npm.taobao.org/):

```
$ npm install cnpm -g --registry=https://registry.npm.taobao.org
```

支持所有 `npm命令`.

同步包：

```
$ cnpm sync [moduleName]
```

查看包文件：

```
$ cnpm doc [name]
$ cnpm doc -g [name] # open git web url directly
```

构建私有 npm:

```
$ npm install cnpm -g

# then alias it
$ alias mynpm='cnpm --registry=http://registry.npm.example.com \
  --registryweb=http://npm.example.com \
  --userconfig=$HOME/.mynpmrc'
```

### 代码

npm install -g cnpm --registry=https://registry.npm.taobao.org

参考：http://npm.taobao.org/    淘宝NPM镜像

# [nurdun](https://www.cnblogs.com/nurdun/)

## 

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/nurdun/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/nurdun)
- [管理](https://i.cnblogs.com/)
- [订阅](javascript:void(0))[![订阅](https://www.cnblogs.com/skins/coffee/images/xml.gif)](https://www.cnblogs.com/nurdun/rss/)

随笔- 21 文章- 0 评论- 2 

# [npm ERR 安装依赖包报错](https://www.cnblogs.com/nurdun/p/6824480.html)

我今天安装依赖包时一直报错

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
$ npm install
npm ERR! Windows_NT 10.0.14393
npm ERR! argv "C:\\Program Files\\nodejs\\node.exe" "C:\\Program Files\\nodejs\\                 node_modules\\npm\\bin\\npm-cli.js" "install"
npm ERR! node v6.10.2
npm ERR! npm  v3.10.10
npm ERR! code ENOTFOUND
npm ERR! errno ENOTFOUND
npm ERR! syscall getaddrinfo

npm ERR! network getaddrinfo ENOTFOUND registry.npm.taobao.or registry.npm.taoba                 o.or:443
npm ERR! network This is most likely not a problem with npm itself
npm ERR! network and is related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settin                 gs.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! Please include the following file with any support request:
npm ERR!     D:\nurdun\dva-cli\npm-debug.log
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 





我之前把npm的registry换成国内的淘宝镜像的所以一开始认为报错跟链接什么的没什么关系。后来我在网上看了一下相关博客，都说换成cnpm就可以，我也尝试了一下，果然成功了。虽然我还不是特别理解这其中的奥妙之处，但是也得到了解决问题的方法。

 

下面三种方法都可以

1.通过config命令

```
npm config set registry http://registry.cnpmjs.org
npm info underscore （如果上面配置正确这个命令会有字符串response）
```

2.命令行指定

```
npm --registry http://registry.cnpmjs.org info underscore
```

3.编辑 `~/.npmrc` 加入下面内容

```
registry = http://registry.cnpmjs.org
```

结果

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 E:\study\angular-phonecat>npm config set registry http://registry.cnpmjs.org

E:\study\angular-phonecat>npm install
npm WARN package.json karma-chrome-launcher@0.1.7 No README data

> angular-phonecat@0.0.0 postinstall E:\study\angular-phonecat
> bower install

bower angular-resource#1.3.x not-cached Git://github.com/angular/bower-angular-resource.git#1.3.x
bower angular-resource#1.3.x resolve git://github.com/angular/bower-angular-resource.git#1.3.x
bower angular#1.3.x cached git://github.com/angular/bower-angular.git#1.3.14
bower angular#1.3.x validate 1.3.14 against git://github.com/angular/bower-angular.git#1.3.x
bower bootstrap#~3.1.1 cached git://github.com/twbs/bootstrap.git#3.1.1
bower bootstrap#~3.1.1 validate 3.1.1 against git://github.com/twbs/bootstrap.git#~3.1.1
bower angular-animate#1.3.x not-cached git://github.com/angular/bower-angular-animate.git#1.3.x
bower angular-animate#1.3.x resolve git://github.com/angular/bower-angular-animate.git#1.3.x
bower angular-mocks#1.3.x cached git://github.com/angular/bower-angular-mocks.git#1.3.14
bower angular-mocks#1.3.x validate 1.3.14 against git://github.com/angular/bower-angular-mocks.git#1.3.x
bower jQuery#~2.1.1 cached git://github.com/jquery/jquery.git#2.1.3
bower jquery#~2.1.1 validate 2.1.3 against git://github.com/jquery/jquery.git#~2.1.1
bower angular-route#1.3.x not-cached git://github.com/angular/bower-angular-route.git#1.3.x
bower angular-route#1.3.x resolve git://github.com/angular/bower-angular-route.git#1.3.x
bower angular-resource#1.3.x download https://github.com/angular/bower-angular-resource/archive/v1.3.14.tar.gz
bower angular-animate#1.3.x download https://github.com/angular/bower-angular-animate/archive/v1.3.14.tar.gz
bower angular-route#1.3.x download https://github.com/angular/bower-angular-route/archive/v1.3.14.tar.gz
bower angular-resource#1.3.x extract archive.tar.gz
bower angular-resource#1.3.x resolved git://github.com/angular/bower-angular-resource.git#1.3.14
bower angular-animate#1.3.x extract archive.tar.gz
bower angular-animate#1.3.x resolved git://github.com/angular/bower-angular-animate.git#1.3.14
bower angular-route#1.3.x extract archive.tar.gz
bower angular-route#1.3.x resolved git://github.com/angular/bower-angular-route.git#1.3.14
bower angular-mocks#1.3.x install angular-mocks#1.3.14
bower angular#1.3.x install angular#1.3.14
bower jquery#~2.1.1 install jquery#2.1.3
bower bootstrap#~3.1.1 install bootstrap#3.1.1
bower angular-resource#1.3.x install angular-resource#1.3.14
bower angular-animate#1.3.x install angular-animate#1.3.14
bower angular-route#1.3.x install angular-route#1.3.14

angular-mocks#1.3.14 app\bower_components\angular-mocks
└── angular#1.3.14

angular#1.3.14 app\bower_components\angular

jquery#2.1.3 app\bower_components\jquery

bootstrap#3.1.1 app\bower_components\bootstrap
└── jquery#2.1.3

angular-resource#1.3.14 app\bower_components\angular-resource
└── angular#1.3.14

angular-animate#1.3.14 app\bower_components\angular-animate
└── angular#1.3.14

angular-route#1.3.14 app\bower_components\angular-route
└── angular#1.3.14

E:\study\angular-phonecat>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

分类: [npm](https://www.cnblogs.com/nurdun/category/998108.html)

[![luminal_Andy](https://www.it610.com/views/front/img/head.png)](javascript:void(0);)

[**luminal_Andy**](javascript:void(0);)

发布时间：2020-07-07 01:45

# npm安装依赖包报错，npm ERR! code ENOTFOUND（2020-07-03）

- [错误累积（错题本）](https://www.it610.com/search/错误累积（错题本）/1.htm)

 

vue项目安装依赖包，报错如下：

```bash
$ npm install
npm WARN registry Using stale data from https://registry.npmjs.org/ because the host is inaccessible -- are you offline?
npm WARN registry Using stale data from https://registry.npmjs.org/ due to a request error during revalidation.
npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm ERR! code ENOTFOUND
npm ERR! errno ENOTFOUND
npm ERR! network request to https://registry.npmjs.org/vue-router/-/vue-router-3.3.4.tgz failed, reason: getaddrinfo ENOTFOUND registry.npmjs.org registry.npmjs.org:443
npm ERR! network This is a problem related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network 
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/luminal/.npm/_logs/2020-07-03T04_12_04_809Z-debug.log
```

解决方式：

```
$ npm config get proxy
null
$ npm config get https-proxy
null

$ npm config set proxy null
$ npm config set https-proxy null
$ npm config set registry http://registry.cnpmjs.org/
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
/Users/luminal/.nvm/versions/node/v10.16.0/bin/cnpm -> /Users/luminal/.nvm/versions/node/v10.16.0/lib/node_modules/cnpm/bin/cnpm
+ cnpm@6.1.1
updated 5 packages in 12.316s

$ cnpm i
bash: cnpm: command not found
$ cnpm install
bash: cnpm: command not found
$ nvm use v10.16.0
Now using node v10.16.0 (npm v6.9.0)
$ cnpm i
⠧ [6/23] Installing uniqs@^2.0.0
WARN node unsupported "node@v10.16.0" is incompatible with babel-loader@7.1.5 › webpack@3.12.0 › watchpack@1.7.2 › watchpack-chokidar2@^2.0.0, expected node@<8.10.0
✔ Installed 23 packages
✔ Linked 750 latest versions
```

之前使用 nvm 对 node 版本进行了管理，需要指定一下版本：nvm use v10.16.0

而后使用 cnpm i 或 cnpm install

 

参考链接：

npm安装任何包都报错的解决办法

 