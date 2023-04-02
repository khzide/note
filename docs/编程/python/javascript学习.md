# JavaScript学习

### 基本语法

变量区分大小写

变量声明与赋值:

var a;  //仅声明  a = undefined

**不加var 直接使用a 时，会创建全局变量a** 

### 变量提升

JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

```
console.log(a);
var a = 1;
```

上面代码首先使用`console.log`方法，在控制台（console）显示变量`a`的值。这时变量`a`还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码。

```
var a;
console.log(a);
a = 1;
```

最后的结果是显示`undefined`，表示变量`a`已声明，但还未赋值。

### 注释

```
/*多行*/  //单行`
```



### 区块

```
{

var a = 1;`

}

a  //1
```

JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。

对于`var`命令来说，JavaScript 的区块不构成单独的作用域（scope）。

上面代码在区块内部，使用`var`命令声明并赋值了变量`a`，然后在区块外部，变量`a`依然有效，区块对于`var`命令不构成单独的作用域，与不使用区块的情况没有任何区别



### switch语句

```
var a = 2;
switch(a){
    case 1:
        console.log(1);
    case 2:
        console.log(2);
    case 3:
        console.log(3);
    case 4:
        console.log(4);
        break;
    case 5:
        console.log(5);
    default:
        console.log('default')
}
>2
>3
>4
```

`switch`语句后面的表达式，与`case`语句后面的表示式比较运行结果时，采用的是严格相等运算符（`===`），而不是相等运算符（`==`），这意味着比较时不会发生类型转换。

另外注意case语句中要加break; 否则会一直执行下去。

### 标签Label

break; continue可以跳转到标签

```
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top; //跳出多层循环
      console.log('i=' + i + ', j=' + j);
    }
  }
  
  foo: {
  console.log(1);
  break foo;  //标签也可以用于跳出代码块。
  console.log('本行不会输出');
}
console.log(2);
```

break; 中断当前语句块或指定Label标签块。

continue; 直接进入下次循环，或进入标签名指定的循环。

## 数据类型

### 特殊数据类类型 ：

NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity

== 自动进行类型转换再比较

===  不进行自动类型转换

NaN  不与类型类型相等，包它自已。唯一运算符是isNaN(NaN).

 注意浮点数比较有误差，1 / 3 === (1 - 2 / 3); // false

所以浮点数比较只能比较差值在一个小的阈值范围内。  Math.abc(1/3 - (1-2/3)) < 0.0000001 // true

null 表示空， underfined 表示未定义。 一般区分二者意义不大。我们都应该用`null`。`undefined`仅仅在判断函数参数是否传递的情况下有用。

变量可以是&或_开头。

变量未声明就使用会自动创建一个全局变量，（多问题用同一变量名时就会出现混乱）。所以就有了'use strict';严格模式，强制要求变量使用前加var声明。





类型判断三种方法:

- typeof  运算符
- instanceof 运算符
- Object.prototype.toString 方法

```
//变量是否存在判断
if (typeof x === 'undefined')

```

### null undefined

兼容问题：

```
typeof null
>'object'
typeof undefined
>'undefined'
//布尔运算中 null, undefined都会转化为false
undefined == null
>true
//数值运算中
null转化为0
undefined 转化为NaN.

Number(null)
>0
5+null
>5
Number(undefined)
>NaN
5+undefined
>NaN
```

### bool

下列运算符会返回布尔值：

- 前置逻辑运算符： `!` (Not)
- 相等运算符：`===`，`!==`，`==`，`!=`
- 比较运算符：`>`，`>=`，`<`，`<=`

如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为`false`，其他值都视为`true`。

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- `""`或`''`（空字符串）

### 整数和浮点数

JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。

```
1=== 1.0 //true
```

浮点数运算结果并不精确，所以比较大小时要注意不要直接比较

```
> 1===1.0
true
> 0.1+0.2 === 0.3
false
> 0.3 / 0.1
2.9999999999999996
> 0.3-0.2
0.09999999999999998
```

进制：

0xff  //16进制

0o77 //8进制

0b11 //二进制

有前导0的数值会视为8进制，但如果后边出现8以上，则视为10进制.

0777 //8进制

0898 //10进制



NaN 表示“非数字" （Not a Number）主要出现在将字符串解析成数字出错的场合。

NaN 类型是Number.

5-'x'  //Nan

```
typeof NaN //'number'
```

isFinite()  //表示某个值是否为正常的数值。

isNaN() //判断一个值是否为`NaN`。



### 字符串

单引号或双引号可以互相嵌套。

字符串中加\\'表示转义

- `\0` ：null（`\u0000`）
- `\b` ：后退键（`\u0008`）
- `\f` ：换页符（`\u000C`）
- `\n` ：换行符（`\u000A`）
- `\r` ：回车键（`\u000D`）
- `\t` ：制表符（`\u0009`）
- `\v` ：垂直制表符（`\u000B`）
- `\'` ：单引号（`\u0027`）
- `\"` ：双引号（`\u0022`）
- `\\` ：反斜杠（`\u005C`）

多行字符串：

```
> var mutistr = 'Long \
... long \
... string';
undefined
> mutistr
'Long long string'
```

反斜杠还有三种特殊用法。

（1）`\HHH`

反斜杠后面紧跟三个八进制数（`000`到`377`），代表一个字符。`HHH`对应该字符的 Unicode 码点，比如`\251`表示版权符号。显然，这种方法只能输出256种字符。

（2）`\xHH`

`\x`后面紧跟两个十六进制数（`00`到`FF`），代表一个字符。`HH`对应该字符的 Unicode 码点，比如`\xA9`表示版权符号。这种方法也只能输出256种字符。

（3）`\uXXXX`

`\u`后面紧跟四个十六进制数（`0000`到`FFFF`），代表一个字符。`XXXX`对应该字符的 Unicode 码点，比如`\u00A9`表示版权符号。



## 算数运算符

- **加法运算符**：`x + y`
- **减法运算符**： `x - y`
- **乘法运算符**： `x * y`
- **除法运算符**：`x / y`
- **指数运算符**：`x ** y`
- **余数运算符**：`x % y`
- **自增运算符**：`++x` 或者 `x++`
- **自减运算符**：`--x` 或者 `x--`
- **数值运算符**： `+x`
- **负数值运算符**：`-x`



### +

两数值相加结果为数值，有字符串的，自动转化为字符串相连.

true,false与字符串相加时，转为字符串'true','false'. 与数值相加时，转为1或0.

```
> 1+1
2
> true+true
2
> 1+true
2
> 1+NaN
NaN
> 1+Infinity
Infinity
> 'a' + 'ab'
'aab'
> 1+'a'
'1a'
> 'a' + 1
'a1'
> '3' + 1
'31'
> 1+ '3'
'13'
> '3' + 4 + 5
'345'
> 4+5+'3'
'93'
> false + 2
2
> false +'abc'
'falseabc'
>
```

除+运算符外，其它算术运算符（如-,/,*）都一律转为数值，再运算。

```
> 1-'2'
-1
> 2*'2'
4
> 1/'2'
0.5
> 1-true
0
> 1-false
1
> true-false
1
> 1-'3a'
NaN
>
```



### 对象的相加：

运算子是对象时，必须转化为原始类型的值。

转化规则如下：

  自动调用valueof(), 一般valueof()会返回对象自身，这时再调用toString().

如果自定义了valueof函数，则不再调用toString.

特例是Date 类型，它是直接调用toString()

```
> var obj = {p:1};
undefined
> obj
{ p: 1 }
> obj.valueOf()
{ p: 1 }
> obj.valueOf().toString()
'[object Object]'
> obj.valueOf = function(){
... return 100;
... }
[Function (anonymous)]
> obj.valueOf()
100
> 1+ obj
101
> obj
{ p: 1, valueOf: [Function (anonymous)] }
> obj.valueOf()
100
> obj.toString()
'[object Object]'
> obj.toString = function(){
... return 's100';
... }
[Function (anonymous)]
> obj.toString()
's100'
> 1+ obj
101
> delete obj.valueOf
true
> 1+ obj
'1s100'
> var myo ={p:2};
undefined
> 1+myo
'1[object Object]'
> myo.valueOf()
{ p: 2 }
> myo.toString()
'[object Object]'
```

```
var obj = new Date();
obj.valueOf = function () { return 1 };
obj.toString = function () { return 'hello' };

obj + 2 // "hello2"
```

### 一元+，-

数值运算符（`+`）同样使用加号，但它是一元运算符（只需要一个操作数），而加法运算符是二元运算符（需要两个操作数）。

数值运算符的作用在于可以将任何值转为数值（与`Number`函数的作用相同）。

```
+true // 1
+[] // 0
+{} // NaN
```

2**4 = 16  指数运算符.

2 ** 3 ** 2  指数运算符是右结合，先计算最右边。

## 比较运算符

JavaScript 一共提供了8个比较运算符。

- `>` 大于运算符
- `<` 小于运算符
- `<=` 小于或等于运算符
- `>=` 大于或等于运算符
- `==` 相等运算符(比较的是值是否相等，比较值时对象可以进行转化。)
- `===` 严格相等运算符(比较的是它们是否是“同一个值", 或者说比较时不进行类型转换。)
- `!=` 不相等运算符
- `!==` 严格不相等运算符

对于非相等的比较，如>< ==  . 比较算法是先看运算子是否都是字符串，如果是，则按字典顺序比较（实际就是比较unicode码). 否则，将运算子转化为数值，再进行比较。

\* NaN 与任何非相等运算符进行比较，结果都是false.

```
1 > NaN // false
1 <= NaN // false
'1' > NaN // false
'1' <= NaN // false
NaN > NaN // false
NaN <= NaN // false
```

如果比较的运算子有一个不是字符串，则会将所有运算子转化为数值再进行比较。

如果比较运算子是object. 则会将object调用valueof(), toString()后进行比较。两个复合类型（对象，数组，函数）进行比较时，比较的是它们是否指向同一个地址。Date类型是直接调用toString. 而不调用valueof().

```
> 1 == '1'
true
> 1 == true
true
> 1 === 1
true
> 1=== '1'
false
> 1 === true
false
```



**undefined 和 null**

`undefined`和`null`与自身__严格__相等。

```
undefined === undefined // true
null === null // true

var v1;
var v2;
v1 === v2  //true.  
```

