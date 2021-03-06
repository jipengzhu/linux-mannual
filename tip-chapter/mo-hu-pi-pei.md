# 模糊匹配
linux中有两种模糊匹配，很多命令都会用到
- glob： 用于对***文件名***的模糊匹配，如`ls`，`find`，`tar`等命令
- regex： 用于对***文件内容***的模糊匹配，如`grep`，`sed`，`awk`等命令


# glob匹配
- glob匹配是指参数为文件名时，可以使用通配符来进行模糊匹配
- 如果匹配，shell会将文件参数展开为多个参数
- 如果想要通配符表达字符原本的含义，需要用反斜杠（\）转义

|通配符 | 说明 |
|--- |--- |
|* | 任意长度的字符 |
|? | 任意的单个字符 |
|[] | 指定范围***内***的任意单个字符 |
|\[^] | 指定范围***外***的任意单个字符，范围里取反 |
|[0-9] | 所有的数字 |
|[a-z] | 所有的小写字母 |
|[A-Z] | 所有的大写字母 |
|[a-zA-Z] | 所有的字母 |
|[0-9a-zA-Z] | 所有的数字和字母 |

代表集合的POSIX通配符

|通配符 | 说明 |
|--- |--- |
|[:digit:] | 所有数字, 相当于0-9 |
|[:lower:] | 所有的小写字母 |
|[:upper:] | 所有的大写字母 |
|[:alpha:] | 所有的字母 |
|[:alnum:] | 相当于[0-9a-zA-Z] |
|[:space:] | 空白字符 |
|[:punct:] | 所有标点符号 |

> 如果[A-Z]匹配了小写字母，原因参考[这里][5]



# regex匹配
## POSIX正则表达式
POSIX定义了两种正则表达式语法
- 基本正则表达式（BRE）
- 扩展正则表达式（ERE）

大多数linux程序至少要符合BRE规范


## 支持情况
linux中不同的程序支持的正则也不同
- grep支持ERE，不过要使用-E选项
- sed只支持BRE的大部分
- awk则使用BRE

> sed只支持BRE的大部分，主要是因为sed要尽可能快的处理数据流


## BRE（basic regex expression）
BRE定义的语法符号

|符号 | 说明 |
|--- |--- |
|. | 匹配任意一个字符 |
|[] | 字符集匹配，匹配方括号中定义的字符集之一 |
|\[^] | 字符集否定匹配，匹配没有在方括号中定义的字符 |
|^ | 匹配字符串的开始位置 |
|$ | 匹配字符串的结束位置 |
|\\(\\) | 定义子表达式 |
|\n | 子表达式向前引用，n为1-9之间的数字 |
| * | 任意次匹配（零次或多次匹配）|
| \\{n\\} | 正好n次匹配 |
| \\{m,n\\} | 至少m次，至多n次匹配 |
| \\{m,\\} | 至少m次匹配 |
| \\{,n\\} | 至多n次匹配 |
> 子表达式向前引用，由于此功能已超出正则语义，需要在字符串中回溯，因此需要使用 NFA 算法进行匹配


# ERE（extended regex expression）
ERE 修改了 BRE 中的部分语法

1. ERE 取消了子表达式 "()" 和 次数匹配 "{m,n}" 语法符号的转义符
2. ERE 也取消了非正则语义的子表达式向前引用能力
3. ERE 增加了更多的匹配量词

新增的匹配量词

|符号 | 说明 |
|--- |--- |
|? | 最多一次匹配（零次或一次匹配）|
|+ | 至少一次匹配（一次或更多次匹配）|
|&#124; | 或运算，其左右操作数均可以为一个子表达式 |

 
## POSIX字符集
- BRE 和 ERE 共享同样的 POSIX 字符类定义
- 它们还支持字符类比较操作 "[. .]"和字符类等于操作 "[= =]" ，但很少被使用
- 大多数语言的正则都是从perl借鉴来的，和linux的正则很不一样

f / fr / wfr / bwfr 等工具默认使用 ERE 模式，同时支持以下 perl 风格的字符

|POSIX类 | perl类 | 描述 |
|--- |--- |--- |
|[:alpha:] | \a | 字母 |
|[:lower:] | \l | 小写字母 |
|[:upper:] | \u | 大写字母 |
|[:digit:] | \d | 十进制数字 |
|[:xdigit:] | \x | 十六进制数字 |
|[:alnum:] |    | 字母和数字 |
|[:word:] | \w | 字母数字和下划线 |
|[:blank:] |    | 空格和制表符 |
|[:space:] | \s | 所有空白符（空格，制表符，换行，回车，垂直制表符，换页）|
|[:cntrl:] |    | 不可打印的控制字符（退格、删除、警铃...）|
|[:graph:] |    | 可打印的非空白字符 |
|[:print:] | \p | 可打印字符 |
|[:punct:] |    | 标点符号 |
> blank 和 space 的区别参考[这里][8]

