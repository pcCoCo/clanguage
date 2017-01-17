数组就是存储一组相同数据类型的数据的集合。

## 一维数组的定义和使用


### 数组引入

写一个程序，接收5个学成的成绩，接收完之后再统一打印输出到控制台。

学生解决方案：
1）for循环5次，每次接收用户数据，并且打印。(不符合题意)
2）定义5个变量，保存5个学生的成绩，最后打印输出。（数据一多，也不行）

针对类似的问题，C语言提供了数组这个概念。
在数组中，每个成员称为元素。 

tfboys每个成员就是一个元素。



### 定义
一维数组的定义形式  `元素类型 数组名[元素个数]  [ = 可能存在的初始化表达式]`;



访问数组的元素形式  `数组名[数组元素下标]`;

值得注意的是，C语言没有提供**数组边界检查的机制**，因此再访问数组元素的时候一定要注意元素下标的合法性。防止造成不可预期的非法访问。  
合法的元素下标是小于该空间大小的非负数。

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

* 定义数组时，\[\]里必须是常量。使用数组时，可以是常量，也可以是变量。
* 数组的下标的取值范围：0 ~ 数组长度-1
* C99中才开始支持数组长度是变量的语法；但是C89的编译器并不能支持

```

#include <stdio.h>
int main()
{
    int n;
    scanf("%d",&n);
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

* 往数组存储数据


* 从数组取出数据


## 数组在内存中的存储方式(画图)

同一个数组的所有成员都是相同的数据类型，同时所有的成员在内存中的地址是连续的，数组名可以表示地址的常量，代表数组中首元素的地址。

数组在内存中存储的完整过程：

* 为数组申请内存，占的内存=数组长度\*单个元素占的字节数
    演示： sizeof(数组名)
* 每个数组元素的值是以补码的形式存储在内存中。



## 数组的简单算法

* 数组长度计算

  int arr\[\] = {1,2,3,4,5,6,7,8};

  sizeof\(arr\); // 就可以得到这个数组占用的总的字节数.

  sizeof\(arr\[0\]\); // 每个元素占的字节数

  int len = sizeof\(arr\) / sizeof\(arr\[0\]\);
  
  

* 数组的几种简单算法

  * 找出数组中的最大值/最小值

```
int arr[] = {10, 21, 3, 442, 5, 46, 57};    
int max =  arr[0];
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

* 求出所有元素的累加和平均值
* 查找数组中的第二大元素

* 数组逆置

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

rand\(\) 函数返回值是一个随机数

可能经常需要使用rand\(\)用到的技巧是** rand\(\) % m + n**

