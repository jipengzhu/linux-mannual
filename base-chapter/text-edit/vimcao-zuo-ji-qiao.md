# 一些实用的快捷键
|快捷键 | 功能 |
|--- |--- |
|K | 打开光标所在词的manpage |
|g + C-G | 统计全文或统计部分的字数 |

# 命令行模式下的快捷键
|快捷键 | 功能 |
|--- |--- |
|上下方向键 | 上一条或者下一条命令，如果已经输入了部分命令，则找匹配的命令 |
|左右方向键 | 左/右移一个字符 |
|C-b | 移动到命令行***开头*** |
|C-e | 移动到命令行***末尾 ***|
|C-h | 向前删除一个***字符***，等同于Backspace|
|C-w | 向前删除一个***单词*** |
|C-u | 删除光标之前的字符 |
|Shift-Left | ***左移***一个单词 |
|Shift-Right | ***右移***一个单词 |
|@ | 重复上一次的命令|


# 执行外部命令
|快捷键 | 功能 |
|--- |--- |
|:! cmd | 执行外部命令 |
|:!! | 执行上一次的外部命令 |
|:sh | 调用shell，用exit返回vim |
|:r !cmd | 将命令的返回结果插入文件当前位置 |
|:m,nw !cmd |将文件的m行到n行之间的内容做为命令输入执行命令 |


# 其他有用的命令
|快捷键 | 功能 |
|--- |--- |
|:pwd | 显示vim的工作目录 |
|:cd path | 改变vim的工作目录 |
|:set autochdir | 让vim根据编辑的文件自动切换工作目录 |

# vim帮助
命令帮助的格式为：
- 第一行指明怎么使用那个命令
- 然后是缩进的一段解释这个命令的作用
- 然后是进一步的信息

|快捷键 | 功能 |
|--- |--- |
|F1 | 打开帮助 |
|:h(elp) | 打开帮助 |
|:help user-manual | 打开用户手册 |
|:helptags somepath | 为somepath中的文档生成索引 |
|:helpgrep | 搜索整个帮助文档，匹配的列表显示在quickfix窗口 |
|:ver | 显示版本信息 |


# vim技巧
## [Vim 中读写特殊字符][4]
## [VIM中执行Shell命令（炫酷）][5]
## [强悍的 vim —— 处理大小写转换][6]
## [vim tab设置为4个空格][7]
## [VIM 文件编码识别与乱码处理][8]
## [vim fileencoding和encoding][9]


# vim问题
## [vim粘贴注释–解决方法][2]
## [vim 退格键（backspace）不能用][3]



<br/>

---

# 参考

[Vim使用笔记][1]  
[vim粘贴注释–解决方法][2]  
[vim 退格键（backspace）不能用][3]  
[Vim 中读写特殊字符][4]  
[VIM中执行Shell命令（炫酷）][5]  
[强悍的 vim —— 处理大小写转换][6]  
[Rationale of fileencoding and encoding in vim or elsewhere][7]
[vim tab设置为4个空格][8]

[1]: http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html
[2]: http://www.chenglin.name/linux/blog-linux/595.html
[3]: https://my.oschina.net/zhangdapeng89/blog/56593
[4]: http://harttle.com/2016/08/22/vim-special-characters.html
[5]: http://blog.csdn.net/bnxf00000/article/details/46618465
[6]: http://blog.csdn.net/lanchunhui/article/details/51542211
[7]: http://blog.csdn.net/jiang1013nan/article/details/6298727
[8]: http://edyfox.codecarver.org/html/vim_fileencodings_detection.html
[9]: https://stackoverflow.com/questions/22044869/rationale-of-fileencoding-and-encoding-in-vim-or-elsewhere

