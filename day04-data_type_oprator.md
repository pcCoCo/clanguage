# day04-数据类型和运算符


    “When in doubt, use brute force. ” “如果局部变量太多，我倾向于拆分子程序。---Ken Thompson  (Unix 之父)


基础数据类型---常量---进制转化

## 基本数据类型 


## 常量

### \#define

在C语言中以#开始的语句都是预处理语句
**注意：预处理语句后面没有分号**

演示在处理的时候 #define 的替换效果



```
#include <stdio.h>
#define HAHA "hello"


int main()
{
    printf("%s",HAHA);
    return 0;
}
```

预处理指令  `gcc -E main.c  -o main1.c`

```
.......
# 2 "main.c" 2



int main()
{
 printf("%s","hello");
 return 0;
}
```






### const

在C语言中const关键字的作用是对定义的变量进行`只读`的限定。



```
const int count = 123;
```

然后在C语言对const语义并没有理论上的那么严谨，在后期学习了指针之后就会发现:


```
#include <stdio.h>
//局域作用域中的const类型的常量  是可以通过指针修改的。

int main()
{
    const int count = 100;
    int *ptr = (int*)&count;
    *ptr = 1001;
    printf("%d",count);
    return 0;
}
```

在开始讲解const关键字的时候应该表明 const是一个限定符。


### 字符串常量


### 整型常量

整型常量可以用二进制、八进制、十进制或十六进制来表示。

## int类型

### int常量，变量

### printf函数输出int值

### printf输出八进制，十六进制

### 有符号和无符号

### 整数溢出

### 大端对齐和小端对齐

## char类型

### char常量，变量

### printf函数输出char值

#### 不能打印char转义符

### char 和 unsigned char

## 浮点类型

```
float, double, long double类型
```

### printf函数输出浮点数

## 进制

二进制

八进制

十进制

十六进制

## 存储类型限定符

### const

### volatile

### register

## 字符串格式化输出和输入

### putchar函数

### printf函数

格式化控制符   %d %x %p %c %s %% 


### getchar函数

### scanf函数，

## 运算符

* \(\)改变优先级

* 强制转换\(显式转换\)

* 隐式转换  
    
    类型转换  
        3/2 = 1;      // 操作数都是整数，结果也是整数。  
        3/2.0 = 1.5 ; // 操作数类型不同，运算之前会先将精度低的操作数隐式转换为精度高的数据类型，再运算，表达式的结果是高精度的数据类型。

// 隐式转换例子

```
int main()
{
    unsigned int a = 99;
    unsigned int b = 100;
    if(a-b < 0)
    {
        printf("%u\n", a);
    }
    else
    {
        printf("b\n");
    }
    return 0;
}
```

* 自增自减运算符++ --

* 逗号表达式

\(先简单介绍，语句时详细讲\)

### 关系运算符

```
< <= > >= == !=
如：2 < 3
```

### 逻辑运算符

在C语言中没有表示真和假的数据类型，

逻辑成立为真；不成立为假；

在C语言中整数值**0表示逻辑假，非0表示真**。

假 比如 : NULL,0
真 比如 : 1,100,-100等非0的值


逻辑与&&

    与；且;并且;
    表达式形式: 子表达式1 && 子表达式2
    
    特点-一假即假
    
逻辑或|| 

    或；或者
    表达式形式: 子表达式1 || 子表达式2
    
    特点-一真即真
    
逻辑非!

    非；
    表达式形式: !子表达式        
    
    特点-真假取反

### 三目运算符  

这是C语言中**唯一一个三目运算符**。

    表达式形式: 
    int res = 1 > 2 ? 1 : 2;
    res的值是几?
    
### &取地址符
    
    int a = 1001;
    printf("a的值是 %d a的地址是 %p\n",a,&a);
    
    

### 运算符优先级和结合方向




### ASCII码表

