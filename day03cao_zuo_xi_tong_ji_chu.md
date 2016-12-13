![](/assets/hard_disk.jpg)# day03-操作系统基础

## 从C源码到可执行程序的历练

### 预处理

### 汇编

### 编译

### 链接

## 计算机系统结构

   计算机（Computer），俗称电脑，是一种能够按照事先存储的程序，自动、高速地进行大量数值计算和各种信息处理的现代化智能电子设备。由硬件和软件所组成，两者是不可分割的。
1954年5月24日，晶体管电子计算机诞生。 1969年10月29日，通过ARPANET，首次实现了两台计算机的互联。
   计算机是20世纪最先进的科学技术发明之一，对人类的生产活动和社会活动产生了极其重要的影响。

   随着科技的发展，现在新出现一些新型计算机有：生物计算机、光子计算机、量子计算机等。 
   计算机发明者约翰·冯·诺依曼，我们目前使用的几乎所有的计算机都是冯诺依曼型计算机。

### 冯诺依曼计算机特点

1)计算机处理的数据和指令一律用二进制数表示

2)顺序执行程序
计算机运行过程中，把要执行的程序和处理的数据首先存入主存储器（内存），计算机执行程序时，将自动地并按顺序从主存储器中取出指令一条一条地执行，这一概念称作顺序执行程序。

3)计算机硬件由运算器、控制器、存储器、输入设备和输出设备五大部分组成。

   


## CPU架构

x86 x86-64 SPARC ARM

### 复杂指令集CISC


x86：Intel从16位微处理器8086开始的整个CPU芯片系列，系列中的每种型号都保持与以前的各种型号兼容，主要有8086，8088（前面两个是16位CPU），80186，80286（这两个是过渡产品）， 80386，80486以及以后各种型号的Pentium芯片[奔腾，P2, P4，赛扬...]（这些都是32位CPU）

x86-64：<维基百科>上x86-64是x86指令集的超集，在x86处理器上可以运行的程序可以运行在x86-64上（这也是为啥现在买的一些64bits CPU可以直接运行Win XP的原因）。x86-64是AMD发明的，也叫AMD64，Intel克隆了一把，叫做Intel 64，也叫EM64T。

x86-64 is a 64-bit superset of the x86 instruction set architecture. Because the x86-64 instruction set is a superset of the x86 instruction set, all instructions in the x86 instruction set can be executed by central processing units (CPUs) that implement the x86-64 instruction set; therefore these CPUs can natively run programs that run on x86 processors from Intel, Advanced Micro Devices (AMD), and other vendors.

x86-64 was designed by AMD, who have since renamed it AMD64. It has been cloned by Intel under the name Intel 64 (formerly known as EM64T among other names).[1] This leads to the common use of the names x86-64 or x64 as more vendor-neutral terms to collectively refer to the two nearly identical implementations.

x86和x86-64可以认为就是一种特定的指令集
i386：也是维基上的解释，也就是指Intel 80386，是第一个32位的x86架构的处理器，用了20多年了，后面出的 486（80486，i486），586（80586，Pentium，P5），686（80686，Pentium Pro，P6）等等都与之兼容。

The Intel 80386, otherwise known as the Intel386, i386 or just 386, is a microprocessor which has been used as the central processing unit (CPU) of many personal computers and workstations since 1986. It was the first x86 processor to have a 32-bit architecture, with a basic programming model that has remained virtually unchanged for over twenty years and remains completely backward compatible.

IA32：可以认为就是x86或者x86-32，也是一个指令集。
英特尔32位架构（英语：Intel Architecture, 32-bit，缩写为IA-32），常被称为i386、x86-32或是x86，由英特尔公司推出的复杂指令集(CISC)架构，至今英特尔最受欢迎的处理器仍然采用此架构。它是x86架构的32位延伸版本，1985年首次应用在Intel 80386芯片中，用来取代之前的x86 16位架构（x86-16），包括8086、80186与80286芯片。
一个IA32中央处理器(CPU)包含一组8个存储32位值的寄存器. 这些寄存器用来存储整型数据和指针英特尔32位架构（英语：Intel Architecture, 32-bit，缩写为IA-32），常被称为i386、x86-32或是x86，由英特尔公司推出的复杂指令集(CISC)架构，至今英特尔最受欢迎的处理器仍然采用此架构。


