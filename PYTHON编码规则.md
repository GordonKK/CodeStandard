# PYTHON编码规则

## 1前言

## 2.代码布局

### 2.1缩进

1. 【强制】使用 4 空格缩进，禁用任何 TAB 符号，每一级缩进使用4个空格。续行应该与其包裹元素对齐，要么使用圆括号、方括号和花括号内的隐式行连接来垂直对齐，要么使用挂行缩进对齐当使用挂行缩进时，应该考虑到第一行不应该有参数，以及使用缩进以区分自己是续行。
2. 【推荐】空格是首选的缩进方式。 
   制表符只能用于与同样使用制表符缩进的代码保持一致。 
   Python3不允许同时使用空格和制表符的缩进。 
   混合使用制表符和空格缩进的Python2代码应该统一转成空格。 
   当在命令行加入-t选项执行Python2时，它会发出关于非法混用制表符与空格的警告。当使用–tt时，这些警告会变成错误。强烈建议使用这样的参数。

```python
# 与左括号对齐
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
# 用更多的缩进来与其他行区分
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
# 挂行缩进应该再换一行
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)1234567891011121314
不推荐：
# 没有使用垂直对齐时，禁止把参数放在第一行
foo = long_function_name(var_one, var_two,
    var_three, var_four)
# 当缩进没有与其他行区分时，要增加缩进
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)123456789
```

### 2.2编码

