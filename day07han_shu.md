“Anyone who considers arithmetical methods of producing random numbers is, of course, in a state of sin.” “任何考虑产生随机数的算术方法的人当然都处于罪的状态。     (冯·诺伊曼)


英文单词function，原意为功能，作用，函数; 职务。

## 数学意义上的函数

在数学领域，函数是一种关系，这种关系使一个集合里的每一个元素对应到另一个（可能相同的）集合里的唯一元素。

A variable so related to another that for each value assumed by one there is a value determined for the other.

自变量，函数一个与他量有关联的变量，这一量中的任何一值都能在他量中找到对应的固定值。

A rule of correspondence between two sets such that there is a unique element in the second set assigned to each element in the first set.函数两组元素一一对应的规则，第一组中的每个元素在第二组中只有唯一的对应量。

例如

`f(x) = x`[^2]`+100`

## 计算机编程中的函数

函数是一段完成特定功能的程序代码，或称其为一个子程序，它可以实现固定运算功能。

如果将上文中的数学函数翻译为C语言描述的话，它可能是这个样子
    


```
int f(int x)
{
    return x\*x + 100;
}
```






一个C语言程序有且只有一个main函数。由main函数调用其他函数，其他函数也可以互相调用。同一个函数可以被一个或多个函数调用任意多次。在程序设计中，常将一些常用的功能模块编写成函数，放在函数库中供公共选用。要善于利用函数，以减少重复编写程序段的工作量。

## 函数分类

可以简单的分为库函数和自定义函数。

函数库封装了一些函数的代码，库函数就是由函数中中提供的函数接口。

用户可以在代码中直接使用库函数，而不需要关心如何实现从而提高开发效率。值得注意的是，程序的需求细节可能没办法直接使用库函数来完成，这个时候就需要我们使用自定义函数来完成。

## 

## 函数的定义

```
函数返回类型 函数名_标识符 (形参列表)

{

函数代码

}
```

比如


```
void func2(int a,int b)
{
    printf("a=%d b=%d\n",a,b);
}
```







```
int func(int a)
{
    if(a % 2 == 0)
        return 1;
    else
        return 0;
}
```







## 函数的声明

函数声明一般可以直接使用**函数头加上分号**即可。
比如 



```
int func(int a);
```




其实还可以更加简单

```
int func(int);
```

例子：

```

void printHello()
{
    printf("********************\n");
    printf("*                  *\n");
    printf("*    大战一触即发    *\n");
    printf("*                  *\n");
    printf("********************\n");
}

```


## 函数的调用

必须要在main函数里调用这个函数.

函数调用的基本形式如下  


```
函数名(实参列表);
```

如果函数返回值类型为**非void类型**，就可以接收你可能感兴趣的返回值。



```
存函数返回值的变量 = 函数名(实参列表);
```

比如



```
int main(void)
{
    int ret = func(100);
    if(ret == 1)
        printf("是偶数");
    else
        printf("不是偶数");
    return 0;
}

```

> 为什么在定义一个函数的形参列表为空的时候都需要手动写成 `返回值类型 函数名(void)`???

```
void test()
{
    printf("call test function");
}
int main(void)
{
    test(2,3,4,5);
    return 0;
}
```

因为在C语言中 test() 等价于 test(...)
而...的意思是不定长参数，比如printf函数的函数原型应该是 int printf(const char *,...);

这样就导致了一个问题 就是你这样调用函数 `test(2,3,4,5,6,7,8);`居然编译器还能通过
这完全就不是我们最初想象的现象了，因为该行为完全就是不可预期的。
所以`规范的C语言的main函数的标准原型`的应该是 

```
int main(void);
int main(int argc,char **argv);
```



3. 有参数无返回值的函数

void isOushu(int num)
{
    if (num % 2 == 0)
    {
        printf("%d是偶数！\n");
    }
    else
    {
        printf("%d是奇数！\n");
    }
}

int main()
{
    isOushu(10);

    int num = 10;

    isOushu(num);

    return 0;    
}

4. 参数的传递

相当于在函数里面定义一个变量num, num的值就是调用这个函数的地方传入的实际的值。
值传递。





5. 有返回值的函数
改造（3）中的代码： 返回是否是偶数的结果(1--偶数， 0--奇数)


注意： 函数只能有一个返回值。




## 函数调用的实现原理 深入Linux内核架构966P

http://www.cnblogs.com/orlion/archive/2015/12/20/5062165.html


## 库函数的使用

