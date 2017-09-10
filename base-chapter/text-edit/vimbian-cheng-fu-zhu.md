# 光标移动
|快捷键 | 功能 |
|--- |--- |
|gd | 跳转到***局部变量的定义处 |
|gD | 跳转到***全局变量***的定义处，从当前文件开头开始搜索 |
|g; | ***上一个***修改过的地方 |
|g, | ***下一个***修改过的地方 |
|[[ | 跳转到***上一个***函数块***开始***，需要有单独一行的{ |
|[] | 跳转到***上一个***函数块***结束***，需要有单独一行的} |
|]] | 跳转到***下一个***函数块***开始***，需要有单独一行的{ |
|][ | 跳转到***下一个***函数块***结束***，需要有单独一行的} |
|[{ | 跳转到***当前块开始***处 |
|]} | 跳转到***当前块结束***处 |
|[/ | 跳转到***当前注释块开始***处 |
|]/ | 跳转到***当前注释块结束***处 |
|% | 不仅能移动到匹配的(),{}或[]上，而且能在#if，#else， #endif之间跳跃|


# 修改、剪切、复制
|快捷键 | 功能 |
|--- |--- |
|ci', di', yi' | 修改、剪切或复制'之间的内容 |
|ca', da', ya' | 修改、剪切或复制'之间的内容，包含' |
|ci", di", yi" | 修改、剪切或复制"之间的内容 |
|ca", da", ya" | 修改、剪切或复制"之间的内容，包含" |
|ci(, di(, yi( | 修改、剪切或复制()之间的内容 |
|ca(, da(, ya( | 修改、剪切或复制()之间的内容，包含() |
|ci[, di[, yi[ | 修改、剪切或复制[]之间的内容 |
|ca[, da[, ya[ | 修改、剪切或复制[]之间的内容，包含[] |
|ci{, di{, yi{ | 修改、剪切或复制{}之间的内容 |
|ca{, da{, ya{ | 修改、剪切或复制{}之间的内容，包含{} |
|ci`<`, di`<`, yi`<`| 修改、剪切或复制<>之间的内容 |
|ca`<`, da`<`, ya`<` | 修改、剪切或复制<>之间的内容，包含<> |


# ctags
遍历源代码文件生成tags文件

> ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .

vim操作

|快捷键 | 功能 |
|--- |--- |
|:set tags=TAGS_PATH | 设置ctags文件的路径 |
|:tag xyz | 跳到xyz的定义处，或者在xyz处按（C-]），返回用（C-t）|
|:stag xyz | 用分割的窗口显示xyz的定义，或者在xyz处按（C-W + ]）|
|:ptag xyz | 在预览窗口中打开xyz的定义，或者在xyz处按（C-W + }）|
|:pclose | 关闭预览窗口（C-W + z）|
|:pedit abc.h | 在预览窗口中编辑abc.h |
|:psearch abc | 搜索当前文件和当前文件include的文件，显示包含abc的行 |

有时一个tag可能有多个匹配，会先跳转到第一个匹配处

|快捷键 | 功能 |
|--- |--- |
|:[n]tnext | 后面第n个匹配 |
|:[n]tprev | 前面第n个匹配 |
|:tfirst | 第一个匹配 |
|:tlast | 最后一个匹配 |
|:tselect TAG_NAME | 打开选择列表 |

tab键补齐，继续按tab键，会显示其他的

|快捷键 | 功能 |
|--- |--- |
|:tag xyz  | 用以xyz开头的tag名补全 |
|:tag /xyz | 用含有xyz的tag名补全 |


# cscope
提供交互式查询语言符号功能，如查询哪些地方使用某个变量或调用某个函数

> cscope -Rbq -f &lt; path/to/cscope.out &gt;

vim操作

|快捷键 | 功能 |
|--- |--- |
|:cs add CSCOPE_PATH WORK_DIR| 添加cscope.out文件到工作目录|
|:cs find c func | 查找func在哪些地方被调用 |
|:cw | 打开quickfix窗口查看结果 |


# gtags
Gtags综合了ctags和cscope的功能

|快捷键 | 功能 |
|--- |--- |
|:Gtags FUNC_NAME | 定位到 funcname 的定义处 |
|:Gtags -r FUNC_NAME | 查询 funcname 被引用的地方 |
|:Gtags -s SYMBOL | 定位到 symbol 出现的地方 |
|:Gtags -g STRING | 定位到 string 出现的地方 |
|:Gtags -gi STRING | 定位到 string 出现的地方，忽略大小写 |
|:Gtags -f FILENAME | 显示 filename 中的函数列表，`:Gtags -f %` 显示当前文件|
|:Gtags -P FILENAME | 显示包含特定模式的文件，`:Gtags -P .h$` 显示所有头文件 |
|:Gtags -P /vm/ | 显示vm目录下的文件 |


# 编译调试
- vim提供了`:make`来编译程序，默认调用的是make 
- 如果你当前目录下有makefile，简单地调用`:make`即可
- 如果你没有make程序，你可以通过配置makeprg选项来更改make调用的程序

如果你只有一个abc.java文件
1. 你可以设置makeprg为java的编译命令
2. `set makeprg=javac\ abc.java`
3. 然后调用`:make`即可

如果程序有错，可以通过quickfix窗口查看错误 
1. 不过如果要正确定位错误，需要设置好errorformat，让vim识别错误信息
2. `:setl efm=%A%f:%l:\ %m,%-Z%p^,%-C%.%#`
3. %f表示文件名，%l表示行号，%m表示错误信息，其它的还不能理解

> 更多信息请参考 `:help errorformat`


# 快速修复窗口
是quickfix插件提供的功能，对编译调试程序非常有用 :)

|快捷键 | 功能 |
|--- |--- |
|:cw | 打开快速修改窗口|
|:copen | 打开快速修改窗口|
|:cclose | 关闭快速修改窗口 |

快速修改窗口在make程序时非常有用，当make之后

|快捷键 | 功能 |
|--- |--- |
|:cc | 显示编译错误的详细信息 |
|:cl | 在快速修改窗口中列出错误 |
|:cn | 定位到***下一个***错误 |
|:cp | 定位到***上一个***错误 |
|:cr | 定位到***第一个***错误 |


<br/>

---

# 参考

[Vim使用笔记][1]  
[将Vim改造为强大的IDE—Vim集成][2]

[1]: http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html
[2]: http://blog.csdn.net/bokee/article/details/6633193