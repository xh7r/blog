# 语言元素

## 注释

单行注释：#

多行注释：    ““”

​                     “”“

​                     或

​                     ‘’‘

​                     ‘‘’



## 变量和数据类型

搞一个新的变量时，变量前不需要定义它的数据类型。如：直接a=1

数据类型：整型：int #python中整型只有int一种类型。浮点型：float。布尔型：bool：Ture，False。字符串型：str。复数型：形如3+5j，跟数学上的复数表示一样，唯一不同的是虚部的i换成了j。complex。

type()检查变量的类型。如：print(type(a))

 

可以使用Python中内置的函数对变量类型进行转换。  

int()：将一个数值或（数值）字符串转换成整数，可以指定进制。

float()：将一个（数值）字符串转换成浮点数。

str()：将指定的对象转换成字符串形式，可以指定编码。

chr()：将整数转换成该编码对应的字符串（一个字符）。

ord()：将字符串（一个字符）转换成对应的编码（整数）

input()函数：获取键盘输入的(字符串)

## 运算符

 

print('%d %% %d = %d' % (a, b, a % b))

其中%d是整数的占位符，%f是小数的占位符，%%表示百分号（因为百分号代表了占位符，所以带占位符的字符串中要表示百分号必须写成%%），字符串之后的%后面跟的变量值会替换掉占位符然后输出到终端中     

 

| **运算符**                    | **描述**                       |
| ----------------------------- | ------------------------------ |
| [] [:]                        | 下标，切片                     |
| **                            | 指数                           |
| ~ + -                         | 按位取反, 正负号               |
| * / % //                      | 乘，除，模，整除               |
| + -                           | 加，减                         |
| >> <<                         | 右移，左移                     |
| &                             | 按位与                         |
| ^ \|                          | 按位异或，按位或               |
| <= < > >=                     | 小于等于，小于，大于，大于等于 |
| == !=                         | 等于，不等于                   |
| is is not                     | 身份运算符                     |
| in not in                     | 成员运算符                     |
| not or and                    | 逻辑运算符                     |
| = += -= *= /= %= //= **= &= ` | = ^= >>= <<=`                  |

**说明：**（优先级从高到低） 在实际开发中，如果搞不清楚运算符的优先级，可以使用括号来确保运算的执行顺序

 

 

print('%.1f华氏度 = %.1f摄氏度' % (f, c))

**说明**：在使用print函数输出时，也可以对字符串内容进行格式化处理，上面print函数中的字符串%.lf是一个占位符，稍后会由一个float类型的变量值替换掉它。同理，如果字符串中有%d，后面可以用一个int类型的变量值替换掉它，而%s会被字符串的值替换掉。除了这种格式化字符串的方式外，还可以用下面的方式来格式化字符串，其中{f:.lf}和{c:.lf}可以先看成是{f}和{c}，表示输出时会用变量f和变量c的值替换掉这两个占位符，后面的:.lf表示这是一个浮点数，小数点后保留1位有效数字。

print(f'{f:.1f}华氏度 = {c:.1f}摄氏度')

## 代码折行

\# 如果代码太长写成一行不便于阅读 可以使用\对代码进行折行

is_leap = year % 4 == 0 and year % 100 != 0 or \

​          year % 400 == 0

print(is_leap)

end=’’

print("\t",end='');

包含end=''作为print()BIF的一个参数，会使该函数关闭“在输出中自动包含换行”的默认行为

 

# 分支结构

## IF语句：

```python
If 条件语句 ：

       执行语句

Elif 条件语句 ：

       执行语句

Else：

      执行语句
```



**注意**：和C/C++、Java等语言不同，Python中没有用花括号来构造代码块而是使用了缩进的方式来表示代码的层次结构，如果if条件成立的情况下需要执行多条语句，只要保持多条语句具有相同的缩进就可以了。换句话说连续的代码如果又保持了相同的缩进那么它们属于同一个代码块，相当于是一个执行的整体。缩进可以使用任意数量的空格，但通常使用4个空格

# 循环结构

## For-in循环

```python


for x in range(101):

    sum += x

print(sum)
```



需要说明的是上面代码中的range(1, 101)可以用来构造一个从1到100的范围，当我们把这样一个范围放到for-in循环中，就可以通过前面的循环变量x依次取出从1到100的整数。当然，range的用法非常灵活，下面给出了一个例子：

range(101)：可以用来产生0到100范围的整数，需要注意的是取不到101。

