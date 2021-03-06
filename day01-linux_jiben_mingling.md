# 操作系统

"未来的计算机，重量也许...可能不会超过1.5吨。"——《大众机械》，1949年

"Computers are good at following instructions, but not at reading your mind."電腦善於遵循指令，但不善於理解你的思維。<Donald Ervin Knuth, Things a Computer Scientist Rarely Talks About,中文名称叫高纳得>

"UNIX是简单的。只不过它需要天才去理解其简朴。"(丹尼斯·利奇（Dennis Ritchie），Unix之父、C语言的之父)


操作系统（Operating System，简称OS）是管理和控制计算机硬件与软件资源的计算机程序，是直接运行在“裸机”上的最基本的系统软件，任何其他软件都必须在操作系统的支持下才能运行。

操作系统是用户和计算机的接口，同时也是计算机硬件和其他软件的接口。操作系统的功能包括管理计算机系统的硬件、软件及数据资源，控制程序运行，改善人机界面，为其它应用软件提供支持，让计算机系统所有资源最大限度地发挥作用，提供各种形式的用户界面，使用户有一个好的工作环境，为其它软件的开发提供必要的服务和相应的接口等。实际上，用户是不用接触操作系统的，操作系统管理着计算机硬件资源，同时按照应用程序的资源请求，分配资源，如：划分CPU时间，内存空间的开辟，调用打印机等。

操作系统就像咱们计算机的大管家，负责帮主人高效地管理所有资源。

