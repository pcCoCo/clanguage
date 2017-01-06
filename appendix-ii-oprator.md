<table class="wikitable">
<tr>
<th style="text-align: left"> 
优先级
</th>
<th style="text-align: left"> 
操作符
</th>
<th style="text-align: left"> 
描述
</th>
<th style="text-align: left"> 
结合性
</th></tr>
<tr>
<th rowspan="6"> 
1
</th>
<td style="border-bottom-style: none"> 
<code>++</code> <code>--</code>
</td>
<td style="border-bottom-style: none"> 
后缀自增与自减
</td>
<td style="vertical-align: top" rowspan="6"> 
从左向右
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>()</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
函数调用
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>[]</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
数组下标
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>.</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
访问结构体和联合体成员
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>−&gt;</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
通过指针访问结构体和联合体成员
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>(<i>类型</i>){<i>列表</i>}</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
复合字面值<span class="t-mark">(C99)</span>
</td></tr>
<tr>
<th rowspan="8"> 
2
</th>
<td style="border-bottom-style: none"> 
<code>++</code> <code>--</code>
</td>
<td style="border-bottom-style: none"> 
前缀自增和自减
</td>
<td style="vertical-align: top" rowspan="8"> 
从右向左
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>+</code> <code>−</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
一元正和负
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>!</code> <code>~</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
逻辑非和按位非
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>(<i>类型</i>)</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
类型转换
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>*</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
间接寻址（取消引用）
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>&amp;</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
取地址
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>sizeof</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
取长度
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>_Alignof</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
取对齐要求字节数<span class="t-mark">(C11)</span>
</td></tr>
<tr>
<th> 
3
</th>
<td> 
<code>*</code> <code>/</code> <code>%</code>
</td>
<td> 
乘法、除法和求余
</td>
<td style="vertical-align: top" rowspan="11"> 
从左向右
</td></tr>
<tr>
<th> 
4
</th>
<td> 
<code>+</code> <code>−</code>
</td>
<td> 
加法和减法
</td></tr>
<tr>
<th> 
5
</th>
<td> 
<code>&lt;&lt;</code> <code>&gt;&gt;</code>
</td>
<td> 
按位左移和右移
</td></tr>
<tr>
<th rowspan="2"> 
6
</th>
<td style="border-bottom-style: none"> 
<code>&lt;</code> <code>&lt;=</code>
</td>
<td style="border-bottom-style: none"> 
关系运算符&lt;和≤
</td></tr>
<tr>
<td style="border-top-style: none"> 
<code>&gt;</code> <code>&gt;=</code>
</td>
<td style="border-top-style: none"> 
关系运算符&gt;和≥
</td></tr>
<tr>
<th> 
7
</th>
<td> 
<code>==</code> <code>!=</code>
</td>
<td> 
关系运算符=和≠
</td></tr>
<tr>
<th> 
8
</th>
<td> 
<code>&amp;</code>
</td>
<td> 
按位与
</td></tr>
<tr>
<th> 
9
</th>
<td> 
<code>^</code>
</td>
<td> 
按位异或
</td></tr>
<tr>
<th> 
10
</th>
<td> 
<code>|</code>
</td>
<td> 
按位或
</td></tr>
<tr>
<th> 
11
</th>
<td> 
<code>&amp;&amp;</code>
</td>
<td> 
逻辑与
</td></tr>
<tr>
<th> 
12
</th>
<td> 
<code>||</code>
</td>
<td> 
逻辑或
</td></tr>
<tr>
<th> 
13
</th>
<td> 
<code>?:</code>
</td>
<td> 
三元条件操作符
</td>
<td style="vertical-align: top" rowspan="6"> 
从右向左
</td></tr>
<tr>
<th rowspan="5"> 
14
</th>
<td style="border-bottom-style: none"> 
<code>=</code>
</td>
<td style="border-bottom-style: none"> 
简单赋值
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>+=</code> <code>−=</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
以和差赋值
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>*=</code> <code>/=</code> <code>%=</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
以积、商和余数赋值
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> 
<code>&lt;&lt;=</code> <code>&gt;&gt;=</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 
以按位左移和右移赋值
</td></tr>
<tr>
<td style="border-top-style: none"> 
<code>&amp;=</code> <code>^=</code> <code>|=</code>
</td>
<td style="border-top-style: none"> 
以按位与、异或和或赋值
</td></tr>
<tr>
<th> 
15
</th>
<td> 
<code>,</code>
</td>
<td> 
逗号
</td>
<td> 
从左向右
</td></tr></table>