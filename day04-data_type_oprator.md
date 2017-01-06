# day04-数据类型和运算符


    “When in doubt, use brute force. ” “如果局部变量太多，我倾向于拆分子程序。---Ken Thompson  (Unix 之父)


基础数据类型---常量---进制转化

## 基本数据类型 


## 常量

### \#define

在C语言中以#开始的语句都是预处理语句
**注意：预处理语句后面没有分号**

演示在处理的时候 #define 的替换效果



```
#include <stdio.h>
#define HAHA "hello"


int main()
{
    printf("%s",HAHA);
    return 0;
}
```

预处理指令  `gcc -E main.c  -o main1.c`

```
.......
# 2 "main.c" 2



int main()
{
 printf("%s","hello");
 return 0;
}
```






### const

在C语言中const关键字的作用是对定义的变量进行`只读`的限定。



```
const int count = 123;
```

然后在C语言对const语义并没有理论上的那么严谨，在后期学习了指针之后就会发现:


```
#include <stdio.h>
//局域作用域中的const类型的常量  是可以通过指针修改的。

int main()
{
    const int count = 100;
    int *ptr = (int*)&count;
    *ptr = 1001;
    printf("%d",count);
    return 0;
}
```

在开始讲解const关键字的时候应该表明 const是一个限定符。


### 字符串常量


### 整型常量

整型常量可以用二进制、八进制、十进制或十六进制来表示。

## int类型

### int常量，变量

### printf函数输出int值

### printf输出八进制，十六进制

### 有符号和无符号

### 整数溢出

### 大端对齐和小端对齐

## char类型

### char常量，变量

### printf函数输出char值

#### 不能打印char转义符

### char 和 unsigned char

## 浮点类型

```
float, double, long double类型
```

### printf函数输出浮点数

## 进制

二进制

八进制

十进制

十六进制

## 存储类型限定符

### const

### volatile

### register

## 字符串格式化输出和输入

### putchar函数

### printf函数

格式化控制符   %d %x %p %c %s %% 


### getchar函数

### scanf函数，

## 运算符


### 赋值
    
    = 赋值号
    
赋值运算符的作用是把=**右边的表达式(变量)的值** 赋予 =号**左边的变量**。
    
    int a = 100;
    int b = 110;
    
    a = b; // 将b的值110 赋予变量a ，a变量之前的值100将被覆盖，a的值将变为110
    
    a = b + 100 ; //将 表达式b + 100的值赋值给变量a，改变a的值为210
    
> 初始化和赋值

变量在定义的时候被赋予一个初始值，这个操作叫初始化
变量在定义完成之后，之后被赋予一个值，这个操作叫赋值

    int count = 0     ;    //初始化
    count     = 1000  ;    //赋值
    
> 对变量(指针变量)进行初始化是一个好习惯。

    
### 算术

\+ - \* / % += -= *= /= %=

/在C语言中有相应的运算符规则。
    
    如果除数和被除数都是整数类型，那么结果为整数类型。如果除数和被除数有一个是浮点数类型，那么结果就是浮点数类型。
    

%  求余，或者称之为模。
    
    a % b 的意义就是 a整除b之后的余数
    比如 60 % 33 的余数就是30，即 60 % 33 == 30
    


()

-    改变优先级
    
    (a+b)*c
    

-    强制类型转换

也称 **显式类型转换**。

    int    s = 1000.0;     //距离
    int    t = 23.44 ;     //时间
    
    double v = s / t ;     //速度
    int d = (int)a + ;     //将浮点数类型的速度值 强制转化为 整型 
    
    

* 隐式转换  
    
    类型转换  
        3/2 = 1;      // 操作数都是整数，结果也是整数。  
        3/2.0 = 1.5 ; // 操作数类型不同，运算之前会先将精度低的操作数隐式转换为精度高的数据类型，再运算，表达式的结果是高精度的数据类型。

// 隐式转换例子

```
int main()
{
    unsigned int a = 99;
    unsigned int b = 100;
    if(a-b < 0)
    {
        printf("%u\n", a);
    }
    else
    {
        printf("b\n");
    }
    return 0;
}
```