1. 【强制】源码文件使用 UTF-8 无 BOM 编码格式
2. 【强制】所有的 Python 脚本文件都应在文件头标上

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# 
```

说明：

​	Python核心发布版本中的代码总是以UTF-8格式编码（或者在Python2中用ASCII编码）。 
​	使用ASCII（在Python2中）或UTF-8（在Python3中）编码的文件不应具有编码声明。 
​	在标准库中，非默认的编码应该只用于测试，或者当一个注释或者文档字符串需要提及一个包含内ASCII字符编码的作者名字的时候；否则，使用\x,\u,\U , 或者 \N 进行转义来包含非ASCII字符。 
​	对于Python 3和更高版本，标准库规定了以下策略（参见 [PEP 3131](http://legacy.python.org/dev/peps/pep-3131/)）：Python标准库中的所有标识符必须使用ASCII标识符，并在可行的情况下使用英语单词（在许多情况下，缩写和技术术语是非英语的）。此外，字符串文字和注释也必须是ASCII。唯一的例外是（a）测试非ASCII特征的测试用例，以及（b）作者的名称。作者的名字如果不使用拉丁字母拼写，必须提供一个拉丁字母的音译。 
​	鼓励具有全球受众的开放源码项目采取类似的政策。

### 2.3注释

业界普遍认同 Python 的注释分为两种，

1. 【推荐】一种是由 # 开头的“真正的”注释，例如，用于表明为何选择当前实现以及这种实现的原理和难点
2. 【推荐】另一种是 docstrings，例如，用于表明如何使用这个包、模块、类、函数（方法），甚至包括使用示例和单元测试

坚持适当注释原则。对不存在技术难点的代码坚持不注释，对存在技术难点的代码必须注释。但与注释不同，建议对每一个包、模块、类、函数（方法）写 docstrings，除非代码一目了然，非常简单。

### 2.4行的最大长度

​	【强制】所有行限制的最大字符数为79。 
​	没有结构化限制的大块文本（文档字符或者注释），每行的最大字符数限制在72。 
​	限制编辑器窗口宽度可以使多个文件并行打开，并且在使用代码检查工具(在相邻列中显示这两个版本)时工作得很好。 
​	大多数工具中的默认封装破坏了代码的可视化结构，使代码更难以理解。避免使用编辑器中默认配置的80窗口宽度，即使工具在帮你折行时在最后一列放了一个标记符。某些基于Web的工具可能根本不提供动态折行。 
​	Python标准库比较保守，需要将行宽限制在79个字符（文档/注释限制在72）。 
​	较长的代码行选择Python在小括号，中括号以及大括号中的隐式续行方式。通过小括号内表达式的换行方式将长串折成多行。这种方式应该优先使用，而不是使用反斜杠续行。 
​	反斜杠有时依然很有用。比如，比较长的，多个with状态语句，不能使用隐式续行，所以反斜杠是可以接受的：

```python
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())123
```

### 2.5空白行

1. 【强制】顶层函数和类的定义，前后用两个空行隔开。 
2. 【强制】类里的方法定义用一个空行隔开。 
3. 【建议】相关的功能组可以用额外的空行（谨慎使用）隔开。一堆相关的单行代码之间的空白行可以省略（例如，一组虚拟实现 dummy implementations）。 
4. 【建议】在函数中使用空行来区分逻辑段（谨慎使用）。 
5. 【推荐】Python接受control-L（即^L）换页符作为空格；许多工具把这些字符当作页面分隔符，所以你可以在文件中使用它们来分隔相关段落。请注意，一些编辑器和基于Web的代码阅读器可能无法识别control-L为换页，将在其位置显示另一个字形。

### 2.6导入

1. 【强制】导入通常在分开的行，例如：

   ```python
   推荐: import os
        import sys
   不推荐:  import sys, os1234
   但是可以这样：
   from subprocess import Popen, PIPE1
   ```
2. 【强制】导入总是位于文件的顶部，在模块注释和文档字符串之后，在模块的全局变量与常量之前。 
   导入应该按照以下顺序分组：
   ​	1).标准库导入
   ​	2).相关第三方库导入
   ​	3).本地应用/库特定导入 
3. 【推荐】使用绝对路径导入，如果导入系统没有正确的配置（比如包里的一个目录在sys.path里的路径后），使用绝对路径会更加可读并且性能更好（至少能提供更好的错误信息）:

   ```python
   import mypkg.sibling
   from mypkg import sibling
   from mypkg.sibling import example123
   ```
4. 【推荐】显示的指定相对导入路径是使用绝对路径的一个可接受的替代方案，特别是在处理使用绝对路径导入不必要冗长的复杂包布局时：

   ```python
   from . import sibling
   from .sibling import example12
   ```
5. 【强制】标准库要避免使用复杂的包引入结构，而总是使用绝对路径。 
   不应该使用隐式相对路径导入，并且在Python 3中删除了它。
6. 【推荐】当从一个包含类的模块中导入类时，常常这么写：

   ```python
   from myclass import MyClass
   from foo.bar.yourclass import YourClass12
   ```
7. 【推荐】如果上述的写法导致名字的冲突，那么这么写：

   ```python
   import myclass
   import foo.bar.yourclass12
   然后使用“myclass.MyClass”和“foo.bar.yourclass.YourClass”。
   ```
8. 【强制】避免通配符的导入（from import *），因为这样做会不知道命名空间中存在哪些名字，会使得读取接口和许多自动化工具之间产生混淆。对于通配符的导入，有一个防御性的做法，即将内部接口重新发布为公共API的一部分（例如，用可选加速器模块的定义覆盖纯Python实现的接口，以及重写那些事先不知道的定义）。 当以这种方式重新发布名称时，以下关于公共和内部接口的准则仍然适用。

### 2.7字符串引号

1. 【推荐】在Python中，单引号和双引号字符串是相同的。PEP不会为这个给出建议。选择一条规则并坚持使用下去。当一个字符串中包含单引号或者双引号字符的时候，使用和最外层不同的符号来避免使用反斜杠，从而提高可读性。 
2. 【推荐】对于三引号字符串，总是使用双引号字符来与[PEP 257](http://legacy.python.org/dev/peps/pep-0257/)中的文档字符串约定保持一致。

### 2.8模块级的呆名

1. 【推荐】像`__all__` , `__author__` , `__version__` 等这样的模块级“呆名“（也就是名字里有两个前缀下划线和两个后缀下划线），应该放在文档字符串的后面，以及除from `__future__` 之外的import表达式前面。Python要求将来在模块中的导入，必须出现在除文档字符串之外的其他代码之前。 
   
```python
"""This is the example module.
This module does stuff."""