range(1, 101)：可以用来产生1到100范围的整数，相当于前面是闭区间后面是开区间。

range(1, 101, 2)：可以用来产生1到100的奇数，其中2是步长，即每次数值递增的值。

range(100, 0, -2)：可以用来产生100到1的偶数，其中-2是步长，即每次数字递减的值。

## While循环

While 逻辑表达式：

## 循环的终止：break和continue

break只能终止它所在的那个循环，除了break之外，还有另一个关键字是continue，它可以用来放弃本次循环后续的代码直接让循环进入下一轮。

# 函数和模块的使用

## 函数的定义

在Python中可以使用def关键字来定义函数，和变量一样每个函数也有一个响亮的名字，而且命名规则跟变量的命名规则是一致的。在函数名后面的圆括号中可以放置传递给函数的参数，这一点和数学上的函数非常相似，程序中函数的参数就相当于是数学上说的函数的自变量，而函数执行完成后我们可以通过return关键字来返回一个值，这相当于数学上说的函数的因变量。

## 函数的参数

函数是绝大多数编程语言中都支持的一个代码的"构建块"，但是Python中的函数与其他语言中的函数还是有很多不太相同的地方，其中一个显著的区别就是Python对函数参数的处理。**在Python中，函数的参数可以有默认值**，也支持使用可变参数，所以Python并不需要像其他语言一样支持函数的重载，因为我们在定义一个函数的时候可以让它有多种不同的使用方式，

## 可变参数

```python
# 在参数名前面的*表示args是一个可变参数

def add(*args):

   total = 0

   for val in args:

        total += val

        return total
        
        # 在调用add函数时可以传入0个或多个参数

print(add())

print(add(1))

print(add(1, 2))

print(add(1, 2, 3))

print(add(1, 3, 5, 7, 9))
```

 

## 用模块管理函数

对于任何一种编程语言来说，给变量、函数这样的标识符起名字都是一个让人头疼的问题，因为我们会遇到命名冲突这种尴尬的情况。最简单的场景就是在同一个.py文件中定义了两个同名函数，由于Python没有函数重载的概念，那么后面的定义会覆盖之前的定义，也就意味着两个函数同名函数实际上只有一个是存在的。

当然上面的这种情况我们很容易就能避免，但是如果项目是由多人协作进行团队开发的时候，团队中可能有多个程序员都定义了名为foo的函数，那么怎么解决这种命名冲突呢？答案其实很简单，Python中每个文件就代表了一个模块（module），我们在不同的模块中可以有同名的函数，在使用函数的时候我们通过import关键字导入指定的模块就可以区分到底要使用的是哪个模块中的foo函数

```python
from module1 import foo

 

\# 输出hello, world!

foo()

 

from module2 import foo

 

\# 输出goodbye, world!

foo()
```

也可以按照如下所示的方式来区分到底要使用哪一个foo函数。

```python
import module1 as m1

import module2 as m2

 

m1.foo()

m2.foo()
```

但是如果将代码写成了下面的样子，那么程序中调用的是最后导入的那个foo，因为后导入的foo覆盖了之前导入的foo

```python
from module1 import foo

from module2 import foo

 

\# 输出goodbye, world!

foo()
```

 

注意：需要说明的是，如果我们导入的模块除了定义函数之外还有可以执行代码，那么Python解释器在导入这个模块时就会执行这些代码，事实上我们可能并不希望如此，因此如果我们在模块中编写了执行代码，最好是将这些执行代码放入如下所示的条件中（放于if语句中），这样的话除非直接运行该模块，if条件下的这些代码是不会执行的，因为只有直接执行的模块的名字才是"__main__"。

 

\# __name__是Python中一个隐含的变量它代表了模块的名字

\# 只有被Python解释器直接执行的模块的名字才是__main__

`if __name__ == '__main__'：`

 # 变量的作用域



```python
def foo():
    a = 200
    print(a)  # 200


if __name__ == '__main__':
    a = 100
    foo()
    print(a)  # 100
```

看看上面这段代码，我们希望通过函数调用修改全局变量`a`的值，但实际上下面的代码是做不到的。

在调用`foo`函数后，我们发现`a`的值仍然是100，这是因为当我们在函数`foo`中写`a = 200`的时候，是重新定义了一个名字为`a`的局部变量，它跟全局作用域的`a`并不是同一个变量，因为局部作用域中有了自己的变量`a`，因此`foo`函数不再搜索全局作用域中的`a`。如果我们希望在`foo`函数中修改全局作用域中的`a`，代码如下所示。

