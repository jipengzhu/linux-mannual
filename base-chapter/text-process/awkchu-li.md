# awk
awk是一种编程语言，用于在linux/unix下对文本和数据进行处理。
- 数据可以来自标准输入(stdin)、一个或多个文件
- 支持用户自定义函数以及动态正则表达式等先进功能
- 有很多内建的功能，比如数组、函数等，和c语言类似



# awk命令
格式如下
```
awk [options] [-v var=value]... <script>  <file>...
awk [options] -f <scriptfile> [-v var=value]... <file>...
```

|选项 | 说明 |
|--- |--- |
|-F FS | 指定输入分隔符，可以是字符串或正则表达式 |
|-v VAR=VALUE | 赋值给一个用户定义变量，并传递给awk | 
|-f SCRIPTFILE | 从脚本文件中读取awk命令 |
|-m[fr] VAL | 对val值设置限制 |
> -mf选项限制分配给val的最大块数目
> -mr选项限制分配给val的记录的最大数目
> 这两个功能是Bell实验室版awk的扩展功能，在标准awk中不适用



# awk脚本
## 基本结构
`awk 'BEGIN{ commands } pattern{ commands } END{ commands }'`


## 工作原理
1. 执行BEGIN{ commands }语句块中的语句
2. 从文件或标准输入(stdin)逐行读取数据，执行pattern{ commands }语句块，直到输入流末尾
3. 执行END{ commands }语句块中的语句

BEGIN语句块是一个可选的语句块，比如变量初始化、打印输出表格的表头等语句通常可以写在BEGIN语句块中。 
END语句块也是一个可选的语句块，比如打印所有行的分析结果这类信息汇总都是在END语句块中完成
pattern语句块中的通用命令是最重要的部分，它也是可选的。
> 如果没有提供pattern语句块，则默认执行{ print }，即打印每一个读取到的行，awk读取的每一行都会执行该语句块


## 模式和操作
awk脚本是由模式和操作组成的

### 模式
模式（PATTERN）可以是以下任意一个： 
- /正则表达式/：使用通配符的扩展集
- 关系表达式：使用运算符进行操作，可以是字符串或数字的比较测试。 
- 模式匹配表达式：用运算符~（匹配）和 ~!（不匹配）
- BEGIN语句块、PATTERN语句块、END语句块

### 操作
操作由一个或多个命令、函数、表达式组成，之间由换行符或分号隔开，并位于大括号内
- 变量或数组赋值 
- 输出命令 
- 内置函数 
- 控制流语句


## 内置变量（预定义变量）
***注意：*** [A][N][P][G]前缀表示第一个能够支持该变量的工具
> [A]=awk、[N]=nawk、[P]=POSIXawk、[G]=gawk，区别参见[这里][2]

|变量 | 说明 |
|--- |--- |
|$0 | 执行过程中当前行的文本内容 |
|$n | 当前记录的第n个字段 |
|[N] ARGC | 命令行参数的个数 |
|[N] ARGV | 包含命令行参数的数组 |
|[G] ARGIND | 命令行中当前文件的位置（从0开始算）| 
|[G] CONVFMT | 数字转换格式（默认值为%.6g）|
|[P] ENVIRON | 环境变量相关的数组 |
|[N] ERRNO | 最后一个系统错误的描述 |
|[G] FIELDWIDTHS | 字段宽度列表（用空格键分隔）|
|[A] FILENAME | 当前输入文件的名称 |
|[A] FS | 输入字段分隔符（默认是任何空白符）|
|[A] RS | 输入记录分隔符（默认是一个换行符） |
|[G] IGNORECASE | 如果为真，则进行忽略大小写的匹配 |
|[A] NF | 表示字段数，在执行过程中对应于当前的字段号 | 
|[A] NR | 表示记录数，在执行过程中对应于当前的行号 | 
|[P] FNR | 同NR，但相对于当前文件 |
|[A] OFMT | 数字的输出格式（默认值是%.6g）|
|[A] OFS | 输出字段分隔符（默认值是一个空格）|
|[A] ORS | 输出记录分隔符（默认值是一个换行符）|
|[N] RSTART | 由match函数所匹配的字符串的第一个位置 | 
|[N] RLENGTH | 由match函数所匹配的字符串的长度 |
|[N] SUBSEP | 数组下标分隔符（默认值是34）|
> ARGC -> argument count |  ARGV -> argument vector  | FMT -> format | ENVIRON -> environment | F -> field | R -> record | O -> output


<br/>

---

# 参考

[awk命令][1]  
[awk、nawk、mawk、gawk的简答介绍][2]

[1]: http://man.linuxde.net/awk
[2]: http://blog.csdn.net/u013152895/article/details/46288389
