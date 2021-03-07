\用pip安装lxml包问题及解决方法

海绵波波107 2020-02-01 12:36:17  573  收藏 2
文章标签： pip python
版权
用pip安装lxml包问题及解决方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200201120223948.png)我的python是3.8版本的，电脑是64位操作系统，所以一开始选用了第二个版本的wheel文件。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200201122407985.png)

然后在安装lxml包时显示版本不符本要求，因为当时自己下载的python也是有位数的，32或者64位。下图是cmd中的查看方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200201122407985.png)

有一种方法可以找到自己的环境能够使用的版本

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200201122638893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTIwODM4,size_16,color_FFFFFF,t_70)

在cmd中输入python打开python,然后输入以下两行代码
import pip._internal.pep425tags
print(pip._internal.pep425tags.get_supported())

在上图显示了我可以选用的版本是第一个。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200201122948316.png)

然后下载第一个，重新安装lxml包，出现问题EnvironmentError,解决方法是在c盘中新建了一个文件夹my packge,然后把下载的wheel文件拷贝到文件夹中

原因是原先wheel文件的path太长，于是把它的位置往前移动了。
最后重新输入pip install lxml,安装成功。

python安装第三方库遇到 ERROR: Command errored out with exit status 1:

RIO小哥 2019-08-16 18:33:05  251326  收藏 161
分类专栏： python 文章标签： python 新手 错误
版权
python安装第三方库遇到 ERROR: Command errored out with exit status 1:…的问题
先来看看错误提示：
本来想用python弄个词云玩玩，没想到在安装wordcloud库的时候居然给我这一大串红叉叉，很是奔溃，出师不利啊！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190816180735992.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDUxNzUwMA==,size_16,color_FFFFFF,t_70)

报错的部分内容如下：
ERROR: Command errored out with exit status 1:
command: ‘c:\users\15870\appdata\local\programs\python\python37-32\python.exe’ -u -c ‘import sys, setuptools, tokenize; sys.argv[0] = ‘"’"‘C:\Users\15870\AppData\Local\Temp\pip-install-2wcyweho\wordcloud\setup.py’"’"’; file=’"’"‘C:\Users\15870\AppData\Local\Temp\pip-install-2wcyweho\wordcloud\setup.py’"’"’;f=getattr(tokenize, ‘"’"‘open’"’"’, open)(file);code=f.read().replace(’"’"’\r\n’"’"’, ‘"’"’\n’"’"’);f.close();exec(compile(code, file, ‘"’"‘exec’"’"’))’ install --record ‘C:\Users\15870\AppData\Local\Temp\pip-record-9qx3thr5\install-record.txt’ --single-version-externally-managed --compile

说实话作为一个渣渣新手，我是真的是看不懂这是个啥错误，但是，没关系，做为非专业人人士搞不懂错因也问题不大，能解决问题就行了，于是，经过一番查询，算是找到一个解决方法如下：

先打开python看看自己的python是什么版本的，多少位的。像我的就是3.7.3版本32位；

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190816182004464.JPG)

去https://www.lfd.uci.edu/~gohlke/pythonlibs/找到对应版本的whl文件，我的话就是找wordcloud-1.5.0-cp37-cp37m-win32.whl这一个，其中cp37代表3.7版本，win32代表Windows系统32位机

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190816182325875.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDUxNzUwMA==,size_16,color_FFFFFF,t_70)。

下载对应的whl文件后，在cmd下进入whl所在的文件夹

python安装第三方库遇到 ERROR: Command errored out with exit status 1:

RIO小哥 2019-08-16 18:33:05  251326  收藏 161
分类专栏： python 文章标签： python 新手 错误
版权
python安装第三方库遇到 ERROR: Command errored out with exit status 1:…的问题
先来看看错误提示：
本来想用python弄个词云玩玩，没想到在安装wordcloud库的时候居然给我这一大串红叉叉，很是奔溃，出师不利啊！

报错的部分内容如下：
ERROR: Command errored out with exit status 1:
command: ‘c:\users\15870\appdata\local\programs\python\python37-32\python.exe’ -u -c ‘import sys, setuptools, tokenize; sys.argv[0] = ‘"’"‘C:\Users\15870\AppData\Local\Temp\pip-install-2wcyweho\wordcloud\setup.py’"’"’; file=’"’"‘C:\Users\15870\AppData\Local\Temp\pip-install-2wcyweho\wordcloud\setup.py’"’"’;f=getattr(tokenize, ‘"’"‘open’"’"’, open)(file);code=f.read().replace(’"’"’\r\n’"’"’, ‘"’"’\n’"’"’);f.close();exec(compile(code, file, ‘"’"‘exec’"’"’))’ install --record ‘C:\Users\15870\AppData\Local\Temp\pip-record-9qx3thr5\install-record.txt’ --single-version-externally-managed --compile

