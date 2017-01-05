# day09-内存管理 内容需要网页预览才可通过 可以考虑将数据多的地方截图

> 学习C语言有两个重要的概念:


```
一个是理解地址的概念，一个就是理解与之相关的内存的概念。
```


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
### 地址空间

> 容量单位

1KB = 2[^10] Byte

1MB = 2[^10] KB

1GB = 2[^20] MB

由于内存区域是同坐指针寻址，因此CPU的字长决定了所能管理的地址空间的最大长度。如322系统\(IA-32 etc\)可以管理的内存时2[^32]B = 4GB,对现在更新的64位处理器（IA-64、AMD64）则理论上可以管理2[^64]Byte。

地址空间的最大长度与实际可用的物理内存数量无关，因此被称作虚拟地址空间。从每个进程的角度讲，地址空间中只有自己一个进程，无法感知也无需感知 别的进程的存在。

Linux将细腻地址空间划分为两部分，分为内核空间和用户空间。  
系统中每个用户进程都有自己的虚拟地址范围，从0-TASK\_SIZE。用户空间之上的内核空间\(从TASK\_SIZE-2[^32]\(2[^64]\)\)保留给内核专用，用户进程不能访问。TASK\_SIZE是一个特定于计算机体系结构的常数，把地址空间按给定的比例划分为两部分。

比如在IA-32系统中 虚拟地址空间的总长度是4GB。0-3G是用户空间，3-4G是内核空间。每个用户进程都认为自身有3GB内存，每个用户进程空间时完全隔离的，而虚拟地址空间顶部的内核空间总是相同的。

Linux中使用两个不同的状态：内核态和用户态。

两种状态的关键差别在于对高于TASK\_SIZE的内存区域的访问。用户态禁止访问内核空间，用户进程不能操作或者读取内核空间的中，也无法执行内核空间的代码。这种机制可以防止进程无意间修改彼此的数据而造成相互干扰。

从用户态到内核态的切换通过系统调用的转换手段完成，且系统调用的执行因具体系统而不同。  
用户进程想要执行任何影响整个系统的操作（输入/输出设备）,只能借助于系统调用向内核发出请求，内核首先检查进程是否允许执行想要的操作，然后代表进程执行所需才做，接下来返回到用户态。

使用ps命令可以看到很多内核的线程 名称置于方括号之内

```
ps fax
```

### 虚拟和物理地址空间

大多数情况下单个虚拟地址空间比系统中可用的物理内存要大。如果每个进程都有自己的虚拟地址空间，情况和物理内存 相比没有什么改善。因此内核和CPU必须考虑如何将实际可用的物理内存映射到虚拟地址空间的区域。

可取的方法就是用页表来为物理地址分配虚拟地址。虚拟地址关系到进程的用户空间和内核空间。

用户进程的虚拟地址空间被划分为很多等长的部分，每一部分成为页。 物理内存也被划分为同样大小的页,物理内存页经常称为页帧。

将虚拟地址空间映射到物理地址空间的用以维护页帧的数据结构多级页表。  
CPU内存有一个专门的期间MMU\(Memmory Management Unit,内存管理单元\)，优化内存访问操作。

### 物理内存的分配

在内核分配内存的时候，必须记录页帧的已分配和未分配状态的，以免两个进程使用同样的内存区域。由于内存分配和释放非常频繁，内核还必须保证相关操作尽快完成。可以只分配完成的页帧，将内存划分为更小部分的工作则委托给用户空间的标准库。标准库将来源于内核的页帧拆分为小的内存块，并未进程分配内存。

### 页面交换

利用磁盘空间作为拓展内存，从而增加了可用的内存。

这块在磁盘上却可以当做备用内存的区域，在Linux称为交换分区，在windows上称为虚拟内存。

在内核需要更多的内存的时候，将不经常使用的页写入磁盘，在内核再次需要访问该页中的数据的时候交换回内存。一旦CPU发现所需的页数据不在内存，将会引发可以被内核截获的CPU的缺页中断，此时内核将该页帧数交换进内存，然后恢复用户进程运行。从而达到对用户程序的透明，无感知。

### 虚拟地址空间

物理内存的页帧与所有的进程虚拟地址空间的页之间的关联:  
逆向映射 reverse mapping技术有助于从虚拟内存页跟踪到对应的物理内存页，而缺页处理 page fault handling则允许从块设备按需读取数据填充虚拟地址空间。

地址空间只有极少的部分与物理内存也直接关联，不经常使用的部分，仅当必要时才与页帧进行关联。  
内核信任自己，但无法新人用户进程。各个用户地址空间的操作都伴随各种检查，以确保程序的权限不会超出应有的限制，进而危害整个OS的稳定性和安全性。

#### 进程地址空间的布局

