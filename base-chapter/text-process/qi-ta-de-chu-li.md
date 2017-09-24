# wc
对文件进行统计

```
wc [OPTION]... [FILE]...
```

|选项 | 说明 |
|--- |--- |
|-c, --bytes | 显示字节数|
|-m, --chars | 显示字符数 |
|-l, --lines | 显示行数 |
|-w, --words | 显示单词数 |
|-L, --max-line-length | 显示最长行的长度 |



# sort 
对文本（来自文件或管道）进行排序

```
sort [OPTION]... [FILE]...
```

|选项 | 说明 |
|--- |--- |
|-b, --ignore-leading-blanks | 忽略每行前面开始出的空格字符 |
|-c, --check, --check=diagnose-first | 检查文件是否已经按照顺序排序 | 
|-d, --dictionary-order | 排序时处理英文字母、数字及空格字符外，忽略其他的字符 | 
|-f, --ignore-case | 排序时将小写字母视为大写字母 |
|-i, --ignore-nonprinting | 排序时处理040至176之间的ASCII字符外，忽略其他的字符 |
|-m, --merge | 不排序，将排序好的文件进行合并 |
|-M, --month-sort | 将前面3个字母依照月份的缩写进行排序 |
|-n, --numeric-sort | 依照数值的大小排序 |
|-o, --output=FILE | 将排序后的结果存入指定的文件 |
|-r, --reverse | 以相反的顺序来排序 | 
|-t, --field-separator=SEP | 指定排序时所用的分隔字符 | 
|-u, --unique | 排序后去重 |
|+N-N | 以指定的列（N）范围来排序，范围由起始列（N）到结束列（N）的前一列 | 



# uniq
报告或忽略文件中的***相邻重复行***，一般与sort命令结合使用

```
uniq [OPTION]... [FILE]...
```

|选项 | 说明 |
|--- |--- |
|-c, --count | 在每列前面显示该行重复出现的次数 | 
|-d, --repeated | 只显示重复的行 | 
|-f, --skip-fields=N | 忽略比较指定的列 | 
|-i, --ignore-case | 比较时忽略大小写 |
|-s, --skip-chars=N | 忽略指定的前N个字符 | 
|-u, --unique | 只显示不重复的行 |
|-w, --check-chars=N | 只比较最多N个字符 |



# cut
显示行中的指定部分，删除文件中指定字段

```
cut [OPTION]... [FILE]...
```

|选项 | 说明 |
|--- |--- |
|-b, --bytes=LIST | 仅显示行中指定范围的字节 |
|-c, --characters=LIST | 仅显示行中指定范围的字符 |
|-d, --delimiter=DELIM | 指定字段的分隔符，默认为“TAB” |
|-f, --fields=LIST| 显示指定字段（数字）的内容 |
|-n | 与“-b”选项连用，不分割多字节字符 |
|--complement | 补足被选择的字节、字符或字段 |
|--output-delimiter=STRING | 指定输出内容的字段分割符 |
| --help  | 显示指令的帮助信息 |
|--version | 显示指令的版本信息 |



# tr
对来自标准输入的字符进行替换、压缩和删除

```
tr [OPTION]... SET1 [SET2]
```

|选项 | 说明 |
|--- |--- |
|-c, -C, --complement | 对字符集求补集 |
|-d, --delete | 删除所有属于字符集1的字符 |
|-s, --squeeze-repeats | 把连续重复的字符替换为一个字符 |
|-t, --truncate-set1 | 删除第一字符集较第二字符集多出的字符 |


大小写转化
> `tr 'A-Z' 'a-z'` 大写转小写  
> `tr 'a-z' 'A-Z'` 小写转大写

文件格式转换
>Mac -> UNIX：`tr "\r" "\n"<macfile > unixfile`
>UNIX -> Mac：`tr "\n" "\r"<unixfile > macfile`
>DOS -> UNIX：`tr -d "\r"<dosfile > unixfile`
>UNIX -> DOS：`awk '{ print $0"\r" }'<unixfile > dosfile`
>DOS -> MAC：`tr -d "\n"<dosfile > macfile`
>MAC -> DOS： Mac -> UNIX, UNIX -> DOS

空行多余的合并
> `tr -s "\n"`

显示PATH的路径
> `echo $PATH | tr ":" "\n"`

用问号显示不可打印字符
> `tr -c '[:cntrl:]' '[?]'`


# split
将一个大文件分割成很多个小文件

```
split [OPTION]... [INPUT [PREFIX]]
```

|选项 | 说明 |
|--- |--- |
|-b, --bytes=SIZE | 每一部分的大小，单位为 byte |
|-C, --line-bytes=SIZE | 单行的最大字节数 |
|-d, --numeric-suffixes[=FROM] | 使用数字作为后缀 |
|-l, --lines=NUMBER | 输出行数 |



# truncate
将文件缩减或扩展至指定大小

```
truncate [OPTION]... FILE...
```

|选项 | 说明 |
|--- |--- |
|-c, --no-create | 不创建文件 |
|-o, --io-blocks | 将SIZE 视为IO 块数而不使用字节数 |
|-r, --reference=RFILE | 使用此文件的大小 |
|-s, --size=SIZE | 使用指定大小 |
|--help	| 显示此帮助信息并退出 |
|--version | 显示版本信息并退出 |




# tee
将数据重定向到文件，并重定向数据的副本作为后续命令的标准输入


```
tee [OPTION]... [FILE]...
```

|选项 | 说明 |
|--- |--- |
|-a, --append |向文件中重定向时使用追加模式 |
|-i, --ignore-interrupts | 忽略中断（interrupt）信号 |



<br/>

---

# 参考

[wc命令][1]  
[sort命令][2]  
[uniq命令][3]   
[cut][4]  
[tr命令][5]  
[split命令][6]  
[truncate命令][7]  
[tee命令][8]   
[linux sort,uniq,cut,wc命令详解][9]  

[1]: http://man.linuxde.net/wc
[2]: http://man.linuxde.net/sort
[3]: http://man.linuxde.net/uniq
[4]: http://man.linuxde.net/cut
[5]: http://man.linuxde.net/tr
[6]: http://man.linuxde.net/split
[7]: http://linux.51yip.com/search/truncate
[8]: http://man.linuxde.net/tee
[9]: http://www.cnblogs.com/ggjucheng/archive/2013/01/13/2858385.html