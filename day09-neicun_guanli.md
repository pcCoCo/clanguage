# day09-内存管理

> 学习C语言有两个重要的概念:
>
> ```
> 一个是理解地址的概念，一个就是理解与之相关的内存的概念。
> ```

通常我们说道计算机的内存大家可能知道的是计算机的硬件之一。

![](/assets/memory.jpg)

```
通常这个内存概念在计算机中表述为物理内存。
```

```
在第一章我们说到计算机是一个管家，管理者整个计算机的资源，比如CPU的调度资源，内存资源等等。
```

RSS ， resident set size ，表示进程实际使用的物理内存空间

## 虚拟地址空间

VSZ ， virtual memory size ，表示进程总共使用的虚拟地址空间大小，包括进程地址空间的代码段、数据段、堆、文件映射区域、栈、内核空间等所有虚拟地址使用的总和，单位是 KB。

## 堆空间的申请和释放

malloc 使用 mmap 分配的内存 \( 大于 128k\) ， free 会调用 munmap 系统调用马上还给 OS ，实现真正释放。

堆内的内存，只有释放堆顶的空间，同时堆顶总连续空闲空间大于 128k 才使用 sbrk\(-SIZE\) 回收内存，真正归还 OS 。

堆内的空闲空间，是不会归还给 OS 的。

`频繁分配释放内存导致的性能问题`

随着系统频繁地 malloc 和 free ，尤其对于小块内存，堆内将产生越来越多不可用的碎片，导致“内存泄露”。而这种“泄露”现象使用 valgrind 是无法检测出来的。

因此，当我们写程序时，不能完全依赖 glibc 的 malloc 和 free 的实现。更好方式是建立属于进程的内存池，即一次分配 \(malloc\) 大块内存，小内存从内存池中获得，

当进程结束或该块内存不可用时，一次释放 \(free\) ，可大大减少碎片的产生。

## elf文件格式  深入Linux内核架构1014P 深入理解

结合邢老师视频 整理
Executable and linkable Format,是一种对可执行文件、目标文件和库使用的文件格式。ELF是一种开放格式，Linux操作系统内核本身也是ELF格式。

ELF文件由各个部分组成。需要区分链接对象和可执行文件。

![](/assets/elf_format.png)
除了用于标识ELF文件的几个字节之外，ELF还包含了有关文件类型和大小信息等。
程序头表 向系统提供了可执行文件在进程虚拟地址空间中的组织结构（比如段熟练、位置等）
各个段   保存了与文件相关的各种形式的数据。符号表、实际的二进制代码、常量值（字符串、常数）


```
gcc test.c -o test
gcc test.c -c -o test.o
```

可以使用file命令显示编译器生成的两个ELF文件信息，一个可执行文件，一个是可重定位的目标文件。


```
pc@iZ25g2i2xsmZ:~/code$ file test
test: ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=9ae069486e0a27c88979726ff12865d09128e77f, not stripped

pc@iZ25g2i2xsmZ:~/code$ file test.o
test.o: ELF 64-bit LSB  relocatable, x86-64, version 1 (SYSV), not stripped
```



## 段错误
非法访问内存

