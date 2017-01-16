
### day01





### day02

* QQ的运行

    * 将qq程序加载到内存
    * CPU再读取内存中QQ程序的指令


* 当我们点击QQ登录按钮后， QQ程序做的事情有哪些？

    * 读取输入的账号
    * 读取输入的密码
    * 将读取的账号和密码发送给腾讯服务器，比较是否正确。

    程序如何存储账号和密码？存在哪儿？
        将号码和密码存储在内存，你要用账号和密码，必须得先获取到。




### day03

* scanf 练习
    1. 模拟需求：用户注册论坛，提示用户输入手机号(随便输入一个数)，接收用户输入的手机号，并打印手机号。

    2. 询问用户今年多大了.用户输入年龄。
    输出一句话:"这么巧啊,我今年也xx岁"

    3. 写一个程序，同时接收班级人数、男孩数、平均分。



* 交换两个变量的值
    * 利用第三方变量
    * 两数相加再相减



* 算术运算符练习

某超市衣服120.88一件，裤子89.9一条，让顾客自己输入买的衣服数量和裤子数量
1）显示他应该付多少钱
2）如果商家打88折，再显示打折以后应该付款多少钱

int main()
{
    
    double kuziPrice = 89.9;
    double yifuPrice = 120.88;
    
    // 定义变量来接收衣服和裤子的数量
    int kuziCount = 0;
    int yifuCount = 0;
    // 用户输入要购买的衣服和裤子的数量
    printf("衣服和裤子买了多少件？\n");
    scanf("%d%d", &kuziCount, &yifuCount);
    
    // 计算总价
    // 衣服单价 * 衣服数量 + 裤子单价 * 裤子数量
    double totalMoney = yifuPrice * yifuCount + kuziPrice * kuziCount;
    
    // 折扣价
    double discountMoney = totalMoney * 0.88;
    
    // 输出
    printf("原总价为:%.2lf,折后价为：%.2lf\n", totalMoney, discountMoney);
    return 0;
}





### day04

* 讲解逻辑运算符案例
    女孩找男朋友： 高 并且 富 并且 帅
    男孩找女朋友： 白 或者 富 或者 美

 
 练习： 输入一个年份,判断是不是闰年
一个年份能被400直接整除(年份%400==0),或者能被4整除但是不能被100整除
(年份%400==0) 或者|| (年份%4==0) 并且&& (年份%100!=0)


* 逻辑运算符的优先级练习
请输入小明的语文成绩和数学成绩，输出以下判断的结果
1)两门成绩都大于90分
2)任意一门大于90分


int main()
{
    // 1.先输入语文和数学成绩
    int chinese, math;
    printf("请输入小明的语文和数学成绩:\n");
    scanf("%d,%d", &chinese, &math);

    // 2.写判断表达式/条件表达式来判断条件
    // 2.1
    int result1 = chinese > 90 && math > 90;

    // 2.2
    int result2 = chinese > 90 || math > 90;

    printf("result1 = %d  result2 = %d\n", result1, result2);
    return 0;
}




* if结构
1. 判断李凯钱包里的钱是否有100块， 如果有100块，下课请吃饭
2. 需求：请用户输入他的儿子的语数外三门课的成绩,如果平均分>=60,给他一个吻.


* 变量作用域
1. 面试题
以下程序执行的结果是多少？

int main()
{
    int a = 20;
    int score = a + 100;
    printf("%d\n", score); // 120
    
    {
        int score = 50;
        {
            score = 10;
            printf("%d\n", score); // 10
        }
        a = 10;
    }
    
    {
        score = a + 250;
        int score = 30;
        printf("%d\n", score); // 30
    }
    
    printf("%d\n", score); // 260
    return 0;
}



2. 编写一个程序，输入某人的身高(cm)和体重(kg), 按以下算法确定他的体重是否为标准、过胖或者过瘦。
(1)标准体重=身高-110；
(2)超过标准体重5kg（即大于5kg）为过胖
(3)低于标准体重（即小于5kg）为过瘦

int main()
{
    
    // 思路
    //1. 获取身高和体重
    float height = 0, weight = 0, standardWeight = 0;
    printf("请输入标准身高和体重：\n");
    scanf("%f,%f", &height, &weight);
    //2. 计算标准体重
    standardWeight = height - 110;
    printf("标准体重是:%fkg\n", standardWeight);
    //3. 实际体重和标准体重比较，输出相应的结果
    
    if (weight - standardWeight > 5) {
        printf("您有点胖哦！健身搞起来!\n");
    }
    
    if (standardWeight - weight > 5) {
        printf("您有点瘦哦，营养不良么？\n");
    }
    
    
    printf("测试结束！\n");
    
    
    return 0;
}