库函数的使用时学习C过程的不可避免的过程。
虽然说C语言功能非常强大，只要有足够的编程能力可以实现一切功能但是对于普通的开发者而言这未免开发效率太低。
所以将常用的功能代码封装为一个库，这个库提供了非常多的函数，每个函数都是一个接口。
大多数的场景下，用户在使用的时候更多的注意力应该放在如果使用上，而不是如何来实现这个接口，不要再重复造一些功能完全一样的轮子。

通常情况下使用标准库或者第三方库
只需要在使用的代码中引入头文件声明
然后调用，很可能还需要链接指定所需的库。

> C语言的数学库函数

```
包含头文件 #include <math.h>
在linux中链接的时候会报错 需要手动在编译(链接)的时候加上-lm选项
```




## 多文件编程

### 编写自己的头文件
预处理宏



## 常用库函数



```
#include <math.h>
#include <stdlib.h>

```


math之

    pow、sqrt、abs
    
double pow (double base, double exponent);

    求base的exponent次方
    
double sqrt (double x);
    
    求x的算术平方根
    
double abs (double x);
float abs (float x);
long double abs (long double x);
    
    求x的绝对值


stdlib之

    atoi(atol atof)、rand、srand、exit
    


## 生活中嵌套的例子


![](/assets/qiantao.jpg)

![](/assets/qiantao2.jpg)

牙雕套球又称“同心球”，制作相当繁复，工艺要求极高。据《格古要论》载，早在宋代就已出现3层套球，时称“鬼工球”。广州牙雕艺人在牙球制作上多有创获，套球可达数十层。乾隆时套球已达十多层，玲珑剔透，巧夺天工。此球为广州民间作坊制品，从此球我们也可看到宫廷好尚对民间工艺的影响。

象牙球是我国著名的手工艺品，就是采用镂空的雕刻方法把一个象牙球雕刻出很多层，每层都能动。

一层象牙球中嵌套的一层象牙球。

看过石头狮子的雕刻的嘴里有一个拿不出来的球吗？其实原理是一样的。把狮子做好以后再在狮子的觜部往里掏空，做球状，里大口小，石球还要连一点，做好以后把连一点的地方打掉稍修一下就好了。 

广州牙雕界最为知名的“翁家蛋”流派。象牙最大的牙球直径不过18厘米，要增加牙球的层次无异于“虎口捋须”。翁氏家族五代人就是在与象牙球的厚度作斗争，象牙球的层次由最初的11层加至现在的57层。

第一代：翁五章，翁荣标的曾祖父，镂雕了11层象牙球，是广州近代象牙球镂雕工艺的创始人。

第二代：翁彤，翁荣标的祖父，他将象牙球镂雕接近20层。

第三代：翁昭，翁荣标的父亲。在1915年旧金山“太平洋万国巴拿马博览会”上,翁昭、梁雄合作雕刻的25层象牙球参赛，当时，日本也以30层象牙球参赛。因有人怀疑象牙球是否由一个整体雕镂而成，主办方决定将两个象牙球放在水中加热验证。结果日本的象牙球四分五裂,原来它是用胶粘的，而中国的象牙球整体不散,且层层转动自如,因此获得一等奖。

第四代：翁荣标，将象牙球的层数从28层增加到45层，被誉为“球王至尊”。

第五代：翁耀祥，翁荣标长子，在公认再无可能的情况下雕出57层象牙球。

今年五月十四日，广州“超群象牙世家牙雕精品展”让市民免费目睹众多巧夺天工的雕刻艺术。据专家介绍，罕见的六十层象牙球雕刻是目前世界上层数最多，体积最大，份量最重的象牙球。象牙球直径长达十八厘米，每层都薄如丝纸，均为镂空雕刻，牙球内六十层，层层可以旋动。 图为大饱眼福的市民欣赏巧夺天工的60层象牙球。


## 函数嵌套调用

### 图例
PPT动画显示

Virtual Stdio的调用堆栈分析

### 函数参数压栈方式
简单说明一下

### 没有函数参数的编写方式

```
#include <stdio.h>

int test()
{
	printf("called test function\n");
	return 0;
}

int main(void)
{
	test(20);
	return 0;
}
```
我伙呆，没有参数居然编译通过。运行也没有问题。在C语言中函数没有参数列表需要显式加上void,否则相当于任意参数。
加上void之后函数调用将会报错。

## 头文件

### 标准头文件

C语言的标准文档要求了一个平台移植C语言的时候至少要实现的一些功能和封装的集合，称为“标准库”，标准库的声明头部通过预处理器命令#include进行引用。

