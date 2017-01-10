## C99
在ANSI的标准确立后，C语言的规范在一段时间内没有大的变动，然而C++在自己的标准化创建过程中继续发展壮大。《标准修正案一》在1994年为C语言创建了一个新标准，但是只修正了一些C89标准中的细节和增加更多更广的国际字符集支持。不过，这个标准引出了1999年ISO 9899:1999的发表。它通常被称为C99。C99被ANSI于2000年3月采用。

在C99中包括的特性有：


```
增加了对编译器的限制，比如源程序每行要求至少支持到 4095 字节，变量名函数名的要求支持到 63 字节（extern 要求支持到 31）。
增强了预处理功能。例如：
宏支持取可变参数 #define Macro(...) __VA_ARGS__
使用宏的时候，允许省略参数，被省略的参数会被扩展成空串。
支持 // 开头的单行注释（这个特性实际上在C89的很多编译器上已经被支持了）
增加了新关键字 restrict, inline, _Complex, _Imaginary, _Bool
支持 long long, long double _Complex, float _Complex 等类型
支持不定长的数组，即数组长度可以在运行时决定，比如利用变量作为数组长度。声明时使用 int a[var] 的形式。不过考虑到效率和实现，不定长数组不能用在全局，或 struct 与 union 里。
变量声明不必放在语句块的开头，for 语句提倡写成 for(int i=0;i<100;++i) 的形式，即i 只在 for 语句块内部有效。
允许采用（type_name）{xx,xx,xx} 类似于 C++ 的构造函数的形式构造匿名的结构体。
初始化结构的时候允许对特定的元素赋值，形式为：
struct test{int a[3]，b;} foo[] =  { [0].a = {1}, [1].a = 2 };
struct test{int a, b, c, d;} foo =  { .a = 1, .c = 3, 4, .b = 5 };  // 3,4 是对 .c,.d 赋值的
格式化字符串中，利用 \u 支持 unicode 的字符。
支持 16 进制的浮点数的描述。
printf scanf 的格式化串增加了对 long long int 类型的支持。
浮点数的内部数据描述支持了新标准，可以使用 #pragma 编译器指令指定。
除了已有的 __line__ __file__ 以外，增加了 __func__ 得到当前的函数名。
允许编译器化简非常数的表达式。
修改了 / % 处理负数时的定义，这样可以给出明确的结果，例如在C89中-22 / 7 = -3, -22 % 7 = -1，也可以-22 / 7= -4, -22 % 7 = 6。 而C99中明确为 -22 / 7 = -3, -22 % 7 = -1，只有一种结果。
取消了函数返回类型默认为 int 的规定。
允许在 struct 的最后定义的数组不指定其长度，写做 [](flexible array member)。
const const int i 将被当作 const int i 处理。
增加和修改了一些标准头文件，比如定义 bool 的 <stdbool.h> ，定义一些标准长度的 int 的 <inttypes.h> ，定义复数的 <complex.h> ，定义宽字符的 <wctype.h> ，类似于泛型的数学函数 <tgmath.h>， 浮点数相关的 <fenv.h>。 在<stdarg.h> 增加了 va_copy 用于复制 ... 的参数。<time.h> 里增加了 struct tmx ，对 struct tm 做了扩展。
输入输出对宽字符以及长整数等做了相应的支持。
```


但是各个公司对C99的支持所表现出来的兴趣不同。当GCC和其它一些商业编译器支持C99的大部分特性的时候[4]，微软和Borland却似乎对此不感兴趣。

## C11

2011年12月8日，ISO正式发布了新的C语言的新标准C11，之前被称为C1X，官方名称为ISO/IEC 9899:2011。
新的标准提高了对C++的兼容性，并增加了一些新的特性。这些新特性包括：


```
对齐处理(Alignment)的标准化(包括_Alignas标志符，alignof运算符, aligned_alloc函数以及<stdalign.h>头文件。
_Noreturn 函数标记，类似于 gcc 的 __attribute__((noreturn))。
_Generic 关键字。
多线程(Multithreading)支持，包括：
_Thread_local存储类型标识符，<threads.h>头文件，里面包含了线程的创建和管理函数。
_Atomic类型修饰符和<stdatomic.h>头文件。
增强的Unicode的支持。基于C Unicode技术报告ISO/IEC TR 19769:2004，增强了对Unicode的支持。包括为UTF-16/UTF-32编码增加了char16_t和char32_t数据类型，提供了包含unicode字符串转换函数的头文件<uchar.h>.
删除了 gets() 函数，使用一个新的更安全的函数gets_s()替代。
增加了边界检查函数接口，定义了新的安全的函数，例如 fopen_s()，strcat_s() 等等。[5]
增加了更多浮点处理宏。
匿名结构体/联合体支持。这个在gcc早已存在，C11将其引入标准。
静态断言(Static assertions)，_Static_assert()，在解释 #if 和 #error 之后被处理。
新的 fopen() 模式，(“…x”)。类似 POSIX 中的 O_CREAT|O_EXCL，在文件锁中比较常用。
新增 quick_exit() 函数作为第三种终止程序的方式。当 exit()失败时可以做最少的清理工作。
```

