# sed
sed是一种流编辑器，默认使用BRE，主要用来
- 自动编辑一个或多个文件
- 简化对文件的反复操作
- 编写转换程序等

```
sed [OPTION]... {script-only-if-no-other-script} [input-file]...
```

|选项 | 说明 |
|--- |--- |
| -e SCRIPT, --expression=SCRIPT | 以指定的***script命令***来处理 |
| -f FILE, --file=FILE | 以指定的***script文件***来处理 |
|-i | 将处理后的结果替换掉原来的文件 |
|-n, --quiet, ——silent | 仅显示script处理的结果 |
|-r, --regexp-extended | 使用扩展的正则表达式(ERE) |
|-h, --help | 显示帮助 |
|-V, --version | 显示版本信息 |



# sed脚本 
格式如下，其中范围可以通过正则表达式来匹配确定

```
[RANGE]<sed命令>/PATTERN/PATTERN/<sed标记>
[/PATTERN/]<sed命令>/PATTERN/PATTERN/<sed标记>
[/PATTERN, PATTERN/]<sed命令>/PATTERN/PATTERN/<sed标记>
```

## sed命令
|命令 | 说明 |
|--- |--- |
|a\ | 在当前行***下面***插入文本（append） |
|i\ | 在当前行***上面***插入文本（insert） |
|c\ | 把匹配的行改为新的文本（change） | 
|d | 删除匹配的行（delete） |
|D | 删除匹配的第一行 |
|s | 替换匹配为指定字符串 |
|h | ***拷贝***匹配的内容到内存中的缓冲区 |
|H | ***追加***匹配的内容到内存中的缓冲区 |
|g | 获得内存缓冲区的内容，并***替换***匹配的文本 |
|G | 获得内存缓冲区的内容，并***追加到***匹配文本的后面 | 
|l | 列出不可打印字符的清单 |
|n | 读取下一个输入行，用下一个命令处理新的行 |
|N | 追加下一个输入行到匹配行后面 |
|p | 打印匹配的行 |
|P | 打印匹配的第一行(大写的p) |
|q | 退出sed |
|b LABLE | 跳到到脚本中带有标记的地方，不存在则到脚本的末尾 |
|r FILE | 从指定文件中读取行 |
|t LABLE | if分支 |
|T LABLE | 错误分支 |
|w FILE | 追加匹配内容到指定文件末尾 |
|W FILE | 追加匹配内容的第一行到指定文件末尾 |
|! | 表示后面的命令对所有没有被选定的行发生作用 |
|= | 打印当前行的号码 | 
|# | 把注释扩展到下一个换行符以前|


## sed标记
|标记 | 说明 |
|--- |--- |
|g | 替换一行内的所有匹配 | 
|p | 打印行 | 
|w | 把行写入一个文件 |
|x | 表示匹配的内容和缓冲区中的内容 |
|y | 表示把一个字符翻译为另外的字符（但是不用于正则表达式）|
|\1 | 子串匹配标记 |
|& | 已匹配字符串标记 |


## sed定界符
sed命令中字符 / 是定界分割符，也可以使用任意的定界符
```
sed 's:test:TEXT:g'
sed 's|test|TEXT|g' 
```
定界符出现在样式内部时，需要进行转义
```
sed 's/\/bin/\/usr\/local\/bin/g'
```


# sed示例
## 追加（行下）（a\）
将 `this is a test line` 追加到以test开头的行后面  
`sed '/^test/a\this is a test line' test.conf` 

在 test.conf 文件第2行之后插入 `this is a test line` 
`sed -i '2a\this is a test line' test.conf `


## 插入（行上）（i\）
将 this is a test line 追加到以test开头的行前面
`sed '/^test/i\this is a test line' test.conf`
 
在test.conf文件第2行之前插入this is a test line： 
`sed -i '2i\this is a test line' test.conf`


## 替换（整行）（c\）
将test开头的行整行替换为 `this is a test line` 
`sed '/^test/c\this is a test line' test.conf`

将第二行整行替换为 `this is a test line` 
`sed '2c\this is a test line' test.conf`


## 替换（部分）（s）
替换第一个test为tests
`sed 's/test/tests/' file`

替换所有的test为tests
`sed 's/test/tests/' file`

在匹配test和west之间的所有行的行末尾添加`ha ha`
`sed '/test/,/west/s/$/ha ha/' file`


## 删除（范围）（d）
删除所有的空白行
`sed '/^$/d' file`

删除文件的第2行
`sed '2d' file`

删除文件最后一行
`sed '$d' file`

删除文件的第2行到末尾的所有行
`sed '2,$d' file`

删除文件中所有test开头的行
`sed '/^test/'d file`


## 打印（范围）（p）
### 使用 `p` 命令
`sed '/test/{p;}' test.txt`

### 使用 `p` 标记
所有在模板test和check所确定的范围内的行都被打印
`sed -n '/test/,/check/p' file`

打印从第5行开始到第一个包含以test开始的行之间的所有行
`sed -n '5,/^test/p' file`

## 读入文件（r）
读取`testfile`的内容并显示在`filename`中与`test`匹配的 ***所有的*** 匹配行后面
`sed '/test/r testfile' filename`


## 写入文件（w）
将`filename`与`test`匹配的 ***所有的*** 匹配行都写到`testfile`文件中
`sed '/test/w testfile' filename`


## 下一个（n）
则移动到匹配test行的下一行，替换这一行的aa，变为bb，并打印该行，然后继续
`sed '/test/{ n; s/aa/bb/; }' file`


## 已匹配字符串
> & 对应于之前所匹配到的内容

正则表达式 \w\+ 匹配每一个单词，使用 [&] 替换它

```
[root@zhujipeng /]# echo this is a test line | sed 's/\w\+/[&]/g'
[this] [is] [a] [test] [line]
```

所有以127.0.0.1开头的行都会被替换成它自已加上空格和localhost
`sed 's/^127.0.0.1/& localhost/' file`


## 引用子串匹配
匹配给定样式的其中一部分
```
[root@zhujipeng /]# echo this is digit 7 | sed 's/digit \([0-9]\)/\1/'
this is 7
```


## 大小写转换
### s命令
小写转大写
`sed 's/\(test\)/\U\1\E/g' file`

大写转小写
`sed 's/\(test\)/\L\1\E/g' file`

### y命令
`abcde`中每个字符转变为对应的大写，不能使用`a-z`这种语法
`sed 'y/abcde/ABCDE/' file`

`ABCDE`中每个字符转变为对应的小写，不能使用`A-Z`这种语法
`sed 'y/ABCDE/abcde/' file`

## 奇偶行
奇数行
`sed -n 'p;n' test.txt`

偶数行
`sed -n 'n;p' test.txt` 


<br/>

---

# 参考

[sed命令][1]  
[Sed to replace lower case string between two strings to upper case][2]

[1]: http://man.linuxde.net/sed
[2]: https://stackoverflow.com/questions/22718518/sed-to-replace-lower-case-string-between-two-strings-to-upper-case