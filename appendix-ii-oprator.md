&lt;html lang="zh-CN" dir="ltr" class="client-nojs"&gt;

&lt;head&gt;

&lt;title&gt;C操作符优先级 &lt;/title&gt;

&lt;meta charset="UTF-8" /&gt;

&lt;style type="text/css"&gt;/\*&lt;!\[CDATA\[\*/

.source-c {line-height: normal;}

.source-c li, .source-c pre {

	line-height: normal; border: 0px none white;

}

.c.source-c .de1, .c.source-c .de2 {font: normal normal 1em/1.2em monospace; margin:0; padding:0; background:none; vertical-align:top;}

.c.source-c  {font-family:monospace;}

.c.source-c .imp {font-weight: bold; color: red;}

.c.source-c li, .c.source-c .li1 {font-weight: normal; vertical-align:top;}

.c.source-c .ln {width:1px;text-align:right;margin:0;padding:0 2px;vertical-align:top;}

.c.source-c .li2 {font-weight: bold; vertical-align:top;}

.c.source-c .kw1 {color: \#0000dd;}

.c.source-c .kw2 {color: \#0000ff;}

.c.source-c .kw3 {color: \#0000dd;}

.c.source-c .kw4 {color: \#0000ff;}

.c.source-c .co1 {color: \#909090;}

.c.source-c .co2 {color: \#339900;}

.c.source-c .coMULTI {color: \#ff0000; font-style: italic;}

.c.source-c .es0 {color: \#008000; font-weight: bold;}

.c.source-c .es1 {color: \#008000; font-weight: bold;}

.c.source-c .es2 {color: \#008000; font-weight: bold;}

.c.source-c .es3 {color: \#008000; font-weight: bold;}

.c.source-c .es4 {color: \#008000; font-weight: bold;}

.c.source-c .es5 {color: \#008000; font-weight: bold;}

.c.source-c .br0 {color: \#008000;}

.c.source-c .sy0 {color: \#008000;}

.c.source-c .sy1 {color: \#000080;}

.c.source-c .sy2 {color: \#000040;}

.c.source-c .sy3 {color: \#000040;}

.c.source-c .sy4 {color: \#008080;}

.c.source-c .st0 {color: \#008000;}

.c.source-c .nu0 {color: \#000080;}

.c.source-c .nu6 {color:\#000080;}

.c.source-c .nu8 {color:\#000080;}

.c.source-c .nu12 {color:\#000080;}

.c.source-c .nu16 {color:\#000080;}

.c.source-c .nu17 {color:\#000080;}

.c.source-c .nu18 {color:\#000080;}

.c.source-c .nu19 {color:\#000080;}

.c.source-c .ln-xtra, .c.source-c li.ln-xtra, .c.source-c div.ln-xtra {background-color: \#ffc;}

.c.source-c span.xtra { display:block; }



/\*\]\]&gt;\*/

&lt;/style&gt;&lt;!--\[if lt IE 7\]&gt;&lt;style type="text/css"&gt;body{behavior:url\("/mwiki/skins/cppreference2/csshover.min.htc"\)}&lt;/style&gt;&lt;!\[endif\]--&gt;&lt;/head&gt;

&lt;body class="mediawiki ltr sitedir-ltr ns-0 ns-subject page-c\_language\_operator\_precedence skin-cppreference2 action-view cpp-navbar"&gt;

        &lt;!-- header --&gt;

        &lt;div id="cpp-content-base"&gt;

            &lt;div id="content"&gt;

                &lt;a id="top"&gt;&lt;/a&gt;

                &lt;div id="mw-js-message" style="display:none;" lang="zh-CN" dir="ltr"&gt;&lt;/div&gt;

                                &lt;!-- firstHeading --&gt;

                &lt;h1 id="firstHeading" class="firstHeading"&gt;C操作符优先级&lt;/h1&gt;

                &lt;!-- /firstHeading --&gt;

                &lt;!-- bodyContent --&gt;

                &lt;div id="bodyContent"&gt;

                                        &lt;!-- tagline --&gt;

                    &lt;div id="siteSub"&gt;来自cppreference.com&lt;/div&gt;

                    &lt;!-- /tagline --&gt;

                                        &lt;!-- subtitle --&gt;

                    &lt;div id="contentSub" lang="zh-CN" dir="ltr"&gt;&lt;span class="subpages"&gt;&lt; &lt;a href="/w/c" title="c"&gt;c&lt;/a&gt;&lrm; \| &lt;a href="/w/c/language" title="c/language"&gt;language&lt;/a&gt;&lt;/span&gt;&lt;/div&gt;

                    &lt;!-- /subtitle --&gt;

                                                            &lt;!-- bodycontent --&gt;

                    &lt;div id="mw-content-text" lang="zh-CN" dir="ltr" class="mw-content-ltr"&gt;&lt;div class="t-navbar" style=""&gt;&lt;div class="t-navbar-sep"&gt;&\#160;&lt;/div&gt;&lt;div class="t-navbar-head"&gt;&lt;a href="/w/c" title="c"&gt; C&lt;/a&gt;&lt;div class="t-navbar-menu"&gt;&lt;div&gt;&lt;div&gt;







&lt;p&gt;下表列出了C操作符的优先级和结合性。操作符以优先级降序从上到下列出。

&lt;/p&gt;

&lt;table class="wikitable"&gt;



&lt;tr&gt;

&lt;th style="text-align: left"&gt; 优先级

&lt;/th&gt;

&lt;th style="text-align: left"&gt; 操作符

&lt;/th&gt;

&lt;th style="text-align: left"&gt; 描述

&lt;/th&gt;

&lt;th style="text-align: left"&gt; 结合性

&lt;/th&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th rowspan="6"&gt; 1

&lt;/th&gt;

&lt;td style="border-bottom-style: none"&gt; &lt;code&gt;++&lt;/code&gt; &lt;code&gt;--&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none"&gt; 后缀自增与自减

&lt;/td&gt;

&lt;td style="vertical-align: top" rowspan="6"&gt; 从左向右

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\(\)&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 函数调用

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\[\]&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 数组下标

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;.&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 访问结构体和联合体成员

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;−&gt;&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 通过指针访问结构体和联合体成员

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\(&lt;i&gt;类型&lt;/i&gt;\){&lt;i&gt;列表&lt;/i&gt;}&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 复合字面值&lt;span class="t-mark"&gt;\(C99\)&lt;/span&gt;

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th rowspan="8"&gt; 2

&lt;/th&gt;

&lt;td style="border-bottom-style: none"&gt; &lt;code&gt;++&lt;/code&gt; &lt;code&gt;--&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none"&gt; 前缀自增和自减

&lt;/td&gt;

&lt;td style="vertical-align: top" rowspan="8"&gt; 从右向左

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;+&lt;/code&gt; &lt;code&gt;−&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 一元正和负

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;!&lt;/code&gt; &lt;code&gt;~&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 逻辑非和按位非

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\(&lt;i&gt;类型&lt;/i&gt;\)&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 类型转换

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\*&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 间接寻址（取消引用）

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;&amp;&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 取地址

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;sizeof&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 取长度

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\_Alignof&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 取对齐要求字节数&lt;span class="t-mark"&gt;\(C11\)&lt;/span&gt;

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 3

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;\*&lt;/code&gt; &lt;code&gt;/&lt;/code&gt; &lt;code&gt;%&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 乘法、除法和求余

&lt;/td&gt;

&lt;td style="vertical-align: top" rowspan="11"&gt; 从左向右

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 4

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;+&lt;/code&gt; &lt;code&gt;−&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 加法和减法

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 5

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;&lt;&lt;&lt;/code&gt; &lt;code&gt;&gt;&gt;&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 按位左移和右移

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th rowspan="2"&gt; 6

&lt;/th&gt;

&lt;td style="border-bottom-style: none"&gt; &lt;code&gt;&lt;&lt;/code&gt; &lt;code&gt;&lt;=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none"&gt; 关系运算符&lt;和≤

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-top-style: none"&gt; &lt;code&gt;&gt;&lt;/code&gt; &lt;code&gt;&gt;=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-top-style: none"&gt; 关系运算符&gt;和≥

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 7

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;==&lt;/code&gt; &lt;code&gt;!=&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 关系运算符=和≠

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 8

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;&amp;&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 按位与

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 9

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;^&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 按位异或

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 10

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;\|&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 按位或

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 11

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;&amp;&amp;&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 逻辑与

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 12

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;\|\|&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 逻辑或

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 13

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;?:&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 三元条件操作符

&lt;/td&gt;

&lt;td style="vertical-align: top" rowspan="6"&gt; 从右向左

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th rowspan="5"&gt; 14

&lt;/th&gt;

&lt;td style="border-bottom-style: none"&gt; &lt;code&gt;=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none"&gt; 简单赋值

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;+=&lt;/code&gt; &lt;code&gt;−=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 以和差赋值

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;\*=&lt;/code&gt; &lt;code&gt;/=&lt;/code&gt; &lt;code&gt;%=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 以积、商和余数赋值

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; &lt;code&gt;&lt;&lt;=&lt;/code&gt; &lt;code&gt;&gt;&gt;=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-bottom-style: none; border-top-style: none"&gt; 以按位左移和右移赋值

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;td style="border-top-style: none"&gt; &lt;code&gt;&amp;=&lt;/code&gt; &lt;code&gt;^=&lt;/code&gt; &lt;code&gt;\|=&lt;/code&gt;

&lt;/td&gt;

&lt;td style="border-top-style: none"&gt; 以按位与、异或和或赋值

&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;

&lt;th&gt; 15

&lt;/th&gt;

&lt;td&gt; &lt;code&gt;,&lt;/code&gt;

&lt;/td&gt;

&lt;td&gt; 逗号

&lt;/td&gt;

&lt;td&gt; 从左向右

&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt;

&lt;p&gt;在对表达式做语法分析时，某一行列出的操作符会比低于它的一行的任何操作符更紧密地与参数结合（就像用括号）。

&lt;/p&gt;&lt;p&gt;在同一单元格中的操作符（可能有数行操作符列在同一单元格中）有相同的优先级并以指定方向结合。例如，由于从右向左的结合性，表达式&lt;span class="t-c"&gt;&lt;span class="mw-geshi c source-c"&gt;a&lt;span class="sy1"&gt;=&lt;/span&gt;b&lt;span class="sy1"&gt;=&lt;/span&gt;c&lt;/span&gt;&lt;/span&gt;被解析为&lt;span class="t-c"&gt;&lt;span class="mw-geshi c source-c"&gt;a&lt;span class="sy1"&gt;=&lt;/span&gt;&lt;span class="br0"&gt;&\#40;&lt;/span&gt;b&lt;span class="sy1"&gt;=&lt;/span&gt;c&lt;span class="br0"&gt;&\#41;&lt;/span&gt;&lt;/span&gt;&lt;/span&gt;，而不是&lt;span class="t-c"&gt;&lt;span class="mw-geshi c source-c"&gt;&lt;span class="br0"&gt;&\#40;&lt;/span&gt;a&lt;span class="sy1"&gt;=&lt;/span&gt;b&lt;span class="br0"&gt;&\#41;&lt;/span&gt;&lt;span class="sy1"&gt;=&lt;/span&gt;c&lt;/span&gt;&lt;/span&gt;。请注意，这并不影响子表达式a、b和c的&lt;a href="/w/c/language/eval\_order" title="c/language/eval order"&gt;求值顺序&lt;/a&gt;。

&lt;/p&gt;&lt;p&gt;&lt;br /&gt;

&lt;/p&gt;

&lt;/div&gt; 

	&lt;/body&gt;

&lt;/html&gt;



