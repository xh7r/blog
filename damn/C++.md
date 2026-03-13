# 万能头文件

#include<bits/stdc++.h>

包含了目前c++所包含的所有头文件(仅刷题时有用)

# 数据类型

int 4个字节: $[-2^{31},2^{31})$

long long 8个字节: $[-2^{63},2^{63})$

# 结构体

## 构造函数

其实就是Java里的构造器,不同的是,Java里的构造器是在创建类的对象时使用的,而结构体的构造函数随时都可以用,给构造体赋值.

# 指针

```C++
int a = 1;
int *p = &a;
// 之后的调用中 p : a的地址		*p : a;
```

# 基本运算

## 幂运算

```C++
#include<math.h>

int main() {
	double x = pow(2,24);
	printf("%lf",x);
}
```



# IO

## input

### scanf

在scanf函数中，如果输入的%d，那么你的输入换行符 （空格也是）会直接被当作结束符号，作为你结束输入的标志。并且这个标志不会被下一个读取字符函数所读取！

long long : %lld

float : %f

double : %lf

在scanf中,需要区分%f与%lf

### cin

#### 读取整串字符串

1. getline()

   可以接收空格

   需包含 #include<string>

   ```C++
   #include<string>
   using namespace std;
   
   string str;
   getline(cin,str);
   ```

2. cin.getline()

   可以接收空格

   ```C++
   #include <iostream>
   using namespace std;
   
   char str[100];
   cin.getline(str,100);
   ```

## output

### printf

**格式化输出**

格式化输出整型 d 格式，用来输出十进制整数。 %d：按整型数据的实际长度输出； %md：m为指定的输出宽度。 如果数据的位数小于m，则左端补空格；若大于m，则按实际位数输出； %0md：同上，但这里如果数据的位数小于m，则左端补0；若大于m，则按实际位数输出。

### cout

### putchar

将单个字符输出到控制台显示

# 数据结构

## 数组

### 数组初始化赋值问题

1. 全局数组，未初始化时，默认值都是 0；
2. 局部数组，未初始化时，默认值为随机的不确定的值；
3. 局部数组，初始化一部分时，未初始化的部分默认值为 0；

### 数组批量初始化

```C++
int d[1000];
memset(d,0,sizeof(d));//给数组d中填充0
```

## 用字符充当数组访问的下标

```C++
flag['a'] = 'a';
```

这里[ ]里的'a'会转换为97

## char

### 赋值char数组

```c++
strcpy(c1,c2); // c2 赋值到 c1
```

### char数组初始化细节

```C++
char s1[3] = {'a', 'b', 'c'};
char s2[] = "abc";
char s3[3] = "abc";
```

### toupper

标准库函数

将字符类型的小写字母转为大写

```C++
int toupper(int c);
```

## set

### 判断元素是否在set中

1. count()
   - 存在:return 1;
   - 不~:return 0
2. find()
   - 存在:返回该元素的迭代器
   - 不存在:返回容器末尾的迭代器

## String

### to_string

```C++
string to_string (int val);
string to_string (long val);
string to_string (long long val);
string to_string (unsigned val);
string to_string (unsigned long val);
string to_string (unsigned long long val);
string to_string (float val);
string to_string (double val);
string to_string (long double val);
```

### 字符串截取

str.substr(start,len)

### 字符串填充

```C++
string s;
s.insert(0, 4 - s.length(), '0');
```

### 字符串转十进制int

1. stoi(string str)
   - stoi()会做范围检查，默认范围是在int的范围内的，如果超出范围的话则会runtime error！
2. atoi(char str[])
   - atoi()不会做范围检查，如果超出范围的话，超出上界，则输出上界，超出下界，则输出下界；\

### 字符串转换成char数组

str.c_str()

### find

在C++中，string类中的find函数可以用来查找一个子字符串在另一个字符串中的位置。它的基本语法是：

```C++
size_t find(const string &str, size_t pos = 0) const;
```

其中，第一个参数是要查找的子字符串，第二个参数是可选的，表示从哪个位置开始查找，默认值是0。

该函数返回一个size_t类型的值，表示找到的子字符串在原字符串中的位置。如果找不到，则返回**string::npos**

# 头文件 algorithm

**常用API**

- max(),min()

  参数必须是两个(可以是浮点数)

- abs()

  参数必须是整数(浮点型的绝对值:math头文件下的fabs)

- swap(x,y)

- reverse(it,it1)

  可以将数组指针或容器的迭代器在[it,it1)之间的元素进行反转

- next_permutation(a,a+len)

  将序列a变为其在全排列下的下一个序列

- fill(a,a+n,1)

  把数组或容器中的某段区间内的元素赋值为某个相同的值

- sort(a,a+len,cmp)

  默认升序

  ```C++
  int arr[] = {10,8,3,6,2,3,4};
  sort(arr,arr+7);
  ```

  

  - 比较函数

    ```C++
    bool cmp(int a,int b) {
    	return a > b; //降序
    }
    ```

- lower_bound(first,last,val)

  返回一段有序序列中第一个等于val或第一个在val右边的数的下标或迭代器

- upper_bound(first,last,val)

  基本同上,这个没有等于



# STL

## vector

### 常用API

```C++
vector<int> v;
v.push_back(1); // 添加元素
v.resize(5); // 设置vector大小
v.clear(); // 清空vector
```

### 二维vecto排序

```C++
vector<vector<int>> full; // 存放满足amount的所以有路径

bool cmp(vector<int> a, vector<int> b) {
    return a[0] < b[0];
}

sort(full.begin(), full.end(), cmp);
```

## unordered_map

### 常用API

```C++
my_map.count(key);
my_map.find(key); // 返回迭代器
my_map.end(); // 和find搭配使用
```



# 其它API

## strcmp

#include <string.h>

strcmp(str1,str2);
比较两个char数组的字典序大小
str1 > str2	return > 0
str1 < str2	return < 0
str1 = str2	return = 0

## isdigit

判断字符是否为数字

isdigit('a')

# 关于C++和Java数据引用的区别

Java中,数据分位2大类:

- 基本数据类型
- 引用数据类型

而在C++中,除了指针,其它都是基本数据类型,包括STL中提供的容器

不论是C++还是Java,将变量传递给函数,函数都是会复制一份,而不会改变原来的变量!