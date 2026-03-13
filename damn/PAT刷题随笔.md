# 备考PAT

备考策略:

确定用C++刷题;先学一下STL;然后看《算法笔记》（胡凡、曾磊主编）以及对应配套的《上机实战指南》;分类刷题;先刷简单题巩固语法

# 数学问题

## 最大公约数与最小公倍数

**最大公约数**

原理1: 设gcd为求两数最大公约数的函数;设正整数a,b;则:gcd(a,b) = gcd(b,a%b)
原理2: 0和任意一个整数x的最大公约数都是x

利用递归可缩小两数,最后当两数中出现0时递归结束,求出最大公约数(0和任意一个整数x的最大公约数都是x,由上等式,求得gcd(x,0)时的最大公约数x即为gcd(a,b)的最大公约数)

由此可得出求最大公约数的算法:

```C++
int gcd(int a,int b){
    if(b == 0) return a;
    else return gcd(b,a%b);
}
```



**最小公倍数**

设正整数a,b,及其最大公约数d;其最小公倍数为ab/d
为防止a乘b溢出,可以写成a/db

```c++
int gcd(int a,int b){
    return !b ? a : gcd(b,a % b);
}

int lcm(int a,int b){
    int d = gcd(a,b);
    return a/d*b;
}
```



## 素数的判断

素数:大于1的自然数中,只能被1和它本身整除的数(1不是素数;自然数:非负整数集合;素数也称质数)

判断自然数n是否为素数--- 原理:只需判定[2,sqrt(n)]中没有能整除n,即为素数(证明过程略)

```C++
bool isPrime(int n) {
    if(n <= 1) return false;
    int sqr = (int)sqrt(1.0 * n); //sqrt函数形参是浮点数
    for(int i = 2;i <= sqr;++i){
        if(n % i == 0) return false;
    }
    return true;
}
```



## 质因子分解

背景知识:
质因子(质因数):给定正整数n,除了1以外能整除整数n的质数
因子(因数,约数):给定正整数n,除了1以外能整除整数n的数

质因子分解:将一个整数分解成它的质因子相乘的形式

原理1:对一个正整数n,如果它存在[2,n]范围内的质因子,其质因子要么全部小于等于根号n,要么只有一个大于根号n,其它全部小于根号n(n也可以作为质因子)

```C++
struct factor {//用来存放质因子
    int x,cnt; //x为质因子,cnt为其个数
}fac[10];//数组长度视题而定,如果只是要求int,10个就够了

int t = n;
int sqr = (int)sqrt(1.0 * n);
int num = 0;//num用来统计质因子的个数
for(int i = 0;i < pNum && prime[i] <= sqr;i++){//prime是素数表;pNum是素数表的长度;
    if(t % prime[i] == 0) {//如果prime[i]是n的质因子
    	fac[num].x = prime[i];//记录该质因子
        fac[num].cnt = 0;//初始化该质因子的数量,这里设为0是因为后面会统计其数量的,这里不必设为1
        while(t % prime[i] == 0) {
            fac[num].cnt += 1;
            t /= prime[i];
        }
        num += 1;
	}
    if(t == 1) break;//n等于1,说明质因子已经找完了,可以终止循环了.
}

if(t != 1) {//说明前面找的质因子不能把原整数n整除完,即还剩余质因子在(根号n,n]的范围内
    fac[num].x = t //此时的t就是要找的最后一个质因子
    fac[num].cnt = 1;
    num += 1;
}

```

**补充关于因子的理论:**
给定正整数n,其各质因子$p_i$的个数分别为$e_1,e_2,...e_k$,则因子个数为$(e_1 + 1)*...*(e_k + 1)$



## 大整数运算

**int放不下,拿个放数组里**



定义

```C++
struct bign {
	int d[1000];
	int len;
	int sign; // 正负号 0:+	 1:- 
	
	bign() {
		memset(d,0,sizeof(d));
		len = 0;
		sign = 0;
	}
};
```

将读到的字符串转换为数字

```C++
bign change(char str[]) { // 将整数转换为bign 
	bign n;
	n.len = strlen(str);
	for(int i = 0;i < n.len;i++) {
		n.d[i] = str[n.len - i - 1] - '0';
	}
	return n;
}
```



高精度加法

```C++
bign add(bign a,bign b) { //求和 a,b同号 
	bign n; 
	int carry = 0; // 进位 
	for(int i = 0;i < a.len || i < b.len;i++) {
		int tmp = a.d[i] + b.d[i] + carry;
		n.d[n.len++] = tmp % 10;
		carry = tmp/10;
	}
	if(carry != 0) {
		n.d[n.len++] = carry;
	}
	if(a.sign == 1 && b.sign == 1) n.sign == 1; 
	return n;
}
```



高精度减法

```C++
bign sub(bign a,bign b) { // a - b;a > 0 b > 0 
	bign n;
	bool res = compare(a,b);
	if(!res) { // a > b
		bign t = a;
		a = b;
		b = t;
	}
	for(int i = 0;i < a.len || i < b.len;i++) {
		if(a.d[i] < b.d[i]) { // 不够往前借 
			a.d[i + 1] - 1;
			a.d[i] += 10;
		}
		n.d[n.len++] = a.d[i] - b.d[i];
	}
	while(n.len >= 2 && n.d[n.len - 1] == 0) { // 去除高位0 
		n.len -= 1; 
	}
	if(!res) { // !res 说明之前交换了a,b;所以这里要改变n的正负 
		n.sign = 1;
	}
	return n; 
}
```