from __future__ import barry_as_FLUFL
__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'
import os
import sys12345678910111213
```
## 3表达式和语句中的空格

### 3.1不能忍受的事情

1. 【强制】避免使用无关的空格，紧跟在小括号，中括号或者大括号后。

   ```python
   Yes: spam(ham[1], {eggs: 2})
   No:  spam( ham[ 1 ], { eggs: 2 } )12
   ```
2. 【强制】避免使用无关的空格，紧贴在逗号、分号或者冒号之前。

   ```python
   Yes: if x == 4: print x, y; x, y = y, x
   No:  if x == 4 : print x , y ; x , y = y , x12
   ```
3. 【强制】避免使用无关的空格，冒号在切片中就像二元运算符，在两边应该有相同数量的空格（把它当做优先级最低的操作符）。在扩展的切片操作中，所有的冒号必须有相同的间距。例外情况：当一个切片参数被省略时，空格就被省略了。 

   ```python
   推荐：
   ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
   ham[lower:upper], ham[lower:upper:], ham[lower::step]
   ham[lower+offset : upper+offset]
   ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
   ham[lower + offset : upper + offset]12345
   不推荐：
   ham[lower + offset:upper + offset]
   ham[1: 9], ham[1 :9], ham[1:9 :3]
   ham[lower : : upper]
   ham[ : upper]1234
   ```

4. 【强制】避免使用无关的空格，紧贴在函数参数的左括号之前。
   ```python
   Yes: spam(1)
   No:  spam (1)12
   ```
5. 【强制】避免使用无关的空格，紧贴索引或者切片的左括号之前。

   ```python
   Yes: dct['key'] = lst[index]
   No:  dct ['key'] = lst [index]12
   ```
6. 【强制】避免使用无关的空格，为了和另一个赋值语句对齐，在赋值运算符附件加多个空格。 
### 3.2其他建议
1. 【推荐】避免在尾部添加空格。因为尾部的空格通常都看不见，会产生混乱：比如，一个反斜杠后面跟一个空格的换行符，不算续行标记。有些编辑器不会保留尾空格，并且很多项目（像CPython）在pre-commit的挂钩调用中会过滤掉尾空格。
2. 【推荐】总是在二元运算符两边加一个空格：赋值（=），增量赋值（+=，-=），比较（==,<,>,!=,<>,<=,>=,in,not,in,is,is not），布尔（and, or, not）。
3. 【推荐】如果使用具有不同优先级的运算符，请考虑在具有最低优先级的运算符周围添加空格。有时需要通过自己来判断；但是，不要使用一个以上的空格，并且在二元运算符的两边使用相同数量的空格。 
   ```python
   推荐：
   i = i + 1
   submitted += 1
   x = x*2 - 1
   hypot2 = x*x + y*y
   c = (a+b) * (a-b)12345
   不推荐：
   i=i+1
   submitted +=1
   x = x * 2 - 1
   hypot2 = x * x + y * y
   c = (a + b) * (a - b)12345
   ```

   

4. 【推荐】在制定关键字参数或者默认参数值的时候，不要在=附近加上空格。 

   ```python
   推荐：
   def complex(real, imag=0.0):
       return magic(r=real, i=imag)
   不推荐：
   def complex(real, imag = 0.0):
       return magic(r = real, i = imag)
       
   ```
5. 【推荐】功能型注释应该使用冒号的一般性规则，并且在使用->的时候要在两边加空格。

   ```python
   推荐：
   def munge(input: AnyStr): 
   def munge() -> AnyStr:
   不推荐：
   def munge(input:AnyStr): 
   def munge()->PosInt: 
   ```

6. 【推荐】当给有类型备注的参数赋值的时候，在=两边添加空格（仅针对那种有类型备注和默认值的参数）。 

   ```python
   推荐：
   def munge(sep: AnyStr = None): 
   def munge(input: AnyStr, sep: AnyStr = None, limit=1000):
   不推荐：
   def munge(input: AnyStr=None): 
   def munge(input: AnyStr, limit = 1000):
   ```
7. 【推荐】复合语句(同一行中的多个语句)通常是不允许的。 
   ```python
   推荐：
   if foo == 'blah':
       do_blah_thing()
   do_one()
   do_two()
   do_three()
   最好别这样：
   if foo == 'blah': do_blah_thing()
   do_one(); do_two(); do_three()12
   ```
8. 【推荐】虽然有时候将小的代码块和 if/for/while 放在同一行没什么问题，多行语句块的情况不要这样用，同样也要避免代码行太长 
   ```python
   最好别这样：
   if foo == 'blah': do_blah_thing()
   for x in lst: total += x
   while t < 10: t = delay()
   绝对别这样：
   if foo == 'blah': do_blah_thing()
   else: do_non_blah_thing()
   try: something()
   finally: cleanup()
   do_one(); do_two(); do_three(long, argument,
                                list, like, this)
   if foo == 'blah': one(); two(); three()
   ```
## 4Comments 注释
### 4.1Block Comments 块注释
1. 【推荐】块注释通常适用于跟随它们的某些（或全部）代码，并缩进到与代码相同的级别。块注释的每一行开头使用一个#和一个空格（除非块注释内部缩进文本）。 
2. 【推荐】块注释内部的段落通过只有一个#的空行分隔。
### 4.2Inline Comments 行内注释
1. 【推荐】有节制地使用行内注释。 
2. 【推荐】行内注释是与代码语句同行的注释。行内注释和代码至少要有两个空格分隔。注释由#和一个空格开始。 
3. 【推荐】如果状态明显的话，行内注释是不必要的，反而会分散注意力。比如说下面这样就不需要：
```python
	x = x + 1                 # Increment x1
	但有时，这样做很有用：
	x = x + 1                 # Compensate for border1