虚拟地址空间中够包含了若干区域，其分布方式是特定于体系结构的，但都有一写共同的分类：  
存放二进制代码的虚拟内存区域，该代码成为text，该区域成为text段;  
存储全局变量和动态产生的数据的堆;  
用于保存局部变量和实现函数调用的栈；  
环境变量和命令行参数的段；  
mmap内存映射的区域；  
动态库代码映射预取；  
.....etc

#### 建立布局

load\_elf\_binary装载一个elf二进制文件时，将创建进程的地址空间。

### 堆的管理

堆是进程中用于动态分配变量和数据的内存区域，是一段连续的内存区域。

### 缺页异常的处理

在实际需要某个进程的虚拟地址空间的数据之前，虚拟和物理之间的关联并没有建立。如果进程访问的虚拟地址空间部分尚未与页帧关联，处理器就会触发缺页终端，需要内核处理。

缺页中断时由于访问用户地址空间中的有效地址而引起，还是应用程序试图访问内核的的受保护区域呢？


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

```
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
```

ELF描述各个段的内容时制定了将哪些节的数据映射到段中，节点表用于管理文件的各个节。

readelf可以显示文件的各个节
pc@iZ25g2i2xsmZ:~/code$ readelf -S test
```
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
```

能够看出来，我们熟悉的有.data 、.bss、 .text、 .rodata等多个section 节
节信息无须复制到虚拟地址空间。
每节都指定了一个类型，定义了节数据的语义。最重要的就是PROGBITS（程序必须解释的信息 比如二进制代码）、SYMTAB（符号表）和REL（重定位信息）。STRTAB用于存储与ELF格式相关的字符串（如节的符号名称 .text）

每节都指定了大小和二进制文件内部的偏移量。address字段指定节加载到虚拟地址空间的位置（如果是一个可链接对象 目标地址是未定义的而为0）。
A标识控制着装载文件时是否将节的数据复制到虚拟地址空间。

规范:系统自身使用的节 标准节名称以.开始，应用程序自定义的就不要以点开始。

常用节的作用：
.data 保存已初始化的数据(全局、静态)
.rodata保存只读数据，只能读取不能修改。
.text 保存可执行程序的二进制代码
.bss  保存未初始化的数据(全局、静态)，程序开始运行前填充0字节
.hash 是一个散列表，提供在不对全表元素进行线性搜索的情况对符号表项的快速访问

### 符号表

符号表是每个ELF文件的重要部分。保存了程序实现或使用的所有（全局）变量和函数。如果程序引用了一个自身代码未定义的符号(比如C标准库的strtok函数)。此类应用必须在静态链接期间用其他目标模块或库解决（或者 加载时间通过动态链接）。nm工具可以生成程序定义和使用的所有符号列表。

pc@iZ25g2i2xsmZ:~/code$ nm test 

```
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
00000000004005c4 T _fini
0000000000400500 t frame_dummy
0000000000600e10 t __frame_dummy_init_array_entry
0000000000400708 r __FRAME_END__
0000000000601000 d _GLOBAL_OFFSET_TABLE_
                 w __gmon_start__
00000000004003e0 T _init
0000000000600e18 t __init_array_end
0000000000600e10 t __init_array_start
00000000004005d0 R _IO_stdin_used
                 w _ITM_deregisterTMCloneTable
                 w _ITM_registerTMCloneTable
0000000000600e20 d __JCR_END__
0000000000600e20 d __JCR_LIST__
                 w _Jv_RegisterClasses
00000000004005c0 T __libc_csu_fini
0000000000400550 T __libc_csu_init
                 U __libc_start_main@@GLIBC_2.2.5
000000000040052d T main
                 U printf@@GLIBC_2.2.5
00000000004004a0 t register_tm_clones
0000000000400440 T _start
0000000000601040 D __TMC_END__
```

符号的任务就是将一个字符串和一个值关联起来。printf符号对应着printf函数在虚拟地址空间的地址，该函数的机器代码就存在该地址。
符号的绑定(binding)确定了符号的可见性：

> 局部符号，只在目标文件内部可见。与程序的其他部分合并时是不可见的。局部符号并不会互相干扰。

> 全局符号，在定义的目标文件内部可见，也可以由构成程序的其他目标文件引用。每个全局符号在一个程序内部只能定义一次，否则报连接错误。指向全局符号的未定义引用，将在重定向期间确定相关符号的位置。如果全局符号的未定义引用无法解决，将会拒绝静态绑定或执行。

> 弱符号，也在整个程序内可见，但可以有多个定义。如果程序中的一个全局符号和一个局部符号相关，优先处理全局符号。
即使一个若符号未定义，程序也可以静态或动态链接，为符号指定0值。



## 段错误
非法访问内存



### 存储类型限定

volatile修饰字段告诉编译器不要对该类型的数据做优化处理，对它的访问都是对内存的访问，而不是对寄存器的访问。 



### 内存结构图

有很多变量   函数 分别写出每个变量和函数的作用域、寿命