IA-32 (Intel Architecture, 32-bit), often generically called x86 or x86-32, is the instruction set architecture of Intel's most commercially successful microprocessors. It is a 32-bit extension, first implemented in the Intel 80386, of the earlier 16-bit Intel 8086, 80186 and 80286 processors and the common denominator for all subsequent x86 designs. This architecture defines the instruction set for the family of microprocessors installed in the vast majority of personal computers in the world.

IA64：就是所谓的安腾，Intel跟HP联合折腾的一种64-bits全新架构，与x86系列不兼容，号称采用了很多非常好的体系结构方面的技术，但是没火起来。再次证明光有好的技术是行不通的，还要有市场眼光啊。

Itanium is the brand name for 64-bit Intel microprocessors that implement the Intel Itanium architecture (formerly called IA-64). Intel has released two processor families using the brand: the original Itanium and the Itanium 2. Starting November 1, 2007, new members of the second family are again called Itanium. The processors are marketed for use in enterprise servers and high-performance computing systems. The architecture originated at Hewlett-Packard (HP) and was later developed by HP and Intel together.

注：所谓16位，32位，64位的CPU一般是指处理器中“算数逻辑单元（ALU）”或者CPU GPRs（General-Purpose Registers，通用寄存器）的数据宽度。此外还有数据总线宽度和地址总线宽度两个参数，前者决定了CPU在进行运算时，一次可以并行拿到的二进制数据bit数（可以想想C语言中short/int/long型数据分别的位数），通常与ALU的宽度相同（极个别例外），而后者决定了内存地址空间的大小（16位的地址总线，就是64K，32位就是4G，64位是128T；可以想一下C语言中指针所占的二进制长度），地址总线宽度自然来讲应该是跟数据总线宽度一致，但由于诸多原因（历史，技术，兼容性等等）不是这样。
另外，还有操作系统的位数区分，可以认为是word size（字长），也就是一个整数和指针数据的长度，原则上就是指上述CPU位数（即通用寄存器的位数），但同时也决定了操作系统能够支持的最大内存容量（每个进程能够使用的虚拟内存大小，严格说来没有这么多）。

### 精简指令集RISC

特点是所有指令的格式都是一致的，所有指令的指令周期也是相同的，并且采用流水线技术。在中高档服务器中采用RISC指令的CPU主要有Compaq（康柏，即新惠普）公司的Alpha、HP公司的PA-RISC、IBM公司的PowerPC、MIPS公司的MIPS和SUN公司的Sparc、Acorn公司的ARM。

### ARM

ARM处理器是英国Acorn有限公司设计的低功耗成本的第一款RISC微处理器。全称为Acorn RISC Machine。ARM处理器本身是32位设计，但也配备16位指令集，一般来讲比等价32位代码节省达35%，却能保留32位系统的所有优势。

　　1978年12月5日，物理学家赫尔曼·豪泽（Hermann Hauser）和工程师Chris Curry，在英国剑桥创办了CPU公司（Cambridge Processing Unit），主要业务是为当地市场供应电子设备。

　　1979年，CPU公司改名为Acorn计算机公司。Acorn公司打算使用摩托罗拉公司的16位芯片，但是发现这种芯片太慢也太贵。“一台售价500英镑的机器，不可能使用价格100英镑的CPU！”他们转而向Intel公司索要80286芯片的设计资料，但是遭到拒绝，于是被迫自行研发。

　　1985年，Roger Wilson和Steve Furber设计了他们自己的第一代32位、6MHz的处理器，用它做出了一台RISC指令集的计算机，简称ARM（Acorn RISC Machine）。

　　1990年11月27日，Acorn公司正式改组为ARM计算机公司。苹果公司出资150万英镑，芯片厂商VLSI出资25万英镑，Acorn本身则以150万英镑的知识产权和12名工程师入股。公司的办公地点非常简陋，就是一个谷仓。公司成立后，由于缺乏资金，ARM做出了一个意义深远的决定：自己不制造芯片，只将芯片的设计方案授权（licensing）给其他公司，由它们来生产。

　　20世纪90年代，ARM公司的业绩平平，处理器的出货量徘徊不前。但是进入21世纪之后，由于手机的快速发展，出货量呈现爆炸式增长，ARM处理器占领了全球手机市场。

　　经过12年的发展，在2002年，ARM架构芯片的出货量正式突破10亿。随着智能设备的爆炸式成长，如今，要完成10亿片的出货量只需要一个月。

　　2004年，Cortex系列的诞生是ARM公司的大事件，从此该公司不再用数字为处理器命名。它分为A、R和M三类，旨在为各种不同的市场提供服务。

　　2006年，全球ARM芯片出货量为20亿片，2010年预计将达到45亿片。

