<!DOCTYPE html>
<html lang="zh-CN" dir="ltr" class="client-nojs">
<head>
<title>C操作符优先级 </title>
<meta charset="UTF-8" />
<style type="text/css">/*<![CDATA[*/
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
.c.source-c .kw1 {color: #0000dd;}
.c.source-c .kw2 {color: #0000ff;}
.c.source-c .kw3 {color: #0000dd;}
.c.source-c .kw4 {color: #0000ff;}
.c.source-c .co1 {color: #909090;}
.c.source-c .co2 {color: #339900;}
.c.source-c .coMULTI {color: #ff0000; font-style: italic;}
.c.source-c .es0 {color: #008000; font-weight: bold;}
.c.source-c .es1 {color: #008000; font-weight: bold;}
.c.source-c .es2 {color: #008000; font-weight: bold;}
.c.source-c .es3 {color: #008000; font-weight: bold;}
.c.source-c .es4 {color: #008000; font-weight: bold;}
.c.source-c .es5 {color: #008000; font-weight: bold;}
.c.source-c .br0 {color: #008000;}
.c.source-c .sy0 {color: #008000;}
.c.source-c .sy1 {color: #000080;}
.c.source-c .sy2 {color: #000040;}
.c.source-c .sy3 {color: #000040;}
.c.source-c .sy4 {color: #008080;}
.c.source-c .st0 {color: #008000;}
.c.source-c .nu0 {color: #000080;}
.c.source-c .nu6 {color:#000080;}
.c.source-c .nu8 {color:#000080;}
.c.source-c .nu12 {color:#000080;}
.c.source-c .nu16 {color:#000080;}
.c.source-c .nu17 {color:#000080;}
.c.source-c .nu18 {color:#000080;}
.c.source-c .nu19 {color:#000080;}
.c.source-c .ln-xtra, .c.source-c li.ln-xtra, .c.source-c div.ln-xtra {background-color: #ffc;}
.c.source-c span.xtra { display:block; }

/*]]>*/
</style><!--[if lt IE 7]><style type="text/css">body{behavior:url("/mwiki/skins/cppreference2/csshover.min.htc")}</style><![endif]--></head>
<body class="mediawiki ltr sitedir-ltr ns-0 ns-subject page-c_language_operator_precedence skin-cppreference2 action-view cpp-navbar">
        <!-- header -->
        <div id="cpp-content-base">
            <div id="content">
                <a id="top"></a>
                <div id="mw-js-message" style="display:none;" lang="zh-CN" dir="ltr"></div>
                                <!-- firstHeading -->
                <h1 id="firstHeading" class="firstHeading">C操作符优先级</h1>
                <!-- /firstHeading -->
                <!-- bodyContent -->
                <div id="bodyContent">
                                        <!-- tagline -->
                    <div id="siteSub">来自cppreference.com</div>
                    <!-- /tagline -->
                                        <!-- subtitle -->
                    <div id="contentSub" lang="zh-CN" dir="ltr"><span class="subpages">&lt; <a href="/w/c" title="c">c</a>&lrm; | <a href="/w/c/language" title="c/language">language</a></span></div>
                    <!-- /subtitle -->
                                                            <!-- bodycontent -->
                    <div id="mw-content-text" lang="zh-CN" dir="ltr" class="mw-content-ltr"><div class="t-navbar" style=""><div class="t-navbar-sep">&#160;</div><div class="t-navbar-head"><a href="/w/c" title="c"> C</a><div class="t-navbar-menu"><div><div>



<p>下表列出了C操作符的优先级和结合性。操作符以优先级降序从上到下列出。
</p>
<table class="wikitable">

<tr>
<th style="text-align: left"> 优先级
</th>
<th style="text-align: left"> 操作符
</th>
<th style="text-align: left"> 描述
</th>
<th style="text-align: left"> 结合性
</th></tr>
<tr>
<th rowspan="6"> 1
</th>
<td style="border-bottom-style: none"> <code>++</code> <code>--</code>
</td>
<td style="border-bottom-style: none"> 后缀自增与自减
</td>
<td style="vertical-align: top" rowspan="6"> 从左向右
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>()</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 函数调用
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>[]</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 数组下标
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>.</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 访问结构体和联合体成员
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>−&gt;</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 通过指针访问结构体和联合体成员
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>(<i>类型</i>){<i>列表</i>}</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 复合字面值<span class="t-mark">(C99)</span>
</td></tr>
<tr>
<th rowspan="8"> 2
</th>
<td style="border-bottom-style: none"> <code>++</code> <code>--</code>
</td>
<td style="border-bottom-style: none"> 前缀自增和自减
</td>
<td style="vertical-align: top" rowspan="8"> 从右向左
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>+</code> <code>−</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 一元正和负
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>!</code> <code>~</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 逻辑非和按位非
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>(<i>类型</i>)</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 类型转换
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>*</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 间接寻址（取消引用）
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>&amp;</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 取地址
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>sizeof</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 取长度
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>_Alignof</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 取对齐要求字节数<span class="t-mark">(C11)</span>
</td></tr>
<tr>
<th> 3
</th>
<td> <code>*</code> <code>/</code> <code>%</code>
</td>
<td> 乘法、除法和求余
</td>
<td style="vertical-align: top" rowspan="11"> 从左向右
</td></tr>
<tr>
<th> 4
</th>
<td> <code>+</code> <code>−</code>
</td>
<td> 加法和减法
</td></tr>
<tr>
<th> 5
</th>
<td> <code>&lt;&lt;</code> <code>&gt;&gt;</code>
</td>
<td> 按位左移和右移
</td></tr>
<tr>
<th rowspan="2"> 6
</th>
<td style="border-bottom-style: none"> <code>&lt;</code> <code>&lt;=</code>
</td>
<td style="border-bottom-style: none"> 关系运算符&lt;和≤
</td></tr>
<tr>
<td style="border-top-style: none"> <code>&gt;</code> <code>&gt;=</code>
</td>
<td style="border-top-style: none"> 关系运算符&gt;和≥
</td></tr>
<tr>
<th> 7
</th>
<td> <code>==</code> <code>!=</code>
</td>
<td> 关系运算符=和≠
</td></tr>
<tr>
<th> 8
</th>
<td> <code>&amp;</code>
</td>
<td> 按位与
</td></tr>
<tr>
<th> 9
</th>
<td> <code>^</code>
</td>
<td> 按位异或
</td></tr>
<tr>
<th> 10
</th>
<td> <code>|</code>
</td>
<td> 按位或
</td></tr>
<tr>
<th> 11
</th>
<td> <code>&amp;&amp;</code>
</td>
<td> 逻辑与
</td></tr>
<tr>
<th> 12
</th>
<td> <code>||</code>
</td>
<td> 逻辑或
</td></tr>
<tr>
<th> 13
</th>
<td> <code>?:</code>
</td>
<td> 三元条件操作符
</td>
<td style="vertical-align: top" rowspan="6"> 从右向左
</td></tr>
<tr>
<th rowspan="5"> 14
</th>
<td style="border-bottom-style: none"> <code>=</code>
</td>
<td style="border-bottom-style: none"> 简单赋值
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>+=</code> <code>−=</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 以和差赋值
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>*=</code> <code>/=</code> <code>%=</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 以积、商和余数赋值
</td></tr>
<tr>
<td style="border-bottom-style: none; border-top-style: none"> <code>&lt;&lt;=</code> <code>&gt;&gt;=</code>
</td>
<td style="border-bottom-style: none; border-top-style: none"> 以按位左移和右移赋值
</td></tr>
<tr>
<td style="border-top-style: none"> <code>&amp;=</code> <code>^=</code> <code>|=</code>
</td>
<td style="border-top-style: none"> 以按位与、异或和或赋值
</td></tr>
<tr>
<th> 15
</th>
<td> <code>,</code>
</td>
<td> 逗号
</td>
<td> 从左向右
</td></tr></table>
<p>在对表达式做语法分析时，某一行列出的操作符会比低于它的一行的任何操作符更紧密地与参数结合（就像用括号）。
</p><p>在同一单元格中的操作符（可能有数行操作符列在同一单元格中）有相同的优先级并以指定方向结合。例如，由于从右向左的结合性，表达式<span class="t-c"><span class="mw-geshi c source-c">a<span class="sy1">=</span>b<span class="sy1">=</span>c</span></span>被解析为<span class="t-c"><span class="mw-geshi c source-c">a<span class="sy1">=</span><span class="br0">&#40;</span>b<span class="sy1">=</span>c<span class="br0">&#41;</span></span></span>，而不是<span class="t-c"><span class="mw-geshi c source-c"><span class="br0">&#40;</span>a<span class="sy1">=</span>b<span class="br0">&#41;</span><span class="sy1">=</span>c</span></span>。请注意，这并不影响子表达式a、b和c的<a href="/w/c/language/eval_order" title="c/language/eval order">求值顺序</a>。
</p><p><br />
</p>
</div> 
	</body>
</html>