### day05

* if else 
1. 请用户输入儿子的语文 数学 英语成绩.
只要有一门不及格.打死
否则给他一个吻.


2. 征婚网站
请用户输入自己性别,1 代表男  0 代表女
如果用户输入的是0,打印"加入我们吧,无论你是否成年!!!总有一个适合你!!\n"
如果用户输入的是1,询问"你满了18岁了吗1/0"如果回答1,打印"先交钱1000会费,帮你找个好的",如果输入的0
"先交100,考虑你的经济问题,我们帮你留一个好的,成年再来"

//分析
//通过判断用户是男孩是女来选择操作
//女---->直接加入
//男---->再判断是否成年---> 成年了直接交钱
//                  ---> 变相收费
//结论 if-ELSE

int main()
{
    // 定义变量接受性别和年龄
    int sex = 3, age = 3;
    // 用户输入性别
    printf("欢迎光临千荷网！！\n 请输入性别1男/0女\n");
    scanf("%d", &sex);
    // 判断男女
    if (sex == 0) {
        printf("加入我们吧,无论你是否成年!!!总有一个适合你!!\n");
    }
    else
    {
        // 用户输入年龄
        printf("请输入年龄1满/0不满\n");
        scanf("%d", &age);
        // 判断年龄
        if(age == 1)
        {
            printf("先交钱1000会费,帮你找个好的\n");
        }
        else
        {
            printf("先交100,考虑你的经济问题,我们帮你留一个好的,成年再来\n");
        }
    }
    return 0;
}



* if else if 

1.
请输入土豪儿子的成绩
90分以上 奖励一台保时捷汽车(带电池)
80分以上 奖励一台奔驰汽车(带遥控器)
70分以上 奖励一台大众
60分以上 奖励挖掘机
60分以下40分以上 打屁股
40分以下 断绝关系



* case 穿透
1. 请土豪输入儿子的成绩，根据这个成绩，判断考试成绩的等级。
90及以上--->优秀
80-89--->优秀
70-79--->优秀
60-69--->良好
60以下-->不及格


int main()
{
    //定义一个变量接受分数
    int tuHaoSonScore = 0;
    printf("输入分数\n");
    scanf("%d",&tuHaoSonScore);
    tuHaoSonScore = tuHaoSonScore / 10;// 99/10 --9  89/10 --> 8
    //判断-->用switch
    switch (tuHaoSonCount) {
        case 10:
        case 9:
        case 8:
        case 7:
            printf("优秀\n");
            break;
        case 6:
            printf("良好\n");
            break;
        default:
            printf("不及格\n");
            break;
    }
    return 0;
}


2. 请用户输入1个年份,再输入1个月份,显示这1年的这1月有多少天.
提示:
1、3、5、7、8、10、12月份,无论是那个年份 都有31天.
4、6、9、11月份,无论是那个年份，都是30天.
如果是2月份,年份是闰年的话那么就有29天 否则就是28天.


int main()
{
    
    // 先输入年份和月份
    int year = 0, month = 0;
    printf("请输入年份和月份：\n");
    scanf("%d%d", &year, &month);

    // 先判断月份
    switch (month) {
        case 1:
        case 3:
        case 5:
        case 7:
        case 8:
        case 10:
        case 12:
            printf("%d年%d月有31天！\n", year, month);
            break;
        case 4:
        case 6:
        case 9:
        case 11:
            printf("%d年%d月有30天！\n", year, month);
            break;
        case 2:
        {
            if ((year % 400 == 0) || (year % 4 == 0 && year % 100 != 0)) {
                printf("%d年%d月有29天！\n", year, month);
            }
            else
            {
                printf("%d年%d月有28天！\n", year, month);
            }
        }
            break;
        default:
            printf("你是火星人！\n");
            break;
    }
    return 0;
}



* while循环

1. 场景1 --- 循环次数确定，循环体确定
打印5次 “我爱黑马”

2. 练习： 使用while循环，打印10次 “欢迎来黑马学习”

3. 练习： (让用户输入1个数，然后打印这个数的2倍) 这个事情来5次






### day06

* 场景2： 循环体确定,循环次数不确定

1. 反复询问用户:你爱我吗？y/n 只要回答不是y,就继续问，知道回答y为止。

2. 让用户输入账号密码，123456,888888,只要一个不正确，就全部重新输入,直到全部正确为止.


* 场景3：遍历一个范围内所有的数

