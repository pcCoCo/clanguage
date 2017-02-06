# 选读-C++基于C的拓展语法

内容范畴规划 不讲C++面向对象、泛型的知识，只涵盖C++基于C的语法拓展

## 此const非彼const

pc@iZ25g2i2xsmZ:~/test$ vim t2.c 

```
int main()
{
    const int cnum = 1001;
    int *ptr = (int*)&cnum;
    *ptr = 1002;
    printf("%d",cnum);
    return 0;
}
```
pc@iZ25g2i2xsmZ:~/test$ gcc t2.c 

pc@iZ25g2i2xsmZ:~/test$ ./a.out 
1002

将后缀改成.cpp
pc@iZ25g2i2xsmZ:~/test$ cp t2.c t2.cpp
pc@iZ25g2i2xsmZ:~/test$ g++ t2.cpp
pc@iZ25g2i2xsmZ:~/test$ ./a.out 
1001

可以看出，C++对const的语法更加严谨。

        	
## 函数重载

在C语言中同一作用域中函数名不能同名，否则会有语法错误。
```
#include <stdio.h>

int add(int n1,int n2)
{
    return n2+n1;
}

int add(int n1,int n2,int n3)
{
    return n1+n2+n3;
}
int main()
{
    printf("%d",add(100,200));
    return 0;
}
```
t2.c:8:5: error: conflicting types for ‘add’

然而将改代码后缀改成.cpp，居然可以合法通过。
pc@iZ25g2i2xsmZ:~/test$ g++ t2.cpp -o cpp_overload
pc@iZ25g2i2xsmZ:~/test$ ./cpp_overload
300


### 奥秘探析-nm命令解析符号表

```
pc@iZ25g2i2xsmZ:~/test$ nm cpp_overload 
0000000000601040 B __bss_start
0000000000601040 b completed.6973
0000000000601030 D __data_start
0000000000601030 W data_start
0000000000400470 t deregister_tm_clones
00000000004004e0 t __do_global_dtors_aux
0000000000600e18 t __do_global_dtors_aux_fini_array_entry
0000000000601038 D __dso_handle
0000000000600e28 d _DYNAMIC
0000000000601040 D _edata
0000000000601048 B _end
0000000000400604 T _fini
0000000000400500 t frame_dummy
0000000000600e10 t __frame_dummy_init_array_entry
0000000000400790 r __FRAME_END__
0000000000601000 d _GLOBAL_OFFSET_TABLE_
                 w __gmon_start__
00000000004003e0 T _init
0000000000600e18 t __init_array_end
0000000000600e10 t __init_array_start
0000000000400610 R _IO_stdin_used
                 w _ITM_deregisterTMCloneTable
                 w _ITM_registerTMCloneTable
0000000000600e20 d __JCR_END__
0000000000600e20 d __JCR_LIST__
                 w _Jv_RegisterClasses
0000000000400600 T __libc_csu_fini
0000000000400590 T __libc_csu_init
                 U __libc_start_main@@GLIBC_2.2.5
000000000040055d T main
                 U printf@@GLIBC_2.2.5
00000000004004a0 t register_tm_clones
0000000000400440 T _start
0000000000601040 D __TMC_END__
000000000040052d T _Z3addii
0000000000400541 T _Z3addiii
```

## 函数默认形参值

## struct只是权宜之计

C++中的struct可以定义函数
在C++中使用struct 定义的结构体类型再定义结构体变量时不需要再带struct关键字



```

#include <cstdio>
#include <cstring>

struct file
{
    char name[64];
    char mode[8];
    FILE *fp;
    int init(const char *name,const char *mode)
    {
        strcpy(this->name,name);
        strcpy(this->mode,mode);
        fp = fopen(name,mode);
        return fp != NULL;
    }
    int close()
    {
        if(this->fp)
        {
            fclose(this->fp);
            this->fp = NULL;
        }
        return 0;
    }
};
int main()
{

    file f;
    f.init("hello","rb");
    f.close();
}

```

### this指针

this指针是一个指针，和我们之前学习的指针在本质上并没有什么区别。
在结构体的成员函数中的this指针，就是一个结构体指针，该指针指向调用该结构体成员函数的结构体变量(对象)。


总而言之，形式上看着还是struct但是其实质已经往C++的class开始过渡了。