```
### 4.3Documentation Strings 文档字符串
1. 【强制】要为所有的公共模块，函数，类以及方法编写文档说明。非公共的方法没有必要，但是应该有一个描述方法具体作用的注释。这个注释应该在def那一行之后。
2. 【强制】多行文档说明使用的结尾三引号应该自成一行
3. 【强制】对于单行的文档说明，尾部的三引号应该和文档在同一行。
## 5命名规范
​	Python库的命名规范很乱，从来没能做到完全一致。但是目前有一些推荐的命名标准。新的模块和包（包括第三方框架）应该用这套标准，但当一个已有库采用了不同的风格，推荐保持内部一致性。
### 5.1最重要的原则
​	【强制】那些暴露给用户的API接口的命名，应该遵循反映使用场景而不是实现的原则。
### 5.2命名风格
​	【推荐】有许多不同的命名风格。这里能够帮助大家识别正在使用什么样的命名风格，而不考虑他们为什么使用。 
以下是常见的命名方式：

- b（单个小写字母）
- B（单个大写字母）
- lowercase 小写字母
- lower_case_with_underscores 使用下划线分隔的小写字母
- UPPERCASE 大写字母
- UPPER_CASE_WITH_UNDERSCORES 使用下划线分隔的大写字母
- CapitalizedWords（或者叫 CapWords，或者叫CamelCase 驼峰命名法 —— 这么命名是因为字母看上去有起伏的外观。有时候也被称为StudlyCaps。 
  注意：当在首字母大写的风格中用到缩写时，所有缩写的字母用大写，因此，HTTPServerError 比 HttpServerError 好。
- mixedCase（不同于首字母大写，第一个单词的首字母小写）
- Capitalized_Words_With_Underscores

用前缀或结尾下划线的特殊格式是被认可的（通常和一些约定相结合）：
- _single_leading_underscore：（单下划线开头）弱“内部使用”指示器。比如 from M import * 是不会导入以下划线开始的对象的。
- single_trailing_underscore_：（单下划线结尾）这是避免和Python内部关键词冲突的一种约定，比如：Tkinter.Toplevel(master, class_=’ClassName’)
- `__double_leading_underscore`：（双下划线开头）当这样命名一个类的属性时，调用它的时候名字会做矫正（在类FooBar中，`__boo`变成了`_FooBar__boo`；见下文）。
- `__double_leading_and_trailing_underscore__`：（双下划线开头，双下划线结尾）“magic”对象或者存在于用户控制的命名空间内的属性，例如：`__init__`,`__import__`或者`__file__`。除了作为文档之外，永远不要命这样的名。
### 5.3约定俗成：命名约定
#### 5.3.1应避免的名字
​	【强制】永远不要使用字母‘l’（小写的L），‘O’（大写的O），或者‘I’（大写的I）作为单字符变量名。 因为在有些字体里，这些字符无法和数字0和1区分，如果想用‘l’，用‘L’代替。
#### 5.3.2包名和模块名
​	【推荐】模块应该用简短全小写的名字，如果为了提升可读性，下划线也是可以用的。Python包名也应该使用简短全小写的名字，但不建议用下划线。 
​	【推荐】当使用C或者C++编写了一个依赖于提供高级（更面向对象）接口的Python模块的扩展模块，这个C/C++模块需要一个下划线前缀（例如：_socket）

#### 5.3.3类名
​	【推荐】类名一般使用首字母大写的约定。 
​	【推荐】在接口被文档化并且主要被用于调用的情况下，可以使用函数的命名风格代替。 

```python
对于内置的变量命名有一个单独的约定：大部分内置变量是单个单词（或者两个单词连接在一起），首字母大写的命名法只用于异常名或者内部的常量。
```
#### 5.3.4异常名
​	【推荐】因为异常一般都是类，所有类的命名方法在这里也适用。然而，你需要在异常名后面加上“Error”后缀。
#### 5.3.5全局变量名
​	【推荐】约定和函数命名规则一样。 
​	【推荐】通过 from M import * 导入的模块应该使用**all**机制去防止内部的接口对外暴露，或者使用在全局变量前加下划线的方式（表明这些全局变量是模块内非公有）。

#### 5.3.6函数名
​	【强制】函数名应该小写，如果想提高可读性可以用下划线分隔。 
​	【推荐】大小写混合仅在为了兼容原来主要以大小写混合风格的情况下使用（比如 threading.py），保持向后兼容性。

#### 5.3.7函数和方法参数
​	【强制】始终要将 self 作为实例方法的的第一个参数。 
​	【强制】始终要将 cls 作为类静态方法的第一个参数。 
​	【强制】如果函数的参数名和已有的关键词冲突，在最后加单一下划线比缩写或随意拼写更好。因此 class_ 比 clss 更好。（也许最好用同义词来避免这种冲突）

#### 5.3.8方法名和实例变量
​	【推荐】遵循这样的函数命名规则：使用下划线分隔小写单词以提高可读性。 
​	【推荐】在非共有方法和实例变量前使用单下划线。 
​	【推荐】通过双下划线前缀触发Python的命名转换规则来避免和子类的命名冲突。 

```python
Python通过类名对这些命名进行转换：如果类 Foo 有一个叫 `__a` 的成员变量， 它无法通过 `Foo.__a` 访问。（执着的用户可以通过 `Foo._Foo__a` 访问。）一般来说，前缀双下划线用来避免类中的属性命名与子类冲突的情况。 
```
#### 5.3.9Constants 常量
常量通常定义在模块级，通过下划线分隔的全大写字母命名。例如： MAX_OVERFLOW 和 TOTAL。
#### 5.3.10继承的设计
​	始终要考虑到一个类的方法和实例变量（统称：属性）应该是共有还是非共有。如果存在疑问，那就选非共有；因为将一个非共有变量转为共有比反过来更容易。 
​	公共属性是那些与类无关的客户使用的属性，并承诺避免向后不兼容的更改。非共有属性是那些不打算让第三方使用的属性；你不需要承诺非共有属性不会被修改或被删除。 
​	我们不使用“私有（private）”这个说法，是因为在Python中目前还没有真正的私有属性（为了避免大量不必要的常规工作）。 
​	另一种属性作为子类API的一部分（在其他语言中通常被称为“protected”）。有些类是专为继承设计的，用来扩展或者修改类的一部分行为。当设计这样的类时，要谨慎决定哪些属性时公开的，哪些是作为子类的API，哪些只能在基类中使用。 
贯彻这样的思想，一下是一些让代码Pythonic的准则：

- 【强制】公共属性不应该有前缀下划线。
- 【强制】如果公共属性名和关键字冲突，在属性名之后增加一个下划线。这比缩写和随意拼写好很多。
- 【强制】对于单一的共有属性数据，最好直接对外暴露它的变量名，而不是通过负责的 存取器（accessor）/突变（mutator） 方法。请记住，如果你发现一个简单的属性需要成长为一个功能行为，那么Python为这种将来会出现的扩展提供了一个简单的途径。在这种情况下，使用属性去隐藏属性数据访问背后的逻辑。 
  注意1：属性只在new-style类中起作用。 
  注意2：尽管功能方法对于类似缓存的负面影响比较小，但还是要尽量避免。 
  注意3：属性标记会让调用者认为开销（相当的）小，避免用属性做开销大的计算。
- 【强制】如果你的类打算用来继承的话，并且这个类里有不希望子类使用的属性，就要考虑使用双下划线前缀并且没有后缀下划线的命名方式。这会调用Python的命名转换算法，将类的名字加入到属性名里。这样做可以帮助避免在子类中不小心包含了相同的属性名而产生的冲突。 
  注意1：只有类名才会整合进属性名，如果子类的属性名和类名和父类都相同，那么你还是会有命名冲突的问题。 
  注意2：命名转换会在某些场景使用起来不太方便，例如调试，`__getattr__()`。然而命名转换的算法有很好的文档说明并且很好操作。 
  注意3：不是所有人都喜欢命名转换。尽量避免意外的名字冲突和潜在的高级调用。
### 5.4公共和内部的接口
​	任何向后兼容保证只适用于公共接口，因此，用户清晰地区分公共接口和内部接口非常重要。 
​	文档化的接口被认为是公开的，除非文档明确声明它们是临时或内部接口，不受通常的向后兼容性保证。所有未记录的接口都应该是内部的。 
​	为了更好地支持内省（introspection），模块应该使用`__all__`属性显式地在它们的公共API中声明名称。将`__all__`设置为空列表表示模块没有公共API。 
​	即使通过`__all__`设置过，内部接口（包，模块，类，方法，属性或其他名字）依然需要单个下划线前缀。 
​	如果一个命名空间（包，模块，类）被认为是内部的，那么包含它的接口也应该被认为是内部的。 
​	导入的名称应该始终被视作是一个实现的细节。其他模块必须不能间接访问这样的名称，除非它是包含它的模块中有明确的文档说明的API，例如 os.path 或者是一个包里从子模块公开函数接口的 `__init__` 模块。

## 6附录：编程建议
- 【强制】代码应该用不损害其他Python实现的方式去编写（PyPy，Jython，IronPython，Cython，Psyco 等）。 
  比如，不要依赖于在CPython中高效的内置字符连接语句 a += b 或者 a = a + b。这种优化甚至在CPython中都是脆弱的（它只适用于某些类型）并且没有出现在不使用引用计数的实现中。在性能要求比较高的库中，可以种 ”.join() 代替。这可以确保字符关联在不同的实现中都可以以线性时间发生。
- 【强制】和像None这样的单例对象进行比较的时候应该始终用 is 或者 is not，永远不要用等号运算符。 
  另外，如果你在写 if x 的时候，请注意你是否表达的意思是 if x is not None。举个例子，当测试一个默认值为None的变量或者参数是否被设置为其他值的时候。这个其他值应该是在上下文中能成为bool类型false的值。
- 【强制】使用 is not 运算符，而不是 not … is 。虽然这两种表达式在功能上完全相同，但前者更易于阅读，所以优先考虑。 
```python
	推荐：
	if foo is not None:1
    不推荐：
    if not foo is None:1
