# wc
wc可以对文件进行统计

```
wc [选项] [文件]...
```

|选项 | 说明 |
|--- |--- |
|-c, --bytes | 显示字节数|
|-m, --chars | 显示字符数 |
|-l, --lines | 显示行数 |
|-w, --words | 显示单词数 |
|-L, --max-line-length | 显示最长行的长度 |



# sort 
sort可以对文本（来自文件或管道）进行排序

```
sort [选项] [文件]...
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
uniq命令用于报告或忽略文件中的***相邻重复行***，一般与sort命令结合使用

```
uniq [选项] [文件]...
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



# tr



# split



# truncate




# tee