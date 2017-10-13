# cat
输出文件的内容，如果不指定，则输出标准输入的内容

格式如下
```
cat [选项] [文件...]
```

选项如下

|选项 | 说明 |
|--- |--- |
|-A, --show-all | 等价于 -vET |
|-b, --number-nonblank | 对非空输出行编号 |
|-e | 等价于 -vE |
|-E, --show-ends | 在每行结束处显示$ |
|-n, --number | 对输出的所有行编号 |
|-s, --squeeze-blank | 合并两行以上的空白行为一行 |
|-t | 与 -vT 等价
|-T, --show-tabs | 将跳格字符显示为 ^I |
|-u | (被忽略) |
|-v, --show-nonprinting | 使用 ^ 和 M- 引用，除了 LFD 和 TAB 之外 |



# tac
tac命令用于将文件已行为单位的反序输出，即第一行最后显示，最后一行先显示

格式如下
```
tac [选项] [文件...]
```



# nl
计算文件中行号并和内容一起输出，行号的显示比`cat -n`更丰富

格式如下
```
nl [选项] [文件...]
```

选项如下

|选项 | 说明 |
|--- |--- |
|-b a | 表示不论是否为空行，也同样列出行号(类似 cat -n) |
|-b t | 如果有空行，空的那一行不要列出行号(默认值) |
|-n ln | 行号在萤幕的最左方显示；
|-n rn | 行号在自己栏位的最右方显示，且不加 0 |
|-n rz | 行号在自己栏位的最右方显示，且加 0 |
|-w | 行号栏位的占用的位数 |
|-p | 在逻辑定界符处不重新开始计算 |



# more
按页显示文件内容

格式如下
```
more [选项] <文件...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|+n | 从笫n行开始显示 |
|-n | 定义屏幕大小为n行 |
|+/PATTERN | 在每个档案显示前搜寻该模式（pattern），然后从该字串前两行之后开始显示 |
|-c | 从顶部清屏，然后显示 |
|-d | 提示“Press space to continue，’q’ to quit（按空格键继续，按q键退出）”，禁用响铃功能 |
|-l | 忽略Ctrl+l（换页）字符 |
|-p | 通过清除窗口而不是滚屏来对文件进行换页，与-c选项相似 |
|-s | 把连续的多个空行显示为一行 |
|-u | 把文件内容中的下画线去掉 |

操作如下（Ctrl代表Control）

|选项 | 说明 |
|--- |--- |
|h &#124; ? | 查看使用帮助 |
|Enter | 向下n行，需要定义，默认为1行 |
|Space | 向下滚动一屏 |
|Ctrl + d | 向下滚动半屏 |
|Ctrl + f | 向下滚动一屏 |
|Ctrl + b | 向上滚动一屏 |
|= | 输出当前行的行号 |
|:f | 输出文件名和当前行的行号 |
|V | 调用编辑器，默认为vi |
|!COMMAND | 调用Shell，并执行命令 |
|q | 退出more |



# less
按页显示文件内容，比more更强大

格式如下
```
less [选项] <命令>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-b | 缓冲区大小 设置缓冲区的大小 |
|-c | 从顶部清屏，然后显示 |
|-e | 当文件显示结束后，自动离开 |
|-f | 强迫打开特殊文件，例如外围设备代号、目录和二进制文件 |
|-g | 只标识最后搜索的关键词 |
|-i | 忽略搜索时的大小写 |
|-m | 显示类似more命令的百分比 |
|-N | 显示每行的行号 |
|-o FILENAME | 将less 输出的内容在指定文件中保存起来 |
|-Q | 不使用警告音 |
|-s | 显示连续空行为一行 |
|-S | 行过长时间将超出部分舍弃 |
|-x n | 将“tab”键显示为规定的数字空格 |

操作如下（Ctrl代表Control）

|选项 | 说明 |
|--- |--- |
|/STRING | 向下搜索“字符串” |
|?STRING | 向上搜索“字符串” |
|n | 下一个搜索（方向与 / 或 ? 有关）|
|N | 上一个搜索（方向与 / 或 ? 有关）| 
|f | 向下滚动一页 |
|b | 向上滚动一页 |
|d | 向下滚动半页 |
|u | 向上滚动半页 |
|e | 向下滚动一行 |
|y | 向上滚动一行 |
|Enter | 向下滚动一行 |
|Space | 向下滚动一页 |
|[pagedown] | 向下滚动一页 |
|[pageup] | 向上滚动一页 |
|h | 显示帮助界面 |
|q | 退出less命令 |
> f -> forward | b -> backward | d -> down | u-> up



# head 
查看文件的开头部分