```
- 【强制】当使用富比较（rich comparisons，一种复杂的对象间比较的新机制，允许返回值不为-1,0,1）实现排序操作的时候，最好实现全部的六个操作符（`__eq__`, `__ne__`, `__lt__`, `__gt__`, `__ge__`）而不是依靠其他的代码去实现特定的比较。 
- 【强制】始终使用def表达式，而不是通过赋值语句将lambda表达式绑定到一个变量上。 
  ```python
  def f(x): return 2*x1
  不推荐：
  f = lambda x: 2*x1
  ```
- 【强制】第一个形式意味着生成的函数对象的名称是“f”而不是泛型“< lambda >”。这在回溯和字符串显示的时候更有用。赋值语句的使用消除了lambda表达式优于显式def表达式的唯一优势（即lambda表达式可以内嵌到更大的表达式中）。
  - 从Exception继承异常，而不是BaseException。直接继承BaseException的异常适用于几乎不用来捕捉的异常。 
    设计异常的等级，要基于扑捉异常代码的需要，而不是异常抛出的位置。以编程的方式去回答“出了什么问题？”，而不是只是确认“出现了问题”
  - 类的命名规范适用于这里，但是你需要添加一个“Error”的后缀到你的异常类，如果异常是一个Error的话。非本地流控制或者其他形式的信号的非错误异常不需要特殊的后缀。
  - 适当地使用异常链接。在Python 3里，为了不丢失原始的根源，可以显式指定“raise X from Y”作为替代。 
    当故意替换一个内部异常时（Python 2 使用“raise X”， Python 3.3 之后 使用 “raise X from None”），确保相关的细节转移到新的异常中（比如把AttributeError转为KeyError的时候保留属性名，或者将原始异常信息的文本内容内嵌到新的异常中）。
  - 在Python 2中抛出异常时，使用 rasie ValueError(‘message’) 而不是用老的形式 raise ValueError, ‘message’。 
    第二种形式在Python3 的语法中不合法 
    使用小括号，意味着当异常里的参数非常长，或者包含字符串格式化的时候，不需要使用换行符。
  - 当捕获到异常时，如果可以的话写上具体的异常名，而不是只用一个except: 块。 
    比如说：
```python
	try:
    	import platform_specific_module
	except ImportError:
    	platform_specific_module = None1234