效果就是使产生的随机数范围在 \[n,m\]

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
>
> 专门有一个从事真随机生成的公司，他们使用硬件，通过搜集大气噪声产生随机二进制位来产生真随机数。[http://www.random.org/](http://www.random.org/)

我们学习C的时候还需要去研制一个真随机数发生器那就有违初衷了。

以时间作为随机数种子，使rand\(\)函数每次产生不一样的随机数。  
虽然不能达到真随机的严格要求，但是对于一般的程序来讲是完全可用的。

只需要这行代码 **srand\(\(unsigned int\)time\(NULL\)\);**

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

## 案例

### 查找数组最大值

假设给定数组，数组成员随机，求出数组中的最大值

参考答案：

```
// 查找数组最大值
int main()
{

    int arr[] = {19, -100, 3, 95, 980, 617, 16};

    int i;
    int max = arr[0];
    for(i = 1; i < sizeof(arr) / sizeof(arr[0]); i++)
    {
        if (arr[i] > max)
        {
            max = arr[i];
        }
    }

    printf("最大值为：%d\n", max);
    return 0;
}
```

### 查找数组第二大元素

```
// 查找数组第二大元素
int main()
{

    int arr[] = {-19, 1000, 3, 95, 980, 617, 16};

    int i;
    int max;
    int smax;

    // 默认数组的第一个和第二个成员分别为最大值和第二大值
    if (arr[0] > arr[1])
    {   
        max = arr[0];
        smax = arr[1];
    }
    else
    {
        max = arr[1];
        smax = arr[0];
    }

    // 从第三个元素开始遍历
    for(i = 2; i < sizeof(arr) / sizeof(arr[0]); i++)
    {
        if (arr[i] > max)
        {
            
            smax = max;

            max = arr[i];
            
        }
        else if (arr[i] < max && arr[i] > smax) // 介于最大值和和第二大值之间的数
        {
            smax = arr[i];
        }
    }

    printf("最大值为：%d\n", max);
    printf("第二大值为：%d\n", smax);
    return 0;
}
```

### 数组逆置

比如有数组arr = \[1,2,3,4,5\];  
 逆置之后，变成了：\[5,4,3,2,1\];

参考答案：

```
// 数组逆置
int main()
{

    int arr[] = {45, 12, 987, 40, 86, 25, 59};

    // 思路： 只要遍历 len/2次，
    /*
    arr[0] --- arr[6]
    arr[1] --- arr[5]

    ...

    结论: i + j = len - 1
    j = len - 1 - i
    */

    int len = sizeof(arr) / sizeof(arr[0]);
    int i; 
    for(i = 0; i<len/2; i++)
    {
        int temp = arr[i];
        arr[i] = arr[len - 1 - i];
        arr[len - 1 - i] = temp;
    }

    for (int i = 0; i < len; ++i)
    {
        printf("%d\t", arr[i]);
    }
    printf("\n");
    return 0 ;
}
```

### 三维数组排序

将以下数组排序，  
int a\[2\]\[3\]\[5\] = { { {32,56,21,74,32}, {56,31,897,93,22}, {47,63,96,333,99} },   
    { {666,888,35,97,2}, {654,87,13,67,3}, {67,56,40,34,10} } };

思路：  
把这个三维数组放到一个一维数组里面  
把一维数组排序  
把一维数组再放回到这个三维数组里

参考答案：

```
int main()
{
    int a[2][3][5] = { { {32,56,21,74,32}, {56,31,897,93,22}, {47,63,96,333,99} }, 
    { {666,888,35,97,2}, {654,87,13,67,3}, {67,56,40,34,10} } };

    int b[30] = { 0 };
    int i, j, k;
    int index = 0;
    for (i = 0; i < 2; i++)
    {
        for (j = 0; j < 3; j++)
        {
            for (k = 0; k < 5; k++)
            {
                b[index] = a[i][j][k];
                index++;
            }
        }
    }

    for (i = 0; i < 30; i++)
    {
        for (j = 1; j < 30 - i; j++)
        {
            if (b[j - 1] > b[j])
            {
                int tmp = b[j];
                b[j] = b[j - 1];
                b[j - 1] = tmp;
            }
        }
    }

    index = 0;
    for (i = 0; i < 2; i++)
    {
        for (j = 0; j < 3; j++)
        {
            for (k = 0; k < 5; k++)
            {
                a[i][j][k] = b[index];
                index++;
            }
        }
    }

    for (i = 0; i < 2; i++)
    {
        for (j = 0; j < 3; j++)
        {
            for (k = 0; k < 5; k++)
            {
                printf("a[%d][%d][%d] = %d\n", i, j, k, a[i][j][k]);
            }
        }
    }
    return 0;
}
```

### 去除字符串中间的空格

比如：  
char str\[100\] = "hello world    ";  
要求：要去掉字符串最右面的空格，而不能去掉字符串中间的空格

思路：  
从后往前数，遇到不是空格的字符就把这个字符的下一个字符设置为0

参考答案：

```
int main()
{
    char a[100] = "hello      abc     wor ld";
    int index = 0;
    while (a[index])
    {
        index++;
    }

    int i;
    for (i = index - 1; i >= 0; i--)
    {
        if (a[i] != ' ')
        {
            a[i + 1] = 0;
            break;
        }
    }
    printf("(%s)\n", a);
    return 0;
}
```

### 汉字字符串逆置 \(课后作业\)

将一下汉字字符串内容逆置，  
char str\[100\] = "我爱你中国"

思路：  
在UTF8模式下，一个汉字占用3个BYTE  
在GBK下，一个汉字占用2个BYTE  
一个汉字的第一个字节总是小于0的一个整数

我爱你  
-111  
-120  
-26

第一个字节和倒数第3个字节交换  
第二个字节和倒数第二个字节交换  
第三个字节和倒数第一个字节交换

参考答案：

```
int main()
{

    char str[100] = "我爱你中国";

    int max = 0;
    int min = 0;
    while(str[max+1])
    {
        max++;
    }

    while(min < max)
    {
        char temp = str[min];
        str[min] = str[max-2];
        str[max-2] = temp;

        temp= str[min+1];
        str[min+1] = str[max-1];
        str[max-1] = temp;

        temp = str[min+2];
        str[min+2] = str[max];
        str[max] = temp;

        max -= 3;
        min += 3;

    }

    printf("(%s)\n", str);
    return 0;
}
```

### 课后作业

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

2. 从屏幕上输入一串字符串\(长度为n\)，统计其中出现的大写字母、小写字母、数字字符、空白字符\(' ','\n'、'\t'等\)等的数量。

3. 给定一个班级10个人的成绩数组，求除去最高分和最低分之后的平均分。


