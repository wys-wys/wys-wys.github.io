# node工具之nodemon

[![img](https://cdn2.jianshu.io/assets/default_avatar/6-fd30f34c8641f6f32f5494df5d6b8f3c.jpg)](https://www.jianshu.com/u/4ff902916e23)

[大月山](https://www.jianshu.com/u/4ff902916e23)关注

0.2832019.10.28 15:34:00字数 168阅读 25,431

## nodemon

nodemon是一种工具，可以自动检测到目录中的文件更改时通过重新启动应用程序来调试基于node.js的应用程序。

## 安装



```cpp
npm install -g nodemon
//或
npm install --save-dev nodemon
```

## 使用



```cpp
nodemon   ./main.js // 启动node服务
```



```cpp
nodemon ./main.js localhost 6677 // 在本地6677端口启动node服务
```



```bash
"start": "ts-node -r tsconfig-paths/register nodemon src/main.ts",
```

## 延迟重启



```css
nodemon -delay10 main.js

nodemon --delay 2.5 server.js

nodemon --delay 2500ms server.js
```

这个就类似于js函数中的函数节流,只在最后一次更改的文件往后延迟重启.避免了短时间多次重启的局面.

## 配置文件

nodemon支持本地和全局配置文件。这些通常是命名的nodemon.json，可以位于当前工作目录或主目录中。可以使用该--config <file>选项指定备用本地配置文件。



```json
{
  "verbose": true,
  "ignore": ["*.test.js", "fixtures/*"],
  "execMap": {
    "rb": "ruby",
    "pde": "processing --sketch={{pwd}} --run"
  }
}
```

## Doc

- [nodemon](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fnodemon)



3人点赞



[Node](https://www.jianshu.com/nb/40451424)