1. 遍历 23 - 68 之间的所有整数



* 场景4： 找出一个范围内指定范围的数

1.简单版本:请找出100-200之间的所有偶数.

2.升级版本:请找出1000-5000之间各位数之和为5的数.

```

int main()
{
    /*
     1235

     1235 / 1000 = 1
     1235 % 1000 = 235 / 100 = 2
     1235 % 1000 = 235 % 100 = 35 / 10 = 3
     1235 % 1000 = 235 % 100 = 35 % 10 = 5
     */

    int i = 1000;
    while (i <= 5000) {
        // 取出各位数
        int qian = i / 1000;
        int bai = i % 1000 / 100;
        int shi = i % 1000 % 100 / 10;
        int ge = i % 1000 % 100 % 10;

        int sum = qian + bai + shi +ge;

        if (sum == 5) {
            printf("%d\n", i);
        }

        i++;
    }

    printf("结束\n");
    return 0;
}


```


* 场景5： 求累加和平均值

1. (举例)请用户输入班级人数，然后让用户依次输入每一个同学的成绩。
求总分和平均分。



* 场景6：求若干个数的最大值和最小值

1.让用户输入5个数,求这5个数的最大值



* 场景7：计数和穷举
// wifi万能钥匙，也是穷举，从密码数据库中一个一个的试。

1.输入用户名/密码,只要不正确就重新输入,知道输入正确为止
当登录成功之后,显示输入了多少次
//拓展:开发中经常能用到,就算你最后输对了,由于次数太多,还是要对你进行验证如:看头像选好友



2.产生1个 1-100 的随机数,判断产生的数字是多少
int main()
{
    int num = arc4random_uniform(100) + 1;
    printf("%d\n",num);
    int i = 1;
    while (i <= 100) {
        if(num == i)
        {
            printf("产生的随机数为:%d\n",i)
            break;
        }
        i++;
    }
    return 0;
}


3. 面试题
有一篮鸡蛋,至少有两个,如果两个两个数,就多出来一个;如果三个三个的数,多出来一个;是多一四个四个的数,还个,至少有多少个鸡蛋?

int main()
{
    int eggs = 2;
    while (1) {
        if(eggs%2==1&&eggs%3==1&&eggs%4==1)
        {
            printf("至少是%d\n",eggs); // 13
            break;
        }
        eggs++;
    }
    return 0;
}



* do-while
1）反复询问用户你爱我吗？ 直到用户的回答是y。


int main()
{
    char ans = 'a';
    do {
        printf("你爱我吗？ y/n \n");
        
        rewind(stdin);
        scanf("%c", &ans);
    } while (ans != 'y');
    
    return 0;
}


2) 张杰表演1次要唱的歌曲，唱完以后问老师满意否。直到老师满意为止。
int main()
{
    char ans = 'a';
    do {
        printf("你存在,我深深的脑海里.我的梦里!\n");
        printf("老师,我唱的好听吗?\n y/n");
        rewind(stdin);
        scanf("%c", &ans);
    } while (ans != 'y');
    
    return 0;
}



### day07

* for 循环

1.利用for循环求1-100之间的偶数的累加和

int main()
{
    int sum = 0;
    for(int i = 1;i <= 100;i++)
    {
        
        if(i%2==0)
        {
            printf("%d\n",i);
            sum += i;
        }
        
    }
    printf("%d\n",sum);
    return 0;
}

2.利用for循环求100-999之间的水仙花数
提示:水仙花数:各位上的数字的立方和==这个数本身


* 循环嵌套

1。打印三角形
1） 
*
**
***
****
*****
******
*******
********
*********
**********


2）
**********
*********
********
*******
******
*****
****
***
**
*


3）


     *
    **
   ***
  ****
 *****
******



2. 九九乘法表




### day08

* 函数

1.写一个函数，判断1个年份是不是闰年。

2。求三个数中最大值的其他实现


void maxNum(int num1,int num2,int num3)
{
    int max = num1;
    //找到num1和num2之间的最大数
    if(num2 > max)
    {
        max = num2;
    }
    //拿num1和num2之间的最大数和num3比较谁大谁就是三个数中最大的
    if(num3>max)
    {
        max = num3;
    }
    
    printf("%d,%d,%d三个数中,最大值是%d\n",num1,num2,num3,max);
    
}


### day09

1、#include 将包含的文件复制到当前文件中
	#include "Desktop/hello.txt"
	包含的文件需要符合C语言规范

2、多文件开发

	团队协作、方便管理

	模块、功能----->函数

### day10



### day11

### day12

### day13