说实话作为一个渣渣新手，我是真的是看不懂这是个啥错误，但是，没关系，做为非专业人人士搞不懂错因也问题不大，能解决问题就行了，于是，经过一番查询，算是找到一个解决方法如下：

先打开python看看自己的python是什么版本的，多少位的。像我的就是3.7.3版本32位；


去https://www.lfd.uci.edu/~gohlke/pythonlibs/找到对应版本的whl文件，我的话就是找wordcloud-1.5.0-cp37-cp37m-win32.whl这一个，其中cp37代表3.7版本，win32代表Windows系统32位机。


下载对应的whl文件后，在cmd下进入whl所在的文件夹


最后再输入pip install wordcloud-1.5.0-cp37-cp37m-win32.whl进行安装就可以了。


最后就可以用了，希望对大家能有帮助！

最后再输入pip install wordcloud-1.5.0-cp37-cp37m-win32.whl进行安装就可以了

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190816183145898.JPG)。


最后就可以用了，希望对大家能有帮助！

安装scrapy库时遇到 Running setup.py install for Twisted ... error解决方案

mqLittleRookie 2019-05-15 17:54:41  9701  收藏 12
分类专栏： python爬虫
版权
安装scrapy时，出现如下问题：

![图1](https://img-blog.csdnimg.cn/20190515174138459.?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMyMTQ1MDk3,size_16,color_FFFFFF,t_70)

出现这种问题的原因是缺少Twisted文件，从官网下载一个该文件的版本（Twisted-xxx-win_amd64.whl）并将其放到自己电脑python安装目录的script下即可。官网：https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted，然后command界面下，python的Script目录下，用pip命令安装按Twisted文件，记住是完整的名字而且需要带后缀，以Twisted-19.2.0-cp37-cp37m-win_amd64.whl为例，pip install Twisted-19.2.0-cp37-cp37m-win_amd64.whl,然后在pip install scrapy 即可。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019051517515299.)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190515175250871.)

完美解决。

python winthows下安装lxml失败解决方法

sqlaowen 2017-01-28 14:01:49  1925  收藏 1
文章标签： python
版权
安装lxml总是失败解决方法

失败提示如下:

    running build_ext
    building 'lxml.etree' extension
    creating build\temp.win-amd64-2.7
    creating build\temp.win-amd64-2.7\Release
    creating build\temp.win-amd64-2.7\Release\src
    creating build\temp.win-amd64-2.7\Release\src\lxml
    C:\Users\wenshiwei\AppData\Local\Programs\Common\Microsoft\Visual C++ for Python\9.0\VC\Bin\amd64\cl.exe /c /nologo /Ox /MD /W3 /GS- /DNDEBUG -Isrc\lxml\inc
ludes -Ic:\apps\tools\python27\include -Ic:\apps\tools\python27\PC /Tcsrc\lxml\lxml.etree.c /Fobuild\temp.win-amd64-2.7\Release\src\lxml\lxml.etree.obj -w
    cl : Command line warning D9025 : overriding '/W3' with '/w'
    lxml.etree.c
    src\lxml\includes\etree_defs.h(14) : fatal error C1083: Cannot open include file: 'libxml/xmlversion.h': No such file or directory
    Compile failed: command 'C:\\Users\\wenshiwei\\AppData\\Local\\Programs\\Common\\Microsoft\\Visual C++ for Python\\9.0\\VC\\Bin\\amd64\\cl.exe' failed with
exit status 2
    C:\Users\wenshiwei\AppData\Local\Programs\Common\Microsoft\Visual C++ for Python\9.0\VC\Bin\amd64\cl.exe /c /nologo /Ox /MD /W3 /GS- /DNDEBUG -I/usr/include
/libxml2 /Tcc:\users\wenshi~1\appdata\local\temp\xmlXPathInitqpboxi.c /Fousers\wenshi~1\appdata\local\temp\xmlXPathInitqpboxi.obj
    xmlXPathInitqpboxi.c
    c:\users\wenshi~1\appdata\local\temp\xmlXPathInitqpboxi.c(1) : fatal error C1083: Cannot open include file: 'libxml/xpath.h': No such file or directory
    *********************************************************************************
    Could not find function xmlCheckVersion in library libxml2. Is libxml2 installed?
    *********************************************************************************
    error: command 'C:\\Users\\wenshiwei\\AppData\\Local\\Programs\\Common\\Microsoft\\Visual C++ for Python\\9.0\\VC\\Bin\\amd64\\cl.exe' failed with exit stat
us 2

    ----------------------------------------
