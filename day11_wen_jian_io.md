# 章节11-文件IO

## 文件概念

再融合一下这个概念 

在UNIX/Linux上 **一切皆文件**，包括设备文件和普通文件。

文件就是字节序列，字节流。
流是程序输入或输出的一个连续的字节序列，设备(例如鼠标、键盘、磁盘、显示器、网络)的输入和输出都是用流来处理的。

只由`ASCII码`字符构成的文件称之为文本文件，其余的都称之为二进制文件。
从另外的角度来看，我们应该认为所有的文件都是二进制文件，只是文本文件是一种特殊的二进制文件，其中只有ASCII码的字符。

这样处理文件内容的应用的程序员就可以无需了解具体的磁盘技术，专心于如何做好文件内容应用。


## 打开文件



```
FILE * fopen ( const char * filename, const char * mode );
```

**参数1** 路径/文件名

**参数2** 文件的打开模式
r -read  表示读
w -write 表示写
b -binary表示二进制方式
a -append表示追加

"r"  表示只读 
"rb" 表示以二进制方式只读
"r+" 
"rb+"

"w"  
"wb" 
"w+" 
"wb+"

**返回值**

文 件结构体代表一个打开的文件，系统中的每个打开的文件在内核空间都有一个关联的struct file。它由内核在打开文件时创建，并传递给在文件上进行操作的任何函数。在文件的所有实例都关闭后，内核释放这个数据结构。


如果你不小心写成这样 


```
FILE *fp = ("test.txt","r");
if(fp == NULL)
{
    fprintf(stderr,"file not found");
    return -1;
}

```
> 如果这样写会出什么错误，有什么危害？



### FILE结构体剖析 

```
grep -rn "struct _IO_FILE {" --include="*.h" /usr/include

```



```
现代的FILE结构体在不断变化，不同的环境有所区别。

```

其中一种实现方式  VS2010

typedef  struct _iobuf 
{
　　　　char *_ptr;      
　　　　int _cnt;        
　　　　char *_base;     //文件缓冲区指针 
　　　　int _flag;       //文件标志位
　　　　int _file;       //文件描述符
　　　　int _charbuf;    //检查缓冲区状况,如果无缓冲区则不读取
　　　　int _bufsiz;     //缓冲区长度
　　　　char *_tmpfname; //临时文件名
}FILE;




`但是万变不离其宗，他们都至少有很多通用的结构体成员。`

* 文件读写位置

    该成员的记录着当前读/写的位置 相对于文件开始位置的偏移
    
    
* 文件读写模式

    该成员表示着在**打开**该结构体所标识的**文件的时候是以什么权限打开的**。
    防止用户对文件的不合法的操作。
比如 以只读方式打开的文件，在调用函数往该文件写入的时候能够进行一个错误检测。

    
* 文件缓冲区指针和缓冲区长度
    
    文件缓冲区指针保存着该文件的文件缓冲区的首地址。
    缓冲区长度在Linux下一般为8192字节。

### 预定义的标准输入输出

属于C标准库预定义的三个标准文件流

```
#include <stdio.h>
extern FILE *stdin;
extern FILE *stdout;
extern FILE *stderr;
```

标准输入 stdin、
标准输出 stdout、
标准错误 stderr

定义形式
```
Linux中的

/* Standard streams.  */
extern struct _IO_FILE *stdin;      /* Standard input stream.  */
extern struct _IO_FILE *stdout;     /* Standard output stream.  */
extern struct _IO_FILE *stderr;     /* Standard error output stream.  */
/* C89/C99 say they're macros.  Make them happy.  */
#define stdin stdin
#define stdout stdout
#define stderr stderr

```



VS中
```
#define stdin  (__acrt_iob_func(0))
#define stdout (__acrt_iob_func(1))
#define stderr (__acrt_iob_func(2))
```



执行一个shell命令 创建一个进程时通常会自动打开三个标准文件，即标准输入文件（stdin），默认对应终端的键盘；标准输出文件（stdout）和标准错误输出文件（stderr），这两个文件默认都对应终端的屏幕。进程将从标准输入文件中得到输入数据，将正常输出数据输出到标准输出文件，而将错误信息送到标准错误文件中。

C库提供的标准I/O函数，这些函数操作的是文件描述符，是标准输入流、输出流或者错误流，而不是键盘的设备文件<一种标准输入设备>和显示器的设备文件<一种标准输出设备>。如果改变了标准输出流和显示器设备文件之间的对应关系，那么可能结果就不会在显示器上。这种情况出现在命令行中使用重定向符号的时候，标准输入、标准输出和标准错误对应的就不是键盘设备文件和显示器设备文件，而是指定的某个普通的文件。

在默认情况下，stdout是行缓冲的，他的输出会放在输出缓冲区里面，只有到换行的时候，才会输出到输出设备中。而stderr是无缓冲的，会直接输出到输出设备中。

**标准流在调用 exit(3) 和程序正常中止时被关闭。**

## 关闭文件

fclose()函数原型

```
int fclose ( FILE * stream );
```
函数功能 关闭stream所标识的(打开的)文件。



### 自己打开的文件含着泪也要关闭

要问为什么？

![](/assets/cantopenfile.png)

一个进程所能打开的文件句柄数量是有限制的，如果只打开不关闭只会导致该进程后面可以打开的文件数量越来越少，这是 **文件句柄资源泄露**。
![](/assets/kule1.jpg)



