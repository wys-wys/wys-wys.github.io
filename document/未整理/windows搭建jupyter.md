![Python安装Jupyter Notebook配置使用教程](https://pic1.zhimg.com/v2-310c3fd1176157d4a3c540d38f274682_1440w.jpg?source=172ae18b)

# Python安装Jupyter Notebook配置使用教程

[![天意帝](https://pic3.zhimg.com/v2-0496a9a7b0ecb544e233bb4ab2bed4f4_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/kamchiu-35)

[天意帝](https://www.zhihu.com/people/kamchiu-35)

一个人可以被毁灭但不能被打败。

关注他

34 人赞同了该文章

> **为什么要用Jupyter Notebook**

推荐新手写python用什么编辑器就有有人问：为什么没有Jupyter Notebook。本来想数据分析和可视化的时候才介绍的，所以没有加上。最近要截图比较多，用Jupyter Notebook可以很好看到代码和结果。



![img](https://pic4.zhimg.com/v2-0475cdaa5161869d464da52ab5c2085f_r.jpg)



------

> **Jupyter Notebook是什么**

- Jupyter Notebook是一个开源的web应用程序,一个交互式笔记本，支持运行 40 多种编程语言。
- 它允许您创建和共享文档,包含代码,方程,可视化和叙事文本。
- 用途包括:数据清洗和转换,数值模拟,统计建模、数据可视化、机器学习等等。
- 支持以网页的形式分享，GitHub 中天然支持 Notebook 展示，也可以通过 nbviewer 分享你的文档。当然也支持导出成 HTML、Markdown 、PDF 等多种格式的文档。
- 不仅可以输出图片、视频、数学公式，甚至可以呈现一些互动的可视化内容，比如可以缩放的地图或者是可以旋转的三维模型。



------

> **怎么样安装 Jupyter notebook**

**怎么打开cmd命令提示符窗口：**
1、选择开始=》所有程序=》附件=》cmd程序。
2、也可以开始=》搜索=》输入：cmd/cmd.exe 回车。
3、windows键加上R，然后输入cmd，也可以打开命令提示符窗口。

> **通过 pip 安装：pip install jupyter**



![img](https://pic4.zhimg.com/v2-68dc821dd060c1f9a37e2f98e2364f2b_r.jpg)



**安装成功提示有：jupyter、jupyter-client、jupyter-console、jupyter-core。**



![img](https://pic4.zhimg.com/v2-8fb767068bb07d476728794e32cf8057_r.jpg)



------

> **配置Jupyter notebook目录路径**

安装完成先不要启动，先配置目录路径。要不然默认打开和保存Jupyter notebook文件目录在C盘。

打开cmd命令提示符窗口输入：**jupyter notebook--generate-config** ，生成默认配置文件到C:\Users\Administrator\.jupyter\jupyter_notebook_config.py



![img](https://pic1.zhimg.com/v2-1d1f9f3fe2234173cae79eda071a5f64_r.jpg)



找到默认配置文件的目录。很多配置文件都是生成到这个目录中。



![img](https://pic3.zhimg.com/v2-e28f7092c32baaad0bd55d7c527557ba_r.jpg)





![img](https://pic4.zhimg.com/v2-946fcdb3ec56c094ca960ed5b1cbdb33_r.jpg)



打开jupyter_notebook_config.py搜索c.NotebookApp.notebook_dir（大概在261行）



![img](https://pic2.zhimg.com/v2-9ec2640863b53dd086b52cfd72613329_r.jpg)



把#号去掉，把值改为你要存放Jupyter notebook文件的目录路径。



![img](https://pic1.zhimg.com/v2-b88c620a9bbe2a086bbc1282be8adaf4_r.jpg)



以后Jupyter notebook创建的文件都会保存到这个目录路径中。

------

> **怎么样去启动Jupyter notebook**

打开打开cmd命令提示符窗口输入jupyter notebook 回车，然后浏览器就会打开Jupyter notebook。



![img](https://pic2.zhimg.com/v2-f934c002b289bfce6fd225992c3b5c99_r.jpg)



------

> **如何快速使用notebook**

**Jupyter notebook界面**



![img](https://pic2.zhimg.com/v2-dca27cb315c0dfbce133765e8394017d_r.jpg)



**左边选项**



![img](https://pic2.zhimg.com/80/v2-361b5b0de9ce07af42f24313471f1811_720w.jpg)



- Files 对应下面的文件列表。
- running里面可以看到命令行窗口和notebooks文件运行的管理窗口，好像电脑的任务管理器。
- Clusters里面跳转页面可以看有关安装详细信息，请参阅“IPython parallel”。

**右边选项**



![img](https://pic3.zhimg.com/80/v2-57191a92618d771efc89711f5eb302ce_720w.jpg)



- Quit 和Logout 退出和注销。Upload上传文件，本地应该用不到。
- New就是新建文件的选项。



![img](https://pic3.zhimg.com/80/v2-dcfcf292ae5ca0dc8e5d1bab29d336be_720w.jpg)



**下边文件列表**



![img](https://pic3.zhimg.com/80/v2-ca5e9c1f0a95eb726180bf9524654ca2_720w.jpg)



小三角可以分类选择文件夹或者文件



![img](https://pic3.zhimg.com/80/v2-6a89f51f2cb888fad98bae7f4f76d53a_720w.png)



- Folders：所有文件夹勾选
- All Notebooks：所有Notebooks（.ipynb）勾选
- Running：所有在运行的勾选
- Files：所有文件勾选

------

**勾选文件，就会出现一排的选项。**



![img](https://pic1.zhimg.com/80/v2-c709c161f18bb61343d547c523fc5b3c_720w.jpg)



- Duplicate：复制
- Rename：重命名
- Move：移动（剪切）
- Download：下载
- Shutdown：关闭
- View：视图
- Edit：修改
- 垃圾桶标志不用过多解释删除啦。

有几种情况：Shutdown只有选择运行的文件才会出现。文件夹只有重命名、移动和删除。

------

> **进入Jupyter notebook文件页面**

首先要理解Jupyter notebook是以单元格形式存在的，单元格可以写代码、标记语言（Markdown是一种可以使用普通文本编辑器编写的标记语言）。

**点击文件名可以重命名**



![img](https://pic1.zhimg.com/v2-0231e58b75237fab5e3ca393876b8340_r.jpg)



------

> **菜单栏：**



![img](https://pic2.zhimg.com/v2-c90d603346bd8f396984041501dd8c59_r.jpg)



**菜单栏File（文件）:**



![img](https://pic1.zhimg.com/v2-fdcc3dacde893db2f976a8f70017ed4c_r.jpg)



- New Notebook：新建Notebook文件
- Open：重新打开另外一个文件
- Make a Copy：复制一份
- Save as：另存为
- Rename：重命名
- Save and Checkpoint：保存和检查点，备份
- Revert to Checkpoint：恢复检查点，恢复备份
- Print Preview：打印预览
- Download as：下载为Notebook文件、python文件、html、txt等等多种格式。
- Close and Halt：关闭并停止

**菜单栏Edit（编辑）:**



![img](https://pic2.zhimg.com/v2-dc81ab5d374ce603e19ea059b746a669_r.jpg)



- Cut Cells：剪切单元格
- Copy Cells：复制单元格
- Paste Cells Above：粘贴单元格上方部分
- Paste Cells Below：粘贴单元格下方部分
- Paste Cells Replace：粘贴单元格替换
- Delete Cells：删除单元格
- Undo Delete Cells：撤消删除单元格
- Split Cell：拆分单元格
- Merge Cell Above：合并单元格上方
- Merge Cell Below：合并单元格下方
- Move Cell Up：向上移动单元格
- Move Cell Down：向下移动单元格
- Edit Notebook Metadata：编辑Notebook数据
- Find and Replace：查找和替换
- Cut Cell Attachments：切割单元格附件
- Copy Cell Attachments：复制单元格附件
- Paste Cell Attachments：粘贴单元格附件
- Insert Image：插入图片

**菜单栏View（视图）:**



![img](https://pic2.zhimg.com/80/v2-507978a0fd90da3448a2288e0a411bb9_720w.jpg)



- Toggle Header：显示隐藏标题
- Toggle Toolbar：显示隐藏工具栏
- Toggle Line Numbers：显示隐藏行号
- Cell Toolbar：单元格工具栏

**菜单栏Insert（插入）:**



![img](https://pic3.zhimg.com/80/v2-7891c59366eb0d8018577be845d15f72_720w.jpg)



- Insert Cell Above：插入单元格上方
- Insert Cell Below：插入单元格下方

**菜单栏Cell（单元格）:**



![img](https://pic1.zhimg.com/80/v2-79c8a4881ab059edbedd6bd2df4c711c_720w.jpg)



- Run Cells：运行所有单元格
- Run Cells and Select Below：运行单元格并选择下方
- Run Cells and Insert Below：运行单元格并在下面插入
- Run All：全部运行
- Run All Above：全部运行上方
- Run All Below：全部运行下方
- Cell Type：单元格类型
- Current Outputs：当前输出
- All Output：所有输出

**菜单栏Kernel（核心）:**



![img](https://pic4.zhimg.com/80/v2-02c537f6b981b7be835d90b24b2a63c3_720w.jpg)



- Interrupt：中断
- Restart：重启
- Restart Clear Output：重启清除输出
- Restart Run All：重启全部运行
- Reconnect：重新连接
- Shutdown：关掉
- Change kernel：改变核心

**菜单栏Widgets（小工具）:**



![img](https://pic1.zhimg.com/80/v2-d40f36e1077807b34d9ff99880518708_720w.jpg)



- Save Notebook Widget State：保存Notebook小部件状态
- Clear Notebook Widget State：清除Notebook小部件状态
- Download Widget State：下载小部件状态
- Embed Widgets：嵌入小部件

**菜单栏Help（帮助）:**



![img](https://pic2.zhimg.com/80/v2-6d6c229ae640770f082a32b682e1046d_720w.jpg)



- User Interface Tour：用户界面预览，这个可以带你了解界面。新手去看看。
- Keyboard Shortcuts：键盘快捷键
- Edit Keyboard Shortcuts：编辑键盘快捷键
- Notebook Help：Notebook帮助网址
- Markdown：Markdown网址
- Python Reference：Python参考手册
- IPython Reference：IPython参考手册
- NumPy Reference：NumPy参考手册
- SciPy Reference：SciPy参考手册
- Matplotlib Reference：Matplotlib参考手册
- SymPy Reference：SymPy参考手册
- pandas Reference：pandas参考手册
- About：关于

------

**工具栏：每个图标都有中文注释，重要看一下鼠标图标，里面可以搜索看到快捷键说明。**



![img](https://pic3.zhimg.com/v2-5ae99e415dd0f4225bea8cbe0928d49a_r.jpg)



**单元代码区：**

每一个单元代码即有影响又可以互不影响。多个运行结果可以同时在同一个界面，不像pycharm后面运行结果会关闭前一个再显示。这样可以对比结果，对比数据。



![img](https://pic3.zhimg.com/v2-9fac2a533f41a911a44b4211afaec6ea_r.jpg)



所以JupyterNotebook很适合数据可视化、科学计算等等这些多数据、多展示图的项目测试对比。



![img](https://pic4.zhimg.com/v2-e16b461d7f79ee40bfb5b7b214c45907_r.jpg)



发布于 2019-01-08