# 第一章 linux基本命令

## 操作系统

操作系统（Operating System，简称OS）是管理和控制计算机硬件与软件资源的计算机程序，是直接运行在“裸机”上的最基本的系统软件，任何其他软件都必须在操作系统的支持下才能运行。

操作系统是用户和计算机的接口，同时也是计算机硬件和其他软件的接口。操作系统的功能包括管理计算机系统的硬件、软件及数据资源，控制程序运行，改善人机界面，为其它应用软件提供支持，让计算机系统所有资源最大限度地发挥作用，提供各种形式的用户界面，使用户有一个好的工作环境，为其它软件的开发提供必要的服务和相应的接口等。实际上，用户是不用接触操作系统的，操作系统管理着计算机硬件资源，同时按照应用程序的资源请求，分配资源，如：划分CPU时间，内存空间的开辟，调用打印机等。

操作系统就像咱们计算机的大管家，负责帮主人高效地管理所有资源。

## Linux是什么

![](/assets/linux.jpg)

Linux操作系统内核诞生于1991 年10 月5 日（这是Linus完成代码后第一次正式向外公布时间）。

严格来讲，Linux这个词本身只表示Linux内核，但实际上人们已经习惯了用Linux来形容整个基于Linux内核并使用GNU 工程各种工具和数据库的操作系统。

linux内核代码在linux.org 上可以下载。

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



## Linux 的诞生

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

## Linux发行版

我会告诉你，很多很多.....

ubuntu 乌邦图

![](/assets/ubuntul.jpg)

老司机评论: 就桌面应用而言是Linux发行版中的翘楚

redhat  小红帽

![](/assets/redhat.jpg)

Linux家族中的贵族

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

`shell可以分成两类：`

`第一类是由Bourneshell衍生出来的包括sh、ksh、bash、zsh等；`

`第二类是由Cshell衍生出来的，包括csh与tcsh等。`

当前比较通用的shell就是bashshell。

### 查看当前shell种类

```
综端上键入echo $SHELL
/bin/bash
```

## 为什么要学习Shell命令

shell作为用户和操作系统内核之间的信使。如果我们想要让操作系统高效的帮用户进行数据处理，就需要和信使shell进行沟通并掌握和信使的沟通技巧。
因此了解信使的性格（操作命令）是尤为必要的。


## 重要概念

### 通配符

? 通配一个任意字符

* 通配多个任意字符


### Inode

Inode是linux/unix操作系统中的一种数据结构，包含了各文件相关的一些重要信息。在创建文件系统时，就会同时创建大量的inode。
 
与Inode相关的还有一个概念就是inumber。
Inumber只是文件相关信息中的一项信息。
Inode是指的数据结构结点，而inumber结点对应的索引编号。

我们对一个文件进行操作，如vi编辑，系统是在inode表中找到inode编号（inumber)，才允许我们打开该inode。当文件的inode分派给一个用户时，另一个用户要操作这个文件时，就要等该inode释放了才可以操作。
 
Inode是数据结构，这个结构是什么样的呢？都包含了哪些主要信息呢？

Inode的结构：

```
inode编号[inumber]
用来识别文件类型，以及用于 stat C 函数的模式信息
文件的链接数目  [ln -s ]
属主的 UID
属主的组 ID (GID)
文件的大小
文件所使用的磁盘块的实际数目
最近一次修改的时间
```
1、一个文件只对应一个Inode，而一个文件根据其大小，会占用多块blocks。
2、当我们删除文件的时候，只是把Inode标记为可用，文件在block中的内容是没有被清除的，只有在有新的文件需要占用block的时候，才会被覆盖。


### 软链接与硬链接

**软链接**

pc@iZ25g2i2xsmZ:~/code$ ls -i
786883 a.c  786866 test  786890 test.o
pc@iZ25g2i2xsmZ:~/code$ ls -i a.c
786883 a.c
pc@iZ25g2i2xsmZ:~/code$ 
pc@iZ25g2i2xsmZ:~/code$ ln -s a.c a
pc@iZ25g2i2xsmZ:~/code$ ll
total 28
drwxrwxr-x 2 pc pc 4096 Dec 15 17:01 ./
drwxr-xr-x 4 pc pc 4096 Dec 15 16:57 ../
lrwxrwxrwx 1 pc pc    3 Dec 15 17:01 a -> a.c
-rw-rw-r-- 1 pc pc   71 Dec 14 14:31 a.c
-rw-rw-r-- 1 pc pc    0 Dec 15 16:58 .aout
-rwxrwxr-x 1 pc pc 8557 Dec 14 14:31 test*
-rw-rw-r-- 1 pc pc 1504 Dec 14 14:31 test.o





**硬链接**


软硬有何不同

硬链接是不会占用磁盘的空间的。
如果说删除硬链接的话，就会改变Inode count的数量。硬链接还有其他的两个特性：不能跨Filesystem也不能link目录。

下面再来看看这个软链接

[root@yufei test]# ls -il testfile.soft testfile
976 -rw-r--r--. 3 root root 0 Apr  5 21:50 testfile
978 lrwxrwxrwx. 1 root root 8 Apr  5 21:52 testfile.soft -> testfile
他的Inode number和原文件不一样。而且大小也发生了变化。可见，这个软链接是重新建立了一个文件，而文件是指向到原文件，而不是指向原Inode。当然他会占用掉 inode 与 block。当我们删除了源文件后，链接文件不能独立存在，虽然仍保留文件名，但我们却不能查看软链接文件的内容了。

但软链接是可以跨文件系统，而且是可以链接目录。他就相当于windows系统下的快捷方式一样。通过这个特性，我们可以通过软链接解决某个分区inode conut不足的问题(软链接到另一个inode count足够多的分区)。

### 重定向

输入重定向 < 、输出重定向 > 、追加输出重定向 >>


### 管道

### 相对路径

### 绝对路径

## 重要技能

键入shell命令的时候能够擅用Tab键自动补齐

## 常用命令集锦

### ls

list,列举当前目录下的文件列表\(包括目录\)
常用选项 
a 显示所有文件(目录、默认隐藏不显示的.打头的文件)
l 详细信息
i 显示iNode编号(iNumber)

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

. 代表当前路径  
..代表上一级路径  
/ 代表根目录  
~ 代表当前用户的主目录\(home directory，家目录\)

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

more cat less tail head

chmod chown

find

grep

ps top kill

a

a

a

a

a

a

a

a

结束

