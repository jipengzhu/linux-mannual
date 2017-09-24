# grep 
主要用来提取文件或标准输入中的满足条件的行，默认使用BRE

```
grep [OPTIONS] PATTERN [FILE...]
grep [OPTIONS] [-e PATTERN | -f FILE] [FILE...]
```

|选项 | 含义 |
|--- |--- |
|-c | 只输出匹配行的数量 |
|-i | 搜索时忽略大小写 |
|-h, --no-filename | 查询多文件时***不显示***文件名 |
|-H,  --with-filename | 查询多文件时***显示***文件名 |
|-l, --file-with-matches  | 只列出***符合***匹配的文件名，而不列出具体的匹配行 |
|-L, --files-without-match  | 只列出***不符合***匹配的文件名，而不列出具体的匹配行 |
|-n, --line-number  | 列出所有的匹配行，并显示行号 |
|-s, --no-messages | 不显示文件不存在或无匹配文本的错误信息 |
|-v, --revert-match | 显示不匹配文本的所有行 |
|-w, --word-regexp  | 匹配整词 |
|-x, --line-regexp  | 匹配整行 |
|-r, --recursive | 当指定要查找的是目录而非文件时，必须使用这项参数 |
|-q, --quiet， --silent | 禁止输出任何结果，以退出状态表示搜索是否成功 |
|-b, --byte-offset  | 打印匹配行距文件头部的偏移量，以字节为单位 |
|-o | 与-b选项结合使用，只显示搜索文字 |
|-E | 使用支持扩展的正则表达式(ERE) |
|-F | 不支持正则表达式，按照字符串的字面意思进行匹配 |

BRE和ERE的知识请参考***前言篇中的模糊匹配章节***



# egrep
`egrep` 执行效果与 `grep -E` 相似



# fgrep
`fgrep` 执行效果与 `grep -F` 相似



<br\>

---

# 参考

[grep命令][1]  
[Linux 的(cut,sed,awk,grep,sort)工具][2]  
[What is the difference between `grep`, `egrep`, and `fgrep`][3]  
[]

[1]: http://man.linuxde.net/grep
[2]: http://youbingchenyoubing.leanote.com/post/Linux-%E7%9A%84-cut-sed-awk-grep-sort-%E5%B7%A5%E5%85%B7
[3]: https://unix.stackexchange.com/questions/17949/what-is-the-difference-between-grep-egrep-and-fgrep