```python
def foo():
    global a
    a = 200
    print(a)  # 200


if __name__ == '__main__':
    a = 100
    foo()
    print(a)  # 200
```

# 字符串和常用数据结构

## 字符串

### 字符串的输入

```python
s1 = 'hello, world!'
s2 = "hello, world!"
# 以三个双引号或单引号开头的字符串可以折行
s3 = """
hello, 
world!
"""
print(s1, s2, s3, end='')
```



可以在字符串中使用`\`（反斜杠）来表示转义，也就是说`\`后面的字符不再是它原来的意义，例如：`\n`不是代表反斜杠和字符n，而是表示换行；而`\t`也不是代表反斜杠和字符t，而是表示制表符。所以如果想在字符串中表示`'`要写成`\'`，同理想表示`\`要写成`\\`。可以运行下面的代码看看会输出什么。

```python
s1 = '\'hello, world!\''
s2 = '\n\\hello, world!\\\n'
print(s1, s2, end='')
```

在`\`后面还可以跟一个八进制或者十六进制数来表示字符，例如`\141`和`\x61`都代表小写字母`a`，前者是八进制的表示法，后者是十六进制的表示法。也可以在`\`后面跟Unicode字符编码来表示字符，例如`\u9a86\u660a`代表的是中文“骆昊”。运行下面的代码，看看输出了什么

```python
s1 = '\141\142\143\x61\x62\x63'
s2 = '\u9a86\u660a'
print(s1, s2)
```

如果不希望字符串中的`\`表示转义，我们可以通过在字符串的最前面加上字母`r`来加以说明，再看看下面的代码又会输出什么。

```python
s1 = r'\'hello, world!\''
s2 = r'\n\\hello, world!\\\n'
print(s1, s2, end='')
```

### 字符串的运算符

Python为字符串类型提供了非常丰富的运算符，我们可以使用`+`运算符来实现字符串的拼接，可以使用`*`运算符来重复一个字符串的内容，可以使用`in`和`not in`来判断一个字符串是否包含另外一个字符串（成员运算），我们也可以用`[]`和`[:]`运算符从字符串取出某个字符或某些字符（切片运算），代码如下所示。

```python
s1 = 'hello ' * 3
print(s1) # hello hello hello 
s2 = 'world'
s1 += s2
print(s1) # hello hello hello world
print('ll' in s1) # True
print('good' in s1) # False
str2 = 'abc123456'
# 从字符串中取出指定位置的字符(下标运算)
print(str2[2]) # c
# 字符串切片(从指定的开始索引到指定的结束索引)
print(str2[2:5]) # c12
print(str2[2:]) # c123456
print(str2[2::2]) # c246
print(str2[::2]) # ac246
print(str2[::-1]) # 654321cba
print(str2[-3:-1]) # 45
```

### 用函数处理字符串

在Python中，我们还可以通过一系列的方法来完成对字符串的处理，代码如下所示。

```python
str1 = 'hello, world!'
# 通过内置函数len计算字符串的长度
print(len(str1)) # 13
# 获得字符串首字母大写的拷贝
print(str1.capitalize()) # Hello, world!
# 获得字符串每个单词首字母大写的拷贝
print(str1.title()) # Hello, World!
# 获得字符串变大写后的拷贝
print(str1.upper()) # HELLO, WORLD!
# 从字符串中查找子串所在位置
print(str1.find('or')) # 8
print(str1.find('shit')) # -1
# 与find类似但找不到子串时会引发异常
# print(str1.index('or'))
# print(str1.index('shit'))
# 检查字符串是否以指定的字符串开头
print(str1.startswith('He')) # False
print(str1.startswith('hel')) # True
# 检查字符串是否以指定的字符串结尾
print(str1.endswith('!')) # True
# 将字符串以指定的宽度居中并在两侧填充指定的字符
print(str1.center(50, '*'))
# 将字符串以指定的宽度靠右放置左侧填充指定的字符
print(str1.rjust(50, ' '))
str2 = 'abc123456'
# 检查字符串是否由数字构成
print(str2.isdigit())  # False
# 检查字符串是否以字母构成
print(str2.isalpha())  # False
# 检查字符串是否以数字和字母构成
print(str2.isalnum())  # True
str3 = '  jackfrued@126.com '
print(str3)
# 获得字符串修剪左右两侧空格之后的拷贝
print(str3.strip())
```

### 格式化输出字符串

我们之前讲过，可以用下面的方式来格式化输出字符串。

```python
a, b = 5, 10
print('%d * %d = %d' % (a, b, a * b))
```

当然，我们也可以用字符串提供的方法来完成字符串的格式，代码如下所示。

```python
a, b = 5, 10
print('{0} * {1} = {2}'.format(a, b, a * b))
```

Python 3.6以后，格式化字符串还有更为简洁的书写方式，就是在字符串前加上字母`f`，我们可以使用下面的语法糖来简化上面的代码。

```python
a, b = 5, 10
print(f'{a} * {b} = {a * b}')
```

## 列表

### 列表的增减调用

在列表中每个值对应的下标从0开始。也就是说第一个数的下标为0，以此类推。

```python
list1 = [1,2,3,4,5]
print(list1[0]) #1
print(list1[4]) #5
print(list1[-1]) #5
print(list1[-3]) #3
# 可以通过list1[]取出列表中的值
len(list1) #5
```

下面的代码演示了如何向列表中添加元素以及如何从列表中移除元素。

```python
list1 = [1, 3, 5, 7, 100]
# 添加元素
list1.append(200)
list1.insert(1, 400)
# 合并两个列表
# list1.extend([1000, 2000])
list1 += [1000, 2000]
print(list1) # [1, 400, 3, 5, 7, 100, 200, 1000, 2000]
print(len(list1)) # 9
# 先通过成员运算判断元素是否在列表中，如果存在就删除该元素
if 3 in list1:
	list1.remove(3)
