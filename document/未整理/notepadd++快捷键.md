# [NOtePad++快捷键大全](https://www.cnblogs.com/jungege/p/6003992.html)

Notepad++ 快捷键 大全，

notepad++也情有独钟，最近发现了一个快捷键，就是选中单词，ctrl+shift+enter。不过现在想知道一个快捷键，假设有三行代码，选中后一般按TAB就可以三行全部缩进. 

Notepad++绝对是windows下进行程序编辑的神器之一，要更快速的使用以媲美VIM，必须灵活掌握它的快捷键，下面对notepad++默认的快捷键做个整理;

**1. 文件相关**

| 快捷键         | 动作定义                         |
| -------------- | -------------------------------- |
| Ctrl-O         | 打开文件                         |
| Ctrl-N         | 新建文件                         |
| Ctrl-S         | 保存文件                         |
| Ctrl-Alt-S     | 文件另存为                       |
| Ctrl-Shift-S   | 保存所有打开文件                 |
| Ctrl-P         | 打印                             |
| Alt-F4         | 退出程序                         |
| Ctrl-Tab       | 文件标签跳转，跳至下一个打开文件 |
| Ctrl-Shift-Tab | 文件标签跳转，跳至上一个打开文件 |
| Ctrl-W         | 关闭当前文件                     |

**2.编辑相关**

| 快捷键                                          | 动作定义                                                     |
| ----------------------------------------------- | ------------------------------------------------------------ |
| Ctrl-C                                          | 复制                                                         |
| Ctrl-Insert                                     | 同上，复制                                                   |
| Ctrl-Shift-T                                    | 复制当前行至剪贴板                                           |
| Ctrl-X                                          | 剪切                                                         |
| Shift-Delete                                    | 同上，剪切                                                   |
| Ctrl-V                                          | 粘帖                                                         |
| Shift-Insert                                    | 同上，粘帖                                                   |
| Ctrl-Z                                          | 撤销上一次操作                                               |
| Alt-Backspace                                   | 同上                                                         |
| Ctrl-Y                                          | 重做，注：撤销后，重做刚刚撤销的动作                         |
| Ctrl-A                                          | 全选                                                         |
| Alt-Shift-方向键 或 Alt + 鼠标左键              | 列选择模式                                                   |
| Ctrl + 鼠标左键                                 | 非连续性的多区域选择                                         |
| ALT-C                                           | 列编辑器                                                     |
| Ctrl-D                                          | 复制当前行至下方，或者复制选中区域至其后                     |
| Ctrl-T                                          | 复制当前行至剪贴板（注：帮助中说是将当前行与上一行交换位置） |
| Ctrl-Alt-T                                      | 与上一行进行交换                                             |
| Ctrl-Shift-Up                                   | 将当前行上移一行                                             |
| Ctrl-Shift-Down                                 | 将当前行下移一行                                             |
| Ctrl-L                                          | 删除当前行                                                   |
| Ctrl-I                                          | -（注：帮助中是分割多行，不过最新版中不起作用）              |
| Ctrl-J                                          | 合并多行（注：使用时要选择中需要合并的行）                   |
| Ctrl-G                                          | 跳转至某行对话框                                             |
| Ctrl-Q                                          | 添加/删除注释                                                |
| Ctrl-Shift-Q                                    | 区块添加/删除注释                                            |
| Tab (selection of one or more full lines)       | 插入Tab                                                      |
| Shift-Tab (selection of one or more full lines) | 删除位置之前的Tab                                            |
| Ctrl-BackSpace                                  | 删除当前位置至单词开始的内容                                 |
| Ctrl-Delete                                     | 删除当前位置至单词结尾的内容                                 |
| Ctrl-Shift-BackSpace                            | 删除当前位置至行首的内容                                     |
| Ctrl-Shift-Delete                               | 删除当前位置至行尾的内容                                     |
| Ctrl-U                                          | 转换为小写                                                   |
| Ctrl-Shift-U                                    | 转换为大写                                                   |
| Ctrl-B                                          | 跳转至配对的括号                                             |
| Ctrl-Space                                      | 触发函数自动完成列表                                         |
| Ctrl-Shift-Space                                | 触发函数参数提示                                             |
| Ctrl-Enter                                      | 触发关键字自动完成列表                                       |
| Ctrl-Alt-R                                      | 整个页面文字方向从右到左                                     |
| Ctrl-Alt-L                                      | 整个页面文字方向从左到右（注：在安装了zencoding后，此快捷键可能被覆盖） |
| Enter                                           | 回车                                                         |
| Shift-Enter                                     | 同上                                                         |