此外，还有以下特殊字符类

|perl类 | POSIX类 | 描述 |
|--- |--- |--- |
|\o | [0-7] | 八进制数字 |
|\O | \[^0-7] | 非八进制数字 |
|\w | [[:alnum:]_] | 字母数字下划线构成字符 |
|\W | \[^[:alnum:]_] | 非字母数字下划线构成字符 |
|\a | [:alpha:] | 字母 |
|\A | \[^[:alpha:]] | 非字母 |
|\l | [:lower:] | 小写字母 |
|\L | \[^[:lower:]] | 非小写字母 |
|\u | [:upper:] | 大写字母 |
|\U | \[^[:upper:]] | 非大写字母 |
|\s | [:space:] | 空格符 |
|\S | \[^[:space:]] | 非空格符 |
|\d | [:digit:] | 非数字 |
|\D | \[^[:digit:]] | 非数字 |
|\x | [:xdigit:] | 十六进制数字 |
|\X | \[^[:xdigit:]] | 非十六进制数字 |
|\p | [:print:] | 可打印字符 |
|\P | \[^[:print:]] | 非可打印字符 |

还可以使用以下特殊字符换码序列

|换码序列 | 描述 |
|--- |--- |
|\r | 回车 |
|\n | 换行 |
|\b | 退格 |
|\t | 制表符 |
|\v | 垂直制表符 |
|\' | 单引号 |
|\" | 双引号 |
			
## ARE（advanced regex expression）
除了 POSIX BRE 和 ERE 之外，libutilitis 还支持与TCL 8.2兼容的高级正则表达式语法（ARE），通过为 stRegEx 参数增加前缀 "***:" 就可以开启 ARE 模式，这个前缀覆盖 bExtended 选项

## ARE对ERE的扩展
基本上讲，ARE 是 ERE 的超集，和编程语言中的正则非常接近，它在 ERE 的基础上进行了如下几项扩展

### 支持"懒惰匹配"（也叫"非贪婪匹配"或"最短匹配"）
在 '?', '*', '+' 或 '{m,n}'后追加 '?' 符号就可以启用最短匹配，使得该正则表达式子句在满足条件的前提下匹配尽可能少的字符（默认是匹配尽可能多的字符）。
> 例如：将 "a.*b" 作用于 "abab"时，将匹配整个串（"abab"），若使用 "a.*?b"，则将只匹配前两个字符（"ab"）

### 支持子表达式的向前引用匹配
在 stRegEx 中，可以使用 '\n' 向前引用曾经定义的子表达式。
> 例如："(a.*)\1" 可匹配 "abcabc" 等

### 支持无名子表达式
使用 "(?:表达式)" 的方式创建一个无名表达式， 
> 无名表达式不占用一个 '\n' 匹配。

### 向前预判
要命中匹配，必须向前满足指定条件，向前预判分为肯定预判和否定预判两种。

- 肯定预判的语法为："(?=表达式)"
> 例如："bai.*(?=yang)" 匹配 "bai yang"的前四个字符（"bai "），但在匹配时保证字符串在 "bai.*" 后必须包含 "yang".
- 否定判断的语法为："(?!表达式)"
> 例如："bai.*(?!yang)" 匹配 "bai shan" 的前四个字符（"bai "），但在匹配是保证字符串在 "bai.*" 后不出现 "yang"。

### 支持模式切换前缀
在 "\*\*\*:" 之后可以紧跟形如 "(?模式串)" 样式的模式串，模式串影响其后表达式的语义和行为。

模式串可以是以下字符的组合

|字符 | 描述 |
|--- |--- |
|b | 切换至 POSIX BRE 模式，覆盖 bExtended 选项 |
|e | 切换至 POSIX ERE 模式，覆盖 bExtended 选项 |
|q | 切换至普通文本字面匹配模式，"***=" 前缀是其快捷表示 |
|c | 执行大小写敏感的匹配，覆盖 bNoCase 选项 |
|i | 执行忽略大小写的匹配，覆盖 bNoCase 选项 |
|n | 开启行敏感的匹配：'^' 和 '$' 匹配行首和行尾；'.' 和否定集     （'[^...]'）不匹配换行符。此功能等同于 'pw' 模式串。覆盖 bNewLine 选项 |
|m | 等同于 'n' |
|p | '^' 和 '$' 只匹配整个字符串的首尾，不匹配行；'.' 和否定集不匹配换行符。覆盖 bNewLine 选项 |
|w | '^' 和 '$' 匹配行首和行尾；'.' 和否定集匹配换行符。覆盖 bNewLine 选项 |
|s | '^' 和 '$' 只匹配整个字符串的首尾，不匹配行；'.' 和否定集匹配换行符。覆盖 bNewLine 选项。ARE 状态下默认使用此模式 |
|x | 开启扩展模式：在扩展模式中，将忽略表达式中的空白符和注释符 '#' 后的内容    |
|t | 关闭扩展模式，不忽略空白符和注释符后的内容。ARE 状态下默认使用此模式 |