```
- 【强制】如果只有一个except: 块将会捕获到SystemExit和KeyboardInterrupt异常，这样会很难通过Control-C中断程序，而且会掩盖掉其他问题。如果你想捕获所有指示程序出错的异常，使用 except Exception: （只有except等价于 except BaseException:）。 
- 【强制】两种情况不应该只使用‘excpet’块：

1. 如果异常处理的代码会打印或者记录log；至少让用户知道发生了一个错误。
2. 如果代码需要做清理工作，使用 raise..try…finally 能很好处理这种情况并且能让异常继续上浮。
   - 当给捕捉的异常绑定一个名字时，推荐使用在Python 2.6中加入的显式命名绑定语法：
```python
try:
    process_data()
except Exception as exc:
    raise DataProcessingFailedError(str(exc))1234
```
为了避免和原来基于逗号分隔的语法出现歧义，Python3只支持这一种语法。
- 【强制】当捕捉操作系统的错误时，推荐使用Python 3.3 中errno内定数值指定的异常等级。
- 【强制】另外，对于所有的 try/except 语句块，在try语句中只填充必要的代码，这样能避免掩盖掉bug。 
```python
推荐：
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)
不推荐：
try:
    # Too broad!
    return handle_value(collection[key])
except KeyError:
    # Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```