Command "c:\apps\tools\python27\python.exe -u -c "import setuptools, tokenize;__file__='c:\\users\\wenshi~1\\appdata\\local\\temp\\pip-build-mavckn\\lxml\\setup
.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" install --record c:\users\
wenshi~1\appdata\local\temp\pip-jal9v1-record\install-record.txt --single-version-externally-managed --compile" failed with error code 1 in c:\users\wenshi~1\ap
pdata\local\temp\pip-build-mavckn\lxml\

如果安装了VC++一样失败, 可以试试使用 wheel 安装, 已经被编绎过的
pip install wheel

接着下载 相应的.whl包

下载地址     http://www.lfd.uci.edu/~gohlke/pythonlibs

lxml安装遇到的问题

冯西的技术博客 2016-01-07 21:37:37  12773  收藏 1
版权
今天需要在自己的电脑上安装Python。这倒好说，驾轻就熟，很快就安装完成，并且将Python加到了环境路径中。但是在运行程序的时候发现好多一些package没有，这显然是因为我的Python中没有安装这些包导致的。于是就安装pip，这个也很快就下载并安装成功，但是执行pip的时候竟然说 这不是一个内部命令，奇怪，我之前在公司的电脑里也安装过，并没有遇到这个问题呀。于是上网找资料，原来是这个pip的路径也需要添加到环境变量中。添加完之后发现还是报同样的错误，这就奇怪了。再重新打开一个新的终端，再次执行pip命令，结果好了。看来需要重新打开一个终端才能让之前的设置生效。

然后就是安装lxml这个包了。执行

pip install lxml
最后竟然又出现了错误。关键错误信息如下：
    building 'lxml.etree' extension
    error: Microsoft Visual C++ 9.0 is required (Unable to find vcvarsall.bat). Get it from http://aka.ms/vcpython27
从字面意义理解，是需要Microsoft Visual C++ 9.0，而我的电脑中已经安装了Visual Studio 2010了呀。后来在网上查，原来是在windows下使用pip安装包的时候需要机器装有vs2008，别的版本还不行。如果不想安装VS2008，可以安装 Microsoft Visual C++ Compiler for Python 2.7
安装完这个Visual C++的文件后，再次安装lxml，竟然还是错误。不过这次的错误和上一次有所区别，错误提示内容为：

*********************************************************************************
Could not find function xmlCheckVersion in library libxml2. Is libxml2 installed?
*********************************************************************************
和

src\lxml\includes\etree_defs.h(14) : fatal error C1083: Cannot open include file: 'libxml/xmlversion.h': No such file or directory
c:\users\xzfeng\appdata\local\temp\xmlXPathInit0wevj7.c(1) : fatal error C1083: Cannot open include file: 'libxml/xpath.h': No such file or directory
这个大多是因为在对C代码在编译的时候没有找到对应的文件导致的。简单来说，解决方法要么就安装它提示所缺失的文件，从而使得编译行为可以顺利进行下去；还有一个方法就是安装.wheel版本，因为该版本是已经prebuild过的版本，在本机上安装已经不需要在重新编译一下了。当然还有更便捷的方法，如下这篇Stack Overflow上找到的关于这个问题的帖子： 点击打开链接
里面有两个解决方法，方法一有一些麻烦，没有去试，应该能解决问题；方法二超级简单，舍弃用pip来安装，直接用easy_install来安装，果然什么问题也没有遇到，很顺利便安装成功了。
easy_install lxml
真是选对了工具能给你节省太多时间了。

[更新2016/08/28]使用easy_install的方法并不是每次都能成功。屡试不爽的方法还是通过.wheel来安装。当所有方法都试了，仍然没能安装成功的话，试一试用wheel安装吧，百分百成功。

此文也有别的解决方法。

基于pip的安装lxml库报错解决方案

xiaosakun 2018-08-22 15:20:00  1061  收藏 1
版权
pip是python中经常使用可以便捷安装python其他库的一款软件，我们经常在命令行cmd中使用它。
安装lxml库的时候容易出现没法从网上安装twisted库的错误，解决方案是从将twisted库下载到本地后，用命令进行安装。
twisted库下载链接: https://pan.baidu.com/s/1BiCc0HRpGnh-O2wk0ySKtw 密码: y9gq
注意：此链接下载的版本适用于win64系统下的Python3.6版本！！如果你的Python版本不同，请在浏览器中访问此网站：https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted，网站如下图所示：


twisted下载网址.png

你可以根据自己的操作系统和python版本来 下载需要的版本。
在桌面新建一个文件夹，并放入下载好的后缀名为whl的文件。

新建文件夹.png

在资源管理器的路径中输入cmd，并按Enter进入命令行。
这一步的作用是cmd打开时就在此目录下。

进入cmd.png

进入命令行后，输入命令： pip install Twisted-18.7.0-cp36-cp36m-win_amd64.whl

命令行安装twisted库.png

成功运行命令后，再次运行 pip install lxml就可以成功安装lxml库。