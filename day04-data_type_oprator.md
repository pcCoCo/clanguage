# day04-数据类型和运算符

## 基本数据类型 

## 常量
### #define
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
    
    float, double, long double类型
    
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

* ()改变优先级

* 强制转换(显式转换) 
 
* 隐式转换
    类型转换
        3/2 = 1 ---> 操作数都是整数，结果也是整数。
        3/2.0 = 1.5 ---> 操作数类型不同，运算之前会先将精度低的操作数隐式转换为精度高的数据类型，再运算，表达式的结果是高精度的数据类型。
        
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

(先简单介绍，语句时详细讲)
## 关系运算符

    < <= > >= == !=
    如：2 < 3

## 逻辑运算符

&& 
|| 
！


三目运算符
int res = 1>2? 1: 2

运算符优先级





### 反汇编演示
INC ADD
++  +

从汇编的角度看a++ 和++b的指令

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
011B17A0 55                   push        ebp  
011B17A1 8B EC                mov         ebp,esp  
011B17A3 81 EC FC 00 00 00    sub         esp,0FCh  
011B17A9 53                   push        ebx  
011B17AA 56                   push        esi  
011B17AB 57                   push        edi  
011B17AC 8D BD 04 FF FF FF    lea         edi,[ebp-0FCh]  
011B17B2 B9 3F 00 00 00       mov         ecx,3Fh  
011B17B7 B8 CC CC CC CC       mov         eax,0CCCCCCCCh  
011B17BC F3 AB                rep stos    dword ptr es:[edi]  
     4: 
     5: 	int a = 100;
011B17BE C7 45 F8 64 00 00 00 mov         dword ptr [a],64h  
     6: 	int b = 101;
011B17C5 C7 45 EC 65 00 00 00 mov         dword ptr [b],65h  
     7: 	int c = 102;
011B17CC C7 45 E0 66 00 00 00 mov         dword ptr [c],66h  
     8: 	int d = 103;
011B17D3 C7 45 D4 67 00 00 00 mov         dword ptr [d],67h  
     9: 	int e = 104;
011B17DA C7 45 C8 68 00 00 00 mov         dword ptr [e],68h  
    10: 
    11: 	a = ++b;
011B17E1 8B 45 EC             mov         eax,dword ptr [b]  
011B17E4 83 C0 01             add         eax,1  
011B17E7 89 45 EC             mov         dword ptr [b],eax  
011B17EA 8B 4D EC             mov         ecx,dword ptr [b]  
011B17ED 89 4D F8             mov         dword ptr [a],ecx  
    12: 	
    13: 	a = c++;
011B17F0 8B 45 E0             mov         eax,dword ptr [c]  
011B17F3 89 45 F8             mov         dword ptr [a],eax  
011B17F6 8B 4D E0             mov         ecx,dword ptr [c]  
011B17F9 83 C1 01             add         ecx,1  
011B17FC 89 4D E0             mov         dword ptr [c],ecx  
    14: 
    15: 	d = d + 1;
011B17FF 8B 45 D4             mov         eax,dword ptr [d]  
011B1802 83 C0 01             add         eax,1  
011B1805 89 45 D4             mov         dword ptr [d],eax  
    16: 
    17: 	e += 1;
011B1808 8B 45 C8             mov         eax,dword ptr [e]  
011B180B 83 C0 01             add         eax,1  
011B180E 89 45 C8             mov         dword ptr [e],eax  
    18: 
    19: 
    20: 
    21: 	printf("%d %d %d %d %d\n",a,b,c,d,e);
011B1811 8B 45 C8             mov         eax,dword ptr [e]  
011B1814 50                   push        eax  
011B1815 8B 4D D4             mov         ecx,dword ptr [d]  
011B1818 51                   push        ecx  
011B1819 8B 55 E0             mov         edx,dword ptr [c]  
011B181C 52                   push        edx  
011B181D 8B 45 EC             mov         eax,dword ptr [b]  
011B1820 50                   push        eax  
011B1821 8B 4D F8             mov         ecx,dword ptr [a]  
011B1824 51                   push        ecx  
011B1825 68 30 6B 1B 01       push        offset string "%d %d %d %d %d\n" (011B6B30h)  
011B182A E8 F1 FA FF FF       call        _printf (011B1320h)  
011B182F 83 C4 18             add         esp,18h  
    22: 	getchar();
011B1832 8B F4                mov         esi,esp  
011B1834 FF 15 74 91 1B 01    call        dword ptr [__imp__getchar (011B9174h)]  
011B183A 3B F4                cmp         esi,esp  
011B183C E8 D2 F8 FF FF       call        __RTC_CheckEsp (011B1113h)  
    23: 	return 0;
011B1841 33 C0                xor         eax,eax  
    24: }
```

