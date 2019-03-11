# 基本语法

## 1. python基础

### 1.字符串和编码

1.转义符

| 转义字符 | 意义 | ASCII码值（十进制） |
| :--- | :--- | :--- |
| \a | 响铃\(BEL\) | 007 |
| \b | 退格\(BS\) ，将当前位置移到前一列 | 008 |
| \f | 换页\(FF\)，将当前位置移到下页开头 | 012 |
| \n | 换行\(LF\) ，将当前位置移到下一行开头 | 010 |
| \r | 回车\(CR\) ，将当前位置移到本行开头 | 013 |
| \t | 水平制表\(HT\) （跳到下一个TAB位置） | 009 |
| \v | 垂直制表\(VT\) | 011 |
| \\ | 代表一个反斜线字符''\' | 092 |
| \' | 代表一个单引号（撇号）字符 | 039 |
| \" | 代表一个双引号字符 | 034 |
| \? | 代表一个问号 | 063 |
| \0 | 空字符\(NUL\) | 000 |
| \ddd | 1到3位八进制数所代表的任意字符 | 三位八进制 |
| \xhh | 1到2位十六进制所代表的任意字符 | 二位十六进制 |

2. ASIC & Unicode & utf-8

ASIC编码为一个字节，Unicode为2个字节，utf-8为可变长编码，根据不同数据大小编码为1~6个字节，ASIC编码被看做utf-8编码的一部分

* 在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码
* 保存源码时，需指定为utf-8编码

```python
#!/usr/bin/env python3  告知linux系统该文件为可执行程序，Windows会忽略这个注释
#-*- coding : utf-8 -*- 告知python解释器按照utf-8读取源代码
```

3. 字符串格式化

| 占位符 | 替换内容 |
| :--- | :--- |
| %d | 整数 |
| %f | 浮点数 |
| %s | 字符串 |
| %x | 十六进制整数 |

 另一种格式化字符串的方法是使用字符串的`format()`方法，它会用传入的参数依次替换字符串内的占位符`{0}`、`{1}`

```python
>>> 'Age: %s. Gender: %s' % (25, True)
'Age: 25. Gender: True'
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%
```

### 2. 循环

 `break`语句可以在循环过程中直接退出循环，而`continue`语句可以提前结束本轮循环，并直接开始下一轮循环。这两个语句通常都_必须_配合`if`语句使用

```python
n = 1
while n <= 100:
    if n > 10: # 当n = 11时，条件满足，执行break语句
        break # break语句会结束当前循环
    print(n)
    n = n + 1
print('END')

n = 0
while n < 10:
    n = n + 1
    if n % 2 == 0: # 如果n是偶数，执行continue语句
        continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
    print(n)
```

### 3.函数

1）return

函数体内部的语句在执行时，一旦执行到`return`时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。

 如果没有`return`语句，函数执行完毕后也会返回结果，只是结果为`None`。`return None`可以简写为`return`。

* ​用`from abstest import my_abs`来导入`my_abs()`函数，注意`abstest`是文件名（不含`.py`扩展名）

2）函数参数

在Python中定义函数，可以用`必选参数、默认参数、可变参数、命名关键字参数、关键字参数`

* 默认参数：默认参数必须指向不变对象
* 命名关键字参数： 命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数； 如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符`*`

```python
def person(name, age, *, city, job):  #只接收city和job作为关键字参数
    print(name, age, city, job)
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

```python
def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)
    
>>> f1(1, 2)
a = 1 b = 2 c = 0 args = () kw = {}
>>> f1(1, 2, c=3)
a = 1 b = 2 c = 3 args = () kw = {}
>>> f1(1, 2, 3, 'a', 'b')
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}
>>> f1(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
>>> f2(1, 2, d=99, ext=None)
a = 1 b = 2 c = 0 d = 99 kw = {'ext': None}

>>> args = (1, 2, 3, 4)
>>> kw = {'d': 99, 'x': '#'}
>>> f1(*args, **kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'d': 99, 'x': '#'}
>>> args = (1, 2, 3)
>>> kw = {'d': 88, 'x': '#'}
>>> f2(*args, **kw)
a = 1 b = 2 c = 3 d = 88 kw = {'x': '#'}
```

{% hint style="info" %}
`*args`是可变参数，args接收的是一个tuple；

`**kw`是关键字参数，kw接收的是一个dict。

可变参数既可以直接传入：`func(1, 2, 3)`，又可以先组装list或tuple，再通过`*args`传入：`func(*(1, 2, 3))`；

关键字参数既可以直接传入：`func(a=1, b=2)`，又可以先组装dict，再通过`**kw`传入：`func(**{'a': 1, 'b': 2})`
{% endhint %}

### 4.列表生成器 \| 生成器

```python
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```

一边循环一边计算的机制，称为生成器， 如果要一个一个打印出来，可以通过`next()`函数获得generator的下一个返回值 ，直到计算到最后一个元素，没有更多的元素时，抛出`StopIteration`的错误。

另外一种定义生成器的方法函数中将 `print(b)`改为`yield b`

* 函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回；普通函数返回结果
* generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行；生成器函数返回的是generator对象

```python
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> next(g)
0
>>> next(g)
1
>>> next(g)
4

def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done
```

### 5.迭代器

集合数据类型，如`list`、`tuple`、`dict`、`set`、`str`等；`generator`，包括生成器和带`yield`的generator function。

这些可以直接作用于`for`循环的对象统称为可迭代对象：`Iterable`

 可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`

## 2.一些代码栗子

### 1.汉诺塔问题

 `move(n, a, b, c)`函数，它接收参数`n`，表示3个柱子A、B、C中第1个柱子A的盘子数量，然后打印出把所有盘子从A借助B移动到C的方法

```python
# 无论多少个圆块，可以抽象成为同一套思路：就是想办法把(n-1)个a柱上的圆块先移动到b柱，然后把最底部最大的一个圆块移动到c柱，最后把b柱上的(n-1)个圆块移动到c柱
def hanoi(n, a, buffer, c):
    if n == 1:
        print(a, '--->', c) # 定义从a柱移动到c柱的操作
    else:
        hanoi(n-1, a, c, buffer) # 把(n-1)个a柱上的圆块移动到缓冲区buffer柱
        hanoi(1, a, buffer, c) # 把最底部的最大的圆块移动到c柱
        hanoi(n-1, buffer, a, c) # 把(n-1)个缓冲区buffer柱上的圆块移动到c柱

hanoi(3, 'A', 'B', 'C')
```



### 2.杨辉三角



```text
          1
         / \
        1   1
       / \ / \
      1   2   1
     / \ / \ / \
    1   3   3   1
   / \ / \ / \ / \
  1   4   6   4   1
 / \ / \ / \ / \ / \
1   5   10  10  5   1
```

把每一行看做一个list，试写一个generator，不断输出下一行的list

```python
def triangles():
    L = [1]
    while True:
        yield L
        L = [1] + [L[i] + L[i+1] for i in range(len(L)-1)] + [1]
```

