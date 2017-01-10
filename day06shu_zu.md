# day06-数组

数组就是存储一组相同数据类型的数据的集合。

## 一维数组的定义和使用


一维数组的定义形式  `元素类型 数组名[元素个数]  [ = 可能存在的初始化表达式]`;

访问数组的元素形式  `数组名[元素下标]`;

```
int main()
{
    /*
    这句代码定义了5个int类型的变量。
    第1个变量名是arr[0],
    第2个变量名是arr[1],
    ...
    最后的一个变量名是arr[4],
    */
    int arr[5];
    
    return 0;
}
```



注意：
* 定义数组时，[]里必须是常量。使用数组时，可以是常量，也可以是变量。
* 数组的下标的取值范围：0 ~ 数组长度-1
* C99中才开始支持数组长度是变量的语法；但是C89的编译器并不能支持

```
#include <stdio.h>
int main()
{
    int n;
    scanf("%d",&b);
    int a[n];
    for( int i = 0; i < n; ++i )
    {
        scanf("%d",&a[i]);
    }
    for( int i = 0; i < n; ++i )
    {
        printf("%d",a[i]);
    }    
    return 0;
}

```




## 数组在内存中的存储方式

同一个数组的所有成员都是相同的数据类型，同时所有的成员在内存中的地址是连续的，数组名可以表示地址的常量，代表数组中首元素的地址。

数组在内存中存储的完整过程：

* 为数组申请内存，占的内存=数组长度*单个元素占的字节数
* 将数组元素的补码存储在数组的每个元素中
* 对于单个元素而言，低位存储在低字节，高位存储在高字节

## 一维数组的初始化



```
// 定义数组，并初始化所有成员变量
int arr[10] = {1,2,3,4,5,6,7,8,9,10};
// 初始化前3个成员变量，后面的元素自动初始化为0
int arr[10] = {1,2,3,4,5,6,7,8,9,10};
// 所有成员变量初始化为0
int arr[10] = {1,2,3,4,5,6,7,8,9,10};
// 定义数组，不指定长度，系统根据初始化的元素个数确定数组的长度
int arr[] = {1,2,3,4,5};
```



## 数组的简单算法
* 数组长度计算

    int arr[] = {1,2,3,4,5,6,7,8};
    
    sizeof(arr); // 就可以得到这个数组占用的总的字节数.
    
    sizeof(arr[0]); // 每个元素占的字节数

    int len = sizeof(arr) / sizeof(arr[0]);
    
* 数组的几种简单算法
    - 找出数组中的最大值/最小值
    


```
int arr[] = {10, 21, 3, 442, 5, 46, 57};    
int max = arr[0];
int len = sizeof(arr)/sizeof(arr[0]);
int i;
for(i = 0; i < len; i++)
{
    if(arr[i]) > max)
    {
        max = arr[i];
    }
}

printf("max=%d\n", max);
```



    
    - 求出所有元素的累加和平均值
    - 查找数组中的第二大元素
    
    - 数组逆置

## 冒泡排序



    
## 二维数组
    
    
### 二维数组的定义和使用


### 二维数组的初始化

### 二维数组的存储结构


### 多维数组的奥秘


## 字符串与字符数组

### 字符数组定义

### 字符数组初始化

### 字符数组使用

### 字符串

### scanf函数输入字符串


### 字符串结束的标志

### 字符串处理函数 可以放到指针第二天的课程中讲解

## 随机数产生函数 rand与srand



```
#include <stdlib.h> 

```

rand() 函数返回值是一个随机数

可能经常需要使用rand()用到的技巧是** rand() % m + n**


效果就是使产生的随机数范围在 [n,m]

可是这样产生的随机数却是伪随机的，因为他是有规律的。



```
//file main.c

#include <stdio.h>
int main()
{
    int i ;
    for( i = 0; i <= 3; ++i)
    {
        printf("%d\n",rand());
    }
    return 0;
}
```

执行指令  

`gcc main.c`



`./a.out`


18 676762 89899

`./a.out`

18 676762 89899

两次运行效果完全一致。

这就是规律。

如果我们想程序每次运行的时候不一样怎么做呢？真随机？

> 2015年中国科大研制成功世界上最快的量子随机数发生器，造价十分昂贵。


> 专门有一个从事真随机生成的公司，他们使用硬件，通过搜集大气噪声产生随机二进制位来产生真随机数。http://www.random.org/

我们学习C的时候还需要去研制一个真随机数发生器那就有违初衷了。

以时间作为随机数种子，使rand()函数每次产生不一样的随机数。
虽然不能达到真随机的严格要求，但是对于一般的程序来讲是完全可用的。

只需要这行代码 **srand((unsigned int)time(NULL));**

```
//file main_with_srand.c

#include <stdio.h>
#include <stdlib.h>
int main()
{
    srand((unsigned int)time(NULL));
    int i ;
    for( i = 0; i <= 3; ++i)
    {
        printf("%d\n",rand());
    }
    return 0;
}
```
效果就完全不一样了




What's this fuss about true randomness?

Perhaps you have wondered how predictable machines like computers can generate randomness. In reality, most random numbers used in computer programs are pseudo-random, which means they are generated in a predictable fashion using a mathematical formula. This is fine for many purposes, but it may not be random in the way you expect if you're used to dice rolls and lottery drawings.

RANDOM.ORG offers true random numbers to anyone on the Internet. The randomness comes from atmospheric noise, which for many purposes is better than the pseudo-random number algorithms typically used in computer programs. People use RANDOM.ORG for holding drawings, lotteries and sweepstakes, to drive online games, for scientific applications and for art and music. The service has existed since 1998 and was built by Dr Mads Haahr of the School of Computer Science and Statistics at Trinity College, Dublin in Ireland. Today, RANDOM.ORG is operated by Randomness and Integrity Services Ltd.

As of today, RANDOM.ORG has generated 1.41 trillion random bits for the Internet community.

### 题目

1. 说一下这个代码有什么问题，为什么，怎么改正?

```
#include <stdio.h>
int main(void)
{
    float aH  = 0 ;
    unsigned length;
    scanf("%d",&length);
    
    int i;
    float result = 0;
    
    for (i = O; i <= length-1; i++)
    	result += a[i];
    printf("%f",result);
    return 0;
} 

提示 当length输入为0的时候结果不是输出0，而是错误
```







