# python编译出现SyntaxError: Non-ASCII character '\xe8' in file

出现这个问题主要是编译中出现了中文或特殊字符，所以可以使用以下方式解决：
在文件头部加上（一定要加在第一行）

# -*- coding: utf-8 -*-
1
或

# coding:utf-8 
1