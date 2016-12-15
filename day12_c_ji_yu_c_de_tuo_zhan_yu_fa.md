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
　　	char name[100];
　　	char mode[8];
　　	char uid[8];
　　	char gid[8];
　　	char size[12];
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


拓展延伸-解包tar
