# 章节12-C++基于C的拓展语法

内容范畴规划 不讲C++面向对象、泛型的知识，只涵盖C++基于C的语法拓展

## 此const非彼const

## 函数重载的奥秘

nm命令解析符号表

## 函数默认形参值

## struct只是权宜之计
在C++中使用struct 定义的结构体类型再定义结构体变量时不需要再带struct关键字


## C++简单案例tar文件格式解析

https://www.gnu.org/software/tar/manual/html_node/Standard.html
http://en.academic.ru/dic.nsf/enwiki/11782062
http://www.mkssoftware.com/docs/man4/tar.4.asp
http://www.fileformat.info/format/tar/corion.htm

tar文件格式 http://www.moon-soft.com/program/FORMAT/comm/tar.htm

    struct tar_header
    {
　　	char name[100]; //文件名
　　	char mode[8];
　　	char uid[8];
　　	char gid[8];
　　	char size[12];   //文件大小的八进制数的字符串形式
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

> 在tar文件中 文件信息的数据结构后跟着的就是文件的内容。文件内容以512字节为一个block进行分割，最后一个block不足部分以0补齐。所有文件都存储完了以后，最后存放一个全零的tar结构。

两个文件的合并成的tar包首先存放第一个文件的tar头结构，然后存储文件内容，接着存储第二个文件的tar头结构，然后存储文件内容,文件末尾还有一个全零的tar结构。

> 所有的tar文件大小应该都是512的倍数。

一个空文件打包后为512*3字节，包括一个tar结构头，一个全零的block存储文件内容，一个全零的tar结构。


问题1  
        为什么这些数据成员都是使用char类型而不是用int
    
问题2
        下面输出的结果是多少 ? 512

```
int main()
{
        printf("%u\n",sizeof(struct tar_header));
        return 0;
}  
```

size为文件大小的八进制字节表示，例如文件大小为90个字节，那么这里就是八进制的90，即为132。
文件大小，修改时间，checksum都是存储的对应的八进制字符串，字符串最后一个字符为空格字符 。

checksum的计算方法为出去checksum字段其他所有的512-8共504个字节的ascii码相加的值再加上256(checksum当作八个空格，即8*0x20）。

没有数据的地方全部填充为'\0'。
往tar文件中添加一个空文件，那么tar文件将新增1024Byte大小(512Byte的tar_header加上512Byte的全0数据)


然而根据我们测试发现，在新版本tar工具中机制已经发生了一些变化。

        pc@iZ25g2i2xsmZ:~$ tar --version
        tar (GNU tar) 1.27.1
        Copyright (C) 2013 Free Software Foundation, Inc.
        License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
        This is free software: you are free to change and redistribute it.
        There is NO WARRANTY, to the extent permitted by law.
        Written by John Gilmore and Jay Fenlason.
                
在该版本的tar工具中 **文件大小是10240Byte的整数倍**。，文件大小只能是10240*n,n=0,1,2,3,4,...n


## 解包tar

解包更容易一些 直接有已经打包的tar文件即可进行。


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


在解包的案例中 我们只需要关注最核心的问题，文件名和文件大小。



## 兴趣延伸-打包tar

打包需要准备的参数更多 比如uid、gid、mtime、checksum 如果准备错误就会导致无法解包。