if 1234 in list1:
    list1.remove(1234)
print(list1) # [1, 400, 5, 7, 100, 200, 1000, 2000]
# 从指定的位置删除元素
list1.pop(0)
list1.pop(len(list1) - 1)
print(list1) # [400, 5, 7, 100, 200, 1000]
# 清空列表元素
list1.clear()
print(list1) # []
```

和字符串一样，列表也可以做切片操作，通过切片操作我们可以实现对列表的复制或者将列表中的一部分取出来创建出新的列表，代码如下所示。

```python
fruits = ['grape', 'apple', 'strawberry', 'waxberry']
fruits += ['pitaya', 'pear', 'mango']
# 列表切片
fruits2 = fruits[1:4]
print(fruits2) # apple strawberry waxberry
# 可以通过完整切片操作来复制列表
fruits3 = fruits[:]
print(fruits3) # ['grape', 'apple', 'strawberry', 'waxberry', 'pitaya', 'pear', 'mango']
fruits4 = fruits[-3:-1]
print(fruits4) # ['pitaya', 'pear']
# 可以通过反向切片操作来获得倒转后的列表的拷贝
fruits5 = fruits[::-1]
print(fruits5) # ['mango', 'pear', 'pitaya', 'waxberry', 'strawberry', 'apple', 'grape']
```



### 遍历列表

```python
# 通过循环用下标遍历列表元素
for index in range(len(list1)):
    print(list1[index])
# 通过for循环遍历列表元素
for elem in list1:
    print(elem)
# 通过enumerate函数处理列表之后再遍历可以同时获得元素索引和值
for index, elem in enumerate(list1):
    print(index, elem)
```

### 列表排序

```python
list1 = ['orange', 'apple', 'zoo', 'internationalization', 'blueberry']
list2 = sorted(list1)
# sorted函数返回列表排序后的拷贝不会修改传入的列表
# 函数的设计就应该像sorted函数一样尽可能不产生副作用
list3 = sorted(list1, reverse=True)
# 通过key关键字参数指定根据字符串长度进行排序而不是默认的字母表顺序
list4 = sorted(list1, key=len)
print(list1)
print(list2)
print(list3)
print(list4)
# 给列表对象发出排序消息直接在列表对象上进行排序
list1.sort(reverse=True)
print(list1)
```

## 生成式和生成器

我们还可以使用列表的生成式语法来创建列表，代码如下所示。

```python
f = [x for x in range(1, 10)]
print(f)
f = [x + y for x in 'ABCDE' for y in '1234567']
print(f)
# 用列表的生成表达式语法创建列表容器
# 用这种语法创建列表之后元素已经准备就绪所以需要耗费较多的内存空间
f = [x ** 2 for x in range(1, 1000)]
print(sys.getsizeof(f))  # 查看对象占用内存的字节数
print(f)
# 请注意下面的代码创建的不是一个列表而是一个生成器对象
# 通过生成器可以获取到数据但它不占用额外的空间存储数据
# 每次需要数据的时候就通过内部的运算得到数据(需要花费额外的时间)
f = (x ** 2 for x in range(1, 1000))
print(sys.getsizeof(f))  # 相比生成式生成器不占用存储数据的空间
print(f)
for val in f:
    print(val)