<!DOCTYPE html>
<html lang="zh-CN" dir="ltr" class="client-nojs">
<head>
<title>ASCII码表 - cppreference.com</title>
<meta charset="UTF-8" />
<meta name="generator" content="MediaWiki 1.21.2" /></head>
<body class="mediawiki ltr sitedir-ltr ns-0 ns-subject page-c_language_ascii skin-cppreference2 action-view cpp-navbar">
<div id="cpp-content-base"> <div id="content"><a id="top"></a><div id="mw-js-message" style="display:none;" lang="zh-CN" dir="ltr"></div>
<!-- firstHeading -->                <h1 id="firstHeading" class="firstHeading">ASCII码表</h1>
                <!-- /firstHeading --><!-- bodyContent -->
                <div id="bodyContent"><!-- tagline -->
                    <div id="siteSub">来自cppreference.com</div> <!-- /tagline --><!-- subtitle -->
                    <!-- /subtitle --><!-- bodycontent -->
                    <div id="mw-content-text" lang="zh-CN" dir="ltr" class="mw-content-ltr"><div class="t-navbar" style=""><div class="t-navbar-sep">&#160;</div><div class="t-navbar-head"><a href="/w/c" title="c"> C</a><div class="t-navbar-menu"><div><div>
<table class="t-nv-begin" cellpadding="0" style="line-height:1.1em;">
<p>下表包含所有128个ASCII码对应的十进制<b>(dec)</b>、八进制<b>(OCT)</b>，十六进制<b>(oct)</b>和字符<b>(ch)</b>。
</p>
<table class="wikitable" style="text-align: left;">