格式如下
```
head [选项] <文件...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-c, --bytes=[-]K | 每个文件显示K字节，如果K前有短横杠，则从末尾开始 |
|-n, --lines=[-]K | 每个文件显示K行，如果K前有短横杠，则从末尾开始 |
|-q, --quiet, --silent | 隐藏文件名 |
|-v, --verbose | 显示文件名 |



# tail
查看文件的结尾部分

格式如下
```
tail [选项] <文件...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-c, --bytes=[+]K | 每个文件显示K字节，如果K前有加号，则从开头开始 |
|-n, --lines=[+]K | 每个文件显示K行，如果K前有加号，则从开头开始 |
|-q, --quiet, --silent | 隐藏文件名 |
|-v, --verbose | 显示文件名 |
|-f | 监听并输出文件变化的部分 |
|-F | 和-f --retry 一样的效果|
|--retry | 当文件切割后，重新打开文件 |
|-s, --sleep-interval=N | 文件的监听频率 |



# diff
比较文件之间的差异，格式的说明参照[读懂diff][8]

格式如下
```
diff [选项] <文件> <文件>
```

选项如下

|选项 | 说明 |
|--- |--- |
|- |指定要显示多少行文本，此参数必须与-c或-u参数一并使用 |
|-a, --text |diff预设只会逐行比较文本文件 |
|-b, --ignore-space-change | 不检查空格字符的不同 |
|-B, --ignore-blank-lines | 不检查空白行 |
|-c | 显示全部内文，并标出不同之处 |
|-C, --context | 与执行"- -c"选项相同 |
|-d, --minimal | 使用不同的演算法，以较小的单位来做比较 |
|-D, ifdef |　此参数的输出格式可用于前置处理器巨集 |
|-e, --ed |　此参数的输出格式可用于ed的script文件 |
|-f, -forward-ed | 输出的格式类似ed的script文件，但按照原来文件的顺序来显示不同处 |
|-H, --speed-large-files | 比较大文件时，可加快速度 |
|-l, --ignore-matching-lines | 若两个文件在某几行有所不同，而这几行同时都包含了选项中指定的字符或字符串，则不显示这两个文件的差异 |
|-i, --ignore-case | 不检查大小写的不同 |
|-l, --paginate |　将结果交由pr程序来分页 |
|-n, --rcs | 将比较结果以RCS的格式来显示 |
|-N, --new-file |　在比较目录时，若文件A仅出现在某个目录中，预设会显示：Only in目录：文件A若使用-N参数，则diff会将文件A与一个空白的文件比较 |
|-p | 若比较的文件为C语言的程序码文件时，显示差异所在的函数名称 |
|-P, --unidirectional-new-file |　与-N类似，但只有当第二个目录包含了一个第一个目录所没有的文件时，才会将这个文件与空白的文件做比较 |
|-q, --brief | 仅显示有无差异，不显示详细的信息 |
|-r, --recursive |　比较子目录中的文件 |
|-s, --report-identical-files |　若没有发现任何差异，仍然显示信息。
|-S, --starting-file |　在比较目录时从指定的文件开始比较 |
|-t, -expand-tabs |　在输出时将tab字符展开 |
|-T, --initial-tab |　在每行前面加上tab字符以便对齐 |
|-u, -U, --unified |　以合并的方式来显示文件内容的不同 |
|-v, --version |　显示版本信息 |
|-w, --ignore-all-space | 忽略全部的空格字符 |
|-W, --width |　在使用-y参数时，指定栏宽 |
|-x, --exclude |　排除指定的文件或目录 |
|-X, --exclude-from | 排除文件中指定的文件和目录 |
|-y, --side-by-side |　以并列的方式显示文件的异同之处 |
|--help |　显示帮助 |
|--left-column |　在使用-y参数时，若两个文件某一行内容相同，则仅在左侧的栏位显示该行内容 |
|--suppress-common-lines |　在使用-y参数时，仅显示不同之处 |


<br/>

---

# 参考

[每天一个linux命令 cat 命令][1]    
[每天一个linux命令 nl命令][2]    
[每天一个linux命令 more命令][3]    
[每天一个linux命令 less 命令][4]  
[每天一个linux命令 head 命令][5]  
[每天一个linux命令 tail 命令][6]  
[每天一个linux命令 diff 命令][7]  
[读懂diff][8]  
[What is the difference between "tail -f" and "tail -F"][9]  

[1]: http://www.cnblogs.com/peida/archive/2012/10/30/2746968.html
[2]: http://www.cnblogs.com/peida/archive/2012/11/01/2749048.html
[3]: http://www.cnblogs.com/peida/archive/2012/11/02/2750588.html
[4]: http://www.cnblogs.com/peida/archive/2012/11/05/2754477.html
[5]: http://www.cnblogs.com/peida/archive/2012/11/06/2756278.html
[6]: http://www.cnblogs.com/peida/archive/2012/11/07/2758084.html
[7]: http://www.cnblogs.com/peida/archive/2012/12/12/2814048.html
[8]: http://www.ruanyifeng.com/blog/2012/08/how_to_read_diff.html
[9]: https://unix.stackexchange.com/questions/291932/what-is-the-difference-between-tail-f-and-tail-f