| C89标准头文件 | 简介 |
| :--- | :--- | 
| assert.h | 断言 | 
| ctype.h |	字符类型判断 |
| errno.h |	标准报错机制 |
| float.h |	浮点运算 |
| limits.h |	各种体系结构限制 |
| locale.h |	本地化接口 |
| math.h |	数学函数 |
| setjmp.h |	跨函数跳转 |
| signal.h |	信号（类似UNIX的信号定义，但是差很远） |
| stdarg.h |	可变参处理 |
| stddef.h |	一些标准宏定义 |
| stdio.h |	标准I/O库 |
| stdlib.h |	标准工具库函数 |
| string.h |	ASCII字符串及任意内存处理函数 |
| time.h   |	时间相关 |





### 编写自己的头文件

> 防止重复包含的预处理宏


方法一

```
#ifndef __XXX_HEADER_H__
#define __XXX_HEADER_H__
#endif //__XXX_HEADER_H__
```

> 事实上另外一种大多数情况也行的方法 
`#pragma once`


在一般情况下，二者都可以 `防止头文件的重复包含`。



有一些注意事项:

方法一只能防止重复包含相同宏名的文件;
方法二只能防止重复包含同一个物理文件;


如果多个文件中#define的宏名是相同的，那么就会导致一些文件得不到包含；


解决方法:

1. 定义并遵守  文件名-宏名的对应关系(如果文件名同名还是会导致宏名冲突)

- 不同子系统的文件名分别对应不同的前缀



### 变量的定义和声明

定义define    表示会创建变量并为之分配存储空间
    
声明declaration 表明该变量的类型(存储类型、数据类型)并不在此处定义




以前的Turb C编译器要求 所有的变量定义必须放在函数的开始部分。
如果写成这样


```
int main()
{

    int a = 100;
    
    printf("%d",a);
    int b = 101;
    printf("%d",b);
    
    return 0;
}
```

将会报错。
虽然在现代的C编译器中，对变量的定义、声明、使用没有太多死板的规范 ，但是尽量将变量定义在 一块是可以增加代码的可读性的。




## 过程

    过程是软件中一种很重要的抽象。提供了一种封装代码的方式，用一组指定的参数和一个可选的返回值实现了某种功能。然后可以在程序中的不同地方调用这个函数。
    
    隐藏了操作的具体实现，只是提供了供用户调用的接口(接口说明 所需参数、完成功能、返回值状态、过程对程序的影响 )

    在C语言中过程就叫做函数(funtion)。

    假设过程P调用过程Q，Q执行完成之后返回Q执行之前的地方继续执行(即继续执行过程P)




## 案例


### 求字符串中汉字的数量
char a[100] = "abc我ef哈哈12呵呵"
写一个程序，求这个字符串中有几个汉字.


思路：
汉字的ascii码值都是负数，所以统计ascii码值中负数个数，再除以3(每个汉字3个ascii)

参考答案：

```

int main()
{
    char a[100] = "啪啪abc我ef哈哈12呵呵";
    /*
    int i;
    for(i = 0; i < 30; i++)
    {
        printf("%d\n", a[i]);
    }
    */
    int sum = 0;
    int index = 0;
    while(a[index])
    {
        if (a[index] < 0)
        {
            sum++;
        }
        index++;
    }
    printf("sum = %d\n", sum / 3);
    return 0;
}



```



### 解析字符串

有一个字符数组
整数是任意的，中间可能是* + - / 
char a[100] = "43+56="
写一个程序，将结算的结果追加到字符串a的后面
程序执行完成后a的值是"43+56=99"



参考答案：

```

int main()
{
    char a[100] = "43*56=";
    int i, j;
    char c;
    sscanf(a, "%d%c%d=", &i, &c, &j);//从字符串里面把想得到的字符或者整数提取出来
    //printf("%d, %c, %d\n", i, c, j);
    int res = 0;
    switch(c)
    {
    case '+':
        res = i + j;
        break;
    case '-':
        res = i - j;
        break;
    case '*':
        res = i * j;
        break;
    case '/':
        res = i / j;
        break;
    default:
        res = 0;
    }

    sprintf(a, "%d%c%d=%d", i, c, j, res);
    printf("%s\n", a);

    return 0;
}


```


### 解析字符串的高级应用

char a[100] = "12+5=;45-2=;34*2=;56/3=;
写个程序，执行后=号后面自动添加计算结果
“12+5=17;45-2=43;34*2=68;56/3=18”


参考答案：

```

int main()
{
    char a[100] = "12+5=;45-2=;34*2=;56/3=";
    char b[100] = { 0 };
    char *s = strtok(a, ";");
    while(s)
    {
        //printf("%s\n", s);
        int i, j;
        char c;
        sscanf(s, "%d%c%d=", &i, &c, &j);
        int res = 0;
        switch(c)
        {
        case '+':
            res = i + j;
            break;
        case '-':
            res = i - j;
            break;
        case '*':
            res = i * j;
            break;
        case '/':
            res = i / j;
            break;
        default:
            res = 0;
        }
        char tmp[10] = { 0 };
        sprintf(tmp, "%s%d;", s, res);

        strcat(b, tmp);
        s = strtok(NULL, ";");
    }
    strcpy(a, b);
    printf("%s\n", a);
    return 0;
}


```


