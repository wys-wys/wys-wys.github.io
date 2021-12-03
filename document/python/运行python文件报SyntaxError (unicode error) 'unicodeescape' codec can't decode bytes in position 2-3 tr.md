# 运行python文件报SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes in position 2-3: tr

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[可乐饲养员](https://blog.csdn.net/xd060606) 2019-02-13 10:46:28 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 270296 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 476

分类专栏： [python QS](https://blog.csdn.net/xd060606/category_7780044.html)

版权

  hello~大家新年好，已经好久没有更博了，刚刚在运行python文件的时候竟然报SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes in position 2-3: tr这个错误，其实引起这个错误的原因就是转义的问题。

  举个例子，在文件中我传入的文件路径是这样的

```
sys.path.append('c:\Users\mshacxiang\VScode_project\web_ddt')
```

  **原因分析：**在windows系统当中读取文件路径可以使用\,但是在python字符串中\有转义的含义，如\t可代表TAB，\n代表换行，所以我们需要采取一些方式使得\不被解读为转义字符。目前有3个**解决方案**

**1、在路径前面加r，即保持字符原始值的意思。**

```
sys.path.append(r'c:\Users\mshacxiang\VScode_project\web_ddt')
```

**2、替换为双反斜杠**

```
sys.path.append('c:\\Users\\mshacxiang\\VScode_project\\web_ddt')
```

**3、替换为正斜杠**

```
sys.path.append('c:/Users/mshacxiang/VScode_project/web_ddt')
```