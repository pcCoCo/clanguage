# 章节12-C++基于C的拓展语法

内容范畴规划 不讲C++面向对象、泛型的知识，只涵盖C++基于C的语法拓展

## 此const非彼const

## 函数重载的奥秘

nm命令解析符号表

## 函数默认形参值

## struct只是权宜之计
在C++中使用struct 定义的结构体类型再定义结构体变量时不需要再带struct关键字


## C++简单案例之文件打包

http://www.moon-soft.com/program/FORMAT/comm/tar.htm

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
> 在tar文件中 文件信息的数据结构后跟着的就是文件的内容。

问题1  
        为什么这些数据成员都是使用char类型而不是用int
    
问题2
        下面输出的结果是多少 512

```
int main()
{
        printf("%u\n",sizeof(struct tar_header));
        return 0;
}  
```

size为文件大小的八进制字节表示，例如文件大小为90个字节，那么这里就是八进制的90，即为132。
文件大小，修改时间，checksum都是存储的对应的八进制字符串，字符串最后一个字符为空格字符
checksum的计算方法为出去checksum字段其他所有的512-8共504个字节的ascii码相加的值再加上256(checksum当作八个空格，即8*0x20）
文件内容以512字节为一个block进行分割，最后一个block不足部分以0补齐

两个文件的tar包首先存放第一个文件的tar头结构，然后存储文件内容，接着存储第二个文件的tar头结构，然后存储文件内容
所有文件都存储完了以后，最后存放一个全零的tar结构

　　所有的tar文件大小应该都是512的倍数，一个空文件打包后为512*3字节，包括一个tar结构头，一个全零的block存储文件内容，一个全零的tar结构

## 拓展延伸-解包tar