<tr>
<th> <code>dec</code> </th>
<th> <code>oct</code> </th>
<th> <code>hex</code>
</th>
<th style="text-align: left;"> <code>ch</code>
</th>
<td rowspan="33">
</td>
<th> <code>dec</code> </th>
<th> <code>oct</code> </th>
<th> <code>hex</code>
</th>
<th style="text-align: left;"> <code>ch</code>
</th>
<td rowspan="33">
</td>
<th> <code>dec</code> </th>
<th> <code>oct</code> </th>
<th> <code>hex</code>
</th>
<th style="text-align: left;"> <code>ch</code>
</th>
<td rowspan="33">
</td>
<th> <code>dec</code> </th>
<th> <code>oct</code> </th>
<th> <code>hex</code>
</th>
<th style="text-align: left;"> <code>ch</code>
</th></tr>
<tr>
<td> <code> 0</code></td>
<td> <code>0</code></td>
<td><code>00</code></td>
<td><code><b>NUL</b></code> (null) </td>
<td> <code>32</code></td>
<td><code>40</code></td>
<td><code>20</code></td>
<td>(space) </td>
<td> <code>64</code></td>
<td><code>100</code></td>
<td><code>40</code></td>
<td><code><b>@</b></code> </td>
<td> <code> 96</code></td>
<td><code>140</code></td>
<td><code>60</code></td>
<td><code><b>`</b></code>
</td></tr>
<tr>
<td> <code> 1</code></td>
<td> <code>1</code></td>
<td><code>01</code></td>
<td><code><b>SOH</b></code> (start of header) </td>
<td> <code>33</code></td>
<td><code>41</code></td>
<td><code>21</code></td>
<td><code><b>!</b></code> </td>
<td> <code>65</code></td>
<td><code>101</code></td>
<td><code>41</code></td>
<td><code><b>A</b></code> </td>
<td> <code> 97</code></td>
<td><code>141</code></td>
<td><code>61</code></td>
<td><code><b>a</b></code>
</td></tr>
<tr>
<td> <code> 2</code></td>
<td> <code>2</code></td>
<td><code>02</code></td>
<td><code><b>STX</b></code> (start of text) </td>
<td> <code>34</code></td>
<td><code>42</code></td>
<td><code>22</code></td>
<td><code><b>"</b></code> </td>
<td> <code>66</code></td>
<td><code>102</code></td>
<td><code>42</code></td>
<td><code><b>B</b></code> </td>
<td> <code> 98</code></td>
<td><code>142</code></td>
<td><code>62</code></td>
<td><code><b>b</b></code>
</td></tr>
<tr>
<td> <code> 3</code></td>
<td> <code>3</code></td>
<td><code>03</code></td>
<td><code><b>ETX</b></code> (end of text) </td>
<td> <code>35</code></td>
<td><code>43</code></td>
<td><code>23</code></td>
<td><code><b>#</b></code> </td>
<td> <code>67</code></td>
<td><code>103</code></td>
<td><code>43</code></td>
<td><code><b>C</b></code> </td>
<td> <code> 99</code></td>
<td><code>143</code></td>
<td><code>63</code></td>
<td><code><b>c</b></code>
</td></tr>
<tr>
<td> <code> 4</code></td>
<td> <code>4</code></td>
<td><code>04</code></td>
<td><code><b>EOT</b></code> (end of transmission) </td>
<td> <code>36</code></td>
<td><code>44</code></td>
<td><code>24</code></td>
<td><code><b>$</b></code> </td>
<td> <code>68</code></td>
<td><code>104</code></td>
<td><code>44</code></td>
<td><code><b>D</b></code> </td>
<td> <code>100</code></td>
<td><code>144</code></td>
<td><code>64</code></td>
<td><code><b>d</b></code>
</td></tr>
<tr>
<td> <code> 5</code></td>
<td> <code>5</code></td>
<td><code>05</code></td>
<td><code><b>ENQ</b></code> (enquiry) </td>
<td> <code>37</code></td>
<td><code>45</code></td>
<td><code>25</code></td>
<td><code><b>%</b></code> </td>
<td> <code>69</code></td>
<td><code>105</code></td>
<td><code>45</code></td>
<td><code><b>E</b></code> </td>
<td> <code>101</code></td>
<td><code>145</code></td>
<td><code>65</code></td>
<td><code><b>e</b></code>
</td></tr>
<tr>
<td> <code> 6</code></td>
<td> <code>6</code></td>
<td><code>06</code></td>
<td><code><b>ACK</b></code> (acknowledge) </td>
<td> <code>38</code></td>
<td><code>46</code></td>
<td><code>26</code></td>
<td><code><b>&amp;</b></code> </td>
<td> <code>70</code></td>
<td><code>106</code></td>
<td><code>46</code></td>
<td><code><b>F</b></code> </td>
<td> <code>102</code></td>
<td><code>146</code></td>
<td><code>66</code></td>
<td><code><b>f</b></code>
</td></tr>
<tr>
<td> <code> 7</code></td>
<td> <code>7</code></td>
<td><code>07</code></td>
<td><code><b>EL</b></code> (bell) </td>
<td> <code>39</code></td>
<td><code>47</code></td>
<td><code>27</code></td>
<td><code><b>'</b></code> </td>
<td> <code>71</code></td>
<td><code>107</code></td>
<td><code>47</code></td>
<td><code><b>G</b></code> </td>
<td> <code>103</code></td>
<td><code>147</code></td>
<td><code>67</code></td>
<td><code><b>g</b></code>
</td></tr>
<tr>
<td> <code> 8</code></td>
<td><code>10</code></td>
<td><code>08</code></td>
<td><code><b>BS</b></code> (backspace) </td>
<td> <code>40</code></td>
<td><code>50</code></td>
<td><code>28</code></td>
<td><code><b>(</b></code> </td>
<td> <code>72</code></td>
<td><code>110</code></td>
<td><code>48</code></td>
<td><code><b>H</b></code> </td>
<td> <code>104</code></td>
<td><code>150</code></td>
<td><code>68</code></td>
<td><code><b>h</b></code>
</td></tr>
<tr>
<td> <code> 9</code></td>
<td><code>11</code></td>
<td><code>09</code></td>
<td><code><b>HT</b></code> (horizontal tab) </td>
<td> <code>41</code></td>
<td><code>51</code></td>
<td><code>29</code></td>
<td><code><b>)</b></code> </td>
<td> <code>73</code></td>
<td><code>111</code></td>
<td><code>49</code></td>
<td><code><b>I</b></code> </td>
<td> <code>105</code></td>
<td><code>151</code></td>
<td><code>69</code></td>
<td><code><b>i</b></code>
</td></tr>
<tr>
<td> <code>10</code></td>
<td><code>12</code></td>
<td><code>0a</code></td>
<td><code><b>LF</b></code> (line feed - new line) </td>
<td> <code>42</code></td>
<td><code>52</code></td>
<td><code>2a</code></td>
<td><code><b>*</b></code> </td>
<td> <code>74</code></td>
<td><code>112</code></td>
<td><code>4a</code></td>
<td><code><b>J</b></code> </td>
<td> <code>106</code></td>
<td><code>152</code></td>
<td><code>6a</code></td>
<td><code><b>j</b></code>
</td></tr>
<tr>
<td> <code>11</code></td>
<td><code>13</code></td>
<td><code>0b</code></td>
<td><code><b>VT</b></code> (vertical tab) </td>
<td> <code>43</code></td>
<td><code>53</code></td>
<td><code>2b</code></td>
<td><code><b>+</b></code> </td>
<td> <code>75</code></td>
<td><code>113</code></td>
<td><code>4b</code></td>
<td><code><b>K</b></code> </td>
<td> <code>107</code></td>
<td><code>153</code></td>
<td><code>6b</code></td>
<td><code><b>k</b></code>
</td></tr>
<tr>
<td> <code>12</code></td>
<td><code>14</code></td>
<td><code>0c</code></td>
<td><code><b>FF</b></code> (form feed - new page) </td>
<td> <code>44</code></td>
<td><code>54</code></td>
<td><code>2c</code></td>
<td><code><b>,</b></code> </td>
<td> <code>76</code></td>
<td><code>114</code></td>
<td><code>4c</code></td>
<td><code><b>L</b></code> </td>
<td> <code>108</code></td>
<td><code>154</code></td>
<td><code>6c</code></td>
<td><code><b>l</b></code>
</td></tr>
<tr>
<td> <code>13</code></td>
<td><code>15</code></td>
<td><code>0d</code></td>
<td><code><b>CR</b></code> (carriage return) </td>
<td> <code>45</code></td>
<td><code>55</code></td>
<td><code>2d</code></td>
<td><code><b>-</b></code> </td>
<td> <code>77</code></td>
<td><code>115</code></td>
<td><code>4d</code></td>
<td><code><b>M</b></code> </td>
<td> <code>109</code></td>
<td><code>155</code></td>
<td><code>6d</code></td>
<td><code><b>m</b></code>
</td></tr>
<tr>
<td> <code>14</code></td>
<td><code>16</code></td>
<td><code>0e</code></td>
<td><code><b>SO</b></code> (shift out) </td>
<td> <code>46</code></td>
<td><code>56</code></td>
<td><code>2e</code></td>
<td><code><b>.</b></code> </td>
<td> <code>78</code></td>
<td><code>116</code></td>
<td><code>4e</code></td>
<td><code><b>N</b></code> </td>
<td> <code>110</code></td>
<td><code>156</code></td>
<td><code>6e</code></td>
<td><code><b>n</b></code>
</td></tr>
<tr>
<td> <code>15</code></td>
<td><code>17</code></td>
<td><code>0f</code></td>
<td><code><b>SI</b></code> (shift in) </td>
<td> <code>47</code></td>
<td><code>57</code></td>
<td><code>2f</code></td>
<td><code><b>/</b></code> </td>
<td> <code>79</code></td>
<td><code>117</code></td>
<td><code>4f</code></td>
<td><code><b>O</b></code> </td>
<td> <code>111</code></td>
<td><code>157</code></td>
<td><code>6f</code></td>
<td><code><b>o</b></code>
</td></tr>
<tr>
<td> <code>16</code></td>
<td><code>20</code></td>
<td><code>10</code></td>
<td><code><b>DLE</b></code> (data link escape) </td>
<td> <code>48</code></td>
<td><code>60</code></td>
<td><code>30</code></td>
<td><code><b>0</b></code> </td>
<td> <code>80</code></td>
<td><code>120</code></td>
<td><code>50</code></td>
<td><code><b>P</b></code> </td>
<td> <code>112</code></td>
<td><code>160</code></td>
<td><code>70</code></td>
<td><code><b>p</b></code>
</td></tr>
<tr>
<td> <code>17</code></td>
<td><code>21</code></td>
<td><code>11</code></td>
<td><code><b>DC1</b></code> (device control 1) </td>
<td> <code>49</code></td>
<td><code>61</code></td>
<td><code>31</code></td>
<td><code><b>1</b></code> </td>
<td> <code>81</code></td>
<td><code>121</code></td>
<td><code>51</code></td>
<td><code><b>Q</b></code> </td>
<td> <code>113</code></td>
<td><code>161</code></td>
<td><code>71</code></td>
<td><code><b>q</b></code>
</td></tr>
<tr>
<td> <code>18</code></td>
<td><code>22</code></td>
<td><code>12</code></td>
<td><code><b>DC2</b></code> (device control 2) </td>
<td> <code>50</code></td>
<td><code>62</code></td>
<td><code>32</code></td>
<td><code><b>2</b></code> </td>
<td> <code>82</code></td>
<td><code>122</code></td>
<td><code>52</code></td>
<td><code><b>R</b></code> </td>
<td> <code>114</code></td>
<td><code>162</code></td>
<td><code>72</code></td>
<td><code><b>r</b></code>
</td></tr>
<tr>
<td> <code>19</code></td>
<td><code>23</code></td>
<td><code>13</code></td>
<td><code><b>DC3</b></code> (device control 3) </td>
<td> <code>51</code></td>
<td><code>63</code></td>
<td><code>33</code></td>
<td><code><b>3</b></code> </td>
<td> <code>83</code></td>
<td><code>123</code></td>
<td><code>53</code></td>
<td><code><b>S</b></code> </td>
<td> <code>115</code></td>
<td><code>163</code></td>
<td><code>73</code></td>
<td><code><b>s</b></code>
</td></tr>
<tr>
<td> <code>20</code></td>
<td><code>24</code></td>
<td><code>14</code></td>
<td><code><b>DC4</b></code> (device control 4) </td>
<td> <code>52</code></td>
<td><code>64</code></td>
<td><code>34</code></td>
<td><code><b>4</b></code> </td>
<td> <code>84</code></td>
<td><code>124</code></td>
<td><code>54</code></td>
<td><code><b>T</b></code> </td>
<td> <code>116</code></td>
<td><code>164</code></td>
<td><code>74</code></td>
<td><code><b>t</b></code>
</td></tr>
<tr>
<td> <code>21</code></td>
<td><code>25</code></td>
<td><code>15</code></td>
<td><code><b>NAK</b></code> (negative acknowledge) </td>
<td> <code>53</code></td>
<td><code>65</code></td>
<td><code>35</code></td>
<td><code><b>5</b></code> </td>
<td> <code>85</code></td>
<td><code>125</code></td>
<td><code>55</code></td>
<td><code><b>U</b></code> </td>
<td> <code>117</code></td>
<td><code>165</code></td>
<td><code>75</code></td>
<td><code><b>u</b></code>
</td></tr>
<tr>
<td> <code>22</code></td>
<td><code>26</code></td>
<td><code>16</code></td>
<td><code><b>SYN</b></code> (synchronous idle) </td>
<td> <code>54</code></td>
<td><code>66</code></td>
<td><code>36</code></td>
<td><code><b>6</b></code> </td>
<td> <code>86</code></td>
<td><code>126</code></td>
<td><code>56</code></td>
<td><code><b>V</b></code> </td>
<td> <code>118</code></td>
<td><code>166</code></td>
<td><code>76</code></td>
<td><code><b>v</b></code>
</td></tr>
<tr>
<td> <code>23</code></td>
<td><code>27</code></td>
<td><code>17</code></td>
<td><code><b>ETB</b></code> (end of transmission block) </td>
<td> <code>55</code></td>
<td><code>67</code></td>
<td><code>37</code></td>
<td><code><b>7</b></code> </td>
<td> <code>87</code></td>
<td><code>127</code></td>
<td><code>57</code></td>
<td><code><b>W</b></code> </td>
<td> <code>119</code></td>
<td><code>167</code></td>
<td><code>77</code></td>
<td><code><b>w</b></code>
</td></tr>
<tr>
<td> <code>24</code></td>
<td><code>30</code></td>
<td><code>18</code></td>
<td><code><b>CAN</b></code> (cancel) </td>
<td> <code>56</code></td>
<td><code>70</code></td>
<td><code>38</code></td>
<td><code><b>8</b></code> </td>
<td> <code>88</code></td>
<td><code>130</code></td>
<td><code>58</code></td>
<td><code><b>X</b></code> </td>
<td> <code>120</code></td>
<td><code>170</code></td>
<td><code>78</code></td>
<td><code><b>x</b></code>
</td></tr>
<tr>
<td> <code>25</code></td>
<td><code>31</code></td>
<td><code>19</code></td>
<td><code><b>EM</b></code> (end of medium) </td>
<td> <code>57</code></td>
<td><code>71</code></td>
<td><code>39</code></td>
<td><code><b>9</b></code> </td>
<td> <code>89</code></td>
<td><code>131</code></td>
<td><code>59</code></td>
<td><code><b>Y</b></code> </td>
<td> <code>121</code></td>
<td><code>171</code></td>
<td><code>79</code></td>
<td><code><b>y</b></code>
</td></tr>
<tr>
<td> <code>26</code></td>
<td><code>32</code></td>
<td><code>1a</code></td>
<td><code><b>SUB</b></code> (substitute) </td>
<td> <code>58</code></td>
<td><code>72</code></td>
<td><code>3a</code></td>
<td><code><b>:</b></code> </td>
<td> <code>90</code></td>
<td><code>132</code></td>
<td><code>5a</code></td>
<td><code><b>Z</b></code> </td>
<td> <code>122</code></td>
<td><code>172</code></td>
<td><code>7a</code></td>
<td><code><b>z</b></code>
</td></tr>
<tr>
<td> <code>27</code></td>
<td><code>33</code></td>
<td><code>1b</code></td>
<td><code><b>ESC</b></code> (escape) </td>
<td> <code>59</code></td>
<td><code>73</code></td>
<td><code>3b</code></td>
<td><code><b>;</b></code> </td>
<td> <code>91</code></td>
<td><code>133</code></td>
<td><code>5b</code></td>
<td><code><b>[</b></code> </td>
<td> <code>123</code></td>
<td><code>173</code></td>
<td><code>7b</code></td>
<td><code><b>{</b></code>
</td></tr>
<tr>
<td> <code>28</code></td>
<td><code>34</code></td>
<td><code>1c</code></td>
<td><code><b>FS</b></code> (file separator) </td>
<td> <code>60</code></td>
<td><code>74</code></td>
<td><code>3c</code></td>
<td><code><b>&lt;</b></code> </td>
<td> <code>92</code></td>
<td><code>134</code></td>
<td><code>5c</code></td>
<td><code><b>\ </b></code> </td>
<td> <code>124</code></td>
<td><code>174</code></td>
<td><code>7c</code></td>
<td><code><b>&#124;</b></code>
</td></tr>
<tr>
<td> <code>29</code></td>
<td><code>35</code></td>
<td><code>1d</code></td>
<td><code><b>GS</b></code> (group separator) </td>
<td> <code>61</code></td>
<td><code>75</code></td>
<td><code>3d</code></td>
<td><code><b>=</b></code> </td>
<td> <code>93</code></td>
<td><code>135</code></td>
<td><code>5d</code></td>
<td><code><b>]</b></code> </td>
<td> <code>125</code></td>
<td><code>175</code></td>
<td><code>7d</code></td>
<td><code><b>}</b></code>
</td></tr>
<tr>
<td> <code>30</code></td>
<td><code>36</code></td>
<td><code>1e</code></td>
<td><code><b>RS</b></code> (record separator) </td>
<td> <code>62</code></td>
<td><code>76</code></td>
<td><code>3e</code></td>
<td><code><b>&gt;</b></code> </td>
<td> <code>94</code></td>
<td><code>136</code></td>
<td><code>5e</code></td>
<td><code><b>^</b></code> </td>
<td> <code>126</code></td>
<td><code>176</code></td>
<td><code>7e</code></td>
<td><code><b>~</b></code>
</td></tr>
<tr>
<td> <code>31</code></td>
<td><code>37</code></td>
<td><code>1f</code></td>
<td><code><b>US</b></code> (unit separator) </td>
<td> <code>63</code></td>
<td><code>77</code></td>
<td><code>3f</code></td>
<td><code><b>?</b></code> </td>
<td> <code>95</code></td>
<td><code>137</code></td>
<td><code>5f</code></td>
<td><code><b>_</b></code> </td>
<td> <code>127</code></td>
<td><code>177</code></td>
<td><code>7f</code></td>
<td><code><b>DEL</b></code> (delete)
</td></tr></table></body>
</html>


### 反汇编演示

汇编语言种类   Intel汇编和AT&T汇编
在intel的官方文档中使intel语法，Windows也使用intel语法；而UNIX平台的汇编器一直使用AT&T语法，在Linux内核中源码中部分代码使用AT&T汇编编写。

从汇编的角度看a++ 和++b的指令

前置++和后置++在表达式中单独使用的时候的，我们就可以认为其实完全一样的。



```
#include <stdio.h>
int main()
{
	int a = 100;
	int b = 101;
	int c = 102;
	int d = 103;
	int e = 104;

	++b;	
	c++;

	printf("%d %d %d %d %d\n",a,b,c,d,e);
	getchar();
	return 0;
}
```



```
10: ++b;
000417F1 8B 45 EC mov eax,dword ptr [b]  
000417F4 83 C0 01 add eax,1
000417F7 89 45 EC mov dword ptr [b],eax  
11: c++;
000417FA 8B 45 E0 mov eax,dword ptr [c]  
000417FD 83 C0 01 add eax,1
00041800 89 45 E0 mov dword ptr [c],eax  
```
可以看到 **单独前置和后置对应的汇编指令是完全一致的**。**但也不排除不同的编译器的功能不一样，对这条语句的理解不一样**。



AT&T汇编语句 ；AT&T 中寄存器需要加前缀“%” ；立即数需要加前缀“$” 。 



```
pc@iZ25g2i2xsmZ:~$ gcc -E test_asm.c -o test_asm.i
pc@iZ25g2i2xsmZ:~$ gcc -S test_asm.i -o test_asm.s
```



```
movl    $100, -20(%rbp)
movl    $101, -16(%rbp)
movl    $102, -12(%rbp)
movl    $103, -8(%rbp)
movl    $104, -4(%rbp)
addl    $1, -16(%rbp)
addl    $1, -12(%rbp)
```



非单独使用的场景
```
#include <stdio.h>
int main()
{
    int a = 100;
    int b = 101;
    int c = 102;
    int d = 103;
    int e = 104;

    a = ++b;

    a = c++;

    d = d + 1;

    e += 1;

    printf("%d %d %d %d %d\n",a,b,c,d,e);
    getchar();
    return 0;
}
```

```
--- g:\code\test_asm\test_asm\main.cpp -----------------------------------------
     1: #include <stdio.h>
     2: int main()
     3: {
00E317A0 55                   push        ebp  
00E317A1 8B EC                mov         ebp,esp  
00E317A3 81 EC FC 00 00 00    sub         esp,0FCh  
00E317A9 53                   push        ebx  
00E317AA 56                   push        esi  
00E317AB 57                   push        edi  
00E317AC 8D BD 04 FF FF FF    lea         edi,[ebp-0FCh]  
00E317B2 B9 3F 00 00 00       mov         ecx,3Fh  
00E317B7 B8 CC CC CC CC       mov         eax,0CCCCCCCCh  
00E317BC F3 AB                rep stos    dword ptr es:[edi]  
     4:     int a = 100;
00E317BE C7 45 F8 64 00 00 00 mov         dword ptr [a],64h  
     5:     int b = 101;
00E317C5 C7 45 EC 65 00 00 00 mov         dword ptr [b],65h  
     6:     int c = 102;
00E317CC C7 45 E0 66 00 00 00 mov         dword ptr [c],66h  
     7:     int d = 103;
00E317D3 C7 45 D4 67 00 00 00 mov         dword ptr [d],67h  
     8:     int e = 104;
00E317DA C7 45 C8 68 00 00 00 mov         dword ptr [e],68h  
     9: 
    10:     a = ++b;
00E317E1 8B 45 EC             mov         eax,dword ptr [b]  
00E317E4 83 C0 01             add         eax,1  
00E317E7 89 45 EC             mov         dword ptr [b],eax  
00E317EA 8B 4D EC             mov         ecx,dword ptr [b]  
00E317ED 89 4D F8             mov         dword ptr [a],ecx  
    11:     
    12:     a = c++;
00E317F0 8B 45 E0             mov         eax,dword ptr [c]  
00E317F3 89 45 F8             mov         dword ptr [a],eax  
00E317F6 8B 4D E0             mov         ecx,dword ptr [c]  
00E317F9 83 C1 01             add         ecx,1  
00E317FC 89 4D E0             mov         dword ptr [c],ecx  
    13: 
    14:     d = d + 1;
00E317FF 8B 45 D4             mov         eax,dword ptr [d]  
00E31802 83 C0 01             add         eax,1  
00E31805 89 45 D4             mov         dword ptr [d],eax  
    15: 
    16:     e += 1;
00E31808 8B 45 C8             mov         eax,dword ptr [e]  
00E3180B 83 C0 01             add         eax,1  
00E3180E 89 45 C8             mov         dword ptr [e],eax  
    17: 
    18:     printf("%d %d %d %d %d\n",a,b,c,d,e);
00E31811 8B 45 C8             mov         eax,dword ptr [e]  
00E31814 50                   push        eax  
00E31815 8B 4D D4             mov         ecx,dword ptr [d]  
00E31818 51                   push        ecx  
00E31819 8B 55 E0             mov         edx,dword ptr [c]  
00E3181C 52                   push        edx  
00E3181D 8B 45 EC             mov         eax,dword ptr [b]  
00E31820 50                   push        eax  
00E31821 8B 4D F8             mov         ecx,dword ptr [a]  
00E31824 51                   push        ecx  
00E31825 68 30 6B E3 00       push        offset string "%d %d %d %d %d\n" (0E36B30h)  
00E3182A E8 F1 FA FF FF       call        _printf (0E31320h)  
00E3182F 83 C4 18             add         esp,18h  
    19:     getchar();
00E31832 8B F4                mov         esi,esp  
00E31834 FF 15 74 91 E3 00    call        dword ptr [__imp__getchar (0E39174h)]  
00E3183A 3B F4                cmp         esi,esp  
00E3183C E8 D2 F8 FF FF       call        __RTC_CheckEsp (0E31113h)  
    20:     return 0;
00E31841 33 C0                xor         eax,eax  
    21: }
```







