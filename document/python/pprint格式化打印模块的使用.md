# [Python模块学习]使用pprint模块格式化打印

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[GanZiQim](https://blog.csdn.net/jy692405180) 2017-03-09 11:44:12 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 2425 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 5

分类专栏： [Python](https://blog.csdn.net/jy692405180/category_6373693.html) 文章标签： [python](https://www.csdn.net/tags/MtjaQg4sNDk0LWJsb2cO0O0O.html)

版权

# pprint模块

模块描述：pprint是“pretty-print”的意思，该模块提供了将数据格式化输出的方法。可以提高输出数据的可读性。

------

**pprint.pprint(object, stream=None, indent=1, width=80, depth=None, \*, compact=False)**

1. stream：设置输出流，模块中默认使用sys.stdout。该对象唯一会使用到的函数是write()。
2. indent：控制每层嵌套之间的空格数量。默认为1。
3. width：控制打印显示的宽度。默认为80个字符。**注意：当单个对象的长度超过width时，并不会分多行显示，而是会突破规定的宽度。**
4. depth：控制数据打印出来的层级，如果超过了规定的层级，会以…显示。默认不约束层级数量。
5. compact：3.4版本之后加入的参数，默认为False。如果值为False，超过width规定长度的序列会被分散打印到多行。如果为True，会尽量使序列填满width规定的宽度。

```python
>>> import pprint
>>> x = [1, 2]
>>> pprint.pprint(x, width=7)
[1, 2]
>>> pprint.pprint(x, width=5)
[1,
 2]
>>> pprint.pprint(x, width=5, indent=2)
[ 1,
  2]
>>> y = [1, [2, [3, 4, 5], 6], 7]
>>> pprint.pprint(y, depth=2)
[1, [2, [...], 6], 7]
>>> pprint.pprint(y, width=10, compact=False)
[1,
 [2,
  [3,
   4,
   5],
  6],
 7]
>>> pprint.pprint(y, width=10, compact=True)
[1,
 [2,
  [3, 4,
   5],
  6],
 7]
 >>> pprint.pprint("12345678", width=5)
'12345678'123456789101112131415161718192021222324252627282930
```

**可以用`print = pprint.pprint`使当前程序默认使用pprint进行打印。**

```python
>>> print = pprint.pprint
>>> print({1:"hello", 2:"world"}, width=10, indent=4)
{   1: 'hello',
    2: 'world'}1234
```

**注意：字典在显示前会先经过排序。**

```python
>>> x = {1:"one", 3:"three", 2:"two"}
>>> pprint.pprint(x)
{1: 'one', 2: 'two', 3: 'three'}123
```

------

**pprint.pformat(object, indent=1, width=80, depth=None, \*, compact=False)**

与pprint.pprint的区别是不带stream参数，函数返回一个格式化之后的字符串。

```python
>>> print(pprint.pformat({1: "hello", 2: "你好", 3: "hola"}, width=10))
{1: 'hello',
 2: '你好',
 3: 'hola'}1234
```

------

**pprint.isreadable(object)**

判断对象是不是可读（可以用eval()函数运行）。比如对象中有别的自定义对象时，或者包含了自身时，返回False。

```python
>>> class a():
...  pass
...
>>> pprint.isreadable([a(), 1, 2])
False
>>> pprint.isreadable([1, 2])
True1234567
```

------

**pprint.isrecursive(object)**

判断对象是不是包含自身。（是否递归）

```python
>>> x = []
>>> x.insert(0, x)
>>> pprint.isrecursive(x)
True
>>> pprint.isrecursive([])
False123456
```

------

**pprint.saferepr(object)**

返回一个字符串。如果对象中含有递归的对象，会用<Recursion on typename with id=number>的形式表示。

```python
>>> x = [1, 2, 3]
>>> x.insert(0, x)
>>> pprint.saferepr(x)
'[<Recursion on list with id=2818879365512>, 1, 2, 3]'1234
```

------

pprint模块中定义了一个类PrettyPrinter

**class pprint.PrettyPrinter(indent=1, width=80, depth=None, stream=None, \*, compact=False)**

使用PrettyPrinter构造的实例也可以使用pformat/pprint/isreadable/isrecursive函数。不过只需传入object参数。**事实上，pprint.pformat和pprint.pprint都是通过构造一个PrettyPrinter实例来完成相应功能的。**在实例中使用上述4个函数会比直接调用快一些。

```python
>>> pp = pprint.PrettyPrinter(indent=4, width=20)
>>> pp.pprint([["Python"],["Java"],["CSharp"]])
[   ['Python'],
    ['Java'],
    ['CSharp']]12345
```

需要注意的还有，官方文档3.6版本上说：PrettyPrinter的isreadable函数会在object超过构造时指定的depth时返回False，这点跟pprint.isreadable不一样。**但是实际上depth并不会影响输出，这一点博主会在后续的使用中继续验证。**

官方文档原文：

> If the depth parameter of the PrettyPrinter is set and the object is deeper than allowed, this returns False.

另外，PrettyPrinter新增了一个函数format(object, context, maxlevels, level)。这个函数会返回三个值，第一个是object的格式化版本，第二个标识了函数是不是可读的，第三个标识了对象是否递归。这个函数是为了给子类提供一个修改对象转换到字符串途径的方法。不过不易用，实用性不是很大。

关于上述几个参数的具体意义，官方文档是这么说的：

> The first argument is the object to be presented. The second is a dictionary which contains the id() of objects that are part of the current presentation context (direct and indirect containers for object that are affecting the presentation) as the keys; if an object needs to be presented which is already represented in context, the third return value should be True. Recursive calls to the format() method should add additional entries for containers to this dictionary. The third argument, maxlevels, gives the requested limit to recursion; this will be 0 if there is no requested limit. This argument should be passed unmodified to recursive calls. The fourth argument, level, gives the current level; recursive calls should be passed a value less than that of the current call.

------

总结：pprint是一个非常好用的模块，可以用来向文件、日志、控制台输出格式化后的数据，并且可以控制输出的格式。经过pprint格式化的数据更加易读、易理解，比起自带的内建函数print更加人性化。