　　2015年，ARM基于ARMv8架构推出了一种面向企业级市场的新平台标准。此外，他们还开始在物联网领域发力。同年，福布斯杂志将ARM评为世界上五大最具创新力的公司之一。

## 内存

主存储器，内存存储器，简称内存。

内存（Memory）是计算机中重要的部件之一，它是与CPU进行沟通的桥梁。计算机中所有程序的运行都是在内存中进行的，因此内存的性能对计算机的影响非常大。作用是用于暂时存放CPU运算所需的相关数据。只要计算机在运行中，CPU就会把需要运算的数据调到内存中进行运算，当运算完成后CPU再将结果传送出来，内存的运行也决定了计算机的稳定运行。

速度快。
内存属于易失存储介质，在断电的时候将会丢失数据。

内存一般采用半导体存储单元，包括随机存储器（RAM），只读存储器（ROM），以及高速缓存（CACHE，片外cache）。只不过因为RAM是其中最重要的存储器。

主要介质种类有 SDRAM、DDR、DDR2、DDR3、DDR4。


> 手机内存16G不够使用怎么办???
这是一个误区，手机内存容量大小并不是值得内部存储器的容量，而是指的外部存储器的容量。截止2016年12月，市场上一般的手机内存容量在512M-2G左右。




## 外存

外部存储器，简称外存。是指除计算机内存及CPU缓存以外的储存器，此类储存器一般断电后仍然能保存数据。常见的外存储器有硬盘、软盘、光盘、U盘等。容量较内存大，价格更加便宜，保存的数据持久性好，属于非易失存储介质。


PC机常见的外存储器有软盘存储器、硬盘存储器、光盘存储器等。

U盘的存储介质

存储介质为FLASH闪存，英文名称是"Flash Memory"，一般简称为"Flash"，在没有电流供应的条件下也能够长久地保持数据，其存储特性相当于硬盘，这项特性正是闪存得以成为各类便携型数字设备的存储介质的基础。

![](/assets/u_disk.jpg)

磁盘有软磁盘和硬磁盘两种。

硬盘目前可以分为机械硬盘，固态硬盘。

固态硬盘的存储介质分为两种，一种是主流技术 采用闪存（FLASH芯片）作为存储介质，另外一种是采用DRAM作为存储介质。

光盘有只读型光盘CD-ROM、一次写入型光盘WORM和可重写型光盘MO三种。

![](/assets/soft_disk.jpg)

![](/assets/hard_disk.jpg)





## 操作系统

用户空间：应用程序、C语言库

内核空间：系统内核、设备驱动、硬件、系统调用

UNIX操作系统下运行的应用程序都可以被称作为进程。每个进程都在CPU的虚拟内存中分配地址空间。各个进程的地址空间都是完全独立的，因此每个进程都不会意识到彼此的存在。

### 多任务

Linux是多任务操作系统，看上去支持很多并行执行的若干进程。一个CPU内核在一个时间点只能执行一个进程，因此要执行很多个进程需要内核在很短的时间间隔内在不同的进程间进行切换\(用户无感知\)。

1）内核借助CPU的帮助，负责进程切换的技术细节。必须给各进程一种错觉就是CPU总是可用\(虽然不一定可用\)。

在剥夺某个进程的CPU资源之前保存进程的上下文，在重新激活进程的时候恢复进程的上下文。这个切换过程叫进程切换。

2）内核必须确定如何在现存的进程之间共享CPU资源，确定每个进程运行时间称为调度。

### 地址空间

> 容量单位

1KB = 2[^10] Byte

1MB = 2[^10] KB

1GB = 2[^20] MB

由于内存区域是同坐指针寻址，因此CPU的字长决定了所能管理的地址空间的最大长度。如322系统(IA-32 etc)可以管理的内存时2[^32]B = 4GB,对现在更新的64位处理器（IA-64、AMD64）则理论上可以管理2[^64]Byte。

地址空间的最大长度与实际可用的物理内存数量无关，因此被称作虚拟地址空间。从每个进程的角度讲，地址空间中只有自己一个进程，无法感知也无需感知 别的进程的存在。

Linux将细腻地址空间划分为两部分，分为内核空间和用户空间。




## 系统调用

system\(\)

系统调用的开销

## 随处可见的cache机制

CPU的一级缓存、二级缓存

硬盘的缓存

操作系统的虚拟内存和交换分区

a

a

a

a

a

a

a

a

a

a

a

a

20





[^1]: 20

