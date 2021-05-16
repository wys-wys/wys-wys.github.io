## 方法/步骤

1. 

   方法一：菜单栏快捷键

   在打开的文件窗口的菜单栏，点击要复制的文件（夹），然后在【主页】选项卡点击【复制路径】选项，直接粘贴就行了

   ![win10如何快速复制文件（夹）路径](https://exp-picture.cdn.bcebos.com/dccb47de45078801a775a6f2b18ca608a50f8258.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

2. 

   方法二：按住shift右击复制

   选中你要复制的文件（夹），按住【shift】键，然后鼠标右击，在右键菜单点击【复制为路径】选项就行了

   ![win10如何快速复制文件（夹）路径](https://exp-picture.cdn.bcebos.com/3bcdb808a50f94fcf589e87d4cf88a775dddfc58.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

3. 

   方法三：右键菜单添加复制路径选项

   1.在桌面新建一个【文本文档】文件，双击打开，将下面这些内容输入到文档中：

   Windows Registry Editor Version 5.00

   

   [HKEY_CLASSES_ROOT\Directory\shell\copypath]

    @="复制文件夹路径"

   

   [HKEY_CLASSES_ROOT\Directory\shell\copypath\command] 

   @="mshta vbscript:clipboarddata.setdata(\"text\",\"%1\")(close)"

   

   [HKEY_CLASSES_ROOT\*\shell\copypath] 

   @="复制文件路径"

   

   [HKEY_CLASSES_ROOT\*\shell\copypath\command] 

   @="mshta vbscript:clipboarddata.setdata(\"text\",\"%1\")(close)"

   ![win10如何快速复制文件（夹）路径](https://exp-picture.cdn.bcebos.com/890dfb4a2f27e7ef860318b219dd3340b6f3f558.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

4. 

   2.保存后，将文件夹扩展名修改为“.reg”如图所示（没有显示扩展名的记得随便点开一个文件夹，在菜单栏依次点击【查看】选项卡>>☑【文件扩展名】）

   ![win10如何快速复制文件（夹）路径](https://exp-picture.cdn.bcebos.com/2947750192dd334004f6e234881c99c0affcf158.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

5. 

   3.双击该文件，会出现弹窗提示，因为要修改注册表，我们选择是就行了，完成添加操作

   ![win10如何快速复制文件（夹）路径](https://exp-picture.cdn.bcebos.com/aebdff86242fa8722e1acd57bfdaf05e4a23e958.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

6. 

   此时我们右击我们要复制路径的对象，然后在右键菜单直接选择【复制文件（夹）路径】就行了

   ![win10如何快速复制文件（夹）路径](https://exp-picture.cdn.bcebos.com/4b626771fe1d96d8da1c12932ccd0c6efbf2e158.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

   END

经验内容仅供参考，如果您需解决具体问题(尤其法律、医学等领域)，建议您详细咨询相关领域专业人士。

*作者声明：*本篇经验系本人依照真实经历原创，未经许可，谢绝转载。