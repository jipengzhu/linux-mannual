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
|:set nu | 显示行号 |
|:set nonu | 隐藏行号 |
|:set autoident | 开启自动缩进 |
|:set noautoident | 关闭自动缩进 |
|:set cindent | 开启c风格的缩进 |
|:set nocindent | 关闭c风格的缩进 |
|:set paste | 开启粘贴模式 |
|:set nopaste | 开启粘贴模式 |


# vim帮助
命令帮助的格式为：
- 第一行指明怎么使用那个命令
- 然后是缩进的一段解释这个命令的作用
- 然后是进一步的信息

|快捷键 | 功能 |
|--- |--- |
|F1 | 查看帮助 |
|:h(elp) | 查看帮助 |
|:help command | 查看指定命令的帮助 |
|:help user-manual | 打开用户手册 |
|:helptags somepath | 为somepath中的文档生成索引 |
|:helpgrep | 搜索整个帮助文档，匹配的列表显示在quickfix窗口 |
|:ver | 显示版本信息 |


# vim技巧
- [Vim 中读写特殊字符][4]
- [VIM中执行Shell命令（炫酷）][5]
- [强悍的 vim —— 处理大小写转换][6]
- [vim tab设置为4个空格][7]
- [VIM 文件编码识别与乱码处理][8]
- [Vim的分屏功能][10]
- [在 Vim 中优雅地查找和替换][12]
- [Vim查找替换及正则表达式的使用][13]
- [vim清空文件所有内容][14]
- [轻快的VIM（三）][19]
- [无插件Vim编程技巧][20]
- [在Linux下使用vim配合xxd查看并编辑二进制文件][22]
- [vim编辑器---批量注释与反注释][24]
- [Vimdiff 使用][25]


# vim问题
- [vim粘贴注释–解决方法][2]
- [vim 退格键（backspace）不能用][3]
- [vim fileencoding和encoding][9]
- [vi/vim使用入门: vimrc在哪儿?][11]
- [YouCompleteMe中Ctrl-P/Ctrl-N失效][21]


# vim搭建IDE
- [Mac下打造vim+Python开发环境][15]  
- [VIM的自动补全][16]  
- [如何用Vim搭建IDE？][17]  
- [一步一步带你安装史上最难安装的 vim 插件 —— YouCompleteMe][18] 
- [像 IDE 一样使用 vim][23]


<br/>

---

# 参考

[Vim使用笔记][1]  
[vim粘贴注释–解决方法][2]  
[vim 退格键（backspace）不能用][3]  
[Vim 中读写特殊字符][4]  
[VIM中执行Shell命令（炫酷）][5]  
[强悍的 vim —— 处理大小写转换][6]  
[vim tab设置为4个空格][7]  
[VIM 文件编码识别与乱码处理][8]
[Rationale of fileencoding and encoding in vim or elsewhere][9]  
[Vim的分屏功能][10]  
[vi/vim使用入门: vimrc在哪儿?][11]  
[在 Vim 中优雅地查找和替换][12]  
[Vim查找替换及正则表达式的使用][13] 
[vim清空文件所有内容][14]  
[Mac下打造vim+Python开发环境][15]    
[VIM的自动补全][16]    
[如何用Vim搭建IDE？][17]   
[一步一步带你安装史上最难安装的 vim 插件 —— YouCompleteMe][18]   
[轻快的VIM（三）][19]  
[无插件Vim编程技巧][20]  
[Ctrl-P/Ctrl-N broken; whitelist filetypes for YCM][21]  
[在Linux下使用vim配合xxd查看并编辑二进制文件][22]  
[像 IDE 一样使用 vim][23]  
[vim编辑器---批量注释与反注释][24]  
[Vimdiff 使用][25]

[1]: http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html
[2]: http://www.chenglin.name/linux/blog-linux/595.html
[3]: https://my.oschina.net/zhangdapeng89/blog/56593
[4]: http://harttle.com/2016/08/22/vim-special-characters.html
[5]: http://blog.csdn.net/bnxf00000/article/details/46618465
[6]: http://blog.csdn.net/lanchunhui/article/details/51542211
[7]: http://blog.csdn.net/jiang1013nan/article/details/6298727
[8]: http://edyfox.codecarver.org/html/vim_fileencodings_detection.html
[9]: https://stackoverflow.com/questions/22044869/rationale-of-fileencoding-and-encoding-in-vim-or-elsewhere
[10]: https://coolshell.cn/articles/1679.html
[11]: http://easwy.com/blog/archives/where-is-vimrc/
[12]: http://harttle.com/2016/08/08/vim-search-in-file.html
[13]: https://tanqisen.github.io/blog/2013/01/13/vim-search-replace-regex/
[14]: http://blog.sina.com.cn/s/blog_9f1118490102vdai.html
[15]: http://zcheng.ren/2016/12/28/VimAndZshInMacTerminal/
[16]: http://www.itye.org/archives/3227
[17]: http://harttle.com/2015/11/04/vim-ide.html
[18]: http://www.jianshu.com/p/d908ce81017a
[19]: http://www.cnblogs.com/nerxious/archive/2012/12/21/2828520.html
[20]: https://coolshell.cn/articles/11312.html
[21]: https://github.com/Valloric/YouCompleteMe/issues/178
[22]: http://www.cnblogs.com/killkill/archive/2010/06/23/1763785.html
[23]: https://github.com/yangyangwithgnu/use_vim_as_ide
[24]: http://blog.csdn.net/xiajun07061225/article/details/8488210
[25]: https://www.ibm.com/developerworks/cn/linux/l-vimdiff/index.html