# 章节11-文件IO

## 文件概念

再融合一下这个概念 

在UNIX/Linux上 **一切皆文件**，包括设备文件和普通文件。

流是程序输入或输出的一个连续的字节序列，设备(例如鼠标、键盘、磁盘、屏幕、调制解调器和打印机)的输入和输出都是用流来处理的。在C语言中，所有的流均以文件的形式出现----不一定是物理磁盘文件，还可以是对应于某个输入／输出源的逻辑文件。

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
> 这样写会出什么错误，有什么危害？



### FILE结构体剖析 




## 预定义的标准输入输出

属于C标准库预定义的三个标准文件流

标准输入 stdin、
标准输出 stdout、
标准错误 stderr

定义形式
```
/* Standard streams.  */
extern struct _IO_FILE *stdin;      /* Standard input stream.  */
extern struct _IO_FILE *stdout;     /* Standard output stream.  */
extern struct _IO_FILE *stderr;     /* Standard error output stream.  */
/* C89/C99 say they're macros.  Make them happy.  */
#define stdin stdin
#define stdout stdout
#define stderr stderr

```

```
#include <stdio.h>
extern FILE *stdin;
extern FILE *stdout;
extern FILE *stderr;
```


VS中
```
#ifndef _FILE_DEFINED
struct _iobuf 
{
　　　　char *_ptr;      //文件输入的下一个位置
　　　　int _cnt;        //当前缓冲区的相对位置
　　　　char *_base;     //指基础位置(即是文件的其始位置) 
　　　　int _flag;       //文件标志
　　　　int _file;       //文件的有效性验证
　　　　int _charbuf;    //检查缓冲区状况,如果无缓冲区则不读取
　　　　int _bufsiz;     //缓冲区长度
　　　　char *_tmpfname; //临时文件名
};
typedef struct _iobuf FILE;
#define _FILE_DEFINED
#endif

#define stdin  (__acrt_iob_func(0))
#define stdout (__acrt_iob_func(1))
#define stderr (__acrt_iob_func(2))
```



执行一个shell命令 创建一个进程时通常会自动打开三个标准文件，即标准输入文件（stdin），默认对应终端的键盘；标准输出文件（stdout）和标准错误输出文件（stderr），这两个文件默认都对应终端的屏幕。进程将从标准输入文件中得到输入数据，将正常输出数据输出到标准输出文件，而将错误信息送到标准错误文件中。

C库提供的标准I/O函数，这些函数操作的是文件描述符，是标准输入流、输出流或者错误流，而不是键盘的设备文件<一种标准输入设备>和显示器的设备文件<一种标准输出设别>。如果改变了标准输出流和显示器设备文件之间的对应关系，那么可能结果就不会在显示器上。这种情况出现在命令行中使用重定向符号的时候，标准输入、标准输出和标准错误对应的就不是键盘设备文件和显示器设备文件，而是指定的某个普通的文件。

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

fgetc
getc

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
作为非常懒的C程序员于是发明了一个新的函数 rewind(fp)就可以。


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

C语言中，当把数据以二进制形式存放到文件中时，就会有-1值的出现，此时不能采用EOF作为二进制文件的结束标志。为解决这个问题，ANSI C提供一个feof函数，用来判断文件是否结束。如果遇到文件结束，函数feof（fp）的值为1，否则为0.feof函数既可用以判断二进制文件是否结束，也可以用以判断文本文件是否结束。

Check end-of-file indicator
Checks whether the end-of-File indicator associated with stream is set, returning a value different from zero if it is.

This indicator is generally set by a previous operation on the stream that attempted to read at or past the end-of-file.

Notice that stream's internal position indicator may point to the end-of-file for the next operation, but still, the end-of-file indicator may not be set until an operation attempts to read at that point.

This indicator is cleared by a call to clearerr, rewind, fseek, fsetpos or freopen. Although if the position indicator is not repositioned by such a call, the next i/o operation is likely to set the indicator again.