```

## 元组

Python中的元组与列表类似也是一种容器数据类型，可以用一个变量（对象）来存储多个数据，不同之处在于元组的元素不能修改，在前面的代码中我们已经不止一次使用过元组了。顾名思义，我们把多个元素组合到一起就形成了一个元组，所以它和列表一样可以保存多条数据。下面的代码演示了如何定义和使用元组。

```python
# 定义元组
t = ('骆昊', 38, True, '四川成都')
print(t)
# 获取元组中的元素
print(t[0])
print(t[3])
# 遍历元组中的值
for member in t:
    print(member)
# 重新给元组赋值
# t[0] = '王大锤'  # TypeError
t = ('王大锤', 20, True, '云南昆明')
# 变量t重新引用了新的元组原来的元组将被垃圾回收
print(t)
# 将元组转换成列表
person = list(t)
print(person)
# 列表是可以修改它的元素的
person[0] = '李小龙'
person[1] = 25
print(person)
# 将列表转换成元组
fruits_list = ['apple', 'banana', 'orange']
fruits_tuple = tuple(fruits_list)
print(fruits_tuple)
```



这里有一个非常值得探讨的问题，我们已经有了列表这种数据结构，为什么还需要元组这样的类型呢？

1. 元组中的元素是无法修改的，事实上我们在项目中尤其是多线程环境中可能更喜欢使用的是那些不变对象（一方面因为对象状态不能修改，所以可以避免由此引起的不必要的程序错误，简单的说就是一个不变的对象要比可变的对象更加容易维护；另一方面因为没有任何一个线程能够修改不变对象的内部状态，一个不变对象自动就是线程安全的，这样就可以省掉处理同步化的开销。一个不变对象可以方便的被共享访问）。所以结论就是：如果不需要对元素进行添加、删除、修改的时候，可以考虑使用元组，当然如果一个方法要返回多个值，使用元组也是不错的选择。
2. 元组在创建时间和占用的空间上面都优于列表。

## 集合

Python中的集合跟数学上的集合是一致的，不允许有重复元素，而且可以进行交集、并集、差集等运算。

### 创建和使用集合

可以按照下面代码所示的方式来创建和使用集合。

```python
# 创建集合的字面量语法
set1 = {1, 2, 3, 3, 3, 2}
print(set1)
print('Length =', len(set1))
# 创建集合的构造器语法(面向对象部分会进行详细讲解)
set2 = set(range(1, 10))
set3 = set((1, 2, 3, 3, 2, 1))
print(set2, set3)
# 创建集合的推导式语法(推导式也可以用于推导集合)
set4 = {num for num in range(1, 100) if num % 3 == 0 or num % 5 == 0}
print(set4)
```

### 添加和删除元素

```python
set1.add(4)
set1.add(5)
set2.update([11, 12])
set2.discard(5)
if 4 in set2:
    set2.remove(4)
print(set1, set2)
print(set3.pop()) # 集合中只能用pop()去掉集合中的第一个元素。若括号中加数字，如pop(0)则不行。
print(set3)
```

### 集合的运算

```python
 集合的交集、并集、差集、对称差运算
