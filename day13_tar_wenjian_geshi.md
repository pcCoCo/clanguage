# tar文件格式

Nine people can’t make a baby in a month.” (regarding the addition of more programmers to get a project completed faster)
九个人在一个月内不能生育。“（关于增加更多的程序员以更快地完成项目）

Rome was not built in a day。
传说特洛亚王子的后裔公主来茜西尔维娅被战神马尔斯所幸，生下了孪生兄弟罗马路斯和莱谟斯。当时的国王知道后杀死了他们的母亲，并把兄弟俩装进篮筐，扔进波涛翻滚的台伯尔河。是一只母狼救了他们，并用自己的乳汁哺育了兄弟两人。后来兄弟俩长大成人，为了替母亲报仇，他们想法杀死了国王，这两个天赋异禀的狼养大的孩子一夜之间建造了罗马城。
实际上，原文的意思是“罗马不是在一个白天建成的”，not “in a day”，应该是在晚上“in a night”
后来，随着时间的推移，这句话的意思慢慢转变，由于古罗马城建筑先进、繁复、建筑技术高超、设计精湛，后人用“罗马不是一天建成的”，表示很多先进技术、物质文明、甚至一个成就，都不是简单达成的，而是经由很多人、或者很多努力，才能够完成的。


## tar文件格式解析

参考资料

https://www.gnu.org/software/tar/manual/html_node/Standard.html
http://en.academic.ru/dic.nsf/enwiki/11782062
http://www.mkssoftware.com/docs/man4/tar.4.asp
http://www.fileformat.info/format/tar/corion.htm


tar文件格式

http://www.moon-soft.com/program/FORMAT/comm/tar.htm


```
struct tar_header
{
	char name[100];//文件名
	char mode[8];
	char uid[8];
	char gid[8];
	char size[12]; //文件大小的八进制数的字符串形式
	char mtime[12];
	char chksum[8];
	char typeflag;
	char linkname[100];
	char magic[6];
	char version[2];
	char uname[32];
	char gname[32];
	char devmajor[8];
	char devminor[8];
	char prefix[155];
	char padding[12];
};
```
  
> 在tar文件中 文件信息的数据结构后跟着的就是文件的内容。文件内容以512字节为一个block进行分割，最后一个block不足部分以0补齐。所有文件都存储完了以后，最后存放一个全零的tar结构。

两个文件的合并成的tar包首先存放第一个文件的tar头结构，然后存储文件内容，接着存储第二个文件的tar头结构，然后存储文件内容,文件末尾还有一个全零的tar结构。

> 所有的tar文件大小应该都是512的倍数。

一个空文件打包后为512*3字节，包括一个tar结构头，一个全零的block存储文件内容，一个全零的tar结构。

> size数组所能表示的大小问题

字符串以'\0'即为，意味着字符串只有11位八进制。
即为11111111111转化为十进制为8589934591，即size数组所能表示的文件大小字节数是8589934591 ~= 8GB
足够大，我们生活中绝大数使用完全可以满足。


问题1  
        为什么这些数据成员都是使用char类型而不是用int
        提示：大小端对齐。
    
问题2
        下面输出的结果是多少 ?为什么? 512

```
int main()
{
        printf("%u\n",sizeof(struct tar_header));
        return 0;
}  
```

size为文件大小的八进制字节表示，例如文件大小为90个字节，那么这里就是八进制的90，即为132。
文件大小，修改时间，checksum都是存储的对应的八进制字符串，字符串最后一个字符为空格字符 。

