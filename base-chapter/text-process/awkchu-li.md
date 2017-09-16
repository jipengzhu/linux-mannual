# awk
awk是一种编程语言，用于在linux/unix下对文本和数据进行处理。
- 数据可以来自标准输入(stdin)、一个或多个文件
- 支持用户自定义函数以及动态正则表达式等先进功能
- 有很多内建的功能，比如数组、函数等，和c语言类似



# awk脚本
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



# awk模式和操作
