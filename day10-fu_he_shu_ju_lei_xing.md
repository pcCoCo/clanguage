# 结构体

## 结构体的定义

### 引入
需求：想要保存学生的姓名，年龄，成绩到一个变量中，怎么办？
我们学过的数据类型中有能实现这个需求么？
数组只能保存相同数据类型的数据。

C语言提供了struct关键字 ，可以用它定义出符合条件的结构体类型。


### 定义

1. 语法

```

struct 结构体名称 
{
     数据类型 成员变量1;
     数据类型 成员变量2;
     数据类型 成员变量3;

     ...
};


```

解决问题：
定义一个结构体类型来保存学生的信息。



```
struct Student 
{
     // 姓名
     char name[10];
     
     // 年龄
     int age;

     // 成绩
     int score;
};
```




2.初始化


```
int num = 10;

// 方式1
struct Student xiaoming = {"xiaoming", 18, 99}; // 结构体变量，这个变量的类型是struct Student， 变量名是 xiaoming.


// 方式2： 如果不想按照顺序初始化，就可以使用点语法
struct Student minmin = {.score = 80, .name = "minmin", .age = 20};


```


3.










## 结构体的内存对齐规则

## 结构体的位域宽度  (待完善)



## Inode结构体分析

每个inode都有一个号码，操作系统用inode号码来识别不同的文件。

这里值得重复一遍，Unix/Linux系统内部不使用文件名，而使用inode号码来识别文件。对于系统来说，文件名只是inode号码便于识别的别称或者绰号。

表面上，用户通过文件名，打开文件。实际上，系统内部这个过程分成三步：首先，系统找到这个文件名对应的inode号码；其次，通过inode号码，获取inode信息；最后，根据inode信息，找到文件数据所在的block，读出数据。

```
struct inode 
{
        struct hlist_node       i_hash;              /* 哈希表 */
        struct list_head        i_list;              /* 索引节点链表 */
        struct list_head        i_dentry;            /* 目录项链表 */
        unsigned long           i_ino;               /* 节点号 */
        atomic_t                i_count;             /* 引用记数 */
        umode_t                 i_mode;              /* 访问权限控制 */
        unsigned int            i_nlink;             /* 硬链接数 */
        uid_t                   i_uid;               /* 使用者id */
        gid_t                   i_gid;               /* 使用者id组 */
        kdev_t                  i_rdev;              /* 实设备标识符 */
        loff_t                  i_size;              /* 以字节为单位的文件大小 */
        struct timespec         i_atime;             /* 最后访问时间 */
        struct timespec         i_mtime;             /* 最后修改(modify)时间 */
        struct timespec         i_ctime;             /* 最后改变(change)时间 */
        unsigned int            i_blkbits;           /* 以位为单位的块大小 */
        unsigned long           i_blksize;           /* 以字节为单位的块大小 */
        unsigned long           i_version;           /* 版本号 */
        unsigned long           i_blocks;            /* 文件的块数 */
        unsigned short          i_bytes;             /* 使用的字节数 */
        spinlock_t              i_lock;              /* 自旋锁 */
        struct rw_semaphore     i_alloc_sem;         /* 索引节点信号量 */
        struct inode_operations *i_op;               /* 索引节点操作表 */
        struct file_operations  *i_fop;              /* 默认的索引节点操作 */
        struct super_block      *i_sb;               /* 相关的超级块 */
        struct file_lock        *i_flock;            /* 文件锁链表 */
        struct address_space    *i_mapping;          /* 相关的地址映射 */
        struct address_space    i_data;              /* 设备地址映射 */
        struct dquot            *i_dquot[MAXQUOTAS]; /* 节点的磁盘限额 */
        struct list_head        i_devices;           /* 块设备链表 */
        struct pipe_inode_info  *i_pipe;             /* 管道信息 */
        struct block_device     *i_bdev;             /* 块设备驱动 */
        unsigned long           i_dnotify_mask;      /* 目录通知掩码 */
        struct dnotify_struct   *i_dnotify;          /* 目录通知 */
        unsigned long           i_state;             /* 状态标志 */
        unsigned long           dirtied_when;        /* 首次修改时间 */
        unsigned int            i_flags;             /* 文件系统标志 */
        unsigned char           i_sock;              /* 可能是个套接字吧 */
        atomic_t                i_writecount;        /* 写者记数 */
        void                    *i_security;         /* 安全模块 */
        __u32                   i_generation;        /* 索引节点版本号 */
        union {
                void            *generic_ip;         /* 文件特殊信息 */
        } u;
};
```



## 作业

实现一个代码能从屏幕上接收任意多人数的信息添加录入。在黑窗口中能够支持print命令 将所有的人的信息打印
再黑窗口中能够支持exit命令退出程序

     提示：命令与数据之间都是用空格分开的。
input:
     add tom  23  beijing
     add  jay    33  taiwan
     add andy  55  HK
input:
     print
output:
     tom  23  beijing
     jay    33  taiwan
     andy 55  HK
input:
     exit
     应用程序退出 拜拜
     
