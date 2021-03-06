| 优先级 | 操作符 | 描述 | 结合性 |
| :--- | :--- | :--- | :--- |
| 1 | ++ -- | 后缀自增与自减 | 从左向右 |
|  | \(\) | 函数调用 |  |
|  | \[\] | 数组下标 |  |
|  | . | 访问结构体和联合体成员 |  |
|  | -&gt; | 通过指针访问结构体和联合体成员 |  |
|  | \(类型\){列表} | 复合字面值\(C99\) |  |
| 2 | ++ -- | 前缀自增和自减 | 从右向左 |
|  | + - | 一元正和负 |  |
|  | ! ~ | 逻辑非和按位非 |  |
|  | \(类型\) | 类型转换 |  |
|  | \* | 间接寻址\(解引用\) |  |
|  | & | 取地址 |  |
|  | sizeof | 取长度 |  |
|  | \_Alignof | 取对齐要求字节数\(C11\) |  |
| 3 | \* / % | 乘法、除法和求余 | 从左向右 |
| 4 | + − | 加法和减法 |  |
| 5 | << >> | 按位左移和右移 |  |
| 6 | < <= | 关系运算符&lt;和≤ |  |
|  | > >= | 关系运算符&gt;和≥ |  |
| 7 | == != | 关系运算符=和≠ |  |
| 8 | & | 按位与 |  |
| 9 | ^ | 按位异或 |  |
| 10 | \| | 按位或 |  |
| 11 | && | 逻辑与 |  |
| 12 |  | 逻辑或 |  |
| 13 | ?: | 三目条件运算符 | 从右向左 |
| 14 | = | 简单赋值 |  |
|  | += -= | 以和、差赋值 |  |
|  | \*= /= %= | 以积、商、余数赋值 |  |
|  | <<= >>= | 以按位左移和右移赋值 |  |
|  | = | 以按位与、异或和或赋值 |  |
| 15 | , | 逗号 | 从左到有 |

在对表达式做语法分析时，某一行列出的操作符会比低于它的一行的任何操作符更紧密地与参数结合（就像用括号）。
在同一单元格中的操作符（可能有数行操作符列在同一单元格中）有相同的优先级并以指定方向结合。例如，由于从右向左的结合性，表达式a=b=c被解析为a=(b=c)，而不是(a=b)=c。请注意，这并不影响子表达式a、b和c的求值顺序。

