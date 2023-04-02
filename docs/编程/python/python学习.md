 



# python 学习笔记



## 基本

dir(obj) 列出某个类或者某个模块中的全部内容，包括变量、方法、函数和类等

help(obj) 函数用来查看某个函数或者模块的帮助文档

```python
>>> help(str.lower)
Help on built-in function lower:

lower() method of builtins.str instance
    Return a copy of the string converted to lowercase.
>>> dir(str)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 
'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```



## 词法

### 注释

 以`#` 开头，在物理行末尾截止.

### 编码声明

Python 脚本第一或第二行的注释匹配正则表达式 `coding[=:]\s*([-\w.]+)` 时，该注释会被当作编码声明；

```python
# -*- coding: UTF-8 -*-
```

没有编码声明时，默认编码为 UTF-8

**Ansi并非是一种编码格式，而是指操作系统所使用的编码。**

* 英文操作系统  ASCII,

* 简体中文操作系统 GBK

* 繁体中文  Big-5

微软用一个叫“[Windows code pages](https://en.wikipedia.org/wiki/Code_page)”（在命令行下执行chcp命令可以查看当前code page的值）的值来判断系统默认编码，比如：简体中文的code page值为936（它表示GBK编码，win95之前表示GB2312). 

GBK兼容GB 2312。

GB18030兼容GBK。

GB 18030主要有以下特点 [1] ：

- 采用变长多[字节](https://baike.baidu.com/item/字节)编码，每个字可以由1个、2个或4个字节组成。
- 编码空间庞大，最多可定义161万个字符。
- 完全支持Unicode，无需动用造字区即可支持中国国内[少数民族](https://baike.baidu.com/item/少数民族)文字、中日韩和繁体汉字以及[emoji](https://baike.baidu.com/item/emoji)等字符。

GB 18030在微软视窗系统中的[代码页](https://baike.baidu.com/item/代码页)为54936。



在python中，读取后的字符串统一是unicode.

![这里写图片描述](python学习.assets\20170813174815282)



### Python 专属的编码格式

有一些预定义编解码器是 Python 专属的，因此它们在 Python 之外没有意义。 这些编解码器按其所预期的输入和输出类型在下表中列出（请注意虽然文本编码是编解码器最常见的使用场景，但下层的编解码器架构支持任意数据转换而不仅是文本编码）。 对于非对称编解码器，该列描述的含义是编码方向。



以下编解码器提供了 [`str`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str) 到 [`bytes`](https://docs.python.org/zh-cn/3/library/stdtypes.html#bytes) 的编码和 [bytes-like object](https://docs.python.org/zh-cn/3/glossary.html#term-bytes-like-object) 到 [`str`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str) 的解码，类似于 Unicode 文本编码。

| 编码               | 别名       | 含意                                                         |
| :----------------- | :--------- | :----------------------------------------------------------- |
| idna               |            | 实现 [**RFC 3490**](https://tools.ietf.org/html/rfc3490.html)，另请参阅 [`encodings.idna`](https://docs.python.org/zh-cn/3/library/codecs.html#module-encodings.idna) 。仅支持 `errors='strict'` 。 |
| mbcs               | ansi, dbcs | Windows 专属：根据 ANSI 代码页（CP_ACP）对操作数进行编码。   |
| oem                |            | Windows 专属：根据 OEM 代码页（CP_OEMCP）对操作数进行编码。*3.6 新版功能.* |
| palmos             |            | PalmOS 3.5 的编码格式                                        |
| punycode           |            | 实现 [**RFC 3492**](https://tools.ietf.org/html/rfc3492.html)。 不支持有状态编解码器。 |
| raw_unicode_escape |            | Latin-1 编码格式附带对其他码位以 `\uXXXX` 和 `\UXXXXXXXX` 进行编码。 现有反斜杠不会以任何方式转义。 它被用于 Python 的 pickle 协议。 |
| undefined          |            | 所有转换都将引发异常，甚至对空字符串也不例外。 错误处理方案会被忽略。 |
| unicode_escape     |            | 适合用于以 ASCII 编码的 Python 源代码中的 Unicode 字面值内容的编码格式，但引号不会被转义。 对 Latin-1 源代码进行解码。 请注意 Python 源代码实际上默认使用 UTF-8。 |

## 

### 显式拼接行

行尾加\可以拼接多个物理行为一个逻辑行

```python
if 1900 < year < 2100 and 1 <= month <= 12 \
   and 1 <= day <= 31 and 0 <= hour < 24 \
   and 0 <= minute < 60 and 0 <= second < 60:   # Looks like a valid date
        return 1
```



### 隐式拼接行

圆括号、方括号、花括号内的表达式可以分成多个物理行，不必使用反斜杠。例如：

```python
month_names = ['Januari', 'Februari', 'Maart',      # These are the
               'April',   'Mei',      'Juni',       # Dutch names
               'Juli',    'Augustus', 'September',  # for the months
               'Oktober', 'November', 'December']   # of the year
```

### 缩进

逻辑行开头的空白符（空格符和制表符）用于计算该行的缩进层级，决定语句组块。

首个非空字符前的空格数决定了该行的缩进层次。

反斜杠进行多行拼接时，视为一个逻辑行。

### 变量命名

1. Python 语言中，以下划线开头的标识符有特殊含义，例如:

   - 以单下划线开头的标识符（如 _width），表示不能直接访问的类属性，其无法通过 from...import* 的方式导入；
   - 以双下划线开头的标识符（如__add）表示类的私有成员；
   - 以双下划线作为开头和结尾的标识符（如 __init__），是专用标识符。

   因此，除非特定场景需要，应避免使用以下划线开头的标识符。

   命名不要与保留字冲突，以下命令查询保留字。

   ```python
   >>> import keyword
   >>> keyword.kwlist
   ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
   ```

###  Python 保留字

一览表（大写不是保留字，如ELSE就不是保留字 ）

| and   | as   | assert | break    | class  | continue |
| ----- | ---- | ------ | -------- | ------ | -------- |
| def   | del  | elif   | else     | except | finally  |
| for   | from | False  | global   | if     | import   |
| in    | is   | lambda | nonlocal | not    | None     |
| or    | pass | raise  | return   | try    | True     |
| while | with | yield  |          |        |          |

## 

### 数值字面值

* 数值字面值有三种类型： 整数、浮点数、虚数。没有复数字面值（复数由实数加虚数构成）。

* 负值-5其实是一元运算符-加字面值5合成的。

* 数值中可以含_, _会被忽略，可以让数字更易读。

* 整数长度没有限制，能一直大到占满可用内存。

#### 整数

字面值词法定义如下：

```
integer      ::=  decinteger | bininteger | octinteger | hexinteger
decinteger   ::=  nonzerodigit (["_"] digit)* | "0"+ (["_"] "0")*
bininteger   ::=  "0" ("b" | "B") (["_"] bindigit)+
octinteger   ::=  "0" ("o" | "O") (["_"] octdigit)+
hexinteger   ::=  "0" ("x" | "X") (["_"] hexdigit)+
nonzerodigit ::=  "1"..."9"
digit        ::=  "0"..."9"
bindigit     ::=  "0" | "1"
octdigit     ::=  "0"..."7"
hexdigit     ::=  digit | "a"..."f" | "A"..."F"
```

示例：

```
7     2147483647                        0o177    0b100110111
3     79228162514264337593543950336     0o377    0xdeadbeef
      100_000_000_000                   0b_1110_0101
```



#### 浮点数

```
floatnumber   ::=  pointfloat | exponentfloat
pointfloat    ::=  [digitpart] fraction | digitpart "."
exponentfloat ::=  (digitpart | pointfloat) exponent
digitpart     ::=  digit (["_"] digit)*
fraction      ::=  "." digitpart
exponent      ::=  ("e" | "E") ["+" | "-"] digitpart
```

示例：

```
3.14    10.    .001    1e100    3.14e-10    0e0    3.14_15_93
```

#### 虚数

```
imagnumber ::=  (floatnumber | digitpart) ("j" | "J")
```

虚数字面值生成实部为 0.0 的复数。复数由一对浮点数表示，它们的取值范围相同。创建实部不为零的复数，则需添加浮点数，例如 `(3+4j)`。虚数字面值示例如下：

```
3.14j   10.j    10j     .001j   1e100j   3.14e-10j   3.14_15_93j
```

#### 数据类型

- 整数

  0xffaa4c3d   ：十六进制表示

  10_000_000_000 ： **python支持很大的数**，整数的取值范围是无限的, 对于大整数可以中间加_用于区分。不影响数值结果。

  ```python
  #十六进制
  hex1 = 0x45
  hex2 = 0x4Af
  print("hex1Value: ", hex1)
  print("hex2Value: ", hex2)
  
  #二进制
  bin1 = 0b101
  print('bin1Value: ', bin1)
  bin2 = 0B110
  print('bin2Value: ', bin2)
  
  #八进制
  oct1 = 0o26
  print('oct1Value: ', oct1)
  oct2 = 0O41
  print('oct2Value: ', oct2)
  ```

  

- 浮点数

  浮点数存储会有误差

  12.38e8  科学记数法 把10用e替代，1.23x109就是`1.23e9`，或者`12.3e8`，0.000012可以写成`1.2e-5`

  ```python
  >>> 12.3 * 0.1
  1.2300000000000002   
  # 可以看出，浮点数结果并不精确
  ```

- 复数

  表示 a + bj  或a + bJ

  ```python
  >>> c1 = 12 + 0.2j
  >>> print("c1Value: ", c1)
  c1Value:  (12+0.2j)
  >>> print("c1Type", type(c1))
  c1Type <class 'complex'>
  >>> c2 = 6 - 1.2j
  >>> print("c2Value: ", c2)
  c2Value:  (6-1.2j)
  >>> #对复数进行简单计算
  >>> print("c1+c2: ", c1+c2)
  c1+c2:  (18-1j)
  >>> print("c1*c2: ", c1*c2)
  c1*c2:  (72.24-13.2j)
  ```

    

- 字符串

  ' abc'

  "abc"

  "ab\nc"  \转义

  r'abc\\n'   r打头不转义

  '''abc

  abc

  abc'''  多行文件用三个单字符表示。

- boolean

  True False  

  布尔类型可以当做整数来对待，即 True 相当于整数值 1，False 相当于整数值 0。

  ```python
  >>> False + 1
  1
  >>> True + 1
  2
  ```

  

- 逻辑运算符 and or not

- None

  空值不为0，是特殊的一个值。

- 当一行过长时，可以在结果加\  ，行尾的续行符，即一行未完，转到下一行继续写。

  ```python
  >>> n = 3*3 + \
  ... 2*2
  >>> n   
  13
  >>> s = 'abc\
  ... efg'
  >>> s
  'abcefg'
  # 对于长字符串，也可用```来代替\  但是二者还是有区别的，```会原样输出换行  \则不含换行。
  >>> s = '''abc
  ... efg'''
  >>> s
  'abc\nefg'
  >>> print(s)
  abc
  efg
  ```

#### 类型转换

常用数据类型转换函数

| int(x)                 | 将 x 转换成整数类型                                |
| ---------------------- | -------------------------------------------------- |
| float(x)               | 将 x 转换成浮点数类型                              |
| complex(real，[,imag]) | 创建一个复数                                       |
| str(x)                 | 将 x 转换为字符串                                  |
| repr(x)                | 将 x 转换为表达式字符串                            |
| eval(str)              | 计算在字符串中的有效 Python 表达式，并返回一个对象 |
| chr(x)                 | 将整数 x 转换为一个字符                            |
| ord(x)                 | 将一个字符 x 转换为它对应的整数值                  |
| hex(x)                 | 将一个整数 x 转换为一个十六进制字符串              |
| oct(x)                 | 将一个整数 x 转换为一个八进制的字符串              |

```python
>>> a = input('enter a number:')
enter a number:21
>>> int(a)
21
>>> float(a)
21.0
>>> bool(a)
True
```

input() 函数的用法为：

str = input(tipmsg)

说明：

- str 表示一个字符串类型的变量，input 会将读取到的字符串放入 str 中。
- tipmsg 表示提示信息，它会显示在控制台上，告诉用户应该输入什么样的内容；如果不写 tipmsg，就不会有任何提示信息。

print() 函数的详细语法格式如下：

print (value,...,sep='',end='\n',file=sys.stdout,flush=False)

- value, 输出变量，可以有多个

- sep 参数：变量与变量间的分隔符，默认是空格
- end : 输出结束后默认添加换行

```python
# 输出到文件
f = open("demo.txt","w")#打开文件以便写入
print('沧海月明珠有泪',file=f)
print('蓝回日暖玉生烟',file=f)
f.close()
```



## 

### 运算符

#### 算术运算符： 

| 运算符 | 说明                                | 实例        | 结果      |
| ------ | ----------------------------------- | ----------- | --------- |
| +      | 加                                  | 12.45 + 15  | 27.45     |
| -      | 减                                  | 4.56 - 0.26 | 4.3       |
| *      | 乘                                  | 5 * 3.6     | 18.0      |
| /      | 除法（和数学中的规则一样）          | 7 / 2       | 3.5       |
| //     | 整除（只保留商的整数部分）          | 7 // 2      | 3         |
| %      | 取余，即返回除法的余数              | 7 % 2       | 1         |
| **     | 幂运算/次方运算，即返回 x 的 y 次方 | 2 ** 4      | 16，即 24 |

3+2

  3-2

  3*2

  3/2

  3%2  取余 

  3//2  取整除-返回商的整数部分

  3**2 幂   3的二次方

#### 比较运算符：

| 比较运算符 | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| >          | 大于，如果`>`前面的值大于后面的值，则返回 True，否则返回 False。 |
| <          | 小于，如果`<`前面的值小于后面的值，则返回 True，否则返回 False。 |
| ==         | 等于，如果`==`两边的值相等，则返回 True，否则返回 False。    |
| >=         | 大于等于（等价于数学中的 ≥），如果`>=`前面的值大于或者等于后面的值，则返回 True，否则返回 False。 |
| <=         | 小于等于（等价于数学中的 ≤），如果`<=`前面的值小于或者等于后面的值，则返回 True，否则返回 False。 |
| !=         | 不等于（等价于数学中的 ≠），如果`!=`两边的值不相等，则返回 True，否则返回 False。 |
| is         | 判断两个变量所引用的对象是否相同，如果相同则返回 True，否则返回 False。 |
| is not     | 判断两个变量所引用的对象是否不相同，如果不相同则返回 True，否则返回 False。 |

a==b  是否相等

a!=b  , a<>b  不相等

<  ,  >  , >= , <=

#### 赋值运算符：

| 运算符 | 说 明            | 用法举例 | 等价形式                              |
| ------ | ---------------- | -------- | ------------------------------------- |
| =      | 最基本的赋值运算 | x = y    | x = y                                 |
| +=     | 加赋值           | x += y   | x = x + y                             |
| -=     | 减赋值           | x -= y   | x = x - y                             |
| *=     | 乘赋值           | x *= y   | x = x * y                             |
| /=     | 除赋值           | x /= y   | x = x / y                             |
| %=     | 取余数赋值       | x %= y   | x = x % y                             |
| **=    | 幂赋值           | x **= y  | x = x ** y                            |
| //=    | 取整数赋值       | x //= y  | x = x // y                            |
| &=     | 按位与赋值       | x &= y   | x = x & y                             |
| \|=    | 按位或赋值       | x \|= y  | x = x \| y                            |
| ^=     | 按位异或赋值     | x ^= y   | x = x ^ y                             |
| <<=    | 左移赋值         | x <<= y  | x = x << y，这里的 y 指的是左移的位数 |
| >>=    | 右移赋值         | x >>= y  | x = x >> y，这里的 y 指的是右移的位数 |

=, +=, -=,  *=,  /= , %=,  **=,  //=   

c//=a  等效于 c=c // a

赋值语句：

```
a, b = b, a + b
```

相当于：

```
t = (b, a + b) # t是一个tuple
a = t[0]
b = t[1]
```

#### 位运算符

| 位运算符 | 说明     | 使用形式 | 举 例                                       |
| -------- | -------- | -------- | ------------------------------------------- |
| &        | 按位与   | a & b    | 4 & 5                                       |
| \|       | 按位或   | a \| b   | 4 \| 5                                      |
| ^        | 按位异或 | a ^ b    | 4 ^ 5                                       |
| ~        | 按位取反 | ~a       | ~4                                          |
| <<       | 按位左移 | a << b   | 4 << 2，表示整数 4 按位左移 2 位,可以无限长 |
| >>       | 按位右移 | a >> b   | 4 >> 2，表示整数 4 按位右移 2 位            |

```python
# 位移
>>> 35 << 400
90378745733041800637957171020105415601539702749022822949073077478922666770589441812037587364804824100256611019046162268160
>>> 35 >> 40
0
```



#### 逻辑运算符：

| 逻辑运算符 | 含义                           | 基本格式 | 说明                                                         |
| ---------- | ------------------------------ | -------- | ------------------------------------------------------------ |
| and        | 逻辑与运算，等价于数学中的“且” | a and b  | 当 a 和 b 两个表达式都为真时，a and b 的结果才为真，否则为假。 |
| or         | 逻辑或运算，等价于数学中的“或” | a or b   | 当 a 和 b 两个表达式都为假时，a or b 的结果才是假，否则为真。 |
| not        | 逻辑非运算，等价于数学中的“非” | not a    | 如果 a 为真，那么 not a 的结果为假；如果 a 为假，那么 not a 的结果为真。相当于对 a 取反。 |

and, or, not, 

in   x在y序列中

not in    x不在y序列中

```python
>>> a=[1,2,3,45,6]
>>> 2 in a
True
>>> 4 in a
False
>>> 2 not in a
False
>>> 4 not in a
True
```

is   x与y是不是引用自一个对象

is not  

```python
>>> a=[1,]  
>>> b=[1] 
>>> a
[1]
>>> b
[1]
>>> a is b
False
>>> b = a
>>> a is b
True
>>> a is not b
False
```



#### 其它：

| 运算顺序是从右到左。                         |
| -------------------------------------------- |
| 支持链式运算：一个内存多个引用<br />a=b=c=30 |
| 支持系列解包赋值<br />a,b,c=20,30,40         |

#### 三目运算符:

max = a if a>b else b

**解释：一般max = a 但a>b时max=b**



Python 运算符优先级（从高到低排列）

| 运算符说明 | Python运算符            | 优先级 | 结合性 | 优先级顺序 |
| ---------- | ----------------------- | ------ | ------ | ---------- |
| 小括号     | ( )                     | 19     | 无     | 高         |
| 索引运算符 | x[i] 或 x[i1: i2 [:i3]] | 18     | 左     |            |
| 属性访问   | x.attribute             | 17     | 左     |            |
| 乘方       | **                      | 16     | 右     |            |
| 按位取反   | ~                       | 15     | 右     |            |
| 符号运算符 | +（正号）、-（负号）    | 14     | 右     |            |
| 乘除       | *、/、//、%             | 13     | 左     |            |
| 加减       | +、-                    | 12     | 左     |            |
| 位移       | >>、<<                  | 11     | 左     |            |
| 按位与     | &                       | 10     | 右     |            |
| 按位异或   | ^                       | 9      | 左     |            |
| 按位或     | \|                      | 8      | 左     |            |
| 比较运算符 | ==、!=、>、>=、<、<=    | 7      | 左     |            |
| is 运算符  | is、is not              | 6      | 左     |            |
| in 运算符  | in、not in              | 5      | 左     |            |
| 逻辑非     | not                     | 4      | 右     |            |
| 逻辑与     | and                     | 3      | 左     |            |
| 逻辑或     | or                      | 2      | 左     |            |
| 逗号运算符 | exp1, exp2              | 1      | 左     | 低         |



## 数据类型



### 对象

* python程序中所有数据都是对象。 

* 每个对象都有各自的标识号、类型和值。一个对象被创建后，它的 *标识号* 就绝不会改变；你可以将其理解为该对象在内存中的地址。 '[`is`](https://docs.python.org/zh-cn/3/reference/expressions.html#is)' 运算符可以比较两个对象的标识号是否相同；   在 CPython 中，`id(x)` 就是存放 `x` 的内存的地址。

* 在a = 1; b = 1` 之后，`a` 和 `b` 可能会也可能不会指向同一个值为一的对象，这取决于具体实现，但是在 `c = []; d = []` 之后，`c` 和 `d` 保证会指向两个不同、单独的新建空列表。(请注意 `c = d = []` 则是将同一个对象赋值给 `c` 和 `d`。)



#### 特殊属性

| 属性                                                         | 含意                                                         |      |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| `__doc__`                                                    | 该函数的文档字符串，没有则为 `None`；不会被子类继承。        | 可写 |
| [`__name__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#definition.__name__) | 该函数的名称。                                               | 可写 |
| [`__qualname__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#definition.__qualname__) | 该函数的 [qualified name](https://docs.python.org/zh-cn/3/glossary.html#term-qualified-name)。*3.3 新版功能.* | 可写 |
| `__module__`                                                 | 该函数所属模块的名称，没有则为 `None`。                      | 可写 |
| `__defaults__`                                               | 由具有默认值的参数的默认参数值组成的元组，如无任何参数具有默认值则为 `None`。 | 可写 |
| `__code__`                                                   | 表示编译后的函数体的代码对象。                               | 可写 |
| `__globals__`                                                | 对存放该函数中全局变量的字典的引用 --- 函数所属模块的全局命名空间。 | 只读 |
| [`__dict__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#object.__dict__) | 命名空间支持的函数属性字典。                                 | 可写 |
| `__closure__`                                                | `None` 或包含该函数可用变量的绑定的单元的元组。有关 `cell_contents` 属性的详情见下。 | 只读 |
| `__annotations__`                                            | 包含形参标注的字典。 字典的键是形参名，而如果提供了 `'return'` 则是用于返回值标注。 有关如何使用此属性的更多信息，请参阅 [对象注解属性的最佳实践](https://docs.python.org/zh-cn/3/howto/annotations.html#annotations-howto)。 | 可写 |
| `__kwdefaults__`                                             | 仅包含关键字参数默认值的字典。                               | 可写 |

#### 实例方法（对象中）：

特殊的只读属性: `__self__` 为类实例对象本身，`__func__` 为函数对象；`__doc__` 为方法的文档 (与 `__func__.__doc__` 作用相同)；[`__name__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#definition.__name__) 为方法名称 (与 `__func__.__name__` 作用相同)；`__module__` 为方法所属模块的名称，没有则为 `None`。



`object.__new__`(*cls*[, *...*])

调用以创建一个 *cls* 类的新实例。[`__new__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__new__) 是一个静态方法 (因为是特例所以你不需要显式地声明)，它会将所请求实例所属的类作为第一个参数。其余的参数会被传递给对象构造器表达式 (对类的调用)。[`__new__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__new__) 的返回值应为新对象实例 (通常是 *cls* 的实例)。

如果 [`__new__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__new__) 未返回一个 *cls* 的实例，则新实例的 [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__) 方法就不会被执行。

`object.``__init__`(*self*[, *...*])

在实例 (通过 [`__new__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__new__)) 被创建之后，返回调用者之前调用。其参数与传递给类构造器表达式的参数相同。

`object.``__del__`(*self*)

在实例将被销毁时调用。 这还被称为终结器或析构器（不适当）。 

当解释器退出时不会确保为仍然存在的对象调用 [`__del__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__del__) 方法。

**`del x` 并不直接调用 `x.__del__()` --- 前者会将 `x` 的引用计数减一，而后者仅会在 `x` 的引用计数变为零时被调用。**

`object.``__lt__`(*self*, *other*)      

`object.``__le__`(*self*, *other*)

`object.``__eq__`(*self*, *other*)

`object.``__ne__`(*self*, *other*)

`object.``__gt__`(*self*, *other*)

`object.``__ge__`(*self*, *other*)

以上这些被称为“富比较”方法。运算符号与方法名称的对应关系如下：`x<y` 调用 `x.__lt__(y)`、`x<=y` 调用 `x.__le__(y)`、`x==y` 调用 `x.__eq__(y)`、`x!=y` 调用 `x.__ne__(y)`、`x>y` 调用 `x.__gt__(y)`、`x>=y` 调用 `x.__ge__(y)`。

如果指定的参数对没有相应的实现，富比较方法可能会返回单例对象 `NotImplemented`。按照惯例，成功的比较会返回 `False` 或 `True`。不过实际上这些方法可以返回任意值，因此如果比较运算符是要用于布尔值判断（例如作为 `if` 语句的条件），Python 会对返回值调用 [`bool()`](https://docs.python.org/zh-cn/3/library/functions.html#bool) 以确定结果为真还是假。

在默认情况下，`object` 通过使用 `is` 来实现 [`__eq__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__eq__)，并在比较结果为假值时返回 `NotImplemented`: `True if x is y else NotImplemented`。 对于 [`__ne__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__ne__)，默认会委托给 [`__eq__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__eq__) 并对结果取反，除非结果为 `NotImplemented`。 比较运算符之间没有其他隐含关系或默认实现；例如，`(x<y or x==y)` 为真并不意味着 `x<=y`。 要根据单根运算自动生成排序操作，请参看 [`functools.total_ordering()`](https://docs.python.org/zh-cn/3/library/functools.html#functools.total_ordering)。

#### 可以定义下列方法来自定义对类实例属性访问（`x.name` 的使用、赋值或删除）的具体含义.

- `object.``__getattr__`(*self*, *name*)

  当默认属性访问因引发 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError) 而失败时被调用 (可能是调用 [`__getattribute__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattribute__) 时由于 *name* 不是一个实例属性或 `self` 的类关系树中的属性而引发了 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError)；或者是对 *name* 特性属性调用 [`__get__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__get__) 时引发了 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError))。此方法应当返回（找到的）属性值或是引发一个 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError) 异常。请注意如果属性是通过正常机制找到的，[`__getattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattr__) 就不会被调用。（这是在 [`__getattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattr__) 和 [`__setattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__setattr__) 之间故意设置的不对称性。）这既是出于效率理由也是因为不这样设置的话 [`__getattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattr__) 将无法访问实例的其他属性。要注意至少对于实例变量来说，你不必在实例属性字典中插入任何值（而是通过插入到其他对象）就可以模拟对它的完全控制。请参阅下面的 [`__getattribute__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattribute__) 方法了解真正获取对属性访问的完全控制权的办法。

- `object.``__getattribute__`(*self*, *name*)

  此方法会无条件地被调用以实现对类实例属性的访问。如果类还定义了 [`__getattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattr__)，则后者不会被调用，除非 [`__getattribute__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__getattribute__) 显式地调用它或是引发了 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError)。此方法应当返回（找到的）属性值或是引发一个 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError) 异常。为了避免此方法中的无限递归，其实现应该总是调用具有相同名称的基类方法来访问它所需要的任何属性，例如 `object.__getattribute__(self, name)`。注解 此方法在作为通过特定语法或内置函数隐式地调用的结果的情况下查找特殊方法时仍可能会被跳过。参见 [特殊方法查找](https://docs.python.org/zh-cn/3/reference/datamodel.html#special-lookup)。引发一个 [审计事件](https://docs.python.org/zh-cn/3/library/sys.html#auditing) `object.__getattr__`，附带参数 `obj`, `name`。

- `object.``__setattr__`(*self*, *name*, *value*)

  此方法在一个属性被尝试赋值时被调用。这个调用会取代正常机制（即将值保存到实例字典）。 *name* 为属性名称， *value* 为要赋给属性的值。如果 [`__setattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__setattr__) 想要赋值给一个实例属性，它应该调用同名的基类方法，例如 `object.__setattr__(self, name, value)`。引发一个 [审计事件](https://docs.python.org/zh-cn/3/library/sys.html#auditing) `object.__setattr__`，附带参数 `obj`, `name`, `value`。

- `object.``__delattr__`(*self*, *name*)

  类似于 [`__setattr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__setattr__) 但其作用为删除而非赋值。此方法应该仅在 `del obj.name` 对于该对象有意义时才被实现。引发一个 [审计事件](https://docs.python.org/zh-cn/3/library/sys.html#auditing) `object.__delattr__`，附带参数 `obj`, `name`。

- `object.``__dir__`(*self*)

  此方法会在对相应对象调用 [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir) 时被调用。返回值必须为一个序列。 [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir) 会把返回的序列转换为列表并对其排序。



#### 运算符优先级

| 运算符                                                       | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| `(expressions...)`,`[expressions...]`, `{key: value...}`, `{expressions...}` | 绑定或加圆括号的表达式，列表显示，字典显示，集合显示         |
| `x[index]`, `x[index:index]`, `x(arguments...)`, `x.attribute` | 抽取，切片，调用，属性引用                                   |
| [`await x`](https://docs.python.org/zh-cn/3/reference/expressions.html#await) | await 表达式                                                 |
| `**`                                                         | 乘方 [[5\]](https://docs.python.org/zh-cn/3/reference/expressions.html#footnote-5) |
| `+x`, `-x`, `~x`                                             | 正，负，按位非 NOT                                           |
| `*`, `@`, `/`, `//`, `%`                                     | 乘，矩阵乘，除，整除，取余 [[6\]](https://docs.python.org/zh-cn/3/reference/expressions.html#footnote-6) |
| `+`, `-`                                                     | 加和减                                                       |
| `<<`, `>>`                                                   | 移位                                                         |
| `&`                                                          | 按位与 AND                                                   |
| `^`                                                          | 按位异或 XOR                                                 |
| `|`                                                          | 按位或 OR                                                    |
| [`in`](https://docs.python.org/zh-cn/3/reference/expressions.html#in), [`not in`](https://docs.python.org/zh-cn/3/reference/expressions.html#not-in), [`is`](https://docs.python.org/zh-cn/3/reference/expressions.html#is), [`is not`](https://docs.python.org/zh-cn/3/reference/expressions.html#is-not), `<`, `<=`, `>`, `>=`, `!=`, `==` | 比较运算，包括成员检测和标识号检测                           |
| [`not x`](https://docs.python.org/zh-cn/3/reference/expressions.html#not) | 布尔逻辑非 NOT                                               |
| [`and`](https://docs.python.org/zh-cn/3/reference/expressions.html#and) | 布尔逻辑与 AND                                               |
| [`or`](https://docs.python.org/zh-cn/3/reference/expressions.html#or) | 布尔逻辑或 OR                                                |
| [`if`](https://docs.python.org/zh-cn/3/reference/expressions.html#if-expr) -- `else` | 条件表达式                                                   |
| [`lambda`](https://docs.python.org/zh-cn/3/reference/expressions.html#lambda) | lambda 表达式                                                |
| `:=`                                                         | 赋值表达式                                                   |



## 文件、目录系统

### os

```python
os.getcwd()
返回当前工作目录
os.chdir(path)
改变当前工作目录
os.listdir(path)
返回path指定的文件夹包含的文件或文件夹的名字的列表。
os.makedirs(path[, mode])
os.mkdir() 方法用于以数字权限模式创建目录（单级目录）。默认的模式为 0777 (八进制)。
递归文件夹创建函数。像mkdir(), 但创建的所有intermediate-level文件夹需要包含子文件夹。
os.remove(path)
删除路径为path的文件。如果path 是一个文件夹，将抛出OSError; 查看下面的rmdir()删除一个 directory。
os.removedirs(path)
递归删除目录。
os.rename(src, dst)
重命名文件或目录，从 src 到 dst
os.renames(old, new)
递归地对目录进行更名，也可以对文件进行更名。
os.rmdir(path)
删除path指定的空目录，如果目录非空，则抛出一个OSError异常。
```



### os.path --常用路径字符串操作

```python
import os
>>> 
>>> # 返回路径 path 的绝对路径（标准化的）。在大多数平台上，这等同于用 normpath(join(os.getcwd(), path)) 的方式调用 normpath() 函数。
>>> os.path.abspath('.')
'E:\\cod\\python\\helpsk\\app'
>>> 
>>> # 返回路径 path 的基本名称。这是将 path 传入函数 split() 之后，返回的一对值中的第二个元素。
>>> path = os.getcwd()
>>> path
'E:\\cod\\python\\helpsk\\app'    
>>> os.path.basename(path)        
'app'
>>> # 返回路径 path 的目录名称。这是将 path 传入函数 split() 之后，返回的一对值中的第一个元素。
>>> os.path.dirname(path)
'E:\\cod\\python\\helpsk'
>>> 
>>> # 接受包含多个路径的序列 paths，返回 paths 的最长公共子路径。
>>> a = ["c:/abc/vv/tt", "c:/abc/vv/tab", "c:/abc/tt/ab"]
>>> os.path.commonpath(a)
'c:\\abc'
>>>
>>> # 接受包含多个路径的 列表，返回所有路径的最长公共前缀（逐字符比较）。如果 列表 为空，则返回空字符串 ('')。
>>> a = ['/usr/lib', '/usr/local/lib']
>>> os.path.commonprefix(a)
'/usr/l'
>>>
>>> # 如果 path 指向一个已存在的路径或已打开的文件描述符，返回 True。path可以是绝对或相对目录
>>> os.path.exists(path)
True
>>>
>>> # 等同exists(path)
>>> os.path.lexists(path)
True
>>>
>>> # 参数开头的~ 或 ~user 替换为当前 用户 的家目录并返回。
>>> os.path.expanduser('~/abc/aa')
'C:\\Users\\Administrator/abc/aa'
>>>
>>> # 支持$name 或 ${name} 或 %name% 形式环境变量解析 
>>> os.path.expandvars('${windir}/abc')
'C:\\Windows/abc'
>>> os.path.expandvars('$windir/abc')
'C:\\Windows/abc'
>>> os.path.expandvars('%windir%/abc')
'C:\\Windows/abc'
>>> os.path.getatime(path)
1659756499.1863968
>>> # 返回 path 的最后访问时间。返回值是一个浮点数，为纪元秒数
>>> 
>>> os.path.getmtime(path)
1659684111.0016234
>>> # 返回 path 的最后修改时间。返回值是一个浮点数，为纪元秒数
>>>
>>> os.path.getctime(path)
1658482691.7000782
>>> # 返回 path 在系统中的 ctime，在有些系统（比如 Unix）上，它是元数据的最后修改时间，其他系统（比如 Windows）上，它是 path 的创建时间。返回值是一个数，为纪元秒数（参见 time 模块）。
>>>
>>> os.path.getsize(path)
4096
>>> # 返回 path 的大小，以字节为单位。
>>>
>>> os.path.isabs(path)
True
>>> os.path.isabs("\\abc")
True
>>> os.path.isabs("/abc")
True
>>> # path 是一个绝对路径,可以/\开头。
>>>
>>> os.path.isfile(path)
False
>>> # path是现有的 常规文件，则返回 True。
>>>
>>> os.path.isdir(path)
True
>>> # path 是现有的目录，则返回 True。
>>> 
>>> os.path.islink(path)
False
>>> # 如果 path 指向的 现有 目录条目是一个符号链接，则返回 True。
>>>
>>> os.path.ismount(path)
False
>>> # 如果路径 path 是 挂载点 （文件系统中挂载其他文件系统的点.
>>>
>>> os.path.join("c:/abc","/aaa",'ccc')
'c:/aaa\\ccc'
>>> os.path.join("c:/abc","aaa",'ccc')
'c:/abc\\aaa\\ccc'
>>> os.path.join("c:/abc","e:/aaa",'ccc')
'e:/aaa\\ccc'
>>> # os.path.join(path, *paths)
>>> # 智能地拼接一个或多个路径部分。 返回值是 path 和 *paths 的所有成员的拼接，其中每个非空部分后面都紧跟一个目录分隔符，最后一个部分除外，这意味着如果最后一个部分为空，则结果将以分隔符结尾。 如果某个部分为绝对路径，则之前的所有部分会被丢弃并从绝对路径部分开始继续拼接。
>>> # 在 Windows 上，遇到绝对路径部分（例如 r'\foo'）时，不会重置盘符。如果某部分路径包含盘符，则会丢弃所有先前的部分，并重置盘符。请注意，由于每个驱动器都有一个“当前目录”，所以 os.path.join("c:", "foo") 表示驱动器 C: 上当前目录的相对路径 (c:foo)，而不是 c:\foo。
>>>
>>> os.path.normcase("c:/abc/ABC")
'c:\\abc\\abc'
>>> # 规范路径的大小写。在 Windows 上，将路径中的所有字符都转换为小写，并将正斜杠转换为反斜杠。在其他操作系统上返回原路径。
>>>
>>> os.path.normpath('A//B')
'A\\B'
>>> os.path.normpath('A/B/')
'A\\B'
>>> os.path.normpath('A/./B')
'A\\B'
>>> os.path.normpath('A/foo/../B')
'A\\B'
>>> # 通过折叠多余的分隔符和对上级目录的引用来标准化路径名，所以 A//B、A/B/、A/./B 和 A/foo/../B 都会转换成 A/B。这个字符串操作可能会改变带有符号链接的路径的含义。在 Windows 上，本方法将正斜杠转换为反斜杠。要规范大小写，请使用 normcase()。
>>>
>>> # os.path.realpath(path, *, strict=False)
>>> # 返回指定文件的规范路径，消除路径中存在的任何符号链接（如果操作系统支持）。
>>> #如果一个路径不存在或是遇到了符号链接循环，并且 strict 为 True，则会引发 OSError。 如果 strict 为 False，则会尽可能地解析路径并添加结果而不检查路径是否存在。
>>>
>>> os.path.relpath(path, start=os.curdir)
'.'
>>> # 返回从当前目录或可选的 start 目录至 path 的相对文件路径。 这只是一个路径计算：不会访问文件系统来确认 path 或 start 是否存在或其性质。 在 Windows 上，当 path 和 start 位于不同驱动器时将引发 ValueError。
>>>
>>> os.path.samefile(path1, path2)
>>> # 如果两个路径都指向相同的文件或目录，则返回 True。
>>>
>>> os.path.sameopenfile(fp1, fp2)
>>> # 如果文件描述符 fp1 和 fp2 指向相同文件，则返回 True。
>>>
>>> os.path.samestat(stat1, stat2)
>>> # 如果 stat 元组 stat1 和 stat2 指向相同文件，则返回 True。这些 stat 元组可能是由 os.fstat()、os.lstat() 或 os.stat() 返回的。本函数实现了 samefile() 和 sameopenfile() 底层所使用的比较过程。
>>>
>>> os.path.split(path)
('E:\\cod\\python\\helpsk', 'app')
>>> # 将路径 path 拆分为一对，即 (head, tail)，其中，tail 是路径的最后一部分，而 head 里是除最后部分外的所有内容。tail 部分不会包含斜杠，如果 path 以斜杠结尾，则 tail 将为空。如果 path 中没有斜杠，head 将为空。如果 path 为空，则 head 和 tail 均为空。head 末尾的斜杠会被去掉，除非它是根目录（即它仅包含一个或多个斜杠）。在所有情况下，join(head, tail) 指向的位置都与 path 相同（但字符串可能不同）。另请参见函数 dirname() 和 basename()。
>>>
>>> os.path.splitdrive(path)
('E:', '\\cod\\python\\helpsk\\app')
>>> #将路径 path 拆分为一对，即 (drive, tail)，其中 drive 是挂载点或空字符串。在没有驱动器概念的系统上，drive 将始终为空字符串。在所有情况下，drive + tail 都与 path 相同。
>>> #在 Windows 上，本方法将路径拆分为驱动器/UNC 根节点和相对路径。
>>> #如果路径 path 包含盘符，则 drive 将包含冒号之前的所有内容包括冒号本身:
>>>
>>> os.path.splitext(path)
('E:\\cod\\python\\helpsk\\app', '')
>>> #将路径名称 path 拆分为 (root, ext) 对使得 root + ext == path，并且扩展名 ext 为空或以句点打头并最多只包含一个句点。
```

### [`shutil`](https://docs.python.org/zh-cn/3/library/shutil.html#module-shutil) --- 高阶文件操作

[`shutil`](https://docs.python.org/zh-cn/3/library/shutil.html#module-shutil) 模块提供了一系列对文件和文件集合的高阶操作。 特别是提供了一些支持文件拷贝和删除的函数。 对于单个文件的操作，请参阅 [`os`](https://docs.python.org/zh-cn/3/library/os.html#module-os) 模块。

* shutil.`copyfileobj(*fsrc*, *fdst*[, *length*])

将文件类对象 *fsrc* 的内容拷贝到文件类对象 *fdst*。 整数值 *length* 如果给出则为缓冲区大小。 特别地， *length* 为负值表示拷贝数据时不对源数据进行分块循环处理；默认情况下会分块读取数据以避免不受控制的内存消耗。 请注意如果 *fsrc* 对象的当前文件位置不为 0，则只有从当前文件位置到文件末尾的内容会被拷贝。

* shutil.``copyfile`(*src*, *dst*, ***, *follow_symlinks=True*)

将名为 *src* 的文件的内容（不包括元数据）拷贝到名为 *dst* 的文件并以尽可能高效的方式返回 *dst*。 *src* 和 *dst* 均为路径类对象或以字符串形式给出的路径名。*dst* 必须是完整的目标文件名；对于接受目标目录路径的拷贝请参见 [`copy()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copy)。 如果 *src* 和 *dst* 指定了同一个文件，则将引发 [`SameFileError`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.SameFileError)

+ `hutil.``copymode`(*src*, *dst*, ***, *follow_symlinks=True*)

从 *src* 拷贝权限位到 *dst*。 文件的内容、所有者和分组将不受影响。 *src* 和 *dst* 均为路径类对象或字符串形式的路径名。 如果 *follow_symlinks* 为假值，并且 *src* 和 *dst* 均为符号链接，[`copymode()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copymode) 将尝试修改 *dst* 本身的模式（而非它所指向的文件）。 此功能并不是在所有平台上均可用；请参阅 [`copystat()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copystat) 了解详情。 如果 [`copymode()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copymode) 无法修改本机平台上的符号链接，而它被要求这样做，它将不做任何操作即返回。引发一个 [审计事件](https://docs.python.org/zh-cn/3/library/sys.html#auditing) `shutil.copymode` 附带参数 `src`, `dst`。*在 3.3 版更改:* 加入 *follow_symlinks* 参数。

- `shutil.``copystat`(*src*, *dst*, ***, *follow_symlinks=True*)

  从 *src* 拷贝权限位、最近访问时间、最近修改时间以及旗标到 *dst*。 在 Linux上，[`copystat()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copystat) 还会在可能的情况下拷贝“扩展属性”。 文件的内容、所有者和分组将不受影响。 *src* 和 *dst* 均为路径类对象或字符串形式的路径名。

* `shutil.``copy`(*src*, *dst*, ***, *follow_symlinks=True*)

将文件 *src* 拷贝到文件或目录 *dst*。 *src* 和 *dst* 应为 [路径类对象](https://docs.python.org/zh-cn/3/glossary.html#term-path-like-object) 或字符串。 如果 *dst* 指定了一个目录，文件将使用 *src* 中的基准文件名拷贝到 *dst* 中。 如果 *dst* 指定了一个已存在的文件，它将被替换。 返回新创建文件所对应的路径。

* `shutil.``copy2`(*src*, *dst*, ***, *follow_symlinks=True*)

类似于 [`copy()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copy)，区别在于 [`copy2()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copy2) 还会尝试保留文件的元数据。

* `shutil.``copytree`(*src*, *dst*, *symlinks=False*, *ignore=None*, *copy_function=copy2*, *ignore_dangling_symlinks=False*, *dirs_exist_ok=False*)

递归地将以 *src* 为根起点的整个目录树拷贝到名为 *dst* 的目录并返回目标目录。 所需的包含 *dst* 的中间目录在默认情况下也将被创建。目录的权限和时间会通过 [`copystat()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copystat) 来拷贝，单个文件则会使用 [`copy2()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.copy2) 来拷贝。

* `shutil.``rmtree`(*path*, *ignore_errors=False*, *onerror=None*)

删除一个完整的目录树；*path* 必须指向一个目录（但不能是一个目录的符号链接）。 

* `shutil.``move`(*src*, *dst*, *copy_function=copy2*)

递归地将一个文件或目录 (*src*) 移至另一位置 (*dst*) 并返回目标位置。

* `shutil.``disk_usage`(*path*)

返回给定路径的磁盘使用统计数据，形式为一个 [named tuple](https://docs.python.org/zh-cn/3/glossary.html#term-named-tuple)，其中包含 *total*, *used* 和 *free* 属性，分别表示总计、已使用和未使用空间的字节数。 *path* 可以是一个文件或是一个目录。

*在 3.8 版更改:* 在 Windows 上，*path* 现在可以是一个文件或目录。

`shutil.``which`(*cmd*, *mode=os.F_OK | os.X_OK*, *path=None*)

返回当给定的 *cmd* 被调用时将要运行的可执行文件的路径。 如果没有 *cmd* 会被调用则返回 `None`。

```python
>>> shutil.which("python")
'C:\\Python33\\python.EXE'
```

#### copytree 示例

一个使用 [`ignore_patterns()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.ignore_patterns) 辅助函数的例子:

```
from shutil import copytree, ignore_patterns

copytree(source, destination, ignore=ignore_patterns('*.pyc', 'tmp*'))
```

这将会拷贝除 `.pyc` 文件和以 `tmp` 打头的文件或目录以外的所有条目.

另一个使用 *ignore* 参数来添加记录调用的例子:

```
from shutil import copytree
import logging

def _logpath(path, names):
    logging.info('Working in %s', path)
    return []   # nothing will be ignored

copytree(source, destination, ignore=_logpath)
```



#### rmtree 示例

这个例子演示了如何在 Windows 上删除一个目录树，其中部分文件设置了只读属性位。 它会使用 onerror 回调函数来清除只读属性位并再次尝试删除。 任何后续的失败都将被传播。

```
import os, stat
import shutil

def remove_readonly(func, path, _):
    "Clear the readonly bit and reattempt the removal"
    os.chmod(path, stat.S_IWRITE)
    func(path)

shutil.rmtree(directory, onerror=remove_readonly)
```

* `shutil.``make_archive`(*base_name*, *format*[, *root_dir*[, *base_dir*[, *verbose*[, *dry_run*[, *owner*[, *group*[, *logger*]]]]]]])

创建一个归档文件（例如 zip 或 tar）并返回其名称。

*base_name* 是要创建的文件名称，包括路径，去除任何特定格式的扩展名。 *format* 是归档格式：为 "zip" (如果 [`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib) 模块可用), "tar", "gztar" (如果 [`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib) 模块可用), "bztar" (如果 [`bz2`](https://docs.python.org/zh-cn/3/library/bz2.html#module-bz2) 模块可用) 或 "xztar" (如果 [`lzma`](https://docs.python.org/zh-cn/3/library/lzma.html#module-lzma) 模块可用) 中的一个。

*root_dir* 是一个目录，它将作为归档文件的根目录，归档中的所有路径都将是它的相对路径；例如，我们通常会在创建归档之前用 chdir 命令切换到 *root_dir*。

*base_dir* 是我们要执行归档的起始目录；也就是说 *base_dir* 将成为归档中所有文件和目录共有的路径前缀。 *base_dir* 必须相对于 *root_dir* 给出。 请参阅 [使用 base_dir 的归档程序示例](https://docs.python.org/zh-cn/3/library/shutil.html#shutil-archiving-example-with-basedir) 了解如何同时使用 *base_dir* 和 *root_dir*。

*root_dir* 和 *base_dir* 默认均为当前目录。

* `shutil.``get_archive_formats`()

返回支持的归档格式列表。 所返回序列中的每个元素为一个元组 `(name, description)`。

默认情况下 [`shutil`](https://docs.python.org/zh-cn/3/library/shutil.html#module-shutil) 提供以下格式:

- *zip*: ZIP 文件（如果 [`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib) 模块可用）。
- *tar*: 未压缩的 tar 文件。 对于新归档文件将使用 POSIX.1-2001 pax 格式。
- *gztar*: gzip 压缩的 tar 文件（如果 [`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib) 模块可用）。
- *bztar*: bzip2 压缩的 tar 文件（如果 [`bz2`](https://docs.python.org/zh-cn/3/library/bz2.html#module-bz2) 模块可用）。
- *xztar*: xz 压缩的 tar 文件（如果 [`lzma`](https://docs.python.org/zh-cn/3/library/lzma.html#module-lzma) 模块可用）。

* `shutil.``unpack_archive`(*filename*[, *extract_dir*[, *format*]])

解包一个归档文件。 *filename* 是归档文件的完整路径。

*extract_dir* 是归档文件解包的目标目录名称。 如果未提供，则将使用当前工作目录。

* `shutil.``get_unpack_formats`()

返回所有已注册的解包格式列表。 所返回序列中的每个元素为一个元组 `(name, extensions, description)`。

默认情况下 [`shutil`](https://docs.python.org/zh-cn/3/library/shutil.html#module-shutil) 提供以下格式:

- *zip*: ZIP 文件（只有在相应模块可用时才能解包压缩文件）。
- *tar*: 未压缩的 tar 文件。
- *gztar*: gzip 压缩的 tar 文件（如果 [`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib) 模块可用）。
- *bztar*: bzip2 压缩的 tar 文件（如果 [`bz2`](https://docs.python.org/zh-cn/3/library/bz2.html#module-bz2) 模块可用）。
- *xztar*: xz 压缩的 tar 文件（如果 [`lzma`](https://docs.python.org/zh-cn/3/library/lzma.html#module-lzma) 模块可用）。

#### 归档程序示例

```
>>> from shutil import make_archive
>>> import os
>>> archive_name = os.path.expanduser(os.path.join('~', 'myarchive'))
>>> root_dir = os.path.expanduser(os.path.join('~', '.ssh'))
>>> make_archive(archive_name, 'gztar', root_dir)
'/Users/tarek/myarchive.tar.gz'
```

结果归档文件中包含有:

```
$ tar -tzvf /Users/tarek/myarchive.tar.gz
drwx------ tarek/staff       0 2010-02-01 16:23:40 ./
-rw-r--r-- tarek/staff     609 2008-06-09 13:26:54 ./authorized_keys
-rwxr-xr-x tarek/staff      65 2008-06-09 13:26:54 ./config
-rwx------ tarek/staff     668 2008-06-09 13:26:54 ./id_dsa
-rwxr-xr-x tarek/staff     609 2008-06-09 13:26:54 ./id_dsa.pub
-rw------- tarek/staff    1675 2008-06-09 13:26:54 ./id_rsa
-rw-r--r-- tarek/staff     397 2008-06-09 13:26:54 ./id_rsa.pub
-rw-r--r-- tarek/staff   37192 2010-02-06 18:23:10 ./known_hosts
```



#### 使用 *base_dir* 的归档程序示例

在这个例子中，与 [上面的例子](https://docs.python.org/zh-cn/3/library/shutil.html#shutil-archiving-example) 类似，我们演示了如何使用 [`make_archive()`](https://docs.python.org/zh-cn/3/library/shutil.html#shutil.make_archive)，但这次是使用 *base_dir*。 我们现在具有如下的目录结构:

```
$ tree tmp
tmp
└── root
    └── structure
        ├── content
            └── please_add.txt
        └── do_not_add.txt
```

在最终的归档中，应当会包括 `please_add.txt`，但不应当包括 `do_not_add.txt`。 因此我们使用以下代码:

\>>>

```
>>> from shutil import make_archive
>>> import os
>>> archive_name = os.path.expanduser(os.path.join('~', 'myarchive'))
>>> make_archive(
...     archive_name,
...     'tar',
...     root_dir='tmp/root',
...     base_dir='structure/content',
... )
'/Users/tarek/my_archive.tar'
```

列出结果归档中的文件我们将会得到:

```
$ python -m tarfile -l /Users/tarek/myarchive.tar
structure/content/
structure/content/please_add.txt
```



### pathlib 面向对象的文件系统路径

#### 基础使用

导入主类:

\>>>

```
>>> from pathlib import Path
```

列出子目录:

\>>>

```
>>> p = Path('.')
>>> [x for x in p.iterdir() if x.is_dir()]
[PosixPath('.hg'), PosixPath('docs'), PosixPath('dist'),
 PosixPath('__pycache__'), PosixPath('build')]
```

列出当前目录树下的所有 Python 源代码文件:

\>>>

```
>>> list(p.glob('**/*.py'))
[PosixPath('test_pathlib.py'), PosixPath('setup.py'),
 PosixPath('pathlib.py'), PosixPath('docs/conf.py'),
 PosixPath('build/lib/pathlib.py')]
```

在目录树中移动:

\>>>

```
>>> p = Path('/etc')
>>> q = p / 'init.d' / 'reboot'
>>> q
PosixPath('/etc/init.d/reboot')
>>> q.resolve()
PosixPath('/etc/rc.d/init.d/halt')
```

查询路径的属性:

\>>>

```
>>> q.exists()
True
>>> q.is_dir()
False
```

打开一个文件:

\>>>

```
>>> with q.open() as f: f.readline()
...
'#!/bin/bash\n'
```

详细介绍：

https://docs.python.org/zh-cn/3/library/pathlib.html#pathlib.Path.rmdir







## io --流处理

文本I/O预期并生成 [`str`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str) 对象。这意味着，无论何时后台存储是由字节组成的（例如在文件的情况下），数据的编码和解码都是透明的，并且可以选择转换特定于平台的换行符。

```python
# 文件流
f = open("myfile.txt", "r", encoding="utf-8")
# 可读可写
f = open("myfile.txt", "r+", encoding="utf-8")

# 内存文本流
f = io.StringIO("some initial text data")

# 二进制流
f = open("myfile.jpg", "rb")

#内存二进制流
f = io.BytesIO(b"some initial binary data: \x00\x01")
```



mode参数 可以为 `'r'`, `'w'`, `'x'` 或 `'a'` 分别表示读取（默认模式）、写入、新建或添加。

 如果以w或a打开的文件不存在将自动新建；当以w打开时文件将先清空。

 以x模式打开时如果文件已存在则将引发 FileExistsError。 以x模式打开文件也意味着要写入，因此该模式的行为与 `'w'` 类似。

 在模式中附带 `'+'` 将允许同时读取和写入。

在模式后面加上一个 `'b'` 以二进制方式读写。



建议处理文件对象时使用with关键字，  优点是，子句体结束后，文件会正确关闭，即便触发异常也可以。而且，使用 `with` 相比等效的 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)-[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 代码块要简短得多：

```python
>>> with open('workfile', encoding="utf-8") as f:
...     read_data = f.read()

>>> # We can check that the file has been automatically closed.
>>> f.closed
True
```

`f.read(size)` 可用于读取文件内容，它会读取一些数据，并返回字符串（文本模式），或字节串对象（在二进制模式下）。 *size* 是可选的数值参数。省略 *size* 或 *size* 为负数时，读取并返回整个文件的内容；文件大小是内存的两倍时，会出现问题。*size* 取其他值时，读取并返回最多 *size* 个字符（文本模式）或 *size* 个字节（二进制模式）。如已到达文件末尾，`f.read()` 返回空字符串（`''`）。

\>>>

```
>>> f.read()
'This is the entire file.\n'
>>> f.read()
''
```

`f.readline()` 从文件中读取单行数据；字符串末尾保留换行符（`\n`），只有在文件不以换行符结尾时，文件的最后一行才会省略换行符。这种方式让返回值清晰明确；只要 `f.readline()` 返回空字符串，就表示已经到达了文件末尾，空行使用 `'\n'` 表示，该字符串只包含一个换行符。

\>>>

```
>>> f.readline()
'This is the first line of the file.\n'
>>> f.readline()
'Second line of the file\n'
>>> f.readline()
''
```

从文件中读取多行时，可以用循环遍历整个文件对象。这种操作能高效利用内存，快速，且代码简单：

\>>>

```
>>> for line in f:
...     print(line, end='')
...
This is the first line of the file.
Second line of the file
```

如需以列表形式读取文件中的所有行，可以用 `list(f)` 或 `f.readlines()`。

`f.write(string)` 把 *string* 的内容写入文件，并返回写入的字符数。

`f.write(string)` 把 *string* 的内容写入文件，并返回写入的字符数。

\>>>

```
>>> f.write('This is a test\n')
15
```

写入其他类型的对象前，要先把它们转化为字符串（文本模式）或字节对象（二进制模式）：

\>>>

```
>>> value = ('the answer', 42)
>>> s = str(value)  # convert the tuple to string
>>> f.write(s)
18
```

`f.tell()` 返回整数，给出文件对象在文件中的当前位置，表示为二进制模式下时从文件开始的字节数，以及文本模式下的意义不明的数字。

`f.seek(offset, whence)` 可以改变文件对象的位置。通过向参考点添加 *offset* 计算位置；参考点由 *whence* 参数指定。 *whence* 值为 0 时，表示从文件开头计算，1 表示使用当前文件位置，2 表示使用文件末尾作为参考点。省略 *whence* 时，其默认值为 0，即使用文件开头作为参考点。

\>>>

```
>>> f = open('workfile', 'rb+')
>>> f.write(b'0123456789abcdef')
16
>>> f.seek(5)      # Go to the 6th byte in the file
5
>>> f.read(1)
b'5'
>>> f.seek(-3, 2)  # Go to the 3rd byte before the end
13
>>> f.read(1)
b'd'
```

在文本文件（模式字符串未使用 `b` 时打开的文件）中，只允许相对于文件开头搜索（使用 `seek(0, 2)` 搜索到文件末尾是个例外），唯一有效的 *offset* 值是能从 `f.tell()` 中返回的，或 0。其他 *offset* 值都会产生未定义的行为。

文件对象还支持 `isatty()` 和 `truncate()` 等方法，但不常用；文件对象的完整指南详见库参考。



#### IOBase常用操作：

- `close`()

  刷新并关闭此流。如果文件已经关闭

- `closed`

  如果流已关闭，则返回 True。

- `fileno`()

  返回流的底层文件描述符（整数）

- `flush`()

  刷新流的写入缓冲区（如果适用）。这对只读和非阻塞流不起作用。

- `isatty`()

  如果流是交互式的（即连接到终端/tty设备），则返回 `True` 。

- `readable`()

  如果可以读取流，则返回 `True` 。否则为 `False` ，且 `read()` 将引发 [`OSError`](https://docs.python.org/zh-cn/3/library/exceptions.html#OSError) 错误。

- `readline`(*size=- 1*, */*)

  从流中读取并返回一行。如果指定了 *size*，将至多读取 *size* 个字节。对于二进制文件行结束符总是 `b'\n'`；对于文本文件，可以用将 *newline* 参数传给 [`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open) 的方式来选择要识别的行结束符。

- `readlines`(*hint=- 1*, */*)

  从流中读取并返回包含多行的列表。可以指定 *hint* 来控制要读取的行数：如果（以字节/字符数表示的）所有行的总大小超出了 *hint* 则将不会读取更多的行。`0` 或更小的 *hint* 值以及 `None`，会被视为没有 hint。请注意使用 `for line in file: ...` 就足够对文件对象进行迭代了，可以不必调用 `file.readlines()`。

- `seek`(*offset*, *whence=SEEK_SET*, */*)

  将流位置修改到给定的字节 *offset*。 *offset* 将相对于由 *whence* 指定的位置进行解析。 *whence* 的默认值为 `SEEK_SET`。 *whence* 的可用值有：`SEEK_SET` 或 `0` -- 流的开头（默认值）；*offset* 应为零或正值`SEEK_CUR` or `1` -- 当前流位置；*offset* 可以为负值`SEEK_END` or `2` -- 流的末尾；*offset* 通常为负值返回新的绝对位置。*3.1 新版功能:* `SEEK_*` 常量.*3.3 新版功能:* 某些操作系统还可支持其他的值，例如 `os.SEEK_HOLE` 或 `os.SEEK_DATA`。特定文件的可用值还会取决于它是以文本还是二进制模式打开。

- `seekable`()

  如果流支持随机访问则返回 `True`。 如为 `False`，则 [`seek()`](https://docs.python.org/zh-cn/3/library/io.html#io.IOBase.seek), [`tell()`](https://docs.python.org/zh-cn/3/library/io.html#io.IOBase.tell) 和 [`truncate()`](https://docs.python.org/zh-cn/3/library/io.html#io.IOBase.truncate) 将引发 [`OSError`](https://docs.python.org/zh-cn/3/library/exceptions.html#OSError)。

- `tell`()

  返回当前流的位置。

- `truncate`(*size=None*, */*)

  将流的大小调整为给定的 *size* 个字节（如果未指定 *size* 则调整至当前位置）。 当前的流位置不变。 这个调整操作可扩展或减小当前文件大小。 在扩展的情况下，新文件区域的内容取决于具体平台（在大多数系统上，额外的字节会填充为零）。 返回新的文件大小。*在 3.5 版更改:* 现在Windows在扩展时将文件填充为零。

- `writable`()

  如果流支持写入则返回 `True`。 如为 `False`，则 `write()` 和 [`truncate()`](https://docs.python.org/zh-cn/3/library/io.html#io.IOBase.truncate) 将引发 [`OSError`](https://docs.python.org/zh-cn/3/library/exceptions.html#OSError)。

- `writelines`(*lines*, */*)

  将行列表写入到流。 不会添加行分隔符，因此通常所提供的每一行都带有末尾行分隔符。





































## 字符串与编码

#### 编解码

内存中存的统一是unicode编码。

在网络上或磁盘上存的是字节流，需要编解码。

```python
>>> chr(88)
'X'
>>> ord('X')
88
>>> '\u4e2d\u6587'
'中文'
>>> x = 'ab中文c'
>>> x
'ab中文c'
>>> b = x.encode('utf-8')
>>> b
b'ab\xe4\xb8\xad\xe6\x96\x87c'
>>> y = b.decode('utf-8')
>>> y
'ab中文c'
>>> x.encode('unicode')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
LookupError: unknown encoding: unicode
# ansi是指采用操作系统所用编码，简体中文中用的是gbk        
>>> x.encode('ansi')
b'ab\xd6\xd0\xce\xc4c'
>>> y = x.encode('ansi')
>>> y
b'ab\xd6\xd0\xce\xc4c'
>>> y.decode('ansi')
'ab中文c'

还有常见的ghk编码
```

GBK 是我国制定的中文编码标准，规定英文字符母占用 1 个字节，中文字符占用 2 个字节；而 UTF-8 是国际通过的编码格式，它包含了全世界所有国家需要用到的字符，其规定英文字符占用 1 个字节，中文字符占用 3 个字节。

```python
str.encode([encoding="utf-8"][,errors="strict"])
```



| 参数               | 含义                                                         |
| ------------------ | ------------------------------------------------------------ |
| str                | 表示要进行转换的字符串。                                     |
| encoding = "utf-8" | 指定进行编码时采用的字符编码，该选项默认采用 utf-8 编码。例如，如果想使用简体中文，可以设置 gb2312。  当方法中只使用这一个参数时，可以省略前边的“encoding=”，直接写编码格式，例如 str.encode("UTF-8")。 |
| errors = "strict"  | 指定错误处理方式，其可选择值可以是：<br />strict：遇到非法字符就抛出异常。<br />ignore：忽略非法字符。<br />replace：用“？”替换非法字符。<br />xmlcharrefreplace：使用 xml 的字符引用。<br />该参数的默认值为 strict。 |

len函数可以计算str或bytes长度

```python
>>> len('中亠')
2
>>> x = '中亠'.encode('utf8')
>>> x
b'\xe4\xb8\xad\xe4\xba\xa0'
>>> len(x)
6

```

#### str()  与 repr()区别：

 str()内部调用对象的`__str__`方法

repr()内部调用了对象的`__repr__`方法。  report?

```python
>>> from datetime import datetime
>>> now = datetime.now()
>>> str(now)
'2022-02-06 14:36:35.776710'
>>> repr(now)
'datetime.datetime(2022, 2, 6, 14, 36, 35, 776710)'
```

#### 字符串常量

```python
>>> import string
>>> string.hexdigits
'0123456789abcdefABCDEF'
>>> string.whitespace
' \t\n\r\x0b\x0c'
>>> string.printable  
'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'
```



此模块中定义的常量为：

- `string.``ascii_letters`

  下文所述 [`ascii_lowercase`](https://docs.python.org/zh-cn/3/library/string.html#string.ascii_lowercase) 和 [`ascii_uppercase`](https://docs.python.org/zh-cn/3/library/string.html#string.ascii_uppercase) 常量的拼连。 该值不依赖于语言区域。

- `string.``ascii_lowercase`

  小写字母 `'abcdefghijklmnopqrstuvwxyz'`。 该值不依赖于语言区域，不会发生改变。

- `string.``ascii_uppercase`

  大写字母 `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`。 该值不依赖于语言区域，不会发生改变。

- `string.``digits`

  字符串 `'0123456789'`。

- `string.``hexdigits`

  字符串 `'0123456789abcdefABCDEF'`。

- `string.``octdigits`

  字符串 `'01234567'`。

- `string.``punctuation`

  由在 `C` 区域设置中被视为标点符号的 ASCII 字符所组成的字符串: `!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`.

- `string.``printable`

  由被视为可打印符号的 ASCII 字符组成的字符串。 这是 [`digits`](https://docs.python.org/zh-cn/3/library/string.html#string.digits), [`ascii_letters`](https://docs.python.org/zh-cn/3/library/string.html#string.ascii_letters), [`punctuation`](https://docs.python.org/zh-cn/3/library/string.html#string.punctuation) 和 [`whitespace`](https://docs.python.org/zh-cn/3/library/string.html#string.whitespace) 的总和。

- `string.``whitespace`

  由被视为空白符号的 ASCII 字符组成的字符串。 其中包括空格、制表、换行、回车、进纸和纵向制表符。

#### 字符串常用方法

```python
# 拼接字符串
>>> s = 'str1' 'str2''str3'   
>>> s
'str1str2str3'
>>> info = 'python'
>>> dig = 3
>>> s = 'str'+info+dig
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str
# 使用str(obj)或repr(obj)转换number, list,tuple,map等。
>>> s = 'str'+info+ str(dig)
>>> s
'strpython3'
>>> type(s)
<class 'str'>

#获取单个字符
# 从字符串左端为起点时，索引为0，1。。。
# 从字符串右端为起点时，索引为-1，-2。。。
>>> s = 'abcde'
>>> s[0]
'a'
>>> s[-1]
'e'

#字符串切片
strname[start : end : step]

对各个部分的说明：
strname：要截取的字符串；
start：表示要截取的第一个字符所在的索引（截取时包含该字符）。如果不指定，默认为 0，也就是从字符串的开头截取；
end：表示要截取的最后一个字符所在的索引（截取时不包含该字符）。如果不指定，默认为字符串的长度；
step：指的是从 start 索引处的字符开始，每 step 个距离获取一个字符，直至 end 索引出的字符。step 默认值为 1，当省略该值时，最后一个冒号也可以省略。
>>> s
'abcde'
>>> s[1:3]
'bc'
>>> s[:3]
'abc'
>>> s[1:]
'bcde'
>>> s[::2]
'ace'

# 字符串长度
>>> s = '人生苦短，我用python'
>>> len(s)   //unicode-16
13
>>> len(s.encode()) //utf8,汉字及标点占3个字节
27
>>> len(s.encode('utf-8'))
27
>>> len(s.encode('utf8'))  
27
>>> len(s.encode('gbk'))  
20
>>> len(s.encode('gb2312')) 
20

# 分隔字符串
str.split(sep,maxsplit)

此方法中各部分参数的含义分别是：
str：表示要进行分割的字符串；
sep：用于指定分隔符，可以包含多个字符。此参数默认为 None，表示所有空字符，包括空格、换行符“\n”、制表符“\t”等。
maxsplit：可选参数，用于指定分割的次数，最后列表中子串的个数最多为 maxsplit+1。如果不指定或者指定为 -1，则表示分割次数没有限制。

在 split 方法中，如果不指定 sep 参数，需要以str.split(maxsplit=xxx)的格式指定 maxsplit 参数。
需要注意的是，在未指定 sep 参数时，split() 方法默认采用空字符进行分割，但当字符串中有连续的空格或其他空字符时，都会被视为一个分隔符对字符串进行分割
>>> s = 'abc >>> c.fbkj.com'
>>> s.split()  # 默认分隔
['abc', '>>>', 'c.fbkj.com']
>>> s = 'abc >>> c.fbkj.com\r\n15fp.cn'
>>> s
'abc >>> c.fbkj.com\r\n15fp.cn'
>>> s.split()
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s = 'abc >>> c.fbkj.com\r15fp.cn'   
>>> s.split()
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s = 'abc >>> c.fbkj.com\n15fp.cn'   
>>> s.split()
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s = 'abc  >>> c.fbkj.com\r\n15fp.cn' 
>>> s.split()
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s.split('>')
['abc  ', '', '', ' c.fbkj.com\r\n15fp.cn']
>>> s.split()
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s.split(,3)  #错误指定maxsplit
  File "<stdin>", line 1
    s.split(,3)
            ^
SyntaxError: invalid syntax
>>> s.split(maxsplit=3)  #指定 maxsplit,实际出来maxsplit+1个字符。最后一个可以看是未分隔部分。
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s.split(maxsplit=2)
['abc', '>>>', 'c.fbkj.com\r\n15fp.cn']
>>> s
'abc  >>> c.fbkj.com\r\n15fp.cn'
>>> s.split() #默认方式下，多个分隔符会合并为一个
['abc', '>>>', 'c.fbkj.com', '15fp.cn']
>>> s.split(' ') #非默认方式下，多个连续分隔符不合并。
['abc', '', '>>>', 'c.fbkj.com\r\n15fp.cn']
>>>
#join()方法：合并字符串
newstr = str.join(iterable)

此方法中各参数的含义如下：
newstr：表示合并后生成的新字符串；
str：用于指定合并时的分隔符；
iterable：做合并操作的源字符串数据，允许以列表、元组等形式提供。

>>> list = ['www','fbkj','com']
>>> '.'.join(list)
'www.fbkj.com'

>>> s = '','usr','bin','env'
>>> type(s)
<class 'tuple'>
>>> s
('', 'usr', 'bin', 'env')
>>> '/'.join(s)
'/usr/bin/env'

# count()方法：统计字符串出现的次数
count 方法用于检索指定字符串在另一字符串中出现的次数，如果检索的字符串不存在，则返回 0，否则返回出现的次数。

count 方法的语法格式如下：
str.count(sub[,start[,end]])

此方法中，各参数的具体含义如下：
str：表示原字符串；
sub：表示要检索的字符串；
start：指定检索的起始位置，也就是从什么位置开始检测。如果不指定，默认从头开始检索；
end：指定检索的终止位置，如果不指定，则表示一直检索到结尾。
>>> s = 'www.fbkj.com.cn'
>>> s.count('.')
3
>>> s.count('.',3)
3
>>> s.count('.',4) 
2
>>> s.count('.',4,-3)
1

# find()方法：检测字符串中是否包含某子串
find() 方法用于检索字符串中是否包含目标字符串，如果包含，则返回第一次出现该字符串的索引；反之，则返回 -1。

find() 方法的语法格式如下：
str.find(sub[,start[,end]])
还提供了rfind函数，表示从右向左检索。同样返回位置索引。-1表示未找到。
此格式中各参数的含义如下：
str：表示原字符串；
sub：表示要检索的目标字符串；
start：表示开始检索的起始位置。如果不指定，则默认从头开始检索；
end：表示结束检索的结束位置。如果不指定，则默认一直检索到结尾。

>>> s
'www.fbkj.com.cn'
>>> s.find('.')
3
>>> s.rfind('.')
12
>>> s.find('.',4)
8
# index()方法：检测字符串中是否包含某子串
同 find() 方法类似，index() 方法也可以用于检索是否包含指定的字符串，不同之处在于，当指定的字符串不存在时，index() 方法会抛出异常。

index() 方法的语法格式如下：
str.index(sub[,start[,end]])
同样有rindex方法，从右向左检索。

此格式中各参数的含义分别是：
str：表示原字符串；
sub：表示要检索的子字符串；
start：表示检索开始的起始位置，如果不指定，默认从头开始检索；
end：表示检索的结束位置，如果不指定，默认一直检索到结尾。

#字符串对齐方法（ljust()、rjust()和center()）
ljust() 方法的功能是向指定字符串的右侧填充指定字符，从而达到左对齐文本的目的。

ljust() 方法的基本格式如下：
S.ljust(width[, fillchar])

其中各个参数的含义如下：
S：表示要进行填充的字符串；
width：表示包括 S 本身长度在内，字符串要占的总长度；
fillchar：作为可选参数，用来指定填充字符串时所用的字符，默认情况使用空格。
>>> s = 'abcd'
>>> s.ljust(6,'0')
'abcd00'
>>> s.rjust(6,'0')
'00abcd'
>>> s.center(6,'0')
'0abcd0'
>>> s.center(7,'0') 
'00abcd0'

# zill在数字字符串左边填充零，且能识别正负号
>>> '12'.zfill(5)
'00012'
>>> '-3.14'.zfill(7)
'-003.14'
>>> '3.14159265359'.zfill(5)
'3.14159265359'

# startswith, endswith方法，是否起始或结束子串
startswith()方法
startswith() 方法用于检索字符串是否以指定字符串开头，如果是返回 True；反之返回 False。此方法的语法格式如下：
str.startswith(sub[,start[,end]])

此格式中各个参数的具体含义如下：
str：表示原字符串；
sub：要检索的子串；
start：指定检索开始的起始位置索引，如果不指定，则默认从头开始检索；
end：指定检索的结束位置索引，如果不指定，则默认一直检索在结束。
>>> s
'abcd'
>>> s.startswith('ab')
True
# 字符串大小写转换 title()将每个单词首字母大写。其它字母全小写。,lower(), upper().
>>> s = 'heeLLo word pyTHOn'  
>>> s.title()
'Heello Word Python'
>>> s = 'I LIKE C#'
>>> s.title()
'I Like C#'

# 删除首尾空格及特殊字符
这里的特殊字符，指的是制表符（\t）、回车符（\r）、换行符（\n）等。

Python 中，字符串变量提供了 3 种方法来删除字符串中多余的空格和特殊字符，它们分别是：
strip()：删除字符串前后（左右两侧）的空格或特殊字符。
lstrip()：删除字符串前面（左边）的空格或特殊字符。
rstrip()：删除字符串后面（右边）的空格或特殊字符

str.strip([chars])
其中，str 表示原字符串，[chars] 用来指定要删除的字符，可以同时指定多个，如果不手动指定，则默认会删除空格以及制表符、回车符、换行符等特殊字符
>>> str = "  c.biancheng.net \t\n\r"
>>> str.strip()
'c.biancheng.net'
>>> str.strip(' \r')
'c.biancheng.net \t\n'
>>> str.strip(' \r\n') 
'c.biancheng.net \t'




```



## 字符串格式化三种方式：

#### %  C语言的格式化

```python
>>> 'Hi %s,  your score is %d' % ('李明', 100)
'Hi 李明,  your score is 100'
```

  ```
  %[标志][输出最小宽度][.精度][长度][格式字符]
  ```

  ①标志：

| 标志字符 | 意义                                     |
| -------- | ---------------------------------------- |
| –        | 结果左对齐，右边填空格                   |
| +        | 输出符号（正号或负号）                   |
| 空格     | 输出值为正值时冠以空格，为负值时冠以符号 |

  ②输出最小宽度：
  用十进制整数来表示输出的最少位数（包括小数部分及小数点在内）

  若实际位数多于定义的宽度，则按实际位数输出；
  若实际位数少于定义的宽度，则右对齐，左边留空；有负号，则左对齐，右边留空；表示宽度的数字以0开始，则右对齐，左边留空；

  ③精度：
  精度格式符以“.”开头；
  若输出为数字，若实际位数大于定义精度，则四舍五入；若不足，则补0；
  若输出为字符，若实际位数大于定义精度，则截去超过的部分。

  ④长度
  长度格式符为h和1两种，h表示按短整型量输出，1表示按长整型输出。

  ⑤格式字符

| 整数方面 | 意义                                                         |
| -------- | ------------------------------------------------------------ |
| %d       | 整数的参数会被转成有符号的十进制数字                         |
| %u       | 整数的参数会被转成无符号的十进制数字                         |
| %o       | 整数的参数会被转成无符号的八进制数字                         |
| %x       | 整数的参数会被转成无符号的十六进制数字，并以小写abcdef 表示  |
| %X       | 整数的参数会被转成无符号的十六进制数字，并以大写ABCDEF 表示浮点型数 |
| %f       | double 型的参数会被转成十进制数字，并取到小数点以下六位，四舍五入 |
| %e       | double 型的参数以指数形式打印，有一个数字会在小数点前，六位数字在小数点后，而在指数部分会以小写的e 来表示 |
| %E       | 与%e 作用相同，唯一区别是指数部分将以大写的E 来表示          |
| %g       | double 型的参数会自动选择以%f 或%e 的格式来打印，其标准是根据打印的数值及所设置的有效位数来决定。 |
| %G       | 与%g 作用相同，唯一区别在以指数形态打印时会选择%E 格式。     |

| 字符及字符串方面 | 意义                                                |
| ---------------- | --------------------------------------------------- |
| %c               | 整型数的参数会被转成unsigned char 型打印出          |
| %s               | 指向字符串的参数会被逐字输出，直到出现NULL 字符为止 |
| %p               | 如果是参数是"void *"型指针则使用十六进制格式显示    |
| %%               | 输出一个百分号                                      |


  原文链接：https://blog.csdn.net/qq_44921056/article/details/121599746

附加格式：

| 字符            | 含义                                                         |
| --------------- | ------------------------------------------------------------ |
| l               | 附加在d,u,x,o前面，表示长整数，双精度浮点数( 例如:%lf  %ld)  |
| -               | 左对齐                                                       |
| m(代表一个整数) | 数据最小宽度                                                 |
| 0(数字0)        | 将输出的前面补上0直到占满指定列宽为止不可以搭配使用-         |
| n(整数)         | m指域宽，即对应的输出项在输出设备上所占的字符数。n指精度，用于说明输出的实型数的小数位数。 |
| #               | '%#0*X' % 8,                                                 |

```python
>>> '%8d%8d' % (123,4567)
'     123    4567'
>>> '%8X' % 123
'      7B'
>>> '%8x' % 123
'      7b'
>>> '%08d' % 123
'00000123'
>>> '%5.3f' % 123.456789
'123.457'
>>> '%5.3f' % 1.234567
'1.235'
>>> '%05.3f' % 1.234567
'1.235'
>>> '%.2f' % 1.23456
'1.23'
>>> '%#X' % 123
'0X7B'
>>> s = 'abcdefg'
>>> m = 'oiklkhhj'
>>> '%.3s%.3s' % (s,m)
'abcoik'
```



 %d  整形 int

 %f  浮点型 float

 %c  字符型  char 

 %hd 短整型  short

 %ld  长整形  long

 %lld  长长整形  long long 



#### format

  ```python
  str.format(args)
  args格式说明：
  { [index][ : [ [fill] align] [sign] [#] [width] [.precision] [type] ] }
  ```

```
format_spec     ::=  [[fill]align][sign][#][0][width][grouping_option][.precision][type]
fill            ::=  <any character>
align           ::=  "<" | ">" | "=" | "^"
sign            ::=  "+" | "-" | " "
width           ::=  digit+
grouping_option ::=  "_" | ","
precision       ::=  digit+
type            ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "s" | "x" | "X" | "%"
```



  注意，格式中用 [] 括起来的参数都是可选参数，即可以使用，也可以不使用。各个参数的含义如下：

  - index：指定：后边设置的格式要作用到 args 中第几个数据，数据的索引值从 0 开始。如果省略此选项，则会根据 args 中数据的先后顺序自动分配。

  - fill：指定空白处填充的字符。注意，当填充字符为逗号(,)且作用于整数或浮点数时，该整数（或浮点数）会以逗号分隔的形式输出，例如（1000000会输出 1,000,000）。

  - align：指定数据的对齐方式，具体的对齐方式如表 1 所示。

    | align | 含义                                                         |
    | ----- | ------------------------------------------------------------ |
    | <     | 数据左对齐。                                                 |
    | >     | 数据右对齐。                                                 |
    | =     | 数据右对齐，同时将符号放置在填充内容的最左侧，该选项只对数字类型有效。 |
    | ^     | 数据居中，此选项需和 width 参数一起使用。                    |

  - 

  - sign：指定有无符号数，此参数的值以及对应的含义如表 2 所示。

    | sign参数 | 含义                                                         |
    | -------- | ------------------------------------------------------------ |
    | +        | 正数前加正号，负数前加负号。                                 |
    | -        | 正数前不加正号，负数前加负号。                               |
    | 空格     | 正数前加空格，负数前加负号。                                 |
    | #        | 对于二进制数、八进制数和十六进制数，使用此参数，各进制数前会分别显示 0b、0o、0x前缀；反之则不显示前缀。 |

  - width：指定输出数据时所占的宽度。

  - .precision：指定保留的小数位数。

  - type：指定输出数据的具体类型，如表 3 所示。

| type类型值 | 含义                                                  |
| ---------- | ----------------------------------------------------- |
| s          | 对字符串类型格式化。                                  |
| d          | 十进制整数。                                          |
| c          | 将十进制整数自动转换成对应的 Unicode 字符。           |
| e 或者 E   | 转换成科学计数法后，再格式化输出。                    |
| g 或 G     | 自动在 e 和 f（或 E 和 F）中切换。                    |
| b          | 将十进制数自动转换成二进制表示，再格式化输出。        |
| o          | 将十进制数自动转换成八进制表示，再格式化输出。        |
| x 或者 X   | 将十进制数自动转换成十六进制表示，再格式化输出。      |
| f 或者 F   | 转换为浮点数（默认小数点后保留 6 位），再格式化输出。 |
| %          | 显示百分比（默认显示小数点后 6 位）。                 |

  

  ```python
  'hello, {0} 成绩提升 {1:1f}'.format('小明', 17.2345)
  str="网站名称：{:>9s}\t网址：{:s}"
  print(str.format("C语言中文网","c.biancheng.net"))
  #以货币形式显示
  print("货币形式：{:,d}".format(1000000))
  #科学计数法表示
  print("科学计数法：{:E}".format(1200.12))
  #以十六进制表示
  print("100的十六进制：{:#x}".format(100))
  #输出百分比形式
  print("0.01的百分比表示：{:.0%}".format(0.01))
  ```

  

#### f-string

  参考： https://realpython.com/python-f-strings/

  字符串中有{变量名},会自动以对应变量替换.

  ```python
>>> a,b,c=35,'abc', 5.398     
# 变量替换
>>> f'{a} {b} {c}'
'35 abc 5.398'
# 双花括号 '{{' 或 '}}' 被替换为单花括号
>>> f'{{ a }}'
'{ a }'
# 在表达式后加等于号 '='，可在求值后，同时显示表达式文本及其结果（用于调试）。
#没有指定格式时，'=' 默认调用表达式的 repr()。
# 叹号 '!' 后跟转换符"s" | "r" | "a"
# 指定了转换符时，表达式求值的结果会先转换，再格式化。转换符 '!s' 调用 str() 转换求值结果，'!r' 调用 repr()，'!a' 调用 ascii()。
>>> f'{a} {b=} {c=}'
"35 b='abc' c=5.398"
>>> f'{a!s} {b=!s} {c=!s}'
'35 b=abc c=5.398'
# 表达式
>>> f'{c-a}'   
'-29.602'
# 冒号 ':' 后附加格式说明符,使用 format() 协议。
#右对齐，空白填充b,占5个宽度
>>> f'{a:b>5}'  
'bbb35'

#格式表达式中不能有反斜杠,遇到反斜杠，可以先定义变量，再引用。
f"newline: {ord('\n')}" //报错
>>> newline = ord('\n')
>>> f"newline: {newline}"
'newline: 10'

  ```



### tuple(元组) list(列表)



```
  



#### 转义字符 

| 转义字符             | 说明                                               |
| -------------------- | -------------------------------------------------- |
| \n \t \b \\ \  \' \" |                                                    |
| \                    | 在字符串行尾的续行符，即一行未完，转到下一行继续写 |

![preview](python学习.assets\v2-7bfa7ad5b1f5ac64034fc888c320d0d5_r.jpg)

## list 数组或叫列表

​```python
>>> names = [123,'abc',456]
>>> names[0]
123
>>> names[-1]
456
>>> names[3]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

支持len() 取长度

append, insert, pop 函数

lista = listb 为引用复制,修改一个元素另一个也会修改.

切片操作是复制操作，修改切片原数组不受影响



names=(12,3,4,5)

t=()

t=(1,) 

如果只有一个元素,需要加个逗号,不然会认为是普通大括号.

```python
>>> t = ('a','b',[1,2])  
>>> t[1]
'b'
>>> t[2,1]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: tuple indices must be integers or slices, not tuple
>>> t[2][1]
2
>>> t[2][1]= 'A'  //t是tuple, t[2]是list, 可以t[2][1]='A' 来修改list
>>> t[2][1]      
'A'
>>> t[1] = 'C'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment--
    
# 切片 
>>> s = 'abcdefg'
>>> s[2::2]
'ceg'
# 相加
>>> a=[1,2,3]
>>> b = [3,2,4]
>>> a+b
[1, 2, 3, 3, 2, 4]
#  相乘
>>> a*3
[1, 2, 3, 1, 2, 3, 1, 2, 3]
>>> list = [None]*5
>>> list
[None, None, None, None, None]
# 内置函数
>>> sum(a)
6
>>> sorted(b)
[2, 3, 4]
# 删除列表
>>> del b
```
#### 序列相关内置函数

| len()       | 计算序列的长度，即返回序列中包含多少个元素。                 |
| ----------- | ------------------------------------------------------------ |
| max()       | 找出序列中的最大元素。注意，对序列使用 sum() 函数时，做加和操作的必须都是数字，不能是字符或字符串，否则该函数将抛出异常，因为解释器无法判定是要做连接操作（+ 运算符可以连接两个序列），还是做加和操作。 |
| min()       | 找出序列中的最小元素。                                       |
| list()      | 将序列转换为列表。                                           |
| str()       | 将序列转换为字符串。                                         |
| sum()       | 计算元素和。                                                 |
| sorted()    | 对元素进行排序。                                             |
| reversed()  | 反向序列中的元素。                                           |
| enumerate() | 将序列组合为一个索引序列，多用在 for 循环中。                |

**切片**

mylist[start : end : step]

其中，各个参数的含义分别是：

- sname：表示序列的名称；
- start：表示切片的开始索引位置（包括该位置），此参数也可以不指定，会默认为 0，也就是从序列的开头进行切片；
- end：表示切片的结束索引位置（不包括该位置），如果不指定，则默认为序列的长度；
- step：表示在切片过程中，隔几个存储位置（包含当前位置）取一次元素，也就是说，如果 step 的值大于 1，则在进行切片去序列元素时，会“跳跃式”的取元素。如果省略设置 step 的值，则最后一个冒号就可以省略。

#### **列表操作**

append 添加元素，参数中是列表的话，会按一个整体添加到目录列表

extend 添加元素，参数是列表的话会将列表元素添加到目标列表中

insert 插入元素。

del mylist[i] 删除元素

del mylist[start:end] 删除一个范围的元素。（不含end元素)

listname.pop(index)  根据索引删除元素

remove(值)   根据元素值删除，只会删除第一个和指定值相同的元素。

lcean() 删除所有

mylist[3]=5 修改单元素

通过切片修改批量元素,Python 就不要求新赋值的元素个数与原来的元素个数相同；这意味，该操作既可以为列表添加元素，也可以为列表删除元素。

```python
>>> n = [1,2,3,4,5,6]
>>> n[1:3] = [11,12,13,14] 
>>> n
[1, 11, 12, 13, 14, 4, 5, 6]
>>> n[1:5]=[99]
>>> n
[1, 99, 4, 5, 6]
#如果是字符串赋值，则会解元素每个字符串
>>> n[1:-1] = 'abcdefg'
>>> n
[1, 'a', 'b', 'c', 'd', 'e', 'f', 'g', 6]

#tuple元组不可修改，但元组中有list,list内容是可修改的。
>>> n='a','b',[3,5]
>>> n
('a', 'b', [3, 5])
>>> n[2][0]=4
>>> n
('a', 'b', [4, 5])
```

index() ：查找元素索引

listname.index(obj, start, end)

start 和 end 参数用来指定检索范围：

- start 和 end 可以都不写，此时会检索整个列表；
- 如果只写 start 不写 end，那么表示检索从 start 到末尾的元素；
- 如果 start 和 end 都写，那么表示检索 start 和 end 之间的元素。

count:统计元素出现的次数

n.count(3) :3在n中出现的次数。



### dict 字典



| 函数及描述                                                   |
| :----------------------------------------------------------- |
| dict[key]  访问指定键值，如果key不存在会触发异常             |
| del mydict   删除字典                                        |
| del mydict['语文']  删除字典元素。                           |
| ‘语文' in mydict ,  ‘语文' not in mydict  是否存在元素。     |
| [dict.clear()](https://www.runoob.com/python/att-dictionary-clear.html) 删除字典内所有元素 |
| [dict.copy()](https://www.runoob.com/python/att-dictionary-copy.html) 返回一个字典的浅复制 |
| [dict.fromkeys(seq[, val\])](https://www.runoob.com/python/att-dictionary-fromkeys.html) 创建一个新字典，以序列 seq 中元素做字典的键，val 为字典所有键对应的初始值 |
| [dict.get(key, default=None)](https://www.runoob.com/python/att-dictionary-get.html) 返回指定键的值，如果值不在字典中返回default值 |
| [dict.has_key(key)](https://www.runoob.com/python/att-dictionary-has_key.html) 如果键在字典dict里返回true，否则返回false |
| [dict.items()](https://www.runoob.com/python/att-dictionary-items.html) 以列表返回可遍历的(键, 值) 元组数组 |
| [dict.keys()](https://www.runoob.com/python/att-dictionary-keys.html) 以列表返回一个字典所有的键 |
| [dict.setdefault(key, default=None)](https://www.runoob.com/python/att-dictionary-setdefault.html) 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default.否则类似get(),返回值. |
| [dict.update(dict2)](https://www.runoob.com/python/att-dictionary-update.html) 把字典dict2的键/值对更新到dict里 |
| [dict.values()](https://www.runoob.com/python/att-dictionary-values.html) 以列表返回字典中的所有值 |
| [pop(key[,default\])](https://www.runoob.com/python/python-att-dictionary-pop.html) 删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。 |
| [popitem()](https://www.runoob.com/python/python-att-dictionary-popitem.html) 返回并删除字典中的最后一对键和值。类似出栈操作。 |

d ={'张三':25,"李四",30}

dict 内部有索引,list没有,所以dict查找要比较快

| 主要特征                       | 解释                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| 通过键而不是通过索引来读取元素 | 字典类型有时也称为关联数组或者散列表（hash）。它是通过键将一系列的值联系起来的，这样就可以通过键从字典中获取指定项，但不能通过索引来获取。 |
| 字典是任意数据类型的无序集合   | 和列表、元组不同，通常会将索引值 0 对应的元素称为第一个元素，而字典中的元素是无序的。 |
| 字典是可变的，并且可以任意嵌套 | 字典可以在原处增长或者缩短（无需生成一个副本），并且它支持任意深度的嵌套，即字典存储的值也可以是列表或其它的字典。 |
| 字典中的键必须唯一             | 字典中，不支持同一个键出现多次，否则只会保留最后一个键值对。 |
| 字典中的键必须不可变           | 字典中每个键值对的键是不可变的，只能使用数字、字符串或者元组，不能使用列表。 |

```python
# fromkeys方法 
>>> knowledge = ['语文', '数学', '英语']
>>> scores = dict.fromkeys(knowledge, 60)
>>> print(scores)
{'语文': 60, '数学': 60, '英语': 60}
>>> scores = dict.fromkeys(knowledge)
>>> print(scores)
{'语文': None, '数学': None, '英语': None}

# 创建方法，字符串键不能带引号
>>> a = dict(abc=123,efg=456,hij=789)       
>>> a
{'abc': 123, 'efg': 456, 'hij': 789}

# 赋值b后，为引用赋值，修改b影响a
>>> b = a
>>> b['abc']='haha'
>>> b
{'abc': 'haha', 'efg': 456, 'hij': 789}
>>> a
{'abc': 'haha', 'efg': 456, 'hij': 789}
# 拷贝一个新字典
>>> b = a.copy()
a = {'one': 1, 'two': 2, 'three': [1,2,3]}
b = a.copy()
注意，copy() 方法所遵循的拷贝原理，既有深拷贝，也有浅拷贝。拿拷贝字典 a 为例，copy() 方法只会对最表层的键值对进行深拷贝，也就是说，它会再申请一块内存用来存放 {'one': 1, 'two': 2, 'three': []}；而对于某些列表类型的值来说，此方法对其做的是浅拷贝，也就是说，b 中的 [1,2,3] 的值不是自己独有，而是和 a 共有。

# update 用一个字典更新已有字典。
>>> a = {'one': 1, 'two': 2, 'three': 3}
>>> a.update({'one':4.5, 'four': 9.3})
>>> print(a)
{'one': 4.5, 'two': 2, 'three': 3, 'four': 9.3}

# 遍历字典
for f,v in dict.items():
    print(f,'=',v)
```

| 创建格式                                                     | 注意事项                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| a = dict(str1=value1, str2=value2, str3=value3)              | str 表示字符串类型的键，value 表示键对应的值。使用此方式创建字典时，字符串不能带引号。 |
| #方式1 demo = [('two',2), ('one',1), ('three',3)]<br /> #方式2 demo = [['two',2], ['one',1], ['three',3]] <br />#方式3 demo = (('two',2), ('one',1), ('three',3)) <br />#方式4 demo = (['two',2], ['one',1], ['three',3])<br /> a = dict(demo) | 向 dict() 函数传入列表或元组，而它们中的元素又各自是包含 2 个元素的列表或元组，其中第一个元素作为键，第二个元素作为值。 |
| keys = ['one', 'two', 'three'] <br />#还可以是字符串或元组 <br />values = [1, 2, 3] <br />#还可以是字符串或元组 <br />a = dict( zip(keys, values) ) | 通过应用 dict() 函数和 zip() 函数，可将前两个列表转换为对应的字典 |

### Set（集合）

s = set([1,2,3])  值不重复. set是无序的。

`add, remove` 添删.

集合中，只能存储不可变的数据类型，包括整形、浮点型、字符串、元组，无法存储列表、字典、集合这些可变的数据类.

```python
>>> set1 = set("c.biancheng.net")
>>> set2 = set([1,2,3,4,5])
>>> set3 = set((1,2,3,4,5))
>>> print("set1:",set1)
set1: {'b', 'a', 'g', 'i', 'c', 'h', 't', 'e', 'n', '.'}
>>> print("set2:",set2)
set2: {1, 2, 3, 4, 5}
>>> print("set3:",set3)
set3: {1, 2, 3, 4, 5}
{1, 2, 3, 4, 5}
# 添加
>>> set3.add(6)
>>> set3
{1, 2, 3, 4, 5, 6}
# 删除
>>> set3.remove(3)
>>> set3
{1, 2, 4, 5, 6}   
# 包含元素
>>> d = {1,2,3,4} 
>>> 2 in d
True
>>> 2 not in d
False
```



设置 set1={1,2,3} 和 set2={3,4,5}

| 运算操作 | Python运算符 | 含义                              | 例子                                              |
| -------- | ------------ | --------------------------------- | ------------------------------------------------- |
| 交集     | &            | 取两集合公共的元素                | >>> set1 & set2 {3}                               |
| 并集     | \|           | 取两集合全部的元素                | >>> set1 \| set2 {1,2,3,4,5}                      |
| 差集     | -            | 取一个集合中另一集合没有的元素    | >>> set1 - set2 {1,2} <br />>>> set2 - set1 {4,5} |
| 对称差集 | ^            | 取集合 A 和 B 中不属于 A&B 的元素 | >>> set1 ^ set2 {1,2,4,5}                         |

| 方法名                        | 语法格式                               | 功能                                                         | 实例                                                         |
| ----------------------------- | -------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| add()                         | set1.add()                             | 向 set1 集合中添加数字、字符串、元组或者布尔类型             | >>> set1 = {1,2,3} <br />>>> set1.add((1,2)) <br />>>> set1 {(1, 2), 1, 2, 3} |
| clear()                       | set1.clear()                           | 清空 set1 集合中所有元素                                     | >>> set1 = {1,2,3} <br />>>> set1.clear() <br />>>> set1 set()  set()才表示空集合，{}表示的是空字典 |
| copy()                        | set2 = set1.copy()                     | 拷贝 set1 集合给 set2                                        | >>> set1 = {1,2,3} <br />>>> set2 = set1.copy() <br />>>> set1.add(4) <br />>>> set1 {1, 2, 3, 4} <br />>>> set1 {1, 2, 3} |
| difference()                  | set3 = set1.difference(set2)           | 将 set1 中有而 set2 没有的元素给 set3                        | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set3 = set1.difference(set2) <br />>>> set3 {1, 2} |
| difference_update()           | set1.difference_update(set2)           | 从 set1 中删除与 set2 相同的元素                             | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set1.difference_update(set2) <br />>>> set1 {1, 2} |
| discard()                     | set1.discard(elem)                     | 删除 set1 中的 elem 元素                                     | >>> set1 = {1,2,3} >>> set1.discard(2) >>> set1 {1, 3} >>> set1.discard(4) {1, 3} |
| intersection()                | set3 = set1.intersection(set2)         | 取 set1 和 set2 的交集给 set3                                | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set3 = set1.intersection(set2) <br />>> set3 {3} |
| intersection_update()         | set1.intersection_update(set2)         | 取 set1和 set2 的交集，并更新给 set1                         | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set1.intersection_update(set2) <br />>>> set1 {3} |
| isdisjoint()                  | set1.isdisjoint(set2)                  | 判断 set1 和 set2 是否没有交集，有交集返回 False；没有交集返回 True | >>> set1 = {1,2,3} <br />>>> set2 = {3,4}<br /> >>> set1.isdisjoint(set2) False |
| issubset()                    | set1.issubset(set2)                    | 判断 set1 是否是 set2 的子集                                 | >>> set1 = {1,2,3} <br />>>> set2 = {1,2} <br />>>> set1.issubset(set2) False |
| issuperset()                  | set1.issuperset(set2)                  | 判断 set2 是否是 set1 的子集                                 | >>> set1 = {1,2,3} <br />>>> set2 = {1,2} <br />>>> set1.issuperset(set2) True |
| pop()                         | a = set1.pop()                         | 取 set1 中一个元素，并赋值给 a                               | >>> set1 = {1,2,3} <br />>>> a = set1.pop() <br />>>> set1 {2,3}<br /> >>> a 1 |
| remove()                      | set1.remove(elem)                      | 移除 set1 中的 elem 元素                                     | >>> set1 = {1,2,3} <br />>>> set1.remove(2) <br />>>> set1 {1, 3} <br />>>> set1.remove(4) 报错 |
| symmetric_difference()        | set3 = set1.symmetric_difference(set2) | 取 set1 和 set2 中互不相同的元素，给 set3                    | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set3 = set1.symmetric_difference(set2) <br />>>> set3 {1, 2, 4} |
| symmetric_difference_update() | set1.symmetric_difference_update(set2) | 取 set1 和 set2 中互不相同的元素，并更新给 set1              | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set1.symmetric_difference_update(set2) <br />>>> set1 {1, 2, 4} |
| union()                       | set3 = set1.union(set2)                | 取 set1 和 set2 的并集，赋给 set3                            | >>> set1 = {1,2,3} <br />>>> set2 = {3,4} <br />>>> set3=set1.union(set2) <br />>>> set3 {1, 2, 3, 4} |
| update()                      | set1.update(elem)                      | 添加列表或集合中的元素到 set1                                | >>> set1 = {1,2,3} <br />>>> set1.update([3,4]) <br />>>> set1 {1,2,3,4} |



## 模板与包、命名空间与作用域

- 函数有自已的命名空间，类的方法的作用域规则和通常函数的一样。
- 如果在函数内只是引用变量，则该变量可以是全局变量。
- 如果函数内赋值变量，则变量自动为局部变量。
- 如果函数内对全局变量赋值，必须用global声明该变量为全局变量。

```python
Money = 2000
def AddMoney():
   # 无global时，函数报错，因为要赋值money，money未定义。但money=1则可以执行，相当于定义了局域变量。
   # 如果money是对象，比如money['a']=5  则不会报错。money为全局访问。
   global Money
   Money = Money + 1
 
print （Money）
AddMoney()
print （Money）
```



**包->模块->变量或类名** 组成一个完整的授权名称(fully qualified name)，可以防止名称冲突。

模块的搜索路径：

```python
>>> import sys
>>> sys.path
['', 'D:\\Python310\\python310.zip', 'D:\\Python310\\DLLs', 'D:\\Python310\\lib', 'D:\\Python310', 'E:\\cod\\python\\helpsk\\venv', 'E:\\cod\\python\\helpsk\\venv\\lib\\site-packages']

# 运行时添加搜索路径，只影响当前程序，退出即无效。
>>> sys.path.append('/abc/abc/abc')
>>> sys.path
['', 'D:\\Python310\\python310.zip', 'D:\\Python310\\DLLs', 'D:\\Python310\\lib', 'D:\\Python310', 'E:\\cod\\python\\helpsk\\venv', 'E:\\cod\\python\\helpsk\\venv\\lib\\site-packages', '/abc/abc/abc']

# 列出当前导入了哪些模板及其完整路径
>>> sys.modules
{'sys': <module 'sys' (built-in)>, 'builtins': <module 'builtins' (built-in)>, '_frozen_importlib': 
<module '_frozen_importlib' (frozen)>, '_imp': <module '_imp' (built-in)>, '_thread': <module '_thread' (built-in)>, '_warnings': <module '_warnings' (built-in)>, '_weakref': <module '_weakref' (built-in)>, '_io': <module '_io' (built-in)>, 'marshal': <module 'marshal' (built-in)>, 'nt': <module 'nt' (built-in)>, 'winreg': <module 'winreg' (built-in)>, '_frozen_importlib_external': <module '_frozen_importlib_external' (frozen)>, 'time': <module 'time' (built-in)>, 'zipimport': <module 'zipimport' (frozen)>, '_codecs': <module '_codecs' (built-in)>, 'codecs': <module 'codecs' from 'D:\\Python310\\lib\\codecs.py'>, 'encodings.aliases': <module 'encodings.aliases' from 'D:\\Python310\\lib\\encodings\\aliases.py'>, 'encodings': <module 'encodings' from 'D:\\Python310\\lib\\encodings\\__init__.py'>, 'encodings.utf_8': <module 'encodings.utf_8' from 'D:\\Python310\\lib\\encodings\\utf_8.py'>, 
'_codecs_cn': <module '_codecs_cn' (built-in)>, '_multibytecodec': <module '_multibytecodec' (built-in)>, 'encodings.gbk': <module 'encodings.gbk' from 'D:\\Python310\\lib\\encodings\\gbk.py'>, '_signal': <module '_signal' (built-in)>, '_abc': <module '_abc' (built-in)>, 'abc': <module 'abc' from 'D:\\Python310\\lib\\abc.py'>, 'io': <module 'io' from 'D:\\Python310\\lib\\io.py'>, '__main__': <module '__main__' (built-in)>, '_stat': <module '_stat' (built-in)>, 'stat': <module 'stat' from 'D:\\Python310\\lib\\stat.py'>, '_collections_abc': <module '_collections_abc' from 'D:\\Python310\\lib\\_collections_abc.py'>, 'genericpath': <module 'genericpath' from 'D:\\Python310\\lib\\genericpath.py'>, 'ntpath': <module 'ntpath' from 'D:\\Python310\\lib\\ntpath.py'>, 'os.path': <module 'ntpath' from 'D:\\Python310\\lib\\ntpath.py'>, 'os': <module 'os' from 'D:\\Python310\\lib\\os.py'>, '_sitebuiltins': <module '_sitebuiltins' from 'D:\\Python310\\lib\\_sitebuiltins.py'>, 'site': <module 'site' from 'D:\\Python310\\lib\\site.py'>, 'atexit': <module 'atexit' (built-in)>}
```

名称空间包括内建空间，全局空间，局域空间，对应到变量作用域，决定了变量的搜索顺序：

![image-20220722092119292](python学习.assets\image-20220722092119292.png)

```python
# as建立一个别名，一般用于简短原模块或模块属性名
from cgi import FieldStorange as form
```

### from import

import 变量时，会直接在当前模块创建一个与导入模块同名的变量，这会导致在两个模块中出现两个不同的变量。修改一个并不会同步影响另一个。而函数等引用类型的导入不存在此问题。建议访问变量时，带上模块名。

```python
>>>####b.py
foo = 'abc'
def show():
    print( __name__, 'foo is ', foo)
>>>####a.py
import b
from b import foo, show

print(foo)
print(b.foo)
show()
b.show()
foo = '111'
print(foo)
print(b.foo)
show()
b.show()

>>> python a.py
abc
abc
b foo is  abc
b foo is  abc
111
abc
b foo is  abc
b foo is  abc
```

### 搜索路径

当你导入一个模块，Python 解析器对模块位置的搜索顺序是：

- 1、当前目录
- 2、如果不在当前目录，Python 则搜索在 shell 变量 PYTHONPATH 下的每个目录。
- 3、如果都找不到，Python会察看默认路径。UNIX下，默认路径一般为/usr/local/lib/python/。

模块搜索路径存储在 system 模块的 sys.path 变量中。变量里包含当前目录，PYTHONPATH和由安装过程决定的默认目录。





## 函数



```python
# 空函数
def nop():
    pass

def nop(x):
    if not isinstance(x, (float,int)):  #类型检查
        print('type error')
    else:
        print(x)

```

#### 函数可以返回多个值，返回值其实是tuple

```python
def move(x,y,step):
...     return x + step, y + step
... 
>>> a,b= move(2,3,5)
>>> print(a,b)   
7 8 
>>> move(2,3,4)
(6, 7)
```



#### 函数参数：

```python
def power(x,n=2):  //默认参数
 	pass
power(2)
powner(5,2)

def add_end(L=[]): //有问题，因为函数定义时，默认参数L的值就被计算出来了，即[],是个对象，L指向这个对象，所以每次调用都会修改同一个对象。
定义默认参数要牢记一点：默认参数必须指向不变对象！可以修改为
def add_end(L=None):
    if L=None:
        L = []
可变参数：标记*号用于传list.
def calc(*numbers):
    sum = 0
    for n in numbers：
    	sum = sum + n
    return sum

calc(1,2)
nums = [1,2,3]
calc(*nums)  //list,tuple前加*号可以传所有元素到可变参数中去。

关键字参数: 标记**用于传dict.
>>> def person(name, age, **kw):
...     print('name:', name, 'age:', age, 'other:', kw)
... 
>>> person('khz',30)
name: khz age: 30 other: {}
>>> person('bob',35, city='beijing',job ='engineer')  
name: bob age: 35 other: {'city': 'beijing', 'job': 'engineer'}
>>> extra={'city':"beijing", "job":'engineer'}  
>>> person('khz',30, **extra)  //参数加**直接传递dict。
name: khz age: 30 other: {'city': 'beijing', 'job': 'engineer'}            
 
关键字参数不限制参数数量及key(关键字名字），
如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收city和job作为关键字参数。这种方式定义的函数如下：

def person(name, age, *, city, job):
    print(name, age, city, job)
和关键字参数**kw不同，命名关键字参数需要一个特殊分隔符*，*后面的参数被视为命名关键字参数。

>>> def person(name,age,*,city,job):
...     print(name,age,city,job)
... 
>>> person('jack',24, city='beijing', job='engineer')   
jack 24 beijing engineer
>>> person('jack',24, city='beijing')  //不能缺少命名关键字参数               
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: person() missing 1 required keyword-only argument: 'job'
        
使用命名关键字参数时，要特别注意，如果没有可变参数，就必须加一个*作为特殊分隔符。如果缺少*，Python解释器将无法识别位置参数和命名关键字参数：如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了：
        
>>> def person(name,age, *args, city, job='teacher'): //可以有默认参数值
...     print(name,age,args,city,job)      
... 
>>> person('jack',24,'bb','aa',city='beijing',job='engineer')
jack 24 ('bb', 'aa') beijing engineer

                 
在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
>>> def f1(a, b, c=0, *args, **kw):
...     print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)
...
>>> def f2(a, b, c=0, *, d, **kw):
...     print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)
... 
>>> f1(1,2)
a = 1 b = 2 c = 0 args = () kw = {}
>>> f1(1,2,3)
a = 1 b = 2 c = 3 args = () kw = {}
>>> f1(1,2,c=3)
a = 1 b = 2 c = 3 args = () kw = {}
>>> f1(1,2,3,'a','b')
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}
>>> f1(1,2,3,job='engineer')
a = 1 b = 2 c = 3 args = () kw = {'job': 'engineer'}
>>> f2(1,2,d=99, ext=None, ext1=33,ext2='beijing')
a = 1 b = 2 c = 0 d = 99 kw = {'ext': None, 'ext1': 33, 'ext2': 'beijing'}
>>> args={1,2,3,4}
>>> kw={'d':99, 'x':'bb'}
>>> f1(*args,**kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'d': 99, 'x': 'bb'}
>>> args=(1,2,3)
>>> f2(*args, **kw)
a = 1 b = 2 c = 3 d = 99 kw = {'x': 'bb'}
>>>
```

#### 切片： Slice

```python
//切片共支持三个参数，第一个是左起索引，第二个是右侧索引（不包括），第三个是每次跳过几个。
>>> L=[0,1,2,3,4,5]
>>> L[0:3]
[0, 1, 2]
>>> L[1:3]
[1, 2]
>>> L[-2:]
[4, 5]
>>> L[-3:-1]
[3, 4]
>>> L[:3]
[0, 1, 2]
>>> L[-3:]
[3, 4, 5]
>>> L= list(range(101))
>>> L
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
>>> L[::5]
[0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95, 100]
>>> (0,2,3,4,5)[:3]
(0, 2, 3)
>>> L[:] //相当于复制了一个list或tuple,复制后，原本是list还是list,tuple还是tuple.
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
>>> M = L
>>> N = L[:]
>>> N[1] = 'aa'
>>> N
[0, 'aa', 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 
36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
>>> L
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
>>> M[1] = 'b'
>>> L
[0, 'b', 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
>>> L[:30:5]
[0, 5, 10, 15, 20, 25]
```

#### 列表生成式与迭代

列表生成式好像是在迭代的基础上生成列表，扩展了迭代的语法：

```python
>>> [str(x)+'='+str(y) for x in range(0,11) for y in range(20,22)] 
['0=20', '0=21', '1=20', '1=21', '2=20', '2=21', '3=20', '3=21', '4=20', '4=21', '5=20', '5=21', '6=20', '6=21', '7=20', '7=21', '8=20', '8=21', '9=20', '9=21', '10=20', '10=21']
>>> [str(x)+'='+str(y) for x in range(0,11) for y in range(20,22) if x % 2 == 0]
['0=20', '0=21', '2=20', '2=21', '4=20', '4=21', '6=20', '6=21', '8=20', '8=21', '10=20', '10=21']
>>> [str(x)+'='+str(y) for x in range(0,11) if x % 2 == 0 for y in range(20,22)] //if放第二个for的前后都可以，结果一样。
['0=20', '0=21', '2=20', '2=21', '4=20', '4=21', '6=20', '6=21', '8=20', '8=21', '10=20', '10=21']
>>> [x if x % 2 == 0 else -x for x in range(0,11)]  //if放前边就是值表达式一部分，必须提供else
[0, -1, 2, -3, 4, -5, 6, -7, 8, -9, 10]
```

#### 生成器(generator)

创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的`[]`改成`()`，就创建了一个generator

g = (x for x in range(10))  //g现在就是一个generator对象， g中保存的是算法。

next(g) 按顺序获取下一个值，无下一个值时，会报StopIteration错。

for n in g:  //通过迭代可以取出所有值

​	print(n)

函数中出现yield , 就为generator, 每次执行到generator就会返回。函数中也可以出现多个yield.

```python
>>> def fib(max):
...     n,a,b = 0,0,1
...     while n < max:
...         yield b
...         a,b = b, a+b
...         n = n + 1
...     return 'done'
...
>>> for x in fib(5):
...     print(x)
...
1
1
2
3
5
当函数中有yield时，函数就变成了生成器，每次调用next()都会执行到下一个yield. 如果要获取return值，需要如下：
>>> g = fib(6)
>>> while True:
...     try:
...         x = next(g)
...         print('g:', x)
...     except StopIteration as e:
...         print('Generator return value:', e.value)
...         break
...
g: 1
g: 1
g: 2
g: 3
g: 5
g: 8
Generator return value: done
```

#### 迭代器

for 可以循环的一类是数据集合：list, tuple, set, dict,str等.另一类就是 generator.

可以被for循环的对象统称Iterator.

凡是可作用于`for`循环的对象都是`Iterable`类型；

凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；

集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。

Python的`for`循环本质上就是通过不断调用`next()`函数实现的

```python
from collections.abc import Iterable, Iterator
f = fib(5)  //fib是generator.
>>> isinstance(f, Iterable)
True
>>> isinstance(f, Iterator) 
True
>>> isinstance([], Iterator)
False
>>> isinstance({}, Iterator)
False
>>> isinstance('abc', Iterator)
False
如果需要将List变成索引-元素形式，要用到enumerate.
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C

自动解tuple
>>> for x, y in [(1, 1), (2, 4), (3, 9)]:
...     print(x, y)
...
1 1
2 4
3 9
generator都是Iterator对象，但list,dict, str,tuple是Iterable, 却不是Iterator.
iter([]),使用iter函数可以把Iterable变为Iterator.
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True
```



### 返回函数（闭包）：

```python
def count():
    def g(j):
            def f():
                return j * j
            return f
    fs = []
    for i in range(1,4):
        fs.append(g(i))
    return fs

f1,f2,f3 = count()
>>> f1()
1
>>> f2()
4
>>> f3()
9
```

需要注意内部函数（闭包）中不能引用外部会发生改变的变量，for 语句中的i也是会改变变量。如果要引用这种变量就要像上面示例中所示，再定义一层包装函数，把变量当成参数传入内部函数中。

使用闭包时，对外层变量赋值前，需要先使用nonlocal声明该变量不是当前函数的局部变量

```python
def inc():
    x = 0
    def fn():
        nonlocal x
        x = x + 1
        return x
    return fn

f = inc()
print(f()) # 1
print(f()) # 2
```

### 匿名函数(lambda):

```python
>>> f = lambda x: x*x
>>> f(5)
25
```

### 高价函数：

####  map:

`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。`map()`传入的第一个参数是`f`，即函数对象本身。由于结果`r`是一个`Iterator`，`Iterator`是惰性序列，因此通过`list()`函数让它把整个序列都计算出来并返回一个list。

```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

#### reduce:

`reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算，其效果就是：

```
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```

#### filter

和`map()`类似，`filter()`也接收一个函数和一个序列。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。

```python
>>> list(filter(lambda s: s and s.strip(), ['A','',"B", None,'C', ' '])) 
['A', 'B', 'C']
```

#### sort

sorted可对序列进行排序， 可以指定key函数实现自定义排序，指定reverse = True,反向排序 



## 错误处理

```python
try:
    print('try...')
    r = 10 / int('2')
    print('result:', r)
    if r==0:
        raise ValueError('invalid value: %s' % s)  //触发一个错误
except ValueError as e:
    print('ValueError:', e)
    raise ValueError('input error!')   //抛出新的异常
except ZeroDivisionError as e:
    print('ZeroDivisionError:', e)
    raise  //向上抛出
except (Error1, Error2,...) as e: //可以同时处理多种异常类型
    raise
else:
    print('no error!') //如果没有错误发生，可以在except语句块后面加一个else，当没有错误发生时，会自动执行else语句
finally:
    print('finally...')
print('END')

# args：返回异常的错误编号和描述字符串；
# str(e)：返回异常信息，但不包括异常信息的类型；
# repr(e)：返回较全的异常信息，包括异常信息的类型。

>>> try:
...     1/0
... except Exception as e:
...     # 访问异常的错误编号和详细信息
...     print(e.args)
...     print(str(e))
...     print(repr(e))
... 
('division by zero',)
division by zero
ZeroDivisionError('division by zero')
```

Python的错误其实也是class，所有的错误类型都继承自`BaseException`

import logging 可以打印，记录错误到文件

```python
 except Exception as e:
        logging.exception(e)
```

使用exec_info 组合traceback.print_tb获取详细错误信息

```python
import sys
import traceback

try:
    x = int(input('输入一个被除数:'))
    print('30 /',x,'=', 30/x)
except:
    print(sys.exc_info())
    print('')
    traceback.print_exc()
    print('')
    traceback.print_tb(sys.exc_info()[2])
    
 # 输出
输入一个被除数:0
(<class 'ZeroDivisionError'>, ZeroDivisionError('division by zero'), <traceback object at 0x0000000003DE7C80>)

Traceback (most recent call last):
  File "e:\code_python\code\tushare_stock\a.py", line 6, in <module>
    print('30 /',x,'=', 30/x)
ZeroDivisionError: division by zero

  File "e:\code_python\code\tushare_stock\a.py", line 6, in <module>
    print('30 /',x,'=', 30/x)
(myvenv) PS E:\code_python\code\tushare_stock> 
   
使用 traceback 模块查看异常传播轨迹，首先需要将 traceback 模块引入，该模块提供了如下两个常用方法：
traceback.print_exc()：将异常传播轨迹信息输出到控制台或指定文件中。
format_exc()：将异常传播轨迹信息转换成字符串。
当程序处于 except 块中时，该 except 块所捕获的异常信息可通过 sys 对象来获取，其中 sys.exc_type、sys.exc_value、sys.exc_traceback 就代表当前 except 块内的异常类型、异常值和异常传播轨迹。
```



## 调试

assert n != 0, 'n is zeror'  //果到处充斥着`assert`，和`print()`相比也好不到哪去。不过，启动Python解释器时可以用`-O`参数来关闭`assert`   注意：断言的开关“-O”是英文大写字母O，不是数字0

```
$ python -O err.py
```

## 对象

以下演示了类属性与实例属性

```python
>>> class Student(object):
...     name = 'Student'
...
>>> s = Student() # 创建实例s
>>> print(s.name) # 打印name属性，因为实例并没有name属性，所以会继续查找class的name属性
Student
>>> print(Student.name) # 打印类的name属性
Student
>>> s.name = 'Michael' # 给实例绑定name属性
>>> print(s.name) # 由于实例属性优先级比类属性高，因此，它会屏蔽掉类的name属性
Michael
>>> print(Student.name) # 但是类属性并未消失，用Student.name仍然可以访问
Student
>>> del s.name # 如果删除实例的name属性
>>> print(s.name) # 再次调用s.name，由于实例的name属性没有找到，类的name属性就显示出来了
Student
```

#### 动态绑定实例方法：

```python
>>> def set_age(self, age): # 定义一个函数作为实例方法
...     self.age = age
...
>>> from types import MethodType
>>> s.set_age = MethodType(set_age, s) # 给实例绑定一个方法
>>> s.set_age(25) # 调用实例方法
>>> s.age # 测试结果
```

MethodType 就是type( 实例.一个方法),用type通过一个现有的实列方法获取取类型。然后再强制转换动态方法到要赋的实例上。

#### 动态绑定类方法：

```python
>>> def set_score(self, score):
...     self.score = score
...
>>> Student.set_score = set_score
```

绑定类方法后，之前和之后创建的类实例都可以使用该方法。

`__slots__` 限制类实列可添加的属性：

```python
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```

`__slots__` 仅对当前类实例有用，对继承的子类无作用。















# VS Code Python

**示**：如果 activate 命令生成消息“Activate.ps1 is not digitally signed. You cannot run this script on the current system.”，则需要临时更改 PowerShell 执行策略以允许脚本运行（请参阅[关于执行策略](https://go.microsoft.com/fwlink/?LinkID=135170)在 PowerShell 文档中）： 

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process

```

创建虚拟环境：python -m venv myvenv





# Python使用pip更新所有已安装包的方法



[https://blog.csdn.net/sunqiande88/article/details/80155587](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.csdn.net%2Fsunqiande88%2Farticle%2Fdetails%2F80155587)

pip install --upgrade pip 升级pip自身

列出当前安装的包：

pip list
列出可升级的包：

pip list --outdate

更新某一个模块：　　　　　pip install --upgrade itchat

第二：使用pip批量更新

批量下载并更新：
pip install pip-review
pip-review --local --interactive
pip-review --auto

哪个包出错，就单独先安装好那个包 pip install --upgrade itchat
问题出个无法更新 pycurl 这个包，可以先单独把这个包更新以后再重新运行 pip-review --auto 命令。顺便吐槽一下，这个命令好像是先全部下载下来所有更新包以后再安装？所以中间出了一个错误就全部安装失败了。。



# Python 修改 pip 源为国内源

在 python 里经常要安装各种这样的包，安装各种包时最常用的就是 pip，pip 默认从官网下载文件，官网位于国外，下载速度时快时慢，还经常断线，国内的体验并不太好。

解决办法是把 pip 源换成国内的，最常用的并且可信赖的源包括清华大学源、豆瓣源、阿里源：

> pypi 清华大学源：[https://pypi.tuna.tsinghua.edu.cn/simple](https://link.zhihu.com/?target=https%3A//pypi.tuna.tsinghua.edu.cn/simple)
> pypi 豆瓣源 ：[http://pypi.douban.com/simple/](https://link.zhihu.com/?target=http%3A//pypi.douban.com/simple/)
> pypi 腾讯源：[http://mirrors.cloud.tencent.com/pypi/simple](https://link.zhihu.com/?target=http%3A//mirrors.cloud.tencent.com/pypi/simple)
> pypi 阿里源：[https://mirrors.aliyun.com/pypi/simple/](https://link.zhihu.com/?target=https%3A//mirrors.aliyun.com/pypi/simple/)

pip 源具体修改方式是，我们以安装 python 的 markdown 模块为例，通常的方式是直接在命令行运行

```bash
pip install markdown
```

这样会从国外官网下载markdown模块并安装。

若要把 pip 源换成国内的，只需要把上面的代码改成下图这样（下图以清华大学源为例）：

```text
pip install markdown -i https://pypi.tuna.tsinghua.edu.cn/simple
```

![img](python学习.assets\v2-cfc8ee29213ff52ee39d831f14b05f89_720w.jpg)

这样我们就从清华大学源成功安装了markdown模块，速度会比过pip默认的国外源快很多。

上述做法是临时改成国内源，如果不想每次用 pip 都加上 -i [https://pypi.tuna.tsinghua.edu.cn/simple](https://link.zhihu.com/?target=https%3A//pypi.tuna.tsinghua.edu.cn/simple)，那么可以把国内源设为默认，做法是：

```bash
# 清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 或：
# 阿里源
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
# 腾讯源
pip config set global.index-url http://mirrors.cloud.tencent.com/pypi/simple
# 豆瓣源
pip config set global.index-url http://pypi.douban.com/simple/
```

# OS模块文件与目录操作

参考：https://www.cnblogs.com/cherishry/p/5725977.html

http://www.ityouknow.com/python/2019/10/09/python-os-demonstration-026.html

# Logging日志模块

http://www.ityouknow.com/python/2019/10/13/python-logging-032.html

# 生成requirements.txt

```
# 生成依赖包文件
pip freeze > requirements.txt
# 安装依赖文件
pip install -r requirements.txt

```



# IIS 部署 python web框架 Flask

https://blog.51cto.com/luyaliang/1949849

https://zhuanlan.zhihu.com/p/36549676





# Flask

### 路由

```python
@app.route('/python‘)
@app.route('/python/')
这两个规则看起来类似，但在第二个规则中，使用斜杠（/）。使用 /python 或 /python/返回相同的输出。

但是，如果是第一个规则，/flask/ URL会产生“404 Not Found”页面。
           
           
```



### url_for

```python
bp = Blueprint('doc', __name__, url_prefix = '/doc', static_folder='/doc/static')
 url_for('static', filename = 'style.css') 
  >> /static/style.css

#url_for 第一个参数可以指定蓝图的名字，蓝图已用该名字注册到的路由规则中。
 url_for('doc.static', filename = 'style.css')  
>> /doc/static/style.css    
# 相对当前所在路由设置
url_for('.static', hah = 'style.css')
>> /doc/static/style.css    

# 从当前文件的函数名返回其路径（附带参数）
url_for('.page', app = 'app',  page =  'index')
>> /doc/app/index
```

### Buleprint

蓝图有个坑，就是不管路由中注册了多少,查找static, template时总是从第一个注册的里边开始找。

所以后边注册的一定要注意不能跟其它有重名文件。不然就会引用到其它的里边的文件。

```python
bp = Blueprint('doc', __name__, url_prefix = '/doc', static_folder='static', template_folder='templates')
这里的static, templates指的都是相对于当前包。但实际又可能会因为重名，而导致实际采用的文件是其它文件夹。所以最好还是不用吧。要用就类似这样
youapp/doc/templates/doc/vv.css 通过将所有内容放在一个子目录下。避免跟其它路径有重名文件。但实际注意事项太多。还不如都放在/static/doc这样分隔好。至少在nginx中可以指定一个静态目录。
```