高精度与低精度的乘法

两个高精度数乘法相当于把另一个高精度数的每个位上的数取出来,然后分别调用下面这个函数去乘以另一个高精度数,再乘以对应位数的10的次方,然后再把结果都加起来

```C++
bign multiply(bign a,int b) {
	bign n;
	int carry = 0;
	for(int i = 0;i < a.len;i++) {
		int tmp = a.d[i] * b + carry;
		n.d[n.len++] = tmp % 10;
		carry = tmp / 10;
	}
	while(carry != 0) { // 与加法不同,乘法里的进位可能不止一位 
		n.d[n.len++] = carry % 10;
		carry /= 10;
	}
	return n;
}
```



高精度与低精度的除法

```C++
bign divide(bign a,int b) {
	bign n;
	int r = 0;// 余数 
	n.len = a.len;
	for(int i = a.len - 1;i >= 0;i--) { // 从高位开始 
		r = r * 10 + a.d[i]; // 和上一位遗留的余数组合 
		if(r < b) { // 不够除 
			n.d[i] = 0;
		}else {
			n.d[i] = r/b;
			r = r % b;
		}
	}
	while(n.len >= 2 && n.d[n.len - 1] == 0){
		n.len -= 1; // 去除高位的0 
	}
}
```

## 倍数问题

求一个数n中另一个数x的倍数的个数: n/2 (整除)

## 组合数

### 求n!中有多少个质因子p

1. n!中有(n/p + n/p^2 + n/p^3 + ...)个质因子p (/为整除)

   ```C++
   int cal(int n, int p) {
       int ans = 0;
       while(n) {
           ans += n/p;
           n /= p; //相当于分母多乘一个p.这样可以防止指数过大导致溢出
       }
       return ans;
   }
   ```

2. 1~n中p的倍数的个数(n/p)加上(n/p)!中质因子p的个数 (递归实现)

   ```C++
   int cal(int n, int p) {
       if(n < p) return 0; //n<p时,1~n中不可能有p的倍数
       return n / p + cal(n / p, p);
   }
   ```


### 求$C_n^m$

```C++
long long C(long long n, long long m) {
    long long ans = 1;
    for(long long i = 1; i <= m; i++) {
        ans = ans * (n - m + i) / i; //一定要先乘
    }
}
```

# 坑B题目

1061 Dating (20)-PAT甲级真题

the hours from 0 to 23 in a day are represented by the numbers from 0 to 9 and the capital letters from A to N, respectively

上面这句话的意思是0-23用0-9,A-N表示,也就是A表示10,N表示23!!!

# 其它

**二次方探测**

Hash = (key + size * size) % size



**最长连续因子**

1096 Consecutive Factors

注意点:怎么扫描列举全部连续因数



**一串加减乘除运算**

步骤:

1. 中缀表达式转后缀表达式
   1. 用队列存放后缀表达式
   2. 数直接进入队列
   3. 用栈将计算符号优先级高的先进入队列(先计算)
2. 计算后缀表达式
   1. 将队列中的元素去出放到栈
   2. 若是数则直接放入栈
   3. 若是符号则取出栈中的两个数进行计算后再放入栈(一个符号对应两个数)
   4. 最后栈中剩下的那个数就是结果



**关于scanf的使用**

A+B in Hogwarts

做完之后看评论区都说是水题,而且他们的代码都很简洁...

```c++
#include<iostream>
#include<cstdio>
using namespace std;
int a1,b1,c1,a2,b2,c2;
int main()
{
    //学习这里scanf的写法,它能直接帮你把数对应过来,不需要你一个个扫描了!!!
    scanf("%d.%d.%d %d.%d.%d",&a1,&b1,&c1,&a2,&b2,&c2);
    printf("%d.%d.%d",a1+a2+(b1+b2+(c1+c2)/29)/17,(b1+b2+(c1+c2)/29)%17,(c1+c2)%29);
    return 0;
}
```



溢出问题**

1065 A+B and C (64bit) (20)-PAT甲级真题

int : 4 Byte

long long : 8 Byte



# DFS

- The Largest Generation (25)
  
- Highest Price in Supply Chain (25)

- Total Sales of Supply Chain (25)

# 链表

- Deduplication on a Linked List (25) (链表去重)

# Hash

- Find Coins

- 1041 Be Unique (20)-PAT甲级真题（Hash散列）

# 队列

- Mice and Rice (25) 这个题目有点坑,注意每轮中淘汰的老鼠的排名为这轮晋级的老鼠数+1

# Tree

## BST

- Complete Binary Search Tree (30) 

  注意:BST的中序遍历是有序的

- Is It a Binary Search Tree (25)

  判断序列是否为BST的前序或其镜像的前序 --> 前序转后序,看得到的后序长度和前序是否一致

# 二分

- # Shopping in Mars