print(set1 & set2)
# print(set1.intersection(set2))
print(set1 | set2)
# print(set1.union(set2))
print(set1 - set2)
# print(set1.difference(set2))
print(set1 ^ set2) # ^ 相当于取两个集合中不共有的部分
# print(set1.symmetric_difference(set2))
# 判断子集和超集 定义：如果一个集合S2中的每一个元素都在集合S1中，且集合S1中可能包含S2中没有的元素，则集合S1就是S2的一个超集，反过来，S2是S1的子集。 S1是S2的超集，若S1中一定有S2中没有的元素，则S1是S2的真超集，反过来S2是S1的真子集。
print(set2 <= set1)
# print(set2.issubset(set1))
print(set3 <= set1)
# print(set3.issubset(set1))
print(set1 >= set2)
# print(set1.issuperset(set2))
print(set1 >= set3)
# print(set1.issuperset(set3))
```

**说明：** Python中允许通过一些特殊的方法来为某种类型或数据结构自定义运算符（后面的章节中会讲到），上面的代码中我们对集合进行运算的时候可以调用集合对象的方法，也可以直接使用对应的运算符，例如`&`运算符跟intersection方法的作用就是一样的，但是使用运算符让代码更加直观。

## 字典

字典是另一种可变容器模型，Python中的字典跟我们生活中使用的字典是一样一样的，它可以存储任意类型对象，与列表、集合不同的是，字典的每个元素都是由一个键和一个值组成的“键值对”，键和值通过冒号分开。下面的代码演示了如何定义和使用字典。

```python
# 创建字典的字面量语法
scores = {'骆昊': 95, '白元芳': 78, '狄仁杰': 82}
print(scores)
# 创建字典的构造器语法
items1 = dict(one=1, two=2, three=3, four=4)
# 通过zip函数将两个序列压成字典
items2 = dict(zip(['a', 'b', 'c'], '123'))
# 创建字典的推导式语法
items3 = {num: num ** 2 for num in range(1, 10)}
print(items1, items2, items3)
# 通过键可以获取字典中对应的值
print(scores['骆昊'])
print(scores['狄仁杰'])
# 对字典中所有键值对进行遍历
for key in scores:
    print(f'{key}: {scores[key]}')
# 更新字典中的元素
scores['白元芳'] = 65
scores['诸葛王朗'] = 71
scores.update(冷面=67, 方启鹤=85) # 加入多个元素时用update()，注意()中的元素不用加''
print(scores)
if '武则天' in scores:
    print(scores['武则天'])
print(scores.get('武则天'))
# get方法也是通过键获取对应的值但是可以设置默认值
print(scores.get('武则天', 60))
# 删除字典中的元素
print(scores.popitem())
print(scores.popitem())
print(scores.pop('骆昊', 100))
# 清空字典
scores.clear()
print(scores)
```



# 面向对象编程基础

## 定义类及创建和使用对象

```python
class Student(object):

    # __init__是一个特殊方法用于在创建对象时进行初始化操作
    # 通过这个方法我们可以为学生对象绑定name和age两个属性
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self, course_name):
        print('%s正在学习%s.' % (self.name, course_name))

    # PEP 8要求标识符的名字用全小写多个单词用下划线连接
    # 但是部分程序员和公司更倾向于使用驼峰命名法(驼峰标识)
    def watch_movie(self):
        if self.age < 18:
            print('%s只能观看《熊出没》.' % self.name)
        else:
            print('%s正在观看岛国爱情大电影.' % self.name)
```



当我们定义好一个类之后，可以通过下面的方式来创建对象并给对象发消息

```python
def main():
    # 创建学生对象并指定姓名和年龄
    stu1 = Student('骆昊', 38)
    # 给对象发study消息
    stu1.study('Python程序设计')
    # 给对象发watch_av消息
    stu1.watch_movie()
    stu2 = Student('王大锤', 15)
    stu2.study('思想品德')
    stu2.watch_movie()


if __name__ == '__main__':
    main()
```

## 访问可见性问题

## 面向对象的支柱

面向对象有三大支柱：封装、继承和多态。



# 自己发现的

## 交换变量的值

(x,y) = (y,x)

## 遇到的一些函数

### enumerate() 函数

用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

```python
for index, elem in enumerate(list1):
    print(index, elem)
```

以下是 enumerate() 方法的语法:

```python
enumerate(sequence, [start=0])
```

参数

- sequence -- 一个序列、迭代器或其他支持迭代对象。
- start -- 下标起始位置。

### sorted和sort

**区别：**

sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。

list 的 sort 方法返回的是对已经存在的列表进行操作，无返回值，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。

### system()

```python
 os.system('cls')  # os.system('clear') #清空屏幕
```

### sleep()

```python
time.sleep(0.2) # 休眠0.2秒
```

### rfind()

rfind() 返回字符串最后一次出现的位置，如果没有匹配项则返回 -1。

### sqrt()

math.sqrt(100)  # 10  （求一个数的平方根）



## python中基本数据类型（对象）占用的内存

python中各个**基本数据类型（对象）**占用的内存大小和c++/Java完全不一样

什么python各个数据类型占用大小和c++中不一致呢？

这里本质上是由python的实现所决定的，python代码在运行的时候会由python解析器执行，具体会解析为C语言的某种结构。也就是说，python中的一个int（或其他）映射到c语言中会是一种复杂结构体。

前提概述：python中一切都是对象，so python中其实根本不存在int float这些类型，int其实是一个python对象。

- int：28
- float：24
- string：54
- list()：64
- {}：288
- ste()：224