- 【强制】当代码片段局部使用了某个资源的时候，使用with 表达式来确保这个资源使用完后被清理干净。用try/finally也可以。
- 【强制】无论何时获取和释放资源，都应该通过单独的函数或方法调用上下文管理器。举个例子： 
```python
推荐：
with conn.begin_transaction():
    do_stuff_in_transaction(conn)
不推荐：
with conn:
    do_stuff_in_transaction(conn)
```

- 【强制】第二个例子没有提供任何信息去指明`__enter__`和`__exit__`方法在事务之后做出了关闭连接之外的其他事情。这种情况下，明确指明非常重要。

- 【强制】返回的语句保持一致。函数中的返回语句都应该返回一个表达式，或者都不返回。如果一个返回语句需要返回一个表达式，那么在没有值可以返回的情况下，需要用 return None 显式指明，并且在函数的最后显式指定一条返回语句（如果能跑到那的话）。 
```python
推荐：
def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None
def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)
def foo(x):
    if x >= 0:
        return math.sqrt(x)
def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
```

- 【强制】使用字符串方法代替字符串模块。 
  字符串方法总是更快，并且和unicode字符串分享相同的API。如果需要兼容Python2.0之前的版本可以不用考虑这个规则。
- 【强制】使用 ”.startswith() 和 ”.endswith() 代替通过字符串切割的方法去检查前缀和后缀。 
  startswith()和endswith()更干净，出错几率更小。比如：
```python
推荐: if foo.startswith('bar'):
糟糕: if foo[:3] == 'bar':
```

- 【强制】对象类型的比较应该用isinstance()而不是直接比较type。

```python
正确: if isinstance(obj, int):
糟糕: if type(obj) is type(1):
```
- 【强制】当检查一个对象是否为string类型时，记住，它也有可能是unicode string！在Python2中，str和unicode都有相同的基类：basestring，所以你可以这样：
```python
if isinstance(obj, basestring):
注意，在Python3中，unicode和basestring都不存在了（只有str）并且bytes类型的对象不再是string类型的一种（它是整数序列）
```
- 【强制】对于序列来说（strings，lists，tuples），可以使用空序列为false的情况。
```
正确: if not seq:
      if seq:
糟糕: if len(seq):
      if not len(seq):
```

- 【强制】书写字符串时不要依赖单词结尾的空格，这样的空格在视觉上难以区分，有些编辑器会自动去掉他们（比如 reindent.py （译注：re indent 重新缩进））
- 【强制】不要用 == 去和True或者False比较：

```python
正确: if greeting:
糟糕: if greeting == True:
更糟: if greeting is True:.
```