建议添加一个快捷键用来复制当前行至下一行：

在设置->快捷键管理中，选择scintilla commands中，找到SCI_LINEDUPLICATE，给它指定一个快捷键，例如Ctrl+M

**3.搜索相关**

| 快捷键            | 动作定义                                               |
| ----------------- | ------------------------------------------------------ |
| Ctrl-F            | 打开搜索对话框                                         |
| Ctrl-H            | 打开替换搜索对话框                                     |
| F3                | 搜索下一个结果                                         |
| Shift-F3          | 搜索上一个结果                                         |
| Ctrl-Shift-F      | 文件中搜索                                             |
| F7                | 调到寻找结果                                           |
| Ctrl-Alt-F3       | 快速查找下一个                                         |
| Ctrl-Alt-Shift-F3 | 快速查找上一个                                         |
| Ctrl-F3           | 选定并寻找下一个                                       |
| Ctrl-Shift-F3     | 选定并寻找上一个                                       |
| F4                | 下一次寻找结果                                         |
| Shift-F4          | 上一次寻找结果                                         |
| Ctrl-Shift-I      | 增量查找                                               |
| Ctrl-n            | 跳至下一个结果，用第n个风格标识（n为1~5，0是默认风格） |
| Ctrl-Shift-n      | 跳至上一个结果，用第n个风格标识（n为1~5，0是默认风格） |
| Ctrl-F2           | 收缩展开标签                                           |
| F2                | 跳至下一个标签处                                       |
| Shift-F2          | 跳至上一个标签处                                       |

4.显示相关

| 快捷键                                  | 定义内容                     |
| --------------------------------------- | ---------------------------- |
| Ctrl-(Keypad-/Keypad+)或者Ctrl+鼠标滚轮 | 放大/缩小页面                |
| Ctrl-Keypad/                            | 回复到原始页面大小           |
| F11                                     | 开关全屏显示（显示标签页）   |
| F12                                     | 开关全屏显示（不显示标签页） |
| Ctrl-Alt-F                              | 收缩当前折叠                 |
| Ctrl-Alt-Shift-F                        | 展开当前折叠                 |
| Alt-0                                   | 收缩所有折叠                 |
| Alt-(1~8)                               | 展开相应层折叠               |
| Alt-Shift-0                             | 展开所有折叠                 |
| Alt-Shift-(1~8)                         | 展开所有层次折叠             |

 5.运行相关

| 快捷键           | 定义内容                                             |
| ---------------- | ---------------------------------------------------- |
| F5               | 打开运行窗口                                         |
| Alt-F1           | 获得PHP帮助                                          |
| Alt-F2           | 用Google搜索                                         |
| Alt-F3           | 用Wiki搜索哦                                         |
| Alt-F5           | 在本标签页中打开当前目录中，与光标位置文本同名的文件 |
| Alt-F6           | 在新标签页中打开当前目录中，与光标位置文本同名的文件 |
| Ctrl-Alt-Shift-R | 在Chrome中打开                                       |
| Ctrl-Alt-Shift-X | 在Firefox中打开                                      |
| Ctrl-Alt-Shift-I | 在IE中打开                                           |
| Ctrl-Alt-Shift-F | 在Safari中打开                                       |
| Ctrl-Alt-Shift-O | 通过Outlook发送当前文件                              |

Ctrl+C 复制
Ctrl+X 剪切
Ctrl+V 粘贴
Ctrl+Z 撤消
Ctrl+Y 恢复
Ctrl+A 全选
Ctrl+F 键查找对话框启动
Ctrl+H 查找/替换对话框
Ctrl+D 复制并粘贴当行