checksum的计算方法为除去checksum字段其他所有的512-8共504个字节的ascii码相加的值再加上256(checksum当作八个空格，即8*0x20）。

没有数据的地方全部填充为'\0'。
往tar文件中添加一个空文件，那么tar文件将新增1024Byte大小(512Byte的tar_header加上512Byte的全0数据)

checksum的计算方法为出去checksum字段其他所有的512-8共504个字节的ascii码相加的值再加上256(checksum当作八个空格，即8*0x20）


然而根据我们测试发现，在新版本tar工具中机制已经发生了一些变化。

    pc@iZ25g2i2xsmZ:~$ tar --version
    tar (GNU tar) 1.27.1
    Copyright (C) 2013 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.
    Written by John Gilmore and Jay Fenlason.

在该版本的tar工具中 **文件大小是10240Byte的整数倍**。，文件大小只能是10240*n,n=0,1,2,3,4,...n

pc@iZ25g2i2xsmZ:~$ ll tt*
```
-rw-rw-r-- 1 pc pc     0 Feb  9 18:20 tt
```
pc@iZ25g2i2xsmZ:~$ tar cvf tt.tar tt tt tt tt tt tt tt tt tt tt tt tt tt
```
tt
tt
tt
tt
tt
tt
tt
tt
tt
tt
tt
tt
tt
```
pc@iZ25g2i2xsmZ:~$ ll tt*
```
-rw-rw-r-- 1 pc pc     0 Feb  9 18:20 tt
-rw-rw-r-- 1 pc pc 10240 Feb  9 18:24 tt.tar
```
> 空文件打包进tar文件的时候只占头512字节，无数据空间。


### 解包tar

解包更容易一些 直接有已经打包的tar文件即可进行。

```
int main()
{
	//printf("%lu\n",sizeof(struct tar_header));
	char buf[sizeof(struct tar_header)];
	FILE *fp = fopen("my.tar","rb");
	if( fp == NULL )
	{
	    fprintf(stderr,"file not found");
	    return 0;
	}
	fread(buf,1,sizeof(struct tar_header),fp);
	struct tar_header * head = (struct tar_header *)buf;
	printf("name %s,size %s\n",head->name,head->size);
	fclose(fp);
	return 0;
}
```

pc@iZ25g2i2xsmZ:~$ ll
-rw-rw-r-- 1 pc   pc     716 Dec 16 14:15 main.c

pc@iZ25g2i2xsmZ:~$ tar cvf my.tar main.c
main.c
pc@iZ25g2i2xsmZ:~$ ls
a.out  code  main.c  my.tar



pc@iZ25g2i2xsmZ:~$ ./a.out 
name main.c,size 00000001314
pc@iZ25g2i2xsmZ:~$ ll
-rw-rw-r-- 1 pc   pc     716 Dec 16 14:15 main.c
-rw-rw-r-- 1 pc   pc   10240 Dec 16 14:16 my.tar

八进制的1314对应十进制的716。


在解包的案例中 我们只需要关注最核心的问题，文件名和文件大小。其余的属性待大家能完成这个基本功能之后再进行深入学习和理解。


那么问题来了 如何将8进制的字符串转化为十进制数呢?

```
int myatoi(const char * str)
{
    int ret = 0;
    int i ;
    // 每个位(数值*该位权值)之和,前11位为有效字符 最后为'\0'
    for (i = 0; i < 11; ++i)
        ret += (str[i]-'0') * (int)pow(8,11-i-1);
    return ret ;    
}
```

 实现代码

```
#include <stdio.h>
#include <math.h>
#define HEAD_SIZE sizeof(struct tar_header)

int myatoi(const char * str,int fbase,int tobase)
{
    int ret = 0;
    int value = atoi(str);
    //先将该数转化为十进制 每个位(数值*该位权值)之和
    int i ;
    //前11位为有效字符 最后为'\0'
    for (i = 0; i < 11; ++i)
    {
        ret += (str[i]-'0') * (int)pow(fbase,11-i-1);
    }
    if(tobase == 10)
        return ret ;
    else //10 ---> n
    {
        fprintf(stderr,"function have't complete code");
        return 0;
    }
}

int main(int argc,char **argv)
{
    if( argc < 2 )
    {
        fprintf(stderr,"USEAGE %s filename",argv[0]);
        return 1;
    }
    //printf("%lu\n",sizeof(struct tar_header));
    char buf[sizeof(struct tar_header)];
    FILE *fp = fopen(argv[1],"rb");
    if( fp == NULL )
    {
        fprintf(stderr,"file not found");
        return 0;
    }
    unsigned int ret ;
    int need_write_len;
    while ( ret = fread(buf,1,sizeof(struct tar_header),fp) )
    {
        struct tar_header * head = (struct tar_header *)buf;
        if( head->name[0] == '\0')
        {
            printf("tar file END\n");
            break;
        }
        need_write_len = myatoi(head->size);
        printf("name %s,size 0%s is %d\n",head->name,head->size,need_write_len);
        FILE *data_file_p = fopen(head->name,"wb");
        if( data_file_p == NULL)
        {
            fprintf(stderr,"FILE %s can't write",head->name);
            continue;
        }
        while( need_write_len > 0)
        {
            ret = fread(buf,HEAD_SIZE,1,fp);
            if( ret == 0 )
                break;
            fwrite(buf,1,need_write_len > HEAD_SIZE ?HEAD_SIZE:need_write_len, data_file_p);
            printf("ret = %d need_write_len = %d",ret,need_write_len);
            need_write_len -= HEAD_SIZE;
        }
        fclose(data_file_p);
    }
    fclose(fp);
    return 0;
}								

```


效果展示

pc@iZ25g2i2xsmZ:~/code$ gcc main2.c -lm
pc@iZ25g2i2xsmZ:~/code$ ls
```
a.out  main2.c  mmy.tar  my.tar  t2.tar  t.tar
```

pc@iZ25g2i2xsmZ:~/code$ ./a.out t2.tar 
```
name t8,size 000000020000 is 8192
ret = 1 need_write_len = 8192ret = 1 need_write_len = 7680ret = 1 need_write_len = 7168ret = 1 need_write_len = 6656ret = 1 need_write_len = 6144ret = 1 need_write_len = 5632ret = 1 need_write_len = 5120ret = 1 need_write_len = 4608ret = 1 need_write_len = 4096ret = 1 need_write_len = 3584ret = 1 need_write_len = 3072ret = 1 need_write_len = 2560ret = 1 need_write_len = 2048ret = 1 need_write_len = 1536ret = 1 need_write_len = 1024ret = 1 need_write_len = 512name i,size 000000000012 is 10
ret = 1 need_write_len = 10tar file END
```

pc@iZ25g2i2xsmZ:~/code$ ll
```
total 100
drwxrwxr-x 2 pc pc  4096 Dec 17 23:07 ./
drwxr-xr-x 4 pc pc  4096 Dec 17 23:00 ../
-rwxrwxr-x 1 pc pc 16488 Dec 17 22:58 a.out*
-rw-rw-r-- 1 pc pc    10 Dec 17 23:07 i
-rw-rw-r-- 1 pc pc  1969 Dec 17 22:58 main2.c
-rw-rw-r-- 1 pc pc 10240 Dec 17 20:35 mmy.tar
-rw-rw-r-- 1 pc pc 10240 Dec 17 20:35 my.tar
-rw-rw-r-- 1 pc pc 20480 Dec 17 20:35 t2.tar
-rw-rw-r-- 1 pc pc  8192 Dec 17 23:07 t8
-rw-rw-r-- 1 pc pc 10240 Dec 17 20:35 t.tar

```



### 打包tar


了解了tar包的文件格式之后，打包tar就是一个较之于解包的逆向工程。

打包需要准备的参数更多 比如uid、gid、mtime、checksum 如果准备错误就会导致使用标准tar工具无法解包。
如果我们一开始就介入很多属性就无法让我们入手，我们还是只需要最常用的文件名和文件大小。


## gzip


### gzip不是一种算法

网上有人用“算法”来形容gzip，其实gzip根本不是一种算法，可以说它是一种压缩工具（software，见《Data Compression – The CompleteReference》 3.23节），或者说它是一种文件格式（file format，见RFC1952开篇），但绝对不是一种算法！！！这里澄清此概念。

我更倾向于将gzip作为一种文件格式来看待。因为毕竟对应的压缩结果是完全按照gzip压缩文件格式组织的，不管用什么软件去压，也不管用哪种实现库去压，只要最终结果是gzip的压缩结果，那么该结果肯定是按照gzip文件格式组织的！我把gzip文件格式理解为一只虾，一只虾分成三个部分：头、中间、尾巴，gzip也一样，有文件头，文件尾，中间保存被压缩之后的数据（参考文档：RFC1952）

`本质上和zlib都是类似的按照自己的格式对deflate算法处理之后的数据进行的封装。GZIP中字节序是LSB方式，即Little-Endian小端字节序，与ZLIB中的相反。`


1f8b 0800 8e0b 9858

58980b8e 换算成十进制 1486359438 是UNIX/LINUX时间戳 
在线转换  http://tool.chinaz.com/Tools/unixtime.aspx  : 2017/2/6 13:37:18


### gzip文件格式分析


+------+------+------+-------+---+---+---+---+------+-----+
|  ID1 |  ID2 |  CM  |  FLG  |     MTIME     |  XFL |  OS |
+------+------+------+-------+---+---+---+---+------+-----+
if FLG.FEXTRA set
+---+---+=================================+
| XLEN  |   XLEN bytes of "extra field"...| 
+---+---+=================================+
if FLG.FNAME set
+=========================================+
| original file name, zero-terminated...  |
+=========================================+
if FLG.FCOMMENT set
+===================================+
| file comment, zero-terminated...  | 
+===================================+
if FLG.FHCRC set
+---+---+
| CRC16 |
+---+---+
+=======================+
|...compressed blocks...| 
+=======================+
+---+---+---+---+---+---+---+---+
|     CRC32     |     ISIZE     |
+---+---+---+---+---+---+---+---+


> gzip文件格式标准文档

```
https://tools.ietf.org/html/rfc1952
http://www.faqs.org/rfcs/rfc1952.html
http://blog.itpub.net/10794571/viewspace-974302/
http://blog.csdn.net/jison_r_wang/article/details/52068607
```


CRC32（Cyclic Redundancy Check）：用标准循环冗余校验算法对原始数据进行计算的结果。
ISIZE（InputSIZE）：将原始数据大小对2^32取模的结果（因为只能用四个字节存结果，所以只能对2^32取模）。

### zlib库简介


### zlib库解析gzip文件

在contrib和test目录中有相应实现例子。contrib\minizip\中的minizip.c/miniunz.c实现压缩、解压ZIP文件。
test\minigzip.c实现压缩、解压gzip文件（用nmake运行win32\下的Makefile.msc可编译它）。
不同于zip格式，gzip格式(.gz)只用于压缩单个文件。有多个文件时，通常先将它们合并成一个tar文件，再用gzip进行压缩。contrib\untgz\untgz.c实现一次性解压.tar.gz(.tgz)文件。

源码zlib1211.tar.gz

解压 tar -zxvf zlib1211.tar.gz

pc@iZ25g2i2xsmZ:~/code/$           cd zlib-1.2.11/
pc@iZ25g2i2xsmZ:~/code/zlib-1.2.11$configure && make
pc@iZ25g2i2xsmZ:~/code/zlib-1.2.11/project$vim Makefile
```
all:
    gcc -o pcgzip gzjoin.c -I. -L. -lz 
```

pc@iZ25g2i2xsmZ:~/code/zlib-1.2.11/project$ ls
gzjoin.c  libz.a  Makefile  pcgzip  zconf.h  zlib.h



### zlib中最简洁的两个函数

函数原型
`int compress(Bytef *dest, uLongf *destLen, const Bytef *source, uLong sourceLen);`

函数功能

compress函数将 source 缓冲区中的内容压缩到 dest 缓冲区。 sourceLen 表示source 缓冲区的字节大小。`注意函数的第二个参数 destLen 是传址调用。`当调用函数时，destLen表示 dest 缓冲区的大小，destLen > (sourceLen + 12)*100.1%。当函数退出后，destLen 表示压缩后缓冲区的实际大小。此时 destLen / sourceLen 正好是压缩率。

函数返回值

compress 若成功，则返回 Z_OK；若没有足够内存，则返回 Z_MEM_ERROR；若输出缓冲区不够大，则返回 Z_BUF_ERROR。


函数原型 

`int uncompress(Bytef *dest, uLongf *destLen, const Bytef *source, uLong sourceLen);`

函数功能

uncompress 函数将 source 缓冲区的内容解压缩到 dest 缓冲区。sourceLen 是 source 缓冲区的大小(以字节计)。注意函数的第二个参数 destLen 是传址调用。当调用函数时，destLen 表示 dest 缓冲区的大小， dest 缓冲区要足以容下解压后的数据。在进行解压缩时，需要提前知道被压缩的数据解压出来会有多大。这就要求在进行压缩之前，保存原始数据的大小(也就是解压后的数据的大小)。这不是 zlib 函数库的功能，需要我们做额外的工作。当函数退出后， destLen 是解压出来的数据的实际大小。


函数返回值
uncompress 若成功，则返回 Z_OK ；若没有足够内存，则返回 Z_MEM_ERROR；若输出缓冲区不够大，则返回 Z_BUF_ERROR。若输入数据有误，则返回 Z_DATA_ERROR。


由于无法预测压缩包解压之后的大小，所以只能预先分配一段空间。
言外之意就是如果文件太大，就会导致解压失败(一般来说如果内存需求比较大，内存分配失败就会间接导致文件解压失败)。

pc@iZ25g2i2xsmZ:~/code/project$ gcc -o pcgzip 01test_compress.c -I. -L. -lz 
pc@iZ25g2i2xsmZ:~/code/project$ ./pcgzip 
compress OK
len:21,data:xNIMK
unpressing data
uncompress OK
len:13 data:abcdefghijkl


pc@iZ25g2i2xsmZ:~/code/project/tgzip$ ll 
total 28
drwxrwxr-x 2 pc pc  4096 Feb  7 17:41 ./
drwxrwxr-x 3 pc pc  4096 Feb  7 17:02 ../
-rw-rw-r-- 1 pc pc    39 Feb  7 17:41 t.gz

头10字节+0字节拓展+21字节压缩数据+4字节CRC32+4字节文件大小 


Linux压缩保留源文件的方法： 
    
    gzip –c filename > filename.gz 
    
Linux解压缩保留源文件的方法： 

    gunzip –c filename.gz > filename 



## 重新认识地址和指针

### 指针的本质

int number = 0;
int *p = &number;

int *pp = &p;

如果有指针 int \*\*\*\*\*\*\*\* p ; 呢？


### 从Linux内核代码中学习获得结构体成员偏移量的方法
http://blog.csdn.net/livelylittlefish/article/details/20565261