## Perl风格字符类换码序列
> 由于在Markdown中使用实体符号表示尖括号时引入了多余的空格
> ***所以请忽略尖括号左右多余的空格***

|perl类 | 等效POSIX表达式 | 描述 |
|--- |--- |--- |
|\a | - | 响铃字符 |
|\A | - | 不论当前模式如何，仅匹配整个串的最开头 |
|\b | - | 退格字符 ('\x08') |
|\B | - | 转义字符本身 ('\\') |
|\cX | - | 控制符-X (= X & 037) |
|\d | [:digit:] | 10进制数字 ('0' - '9') |
|\D | \[^[:digit:]] | 非10进制数字 |
|\e | - | 退出符 ('\x1B') |
|\f | - | 换页符 ('\x0C') |
|\m | [:&lt; :] | 单词开始位置 |
|\M | [:>:] | 单词结束位置 |
|\n | - | 换行符 ('\x0A') |
|\r | - | 回车符 ('\x0D') |
|\s | [:space:] | 空白符 |
|\S | \[^[:space:]] | 非空白符 |
|\t | - | 制表符 ('\x09') |
|\uX | - | 16 位 UNICODE 字符 (X∈[0000 .. FFFF]) |
|\UX | - | 32 位 UNICODE 字符 (X∈[00000000 .. FFFFFFFF]) |
|\v | - | 纵向制表符 ('\x0B') |
|\w | [[:alnum:]_] | 字母数字和下划线组成单词 |
|\W | \[^[:alnum:]_] | 非字母数字和下划线组成单词 |
|\xX | - | 8位字符 (X∈[00 .. FF]) |
|\y | - | 单词边界（\m 或 \M）|
|\Y | - | 非单词边界 |
|\Z | - | 不论当前模式如何，仅匹配整个串的最尾部 |
|\0 | - | NULL，空字符 |
|\X | - | 子表达式向前引用 (X∈[1 .. 9]) |
|\XX | - | 子表达式向前引用或 8 进制表示的字符 |
|\XXX | - | 子表达式向前引用或 8 进制表示的字符 |



# glob和regex的区别
## 针对对象不同
glob针对***文件名***，regex针对***文件内容***

## 通配符有差异
- 点号（.）在glob中就是字符点号，在regex中表示任意字符
- 星号（*）在glob中表示任意长度的字符，在regex中表示匹配零到多次
- 问号（?）在glob中表示一个字符，在regex中表示匹配最多一次


# 通配符和shell展开
单引号和双引号对模糊匹配中的*和?有影响，本质是[shell展开][7]造成的

```
[root@zhujipeng test-glob]# touch test.txt
[root@zhujipeng test-glob]# touch test
[root@zhujipeng test-glob]# ls test*
test  test.txt
[root@zhujipeng test-glob]# ls 'test*'
ls: cannot access test*: No such file or directory
[root@zhujipeng test-glob]# find . -name test*
find: paths must precede expression: test.txt
Usage: find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec] [path...] [expression]
[root@zhujipeng test-glob]# find . -name 'test*'
./test.txt
./test
[root@zhujipeng test-glob]# find . -name 'test.*'
./test.txt
```

<br/>

---

# 参考

[linux中的通配符和正则表达式][1]   
[Linux中通配符、正则表达式和扩展正则表达式][2]  
[Linux Shell 通配符、元字符、转义符][3]     
[Linux正则表达式][4]  
[Why does [A-Z] match lowercase letters in bash][5]    
[BRE与ERE的差异][6]  
[shell 基本特性之~ shell展开详解][7]  
[What's the difference between [:space:] and [:blank:]?
][8]

[1]: http://evanlinux.blog.51cto.com/7247558/1308363
[2]: http://xzb2015.blog.51cto.com/8796643/1598715
[3]: http://www.cnblogs.com/chengmo/archive/2010/10/17/1853344.html
[4]: http://wiki.jikexueyuan.com/project/linux-command/chap20.html
[5]: https://unix.stackexchange.com/questions/227070/why-does-a-z-match-lowercase-letters-in-bash
[6]: http://blog.chinaunix.net/uid-23045379-id-2562051.html
[7]: http://www.jianshu.com/p/403f3554e2c1
[8]: https://stackoverflow.com/questions/15767863/whats-the-difference-between-space-and-blank