## 顺序读写文件


### 按单个字符读写

fgetc()
getc()

fputc
putc


### 按行读写
fgets()
fputs()


### 按格式读写
fscanf()
fprintf()


## 随机读写文件

fseek()函数
ftell()

### 操作文件游标到文件开始

fseek()函数可以完成功能 fseek(fp,0,SEEK_SET);
作为非常懒的C程序员于是发明了一个新的函数 `rewind(fp);` 就可以了。


## 文件缓冲区

标准I/O库提供缓冲的目的是尽可能地减少使用read和write的次数。他也对每个I/O流自动地进行缓冲管理，从而避免了应用程序需要考虑这一点所带来的麻烦。标准I/O提供了三种类型的缓冲：

1、全缓冲。

    这种情况下，在填满标准I/O缓冲区后才进行实际I/O操作。对于驻留在磁盘上的文件通常是由标准I/O库实施全缓冲。一个流上执行第一次I/O操作时，相关标准I/O函数通常调用malloc获得需使用的缓冲区。
    
    术语冲洗说明I/O缓冲区的写操作。缓冲区可由标准I/O例程自动冲洗，或者可以调用函数fflush冲洗一个流。值得引起注意的是在UNIX环境 中，flush有两种意思。在标准I/O库方面，flush意味着将缓冲区中的内容写到磁盘上。在终端驱动程序方面flush表示丢弃已存储在缓冲区中的数据。
    
2、行缓冲。

    在这种情况下，当在输入和输出中遇到换行符时，标准I/O库执行I/O操作。这允许我们一次输出一个字符，但只有在写了一行之后才进行实际I/O操作。当流涉及一个终端时，通常使用行缓冲。
    
    对于行缓冲有两个限制。第一，因为标准I/O库用来收集每一行的缓冲区的长度是固定的，所以只要填满了缓冲区，那么即使没有写一个换行符，也进行I/O操 作。第二，任何时候只要通过标准I/O库要求从a一个布袋缓冲的流，或者b一个行缓冲的流得到输入数据，那么就会造成冲洗所有行缓冲输出流。在b中带了一 个在括号中的说明，其理由是，所需的数据可能已在缓冲区中，他并不需求在需要数据时才从内核读数据。很明显，从不带缓冲的一个流中进行输入要求当时从内核得到数据。

3、不带缓冲。

    标准I/O库不对字符进行缓冲存储。例如，如果用I/O函数fputs写15个字符到不带缓冲的流中，则该函数很可能用write系统调用函数将这些字符立即写至相关联的打开文件中。标准出错流stderr通常是不带缓冲的，这就使得出错信息可以尽快显示出来，而不管它们是否含有一个换行符。
    
## 文件啥时候结束

### EOF

End Of File,EOF
表示"文字流"（stream）的结尾。这里的"文字流"，可以是文件（file），也可以是标准输入（stdin）。
如果在读取文件的返回EOF表示文件无更多的数据可读取，即文件结束。

It is a macro definition of type int that expands into a negative integral constant expression (generally, -1).
It is used as the value returned by several functions in header <cstdio> to indicate that the End-of-File has been reached or to signal some other failure conditions.

It is also used as the value to represent an invalid character.
可被用于 表示无效字符。

通常EOF在stdio.h头文件定义为:


```
　　#define EOF (-1)
```


比如打印当前目录下的main.c中的所有内容 


```
　　char c;
　　while ((c = fgetc(fp)) != EOF) 
    {
　　　　putchar (c);
　　}
```

值得注意的是EOF并不是文件数据的最后一个字符数据。

### feof

C语言中，当把数据以二进制形式存放到文件中时，就会有-1值的出现，此时不能采用EOF作为二进制文件的结束标志。为解决这个问题，ANSI C提供一个feof函数，用来判断文件是否结束。

如果遇到文件结束，函数feof（fp）的值为1，否则为0.feof函数既可用以判断二进制文件是否结束，也可以用以判断文本文件是否结束。

Check end-of-file indicator
Checks whether the end-of-File indicator associated with stream is set, returning a value different from zero if it is.

This indicator is generally set by a previous operation on the stream that attempted to read at or past the end-of-file.

Notice that stream's internal position indicator may point to the end-of-file for the next operation, but still, the end-of-file indicator may not be set until an operation attempts to read at that point.

This indicator is cleared by a call to clearerr, rewind, fseek, fsetpos or freopen. Although if the position indicator is not repositioned by such a call, the next i/o operation is likely to set the indicator again.




**一般在读取文件的场景中，一般都是以下的使用流程:**
```
1、先读取文件
2、判断feof函数返回值；如果为0继续，否则执行第5步
3、将读取到的数据进行处理
4、继续第1步
5、结束
```

### fgets


## 案例
1. 实现一个cp命令 复制指定文件

- 对文件进行简单的加密

- fgets、fputs实现加密

- 超大文件排序

- 解析文件内容并且追加




## 作业练习

1. 简单的预处理器。写一个程序经过 `./a.out main.c main2.c`可以将main.c中的行注释全部去掉并且存储修改之后的内容到main.c中。

比如 main.c 如下
```
int main()
{
    //这是一个测试程序
    int n;             //变量n存储输入的值
    system("CHCP 936");
    while(1)
    {
        scanf("%d",&n);
        printf("//total times:%d\n",func(n));
    }
    return 0;
}
```