Ctrl+L 删除当前行
Ctrl+T 当行向上移动一行
F3 查找下一个
Shift+F3 查找上一个
Ctrl+Shift+F 组合在文件中查找
Ctrl+F3 查找（volatil）下一页
Ctrl+Shift+F3 查找（volatil）上一页
Ctrl+Shift+I 组合增量搜索
Ctrl+S 保存文件
Ctrl+Alt+S 另存为
Ctrl+Shift+S 保存所有文件
Ctrl+O 打开文件
Ctrl+N 新建立文件
Ctrl+F2 切换书签
F2 转到下一个书签
Shift+F2 转到上一个书签
CTRL+G 定位换行,偏移量
Ctrl+W 关闭当前文档
Alt+Shift+Arrow 键移箭头键或
ALT+鼠标左键 单击列选择
F5 启动运行对话框
Ctrl+空格 输入法切换
Alt+空格 程序单击右键
Tab 插入缩进
Shift+Tab 删除缩进
Alt-Shift-Arrow 或
Ctrl +鼠标滚轮钮 放大缩小
Ctrl +Keypad/恢复原来的大小
F11 全屏模式
Ctrl+Tab 下一个文档
Ctrl+Shift+Tab 上一个文档
Ctrl+Shift+Up 当前线向上移
Ctrl-Shift-Down 当前线向下移
Ctrl+Alt+F 折叠当前层次
Ctrl+Alt+Shift+F展开当前层次
Alt+0 折叠全部
Alt+Shift+0 展开全部
Alt+(1~8) 折叠级别（1~8）
Alt+Shift+(1~8) 展开级别（1~8）
Ctrl+BackSpace 删除开始词
Ctrl+Delete 删除结束词
Ctrl+Shift+BackSpace 删除至行
Ctrl+Shift+Delete 删除至行尾
CTRL+U 转换为小写
Ctrl+Shift+U 转换为大写
Ctrl+B 转至匹配的括号
Ctrl+Shift+R 的开始录制/停止录制宏
Ctrl+Shift+P 播放录制的宏
CTRL+Q 注释/取消注释
Ctrl+Shift+Q 值流评论
Ctrl+Shift+T 当前行复制到剪贴板
Ctrl+P 打印
Alt+F4 退出
Ctrl+I 分割线
Ctrl+J 连接行
Ctrl+Alt+R 从右边阅读
Ctrl+Alt+L 从左边阅读
Ctrl+H 打开Find / Replace 对话框
Ctrl+D 复制当前行
Ctrl+L 删除当前行
Ctrl+T 上下行交换
F3 找下一个
Shift+F3 找上一个
Ctrl+Shift-F 在文件中找
Ctrl+F2 触发书签
F2 到前一个书签
Shift+F2 到下一个书签
F5 打开run对话框
Ctrl+Space 打开CallTip列表框
Tab (selection of several lines) 加入Space
Shift+Tab (selection of several lines) 移除Space
F11 全屏
Alt+0 折叠全部
Alt+Shift+0 展开全部
Ctrl+U 变为小写
Ctrl+Shift+U 变为大写
Ctrl+Q 块注释/消除注释

还有就是Notepad的字体比较小，以前总找不到能放大字体的地方，后来发现Ctrl+鼠标滑轮可以放大视图，字体风格也可以设置，notepad的字体很丰富。

快捷键设置：notepad++ 设置快捷键里面是所有快捷键，可以更加自己的喜欢设置快捷键，ep：设置编码转化的快捷键！

**主要添加或调整的光标操作按键：**

向前(Ctrl+F)，向后(Ctrl+B)，上一行(Ctrl+P)，下一行(Ctrl+N)

行最前(Ctrl+A), 行最后(Ctrl+E)

**方法**

菜单<设置>-<管理快捷键>

在"Main menu"及“Scintilla commands"中修改。

修改旧的快捷键，避免冲突：

新建 -> Ctrl+Alt+N

定位匹配括号 ->Ctrl+Alt+B

查找 -> Ctrl+Alt+F

选择所有 -> Ctrl+Alt+A

标签: [其他归纳](https://www.cnblogs.com/jungege/tag/其他归纳/)