* 自增自减运算符++ --

* 逗号表达式

\(先简单介绍，语句时详细讲\)

### 关系运算符
** < <= > >= == !=**


```

如：2 < 3
```

> 在实际的编程的中 经常会不小心犯的错就是 将 == 写成 =
原意是比较两个表达式的值，结果变成了改变左边的值。




### 逻辑运算符

在C语言中没有表示真和假的数据类型，

逻辑成立为真；不成立为假；

在C语言中整数值**0表示逻辑假，非0表示真**。

假 比如 : NULL,0
真 比如 : 1,100,-100等非0的值


逻辑与&&

    与；且;并且;
    表达式形式: 子表达式1 && 子表达式2
    
    特点-一假即假
    
    7 < 8 && 0 逻辑为假
    
    
逻辑或|| 

    或；或者
    表达式形式: 子表达式1 || 子表达式2
    
    特点-一真即真
    
逻辑非!

    非；
    表达式形式: !子表达式        
    
    特点-真假取反

### 三目运算符  

这是C语言中**唯一一个三目运算符**。

    表达式形式: 
    int res = 1 > 2 ? 1 : 2;
    res的值是几?
    
### &取地址符
    
    int a = 1001;
    printf("a的值是 %d a的地址是 %p\n",a,&a);
    
### sizeof运算符
    
这是C语言中常用的为数不多的以单词形式内置的运算符。

运算符作用是求取 目标参数在系统内存中占用空间大小(字节数)

    sizeof(int) ;//求取int类型的数据占用 字节数
    sizeof(0); //求取整数0(整数默认类型为int类型) 占用的字节数 == sizeof(int）
    
由此可见，sizeof运算的目标参数可以是值，也可是数据类型。


### 运算符优先级和结合方向


![](/assets/oprator.png)

### ASCII码表

![](/assets/ascii.png)


### 反汇编演示

汇编语言种类   Intel汇编和AT&T汇编
在intel的官方文档中使intel语法，Windows也使用intel语法；而UNIX平台的汇编器一直使用AT&T语法，在Linux内核中源码中部分代码使用AT&T汇编编写。

从汇编的角度看a++ 和++b的指令

前置++和后置++在表达式中单独使用的时候的，我们就可以认为其实完全一样的。


```
#include <stdio.h>
int main()
{
	int a = 100;
	int b = 101;
	int c = 102;
	int d = 103;
	int e = 104;

	++b;	
	c++;

	printf("%d %d %d %d %d\n",a,b,c,d,e);
	getchar();
	return 0;
}
```



```
10: ++b;
000417F1 8B 45 EC mov eax,dword ptr [b]  
000417F4 83 C0 01 add eax,1
000417F7 89 45 EC mov dword ptr [b],eax  
11: c++;
000417FA 8B 45 E0 mov eax,dword ptr [c]  
000417FD 83 C0 01 add eax,1
00041800 89 45 E0 mov dword ptr [c],eax  
```
可以看到 **单独前置和后置对应的汇编指令是完全一致的**。**但也不排除不同的编译器的功能不一样，对这条语句的理解不一样**。



AT&T汇编语句 ；AT&T 中寄存器需要加前缀“%” ；立即数需要加前缀“$” 。 



```
pc@iZ25g2i2xsmZ:~$ gcc -E test_asm.c -o test_asm.i
pc@iZ25g2i2xsmZ:~$ gcc -S test_asm.i -o test_asm.s
```



```
movl    $100, -20(%rbp)
movl    $101, -16(%rbp)
movl    $102, -12(%rbp)
movl    $103, -8(%rbp)
movl    $104, -4(%rbp)
addl    $1, -16(%rbp)
addl    $1, -12(%rbp)
```



非单独使用的场景
```
#include <stdio.h>
int main()
{
    int a = 100;
    int b = 101;
    int c = 102;
    int d = 103;
    int e = 104;

    a = ++b;

    a = c++;

    d = d + 1;

    e += 1;

    printf("%d %d %d %d %d\n",a,b,c,d,e);
    getchar();
    return 0;
}
```

