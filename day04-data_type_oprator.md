# day04-数据类型和运算符

## 基本数据类型

## 常量

### \#define

### const

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

### printf函数，putchar函数

### scanf函数，getchar函数

## 运算符

* \(\)改变优先级

* 强制转换\(显式转换\)

* 隐式转换  
    类型转换  
        3/2 = 1 ---&gt; 操作数都是整数，结果也是整数。  
        3/2.0 = 1.5 ---&gt; 操作数类型不同，运算之前会先将精度低的操作数隐式转换为精度高的数据类型，再运算，表达式的结果是高精度的数据类型。

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

## 关系运算符

```
< <= > >= == !=
如：2 < 3
```

## 逻辑运算符

&&   
\|\|   
！

三目运算符  
int res = 1&gt;2? 1: 2

运算符优先级

### 反汇编演示

汇编语言种类   Intel汇编和AT&T汇编

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