### 自定义函数实现atoi功能

c语言有个库函数，名字叫atoi，将一个字符串转化为整数
自定一个函数，实现atoi的功能，要求是不能使用任何c语言已有的库函数



参考答案：

```

int mystrlen(const char *s)//得到字符串的长度
{
    int len = 0;
    while(s[len])
    {
        len++;
    }
    return len;
}

int mypow10(int n)//得到10的n次方
{
    if (n == 0)
        return 1;
    if (n == 1)
        return 10;

    int base = 10;
    int i;
    for(i = 1; i < n; i++)
    {
        base *= 10;
    }
    return base;
}

int mychartoint(char c)//把一个字符转化为一个从0到9的整数
{
    return c - '0';    
}

int my_atoi(const char *nptr)//参数是一个char 的数组
{
    int len = mystrlen(nptr);//得到字符串长度

    int i;
    int value = 0;
    for(i = 0; i < len; i++)
    {
       value +=  mychartoint(nptr[i]) * mypow10(len - i - 1);
    }
    
    return value;
}


int main()
{
    //char c = '1';
    //printf("%d, %d\n", c, '0');
    //return 0;
    char a[] = "23542";
    int i = my_atoi(a);
    printf("%d\n", i);
    return 0;
}



```



### 十进制数转化为十六进制数

编写函数，实现将十进制数转化为十六进制数

参考答案：

```

char hex_char(unsigned int n )
{
    switch (n)
    {
    case 0:
        return '0';
    case 1:
        return '1';
    case 2:
        return '2';
    case 3:
        return '3';
    case 4:
        return '4';
    case 5:
        return '5';
    case 6:
        return '6';
    case 7:
        return '7';
    case 8:
        return '8';
    case 9:
        return '9';
    case 10:
        return 'a';
    case 11:
        return 'b';
    case 12:
        return 'c';
    case 13:
        return 'd';
    case 14:
        return 'e';
    case 15:
        return 'f';
    }
    return '0';
}

void to_hex(unsigned int n)
{
    int i = n % 16;
    if (n>= 16)
        to_hex(n / 16);
    printf("%c", hex_char(i));

}

int main()
{

    int a;
    scanf("%d", &a);
    
    to_hex(a);
    printf("\n");
    return 0;
}



```




## 作业

1. 统计从键盘接收以$结尾的字符数量(包含$)。
    input:123$
    output:4

- 实现函数代码。int isdigit(int ch);判断ASCII码为ch的符是否是数字字符；如果是返回非0；不是返回0。


- 求三个数中最大值。

函数原型是
    void maxNum(int num1,int num2,int num3)


- 写1个函数,传入1个年份和月份,返回这1年的这1月有多少天

- 实现一个atoi函数。

- 实现将UNIX时间戳转化为北京时间(东8区时)的格式。

    unix时间戳（Unix epoch, Unix time, POSIX time 或 Unix timestamp）是从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数，不考虑闰秒。UNIX时间戳的0按照ISO 8601规范为 ：1970-01-01T00:00:00Z.一个小时表示为UNIX时间戳格式为：3600秒；一天表示为UNIX时间戳为86400秒，闰秒不计算。在大多数的UNIX系统中UNIX时间戳存储为32位，这样会引发2038年问题或Y2038。

```
1486373585 s --- 2017/2/6 17:33:5

1486373651 s --- 2017/2/6 17:34:11
```

尝试编写一个或者多个函数完成上述功能。



### 时区那些事儿

1884年在华盛顿召开国际经度会议时，为了克服时间上的混乱，规定将全球划分为24个时区。规定英国（格林尼治天文台旧址）为本初子午线，即零度经线。
![](/assets/timg_zone.jpg)
360度分为24个时区 每个时区时间差1个小时，所以北京早伦敦8个小时。

1918年，中央观象台提出划分全国为五个时区：长白时区（GMT+8:30）、中原时区（GMT+8）、陇蜀时区（GMT+7）、回藏时区（GMT+6）、昆仑时区（GMT+5:30）。
中华人民共和国成立后，为了方便管理，使用了单一时区制，以东八区的北京时间为标准时。中国的五时区划分制也基本退出历史舞台。
1986年，新疆维吾尔自治区人民政府决定，从1986年2月1日起，全疆使用乌鲁木齐时间，凡必须使用北京时间的单位，在行文时要说明是北京时间。