```
--- g:\code\test_asm\test_asm\main.cpp -----------------------------------------
     1: #include <stdio.h>
     2: int main()
     3: {
00E317A0 55                   push        ebp  
00E317A1 8B EC                mov         ebp,esp  
00E317A3 81 EC FC 00 00 00    sub         esp,0FCh  
00E317A9 53                   push        ebx  
00E317AA 56                   push        esi  
00E317AB 57                   push        edi  
00E317AC 8D BD 04 FF FF FF    lea         edi,[ebp-0FCh]  
00E317B2 B9 3F 00 00 00       mov         ecx,3Fh  
00E317B7 B8 CC CC CC CC       mov         eax,0CCCCCCCCh  
00E317BC F3 AB                rep stos    dword ptr es:[edi]  
     4:     int a = 100;
00E317BE C7 45 F8 64 00 00 00 mov         dword ptr [a],64h  
     5:     int b = 101;
00E317C5 C7 45 EC 65 00 00 00 mov         dword ptr [b],65h  
     6:     int c = 102;
00E317CC C7 45 E0 66 00 00 00 mov         dword ptr [c],66h  
     7:     int d = 103;
00E317D3 C7 45 D4 67 00 00 00 mov         dword ptr [d],67h  
     8:     int e = 104;
00E317DA C7 45 C8 68 00 00 00 mov         dword ptr [e],68h  
     9: 
    10:     a = ++b;
00E317E1 8B 45 EC             mov         eax,dword ptr [b]  
00E317E4 83 C0 01             add         eax,1  
00E317E7 89 45 EC             mov         dword ptr [b],eax  
00E317EA 8B 4D EC             mov         ecx,dword ptr [b]  
00E317ED 89 4D F8             mov         dword ptr [a],ecx  
    11:     
    12:     a = c++;
00E317F0 8B 45 E0             mov         eax,dword ptr [c]  
00E317F3 89 45 F8             mov         dword ptr [a],eax  
00E317F6 8B 4D E0             mov         ecx,dword ptr [c]  
00E317F9 83 C1 01             add         ecx,1  
00E317FC 89 4D E0             mov         dword ptr [c],ecx  
    13: 
    14:     d = d + 1;
00E317FF 8B 45 D4             mov         eax,dword ptr [d]  
00E31802 83 C0 01             add         eax,1  
00E31805 89 45 D4             mov         dword ptr [d],eax  
    15: 
    16:     e += 1;
00E31808 8B 45 C8             mov         eax,dword ptr [e]  
00E3180B 83 C0 01             add         eax,1  
00E3180E 89 45 C8             mov         dword ptr [e],eax  
    17: 
    18:     printf("%d %d %d %d %d\n",a,b,c,d,e);
00E31811 8B 45 C8             mov         eax,dword ptr [e]  
00E31814 50                   push        eax  
00E31815 8B 4D D4             mov         ecx,dword ptr [d]  
00E31818 51                   push        ecx  
00E31819 8B 55 E0             mov         edx,dword ptr [c]  
00E3181C 52                   push        edx  
00E3181D 8B 45 EC             mov         eax,dword ptr [b]  
00E31820 50                   push        eax  
00E31821 8B 4D F8             mov         ecx,dword ptr [a]  
00E31824 51                   push        ecx  
00E31825 68 30 6B E3 00       push        offset string "%d %d %d %d %d\n" (0E36B30h)  
00E3182A E8 F1 FA FF FF       call        _printf (0E31320h)  
00E3182F 83 C4 18             add         esp,18h  
    19:     getchar();
00E31832 8B F4                mov         esi,esp  
00E31834 FF 15 74 91 E3 00    call        dword ptr [__imp__getchar (0E39174h)]  
00E3183A 3B F4                cmp         esi,esp  
00E3183C E8 D2 F8 FF FF       call        __RTC_CheckEsp (0E31113h)  
    20:     return 0;
00E31841 33 C0                xor         eax,eax  
    21: }
```







