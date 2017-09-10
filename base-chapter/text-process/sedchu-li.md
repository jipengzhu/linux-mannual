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
|-n, --quiet, ——silent | 仅显示script处理的结果 |
|-r, --regexp-extended | 使用扩展的正则表达式(ERE) |
|-h, --help | 显示帮助 |
|-V, --version | 显示版本信息 |


# sed脚本 
格式如下，其中范围可以通过正则表达式来匹配确定

```
[RANGE]<sed命令>/PATTERN/PATTERN/<sed标记>
[PATTERN/]<sed命令>/PATTERN/PATTERN/<sed标记>
[PATTERN, PATTERN/]<sed命令>/PATTERN/PATTERN/<sed标记>
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

# sed详解
## 追加（行下）a\命令 
将 `this is a test line` 追加到以test开头的行后面  
`sed '/^test/a\this is a test line' test.conf` 

在 test.conf 文件第2行之后插入 `this is a test line` 
`sed -i '2a\this is a test line' test.conf `

## 插入（行上）：i\命令 
将 this is a test line 追加到以test开头的行前面
`sed '/^test/i\this is a test line' test.conf`
 
在test.conf文件第2行之前插入this is a test line： 
`sed -i '2i\this is a test line' test.conf`

## 替换（行内）：c\命令 
将 test开头的行整行替换为 `this is a test line` 
`sed '/^test/c\this is a test line' test.conf`
