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
test: ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, not stripped

pc@iZ25g2i2xsmZ:~/code$ file test.o
test.o: ELF 64-bit LSB  relocatable, x86-64, version 1 (SYSV), not stripped
```

可以使用readelf分析两个文件的组成部分
pc@iZ25g2i2xsmZ:~/code$ readelf -h test   
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              EXEC (Executable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x400440
  Start of program headers:          64 (bytes into file)
  Start of section headers:          4512 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         9
  Size of section headers:           64 (bytes)
  Number of section headers:         30
  Section header string table index: 27

查看程序头表 在目标文件中并不存在
pc@iZ25g2i2xsmZ:~/code$ readelf -l test

Elf file type is EXEC (Executable file)
Entry point 0x400440
There are 9 program headers, starting at offset 64



pc@iZ25g2i2xsmZ:~/code$ readelf -h test.o
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              REL (Relocatable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          0 (bytes into file)
  Start of section headers:          312 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           64 (bytes)
  Number of section headers:         13
  Section header string table index: 10


ELF描述各个段的内容时制定了将哪些节的数据映射到段中，节点表用于管理文件的各个节。

readelf可以显示文件的各个节
pc@iZ25g2i2xsmZ:~/code$ readelf -S test
There are 30 section headers, starting at offset 0x11a0:

Section Headers:
  [Nr] Name              Type             Address           Offset  Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000 0000000000000000  0000000000000000           0     0     0
  [ 1] .interp           PROGBITS         0000000000400238  00000238 000000000000001c  0000000000000000   A       0     0     1
  [ 2] .note.ABI-tag     NOTE             0000000000400254  00000254 0000000000000020  0000000000000000   A       0     0     4
  [ 3] .note.gnu.build-i NOTE             0000000000400274  00000274 0000000000000024  0000000000000000   A       0     0     4
  [ 4] .gnu.hash         GNU_HASH         0000000000400298  00000298 000000000000001c  0000000000000000   A       5     0     8
  [ 5] .dynsym           DYNSYM           00000000004002b8  000002b8 0000000000000060  0000000000000018   A       6     1     8
  [ 6] .dynstr           STRTAB           0000000000400318  00000318 000000000000003f  0000000000000000   A       0     0     1
  [ 7] .gnu.version      VERSYM           0000000000400358  00000358 0000000000000008  0000000000000002   A       5     0     2
  [ 8] .gnu.version_r    VERNEED          0000000000400360  00000360 0000000000000020  0000000000000000   A       6     1     8
  [ 9] .rela.dyn         RELA             0000000000400380  00000380 0000000000000018  0000000000000018   A       5     0     8
  [10] .rela.plt         RELA             0000000000400398  00000398 0000000000000048  0000000000000018   A       5    12     8
  [11] .init             PROGBITS         00000000004003e0  000003e0 000000000000001a  0000000000000000  AX       0     0     4
  [12] .plt              PROGBITS         0000000000400400  00000400 0000000000000040  0000000000000010  AX       0     0     16
  [13] .text             PROGBITS         0000000000400440  00000440 0000000000000182  0000000000000000  AX       0     0     16
  [14] .fini             PROGBITS         00000000004005c4  000005c4 0000000000000009  0000000000000000  AX       0     0     4
  [15] .rodata           PROGBITS         00000000004005d0  000005d0 0000000000000011  0000000000000000   A       0     0     4
  [16] .eh_frame_hdr     PROGBITS         00000000004005e4  000005e4 0000000000000034  0000000000000000   A       0     0     4
  [17] .eh_frame         PROGBITS         0000000000400618  00000618 00000000000000f4  0000000000000000   A       0     0     8
  [18] .init_array       INIT_ARRAY       0000000000600e10  00000e10 0000000000000008  0000000000000000  WA       0     0     8
  [19] .fini_array       FINI_ARRAY       0000000000600e18  00000e18 0000000000000008  0000000000000000  WA       0     0     8
  [20] .jcr              PROGBITS         0000000000600e20  00000e20 0000000000000008  0000000000000000  WA       0     0     8
  [21] .dynamic          DYNAMIC          0000000000600e28  00000e28 00000000000001d0  0000000000000010  WA       6     0     8
  [22] .got              PROGBITS         0000000000600ff8  00000ff8 0000000000000008  0000000000000008  WA       0     0     8
  [23] .got.plt          PROGBITS         0000000000601000  00001000 0000000000000030  0000000000000008  WA       0     0     8
  [24] .data             PROGBITS         0000000000601030  00001030 0000000000000010  0000000000000000  WA       0     0     8
  [25] .bss              NOBITS           0000000000601040  00001040 0000000000000008  0000000000000000  WA       0     0     1
  [26] .comment          PROGBITS         0000000000000000  00001040 0000000000000056  0000000000000001  MS       0     0     1
  [27] .shstrtab         STRTAB           0000000000000000  00001096 0000000000000108  0000000000000000           0     0     1
  [28] .symtab           SYMTAB           0000000000000000  00001920 0000000000000618  0000000000000018          29    45     8
  [29] .strtab           STRTAB           0000000000000000  00001f38 0000000000000235  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), l (large)
  I (info), L (link order), G (group), T (TLS), E (exclude), x (unknown)
  O (extra OS processing required) o (OS specific), p (processor specific)

能够看出来，我们熟悉的有.data 、.bss、 .text、 .rodata等多个section 节
节信息无须复制到虚拟地址空间。
每节都指定了一个类型，定义了节数据的语义。最重要的就是PROGBITS（程序必须解释的信息 比如二进制代码）、SYMTAB（符号表）和REL（重定位信息）。STRTAB用于存储与ELF格式相关的字符串（如节的符号名称 .text）

每节都指定了大小和二进制文件内部的偏移量。address字段指定节加载到虚拟地址空间的位置（如果是一个可链接对象 目标地址是未定义的而为0）。
A标识控制着装载文件时是否将节的数据复制到虚拟地址空间。

规范:系统自身使用的节名称以.开始，应用程序自定义的就不要以点开始。

常用节的作用：
.data 保存已初始化的数据(全局、静态)
.rodata保存只读数据，只能读取不能修改。
.text 保存可执行程序的二进制代码


## 段错误
非法访问内存