操作系统简介---[http://www.iu.hio.no/~mark/os/os.html](http://www.iu.hio.no/~mark/os/os.html)

相关书籍：&lt;&lt;操作系统原理&gt;&gt;

## UNIX

Unix最初受到Multics计划的启发。Multics是由麻省理工学院、通用电气和AT&T底下的贝尔实验室合作进行的操作系统项目，被设计运行在GE-645大型主机上。但是由于整个目标过于庞大，糅合了太多的特性，Multics虽然发布了一些产品，但是性能都很低，AT&T最终撤出了投入Multics项目的资源，退出这项合作计划。

贝尔实验室最初参与Multics计划的部门为计算器技术研发部门（Computing Techniques Research Department），部门主管为道格拉斯·麦克罗伊，其下的工程师，原有丹尼斯·里奇、布莱恩·柯林汉、道格拉斯·麦克罗伊、麦克·列斯克（Mike Lesk）与乔伊·欧桑纳（Joe Ossanna）等人，为了Multics计划，他们又召募了肯·汤普逊加入其中。肯·汤普逊进入Multics计划不久，计划就中止了，但因为机器仍然保留在贝尔实验室，他继续在GE-645上开发软件。肯·汤普逊在GE-645上，写出了一个仿真器，可以让一个文件系统与内存分页机制运作起来。他同时也写了一个程序语言Bon，编写了一个太空旅行游戏。经过实际运行后，他发现游戏速度很慢而且耗费昂贵，每次运行会花费75美元。在GE-645被搬走后，肯·汤普逊在实验室中寻找没人使用的机器，找到了几台PDP-7。丹尼斯·里奇的帮助下，汤普逊用PDP-7的汇编语言重写了这个游戏，并使其在DEC PDP-7上运行起来。这次经历加上Multics项目的经验，促使汤普逊开始在DEC PDP-7上研究如何开发操作系统。

1969年，肯·汤普逊提议在PDP-7上开发一个新的阶层式操作系统的计划。Multics的原有成员，加上Rudd Canady，都投入这个计划。肯·汤普逊发现要编写驱动程序来驱动文件系统，进行测试，并不容易，于是开发了一个壳层（shell）与一些驱动程序，做出一个操作系统的雏形。在团队合作下，Multics的许多功能都被采纳，重新实作，最终做出了一个分时多任务操作系统，成为第一版UNIX。因为Multics来自“MULTiplexed Information and Computing System”的缩写，在1970年，那部PDP-7却只能支持两个用户，彼得·纽曼（Peter G. Neumann）戏称他们的系统其实是:“UNiplexed Information and Computing System”，缩写为“UNICS”。于是这个项目被称为UnICS（Uniplexed Information and Computing System）。因为PDP-7的性能不佳，肯·汤普逊与丹尼斯·里奇决定把第一版UNIX移植到PDP-11/20的机器上，开发第二版UNIX。在性能提升后，真正可以提供多人同时使用，布莱恩·柯林汉提议将它的名称改为UNIX。

第一版UNIX是用PDP-7汇编语言编写的，一些应用是由叫做B语言的解释型语言和汇编语言混合编写的。在进行系统编程时不够强大，所以汤普逊和里奇对其进行了改造，并于1971年共同发明了C语言。1973年汤普逊和里奇用C语言重写了Unix，形成第三版UNIX。在当时，为了实现最高效率，系统程序都是由汇编语言编写，所以汤普逊和里奇此举是极具大胆创新和革命意义的。用C语言编写的Unix代码简洁紧凑、易移植、易读、易修改，为此后Unix的发展奠定了坚实基础。

## Linux
### Linux 的诞生

![](/assets/linux.jpg)

Linux操作系统内核诞生于1991 年10 月5 日（这是Linux完成代码后第一次正式向外公布时间）。

发展和成长过程始终依赖着五个重要支柱：UNIX 操作系统、MINIX 操作系统、GNU计划、POSIX 标准和Internet 网络。

1981 年IBM公司推出微型计算机IBM PC。

1991年，GNU计划已经开发出了许多工具软件，最受期盼的GNU C编译器已经出现，GNU的操作系统核心HURD一直处于实验阶段，没有任何可用性，实质上也没能开发出完整的GNU操作系统，但是GNU奠定了Linux用户基础和开发环境。

1991年初，林纳斯·托瓦兹开始在一台386sx兼容微机上学习minix操作系统。1991年4月，林纳斯·托瓦兹开始酝酿并着手编制自己的操作系统。

1991 年4 月13 日在comp.os.minix 上发布说自己已经成功地将bash 移植到了minix 上，而且已经爱不释手、不能离开这个shell软件了。

1991年7月3日，第一个与Linux有关的消息是在comp.os.minix上发布的（当然此时还不存在Linux这个名称，当时林纳斯·托瓦兹的脑子里想的可能是FREAX，FREAX的英文含义是怪诞的、怪物、异想天开等）。

1991年的10月5日，林纳斯·托瓦兹在comp.os.minix新闻组上发布消息，正式向外宣布Linux内核的诞生（Freeminix-like kernel sources for 386-AT）。

1993年，大约有100余名程序员参与了Linux内核代码编写/修改工作，其中核心组由5人组成，此时Linux 0.99的代码大约有十万行，用户大约有10万左右。

1994年3月，Linux1.0发布，代码量17万行，当时是按照完全自由免费的协议发布，随后正式采用GPL协议。

1995年1月，Bob Young创办了RedHat（小红帽），以GNU/Linux为核心，集成了400多个源代码开放的程序模块，搞出了一种冠以品牌的Linux，即RedHat Linux,称为Linux"发行版"，在市场上出售。这在经营模式上是一种创举。

### Linux内核

![](/assets/shell3.jpg)

严格来讲，Linux这个词本身只表示Linux内核，但实际上人们已经习惯了用Linux来形容整个基于Linux内核并使用GNU 工程各种工具和数据库的操作系统。linux内核代码在linux.org 上可以下载。

Linux存在着许多不同的Linux发行版本，但它们都使用了Linux内核。Linux可安装在各种计算机硬件设备中，比如手机、平板电脑、路由器、视频游戏控制台、台式计算机、大型机和超级计算机。


### 查看Linux系统的内核版本

```
pc@iZ25g2i2xsmZ:~/code$ uname -r
3.13.0-86-generic
```

### 内核版本的规律

Linux内核版本号由3组数字组成：内核主版本.次版本.修订次数

Linux内核版本有两种：稳定版和开发版 ，

第二个组数字：偶数表示稳定版本；奇数表示开发版本。

比如 3.13.0-86-generic

第一个组数字: 3 , 主版本号

第二个组数字: 13 , 次版本号，表开发版本（奇数）

第三个组数字: 0 , 修订版本号。

> 那 4.4.0-53-generic 的意义呢？



## Linux发行版

我会告诉你，很多很多.....

ubuntu 乌邦图

![](/assets/ubuntul.jpg)

老司机评论: 就桌面应用而言是Linux发行版中的翘楚

redhat  小红帽

![](/assets/redhat.jpg)

Linux家族中的贵族.免费给你用，但是服务收费。

centos

![](/assets/centos.jpg)

老司机评论:跟红帽是亲兄弟，是一个x86服务器上使用比较多的Linux发行版本。

看了那么多都是外国做的产品，来点中国特色的吧

red-flag linux 红旗  官网 [http://www.redflag-linux.com/](http://www.redflag-linux.com/)

![](/assets/red_flag.jpg)

## Shell是什么

![](/assets/shell3.jpg)

上图来自Unix编程圣经《APUE》英文第二版。如图，处于最中心的是操作系统内核，负责机器硬件资源管理，进程管理等；shell，函数库（值得记住的是C标准函数库）和某些应用程序均直接构建于内核之上，属于同一层。内核与这层的交互是通过以C风格定义的系统函数进行的，即图中灰色部分。系统函数完全屏蔽了内核的实现细节。Shell是一类程序，专门用来读取用户输入的命令，解析并执行命令。函数库是通过调用系统函数来实现的，了解这一点很重要，在以后用C编程时面对多个功能相似的函数时就知道如何区分选择了。应用程序是通过调用系统函数或库函数或shell命令开发出来，范围相当广泛。

Shell 是一个用C语言编写的程序，它是用户使用Linux的桥梁。Shell既是一种命令语言，又是一种程序设计语言。  
Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。

我们基础阶段课程前两天学习的命令都是shell命令，至于shell编程的部分则在就业班部分学习。

### Shell 的种类

shell可以分成两类：

`第一类是由Bourneshell衍生出来的包括sh、ksh、bash、zsh等；`

`第二类是由Cshell衍生出来的，包括csh与tcsh等。`

当前比较通用的shell就是bashshell。

### 查看当前shell种类

```
终端上键入echo $SHELL
/bin/bash
```

## 为什么要学习Shell命令

shell作为用户和操作系统内核之间的信使。如果我们想要让操作系统高效的帮用户进行数据处理，就需要和信使shell进行沟通并掌握和信使的沟通技巧。  
因此了解信使的性格（操作命令）是尤为必要的。

## 重要概念

### 通配符

```
? 通配一个任意字符

* 通配多个任意字符
```

### Inode

Inode是linux/unix操作系统中的一种数据结构，包含了各文件相关的一些重要信息。在创建文件系统时，就会同时创建大量的inode。

与Inode相关的还有一个概念就是inumber，Inumber只是文件相关信息中的一项信息。  
Inode是指的数据结构结点，而inumber结点对应的索引编号。

文件储存在硬盘上，硬盘的最小存储单位叫做"扇区"（Sector）。每个扇区储存512字节（相当于0.5KB）。  
操作系统读取硬盘的时候，不会一个个扇区地读取，这样效率太低，而是一次性连续读取多个扇区，即一次性读取一个"块"（block）。这种由多个扇区组成的"块"，是文件存取的最小单位。"块"的大小，最常见的是4KB，即连续八个 sector组成一个 block。  
文件数据都储存在"块"中，那么很显然，我们还必须找到一个地方储存文件的元信息，比如文件的创建者、文件的创建日期、文件的大小等等。这种储存文件元信息的区域就叫做inode，中文译名为"索引节点"。  
每一个文件都有对应的inode，里面包含了与该文件有关的一些信息。  
都包含了哪些主要信息呢？

Inode的结构：

```
inode编号[inumber]
用来识别文件类型，以及用于 C函数 stat 的模式信息
文件的链接数目  [ln -s ]
属主的 UID
属主的组 ID (GID)
文件的大小
文件所使用的磁盘块的实际数目
最近一次修改的时间
```

1、一个文件只对应一个Inode，而一个文件根据其大小，会占用多块blocks。  
2、当我们删除文件的时候，只是把Inode标记为可用，文件在block中的内容是没有被清除的，只有在有新的文件需要占用block的时候，才会被覆盖。

表面上，用户通过文件名，打开文件。实际上，系统内部这个过程分成三步：首先，系统找到这个文件名对应的inode号码；其次，通过inode号码，获取inode信息；最后，根据inode信息，找到文件数据所在的block，读出数据。

### 软链接与硬链接

**软链接**

pc@iZ25g2i2xsmZ:~/code$ ls -i  
786883 a.c  786866 test  786890 test.o  
pc@iZ25g2i2xsmZ:~/code$ ls -i a.c  
786883 a.c  
pc@iZ25g2i2xsmZ:~/code$  
pc@iZ25g2i2xsmZ:~/code$ ln -s a.c a

pc@iZ25g2i2xsmZ:~/code$ ls -ail

```
total 28
786851 drwxrwxr-x 2 pc pc 4096 Dec 15 17:01 .
786702 drwxr-xr-x 4 pc pc 4096 Dec 15 16:57 ..
792212 lrwxrwxrwx 1 pc pc    3 Dec 15 17:01 a -> a.c
786883 -rw-rw-r-- 1 pc pc   71 Dec 14 14:31 a.c
786894 -rw-rw-r-- 1 pc pc    0 Dec 15 16:58 .aout
786866 -rwxrwxr-x 1 pc pc 8557 Dec 14 14:31 test
786890 -rw-rw-r-- 1 pc pc 1504 Dec 14 14:31 test.o
```

**硬链接**

软硬有何不同

硬链接是不会占用磁盘的空间的。  
如果说删除硬链接的话，就会改变Inode count的数量。硬链接还有其他的两个特性：不能跨Filesystem也不能link目录。

下面再来看看这个软链接

\[root@yufei test\]\# ls -il testfile.soft testfile  
976 -rw-r--r--. 3 root root 0 Apr  5 21:50 testfile  
978 lrwxrwxrwx. 1 root root 8 Apr  5 21:52 testfile.soft -&gt; testfile  
他的Inode number和原文件不一样。而且大小也发生了变化。可见，这个软链接是重新建立了一个文件，而文件是指向到原文件，而不是指向原Inode。当然他会占用掉 inode 与 block。当我们删除了源文件后，链接文件不能独立存在，虽然仍保留文件名，但我们却不能查看软链接文件的内容了。

但软链接是可以跨文件系统，而且是可以链接目录。他就相当于windows系统下的快捷方式一样。通过这个特性，我们可以通过软链接解决某个分区inode conut不足的问题\(软链接到另一个inode count足够多的分区\)。

### 重定向

\*\*分类:输入重定向 &lt; 、输出重定向 &gt; 、追加输出重定向 &gt;&gt;

把/dev/null看作"黑洞". 它非常等价于一个只写文件. 所有写入它的内容都会永远丢失. 而尝试从它那儿读取内容则什么也读不到.

cat /dev/null &gt; /var/log/messages

将执行命令产生的错误信息重定向到 黑洞中表示忽略。

### 管道

管道也是一种文件，在同一个管道中数据只能单向流动。

管道操作符 '\|'，它只能处理经由前面一个指令传出的正确输出信息，对错误信息信息没有直接处理能力。然后，传递给下一个命令，作为标准的输入.

注意：管道命令只处理前一个命令正确输出，不处理错误输出；

比如

`ls -al | wc -l` 统计`ls -al` 命令的结果集的行数。

### 文件系统

### 相对路径

路径是对目录的层次结构的一种描述。我们想要进入到某个目录下，那从当前路径到目标路径一定有一条 路径是可以到达的。  
相对路径描述的路径是从当前所在出发目录的方法。

### 绝对路径

同理，绝对路径描述的路径是从根目录/开始的路径。

### 根目录/

#### Linux目录结构的来源

Linux目录结构的来源于UNIX目录结构

[http://lists.busybox.net/pipermail/busybox/2010-December/074114.html](http://lists.busybox.net/pipermail/busybox/2010-December/074114.html)

PDP-7计算机介绍

[https://en.wikipedia.org/wiki/PDP-7](https://en.wikipedia.org/wiki/PDP-7)

话说1969年，Ken Thompson和Dennis Ritchie在小型机PDP-7上发明了Unix。1971年，他们将主机升级到了PDP-11。

当时，他们使用一种叫做RK05的储存盘，一盘的容量大约是1.5MB。

没过多久，操作系统（根目录）变得越来越大，一块盘已经装不下了。于是，他们加上了第二盘RK05，并且规定第一块盘专门放系统程序，第二块盘专门放用户自己的程序，因此挂载的目录点取名为/usr。也就是说，根目录"/"挂载在第一块盘，"/usr"目录挂载在第二块盘。除此之外，两块盘的目录结构完全相同，第一块盘的目录（/bin, /sbin, /lib, /tmp...）都在/usr目录下重新出现一次。  
后来，第二块盘也满了，他们只好又加了第三盘RK05，挂载的目录点取名为/home，并且规定/usr用于存放用户的程序，/home用于存放用户的数据。  
从此，这种目录结构就延续了下来。随着硬盘容量越来越大，各个目录的含义进一步得到明确。  
　　/：存放系统程序，也就是At&t开发的Unix程序。  
　　/usr：存放Unix系统商（比如IBM和HP）开发的程序。  
　　/usr/local：存放用户自己安装的程序。  
　　/opt：在某些系统，用于存放第三方厂商开发的程序，所以取名为option，意为"选装"。

## 重要技能

键入shell命令的时候能够擅用Tab键自动补齐

## 常用命令集锦

### ls

list,列举当前目录下的文件列表\(包括目录\)  
常用选项  
a 显示所有文件\(目录、默认隐藏不显示的.打头的文件\)  
l 详细信息  
i 显示iNode编号\(iNumber\)

```
# 后面不加任何参数表示 匹配任何条件

python@ubuntu:~$ ls
class    Documents  examples.desktop  Pictures  Templates  workspace
Desktop  Downloads  Music             Public    Videos

# 查找以D字符开始的文件和目录
python@ubuntu:~$ ls D*
Desktop:

Documents:

Downloads:
node-v6.1.0-linux-x64
```

### pwd

Print Working Directory，打印当前工作目录

pc@iZ25g2i2xsmZ:~/code$ pwd  
/home/pc/code

### cd

change directory,改变当前的工作目录

```
. 代表当前路径  
..代表上一级路径  
/ 代表根目录  
~ 代表当前用户的主目录\(home directory，家目录\)
```

pc@iZ25g2i2xsmZ:~/code$ cd ..  
pc@iZ25g2i2xsmZ:~$ pwd  
/home/pc

cd 后面不跟参数默认的是切换到用户的主目录

cd 想切换到的目录  
pc@iZ25g2i2xsmZ:~$ ls  
code  code1  
pc@iZ25g2i2xsmZ:~$ cd code  
pc@iZ25g2i2xsmZ:~/code$ ls  
a.c  test  test.o

### 查看文件内容

cat、more、less、tail、head

**cat**  
英文单词 catenate的缩写，释义 `vt.连接，使连续;`。  
从文件\(可能多个\)中读取数据并且输出 内容。复制文件（多个）内容到一个新的文档中用于合并或者追加。

**more**  
一次显示一屏幕的文本内容，只能往后。

从第三行开始显示myfile文件  
more +3 myfile.txt

显示以  
more +/"hope" myfile.txt

**less**  
一次显示一屏幕的文本内容，可以往前、往后。

**head**

head表示头部，表示查看文件的前n行，n默认为10。  
pc@iZ25g2i2xsmZ:~/test\_struct$ head ii

```
bbbbbbbb
cccccccc
dddddddd
eeeeeeee
ffffffff
gggggggg
hhhhhhhh
iiiiiiii
jjjjjjjj
```

如果想自定义查看行数。

```
pc@iZ25g2i2xsmZ:~/test_struct$ head -5 ii
bbbbbbbb
cccccccc
dddddddd
eeeeeeee
```

**tail**

tail表示尾部，表示查看文件的后n行，n默认为10。

```
pc@iZ25g2i2xsmZ:~/test_struct$ tail ii
qqqqqqqq
rrrrrrrr
ssssssss
tttttttt
uuuuuuuu
vvvvvvvv
wwwwwwww
xxxxxxxx
yyyyyyyy
zzzzzzzz
```

如果想自定义查看行数。  
pc@iZ25g2i2xsmZ:~/test\_struct$ tail -5 ii  
vvvvvvvv  
wwwwwwww  
xxxxxxxx  
yyyyyyyy  
zzzzzzzz

### 文件\(目录\)操作

cp、mv、mkdir、rmdir、rm

**cp**

copy,表示复制的意思。
将当前目录下的main.c文件复制到上一级目录中  
pc@iZ25g2i2xsmZ:~/code$ cp main.c ../

也可以在复制文件的过程中进行改名  
pc@iZ25g2i2xsmZ:~$ cp test\_file i

也可以进行交互式的复制\(在目标文件存在的时候会进行提醒是否覆盖\)  
pc@iZ25g2i2xsmZ:~$ cp test\_file i -i  
cp: overwrite ‘i’? y

目录是一种文件，所以也可以复制目录 但是需要加-R选项  
pc@iZ25g2i2xsmZ:~$ cp -R code code1

也可以在复制的时候带上过滤条件  
pc@iZ25g2i2xsmZ:~$ cp code/\*.c test/ -r

**mv**

move,表示移动、剪切的意思。
移动指定文件 t.tar 到指定目录 test下  
pc@iZ25g2i2xsmZ:~$ mv t.tar test/

对文件进行改名  
pc@iZ25g2i2xsmZ:~$ mv my.tar your.tar

同理也可以移动目录  
pc@iZ25g2i2xsmZ:~$ mv code1 test/

也可以在移动目录的时候进行改名  
pc@iZ25g2i2xsmZ:~$ mv test tt

**mkdir**  
创建目录 make directory

-p选项 在创建多层级目录的时候，如果父 目录结点不存在mkdir将首先创建。  
Creates the directory /home/chope/a/b/c. If the parent directory /home/chope/a/b does not already exist, mkdir will create that directory first.

mkdir -p /home/chope/a/b/c

**rmdir**
remove directory

删除目录目录 ，前提是目录为空，否则将删除失败。

**rm**  
单词 remove的缩写 ,表示删除、移除的意思。  
可以用于删除文件\(目录\)， removes \(deletes\) files or directories.。

-r \(--recursive\) 递归-  
-i 交互  
-f 强制的 忽略一切

rm myfile.txt  
rm -f myfile.txt  
rm \*

这是一个**容易**带来灾难的命令，使用之前请三思再下手。

> 若是重要数据的销毁，绝对要提一下这个命令。  
> 和rm不同的时候，shred命令会对删除的进行覆盖重写，一般使用 shred -u -z filename

2017年初`rm -rf 惨案：GitLab丢了300GB实时产品数据`

一位身处荷兰的GitLab系统管理员在进行数据库复制过程中不小心在一台错误的服务器上删除了一个目录，他删除了一个包含 300GB 实时产品数据的文件夹，在取消 rm -rf 删除命令后该文件夹只剩下 4.5GB 数据。并且最近的数据还是在6小时前备份的。
(移步灾祸现场)[http://top.jobbole.com/36129/]

### 更改文件权限与所属

**chmod**

英文 change mode的缩写。在Linux\(或者类UNIX系统\)上，有一套规则 谁能能够访问那些文件，以及他们能如何访问。  
这种规则就叫文件权限（file permissions or file modes）。  
chmod提供了方法可以用于改变规则。

permissions defines the permissions for the owner of the file \(the "user"\), members of the group who owns the file \(the "group"\), and anyone else \("others"\). There are two ways to represent these permissions: with symbols \(alphanumeric characters\), or with octal numbers \(the digits 0 through 7\).

每一组权限定义了 文件拥有者\(user\)，文件拥有者同组用户\(group\)，其他用户\(other\)。  
有两种方式方式权限:

字母数字字符

```
pc@iZ25g2i2xsmZ:~$ ll test_file 
-rwxrw-r-- 1 pc pc 10 Dec 20 15:09 test_file
```

`rwxrw-r--` 可以看出

```
user 对于该文件can **r**ead,can **w**rite,can e**x**ecute。
group对于该文件can **r**ead,can **w**rite
other对于该文件can **r**ead
```

相对的方式设置权限  
优点  
 直接简单，只需要关注目标和现在之间的差距进行操作即可。  
缺点  
 如果差距较多 可能进行的操作很复杂  
chmod g+wx,o+w test\_file

绝对的方式来设置权限  可以忽略当前的权限设置  
chmod u=rwx,g=rx,o=r test\_file

八进制数  
数字法设置权限比较直接。比如 `chmod 754 myfile`  
10进制就是满10进1位，每一位上的数有0、1、2、3、4、5、6、7、8、9  
 8进制就是满 8进1位，每一位上的数有0、1、2、3、4、5、6、7

权限为上的每个8进制数 比如7都是由三个比特位上的值x权值的乘积之和  
一个8进制数由3个bit位构成  
421

```
000
001
010
011
100
101
110
111
```

4 stands for "read",  
2 stands for "write",  
1 stands for "execute"

八进制数7就是4\_1+2\_1+1\_1构成的，也即 rwx。  
八进制数6就是4\_1+2\_1+1\_0构成的，也即 rw-。

>那八进制数3 表示的权限是什么?

**chown**

使用基本形式 chown \[OPTION\]... \[OWNER\]\[:\[GROUP\]\] FILE...

改变file.txt文件所属用户为chope  
chown chope file.txt

如果我想改变一个目录下的所有文件呢? -R选项  
chown -R chope /files/work

在工作场景中需要经常碰到这样一个场景，手动将某目录下的所有子目录和文件全部给 属于某个组的一个用户  
chown -R orancle:oinstall /usr/path/data/

### 查找文件 find

-name pattern    Returns true if the base of a file name \(the path with the leading directories removed\) matches shell pattern pattern. The metacharacters \('\*', '?', and '\[ \]'\) match a '.' at the start of the base name. To ignore a directory and the files under it, use -prune; see an example in the description of -path. Braces are not recognised as being special, despite the fact that some shells including Bash imbue braces with a special meaning in shell patterns. The filename matching is performed with the use of the fnmatch library function. Don't forget to enclose the pattern in quotes in order to protect it from expansion by the shell.  
查找 根目录下及其子目录下 所有的C源代码文件。

find / -name \*.C

查找 /usr/bin /usr/lib目录下的zip压缩文件

find /usr/bin /usr/lib -name '_zip_'

-iname 忽略文件名大小写

-size \[-\|+\] n \[cwbkMG\]根据文件大小查找文件

b    for 512-byte blocks \(this is the default if no suffix is used\)  
  c    for bytes  
  w    for two-byte words  
  k    for Kilobytes \(units of 1024 bytes\)  
  M    for Megabytes \(units of 1048576 bytes\)  
  G    for Gigabytes \(units of 1073741824 bytes\)

大于2MB的  
find / -name \*.zip -size +2M

小于2G的  
find / -name \*.zip -size -2G

等于  
find / -name \*.zip -size 2K

-type  
Returns true if a file is of type c:  
 d    directories目录文件  
 f    regular files普通文件  
 l    symbolic links.链接文件

### 查找文件内容grep

grep是一套工具，在Linux系统中有多种实现。

### tar
 
-f选项后面跟上归档文件名称，所以一般都放置在参数列表的最后一个。

tar -zcvf /tmp/etc.tar.gz /etc 
打包后以 gzip 压缩

tar -jcvf /tmp/etc.tar.bz2 /etc 
打包后，以 bzip2 压缩

### gzip/gunzip命令

>gzip命令只能将一个文件压缩成一个.gz压缩包,并且不保留原文件。

pc@iZ25g2i2xsmZ:~/code/project$ ls
01test_compress.c  a.gz            gzjoin.c  mygzip.h     tuixiangzi
02_compress_gz.c   a.out           libz.a    pcgzip       zconf.h
03_gz.c            compress2.data  Makefile  shuangseqiu  zlib.h
04_gzgetc.c        compress.data   migong    tgzip
pc@iZ25g2i2xsmZ:~/code/project$ gzip *.c
pc@iZ25g2i2xsmZ:~/code/project$ ls
01test_compress.c.gz  a.gz            gzjoin.c.gz  mygzip.h     tuixiangzi
02_compress_gz.c.gz   a.out           libz.a       pcgzip       zconf.h
03_gz.c.gz            compress2.data  Makefile     shuangseqiu  zlib.h
04_gzgetc.c.gz        compress.data   migong       tgzip
pc@iZ25g2i2xsmZ:~/code/project$ gunzip *.gz
pc@iZ25g2i2xsmZ:~/code/project$ ls
01test_compress.c  a               gzjoin.c  mygzip.h     tuixiangzi
02_compress_gz.c   a.out           libz.a    pcgzip       zconf.h
03_gz.c            compress2.data  Makefile  shuangseqiu  zlib.h
04_gzgetc.c        compress.data   migong    tgzip

如果想保留源文件且进行(解)压缩这么操作

```
pc@iZ25g2i2xsmZ:~/code/project$ gzip -c mygzip.h > mygzip.h.gz
pc@iZ25g2i2xsmZ:~/code/project$ ls
01test_compress.c  a               libz.a    mygzip.h.gz  tuixiangzi
02_compress_gz.c   compress2.data  Makefile  pcgzip       zconf.h
03_gz.c            compress.data   migong    shuangseqiu  zlib.h
04_gzgetc.c        gzjoin.c        mygzip.h  tgzip
```

由于zip不能将多个源文件压缩并且合并为一个文件，但是tar却能将多个文件归档为一个文件。所以在这种情况下先用tar进行归档 然后使用压缩工具gzip进行压缩。

虽然有诸如 cat file1 file2 | gzip > foo.gz等命令可以达到这个目的但是且无法再解压的时候分离出两个文件。
### 进程管理ps top kill

### 切换sudo su exit

sudo command可以让命令在root权限下运行而不用切换至root用户。  
前提是 该用户属于sudoer,否则失败。

su \[-\] \[用户名\]  
-代表切换用户的时候默认进入该用户的主目录；如果在切换的时候不带- 则不会切换目录。  
用户名为你想切换到的用户。  
用户名如果不写，默认切换到root用户。  
root用户可以切换到任何用户。

### 网络ifconfig

主要用于查看用户当前计算机的各个网卡相关信息（网络IP地址、子网掩码等等）

## 参考资料

包括但不限于  
[http://www.computerhope.com/unix.htm](http://www.computerhope.com/unix.htm)

### Linux命令行常用快捷键

Ctrl+a：光标回到命令行首。 （a：ahead） 
Ctrl+e：光标回到命令行尾。 （e：end）
Ctrl+l：清屏，光标到第一行。

