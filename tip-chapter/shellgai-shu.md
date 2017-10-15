# shell
在计算机科学中，Shell俗称外壳（用来区别于内核），它类似于Windows的DOS，够接收用户的命令并翻译给操作系统执行，是用户与操作系统（内核）之间的桥梁。



# shell的分类
1. bash
    - 现在大多数linux系统默认使用的shell。
    - 是 Bourne shell（最早的Unix shell）的一个免费版本。
    - 可以通过help命令来查看帮助

2. csh
    - C shell 使用的是“类C”语法，具有C语言风格
    - 目前使用的并不多，已经被/bin/tcsh所取代
    - 内部有52个命令，较为庞大

3. ksh
    - Korn shell 的语法与 Bourne shell 相同
    - 同时具备了 C shell 的易用特点。许多安装脚本都使用 ksh 
    - 内部有42条命令
    
4. tcsh
    - tcsh是csh的增强版，与 C shell 完全兼容
      
5. zsh
    - 传说中的[终极shell](https://zhuanlan.zhihu.com/p/19556676?columnSlug=mactalk)
    
6. sh
    - sh 通常是指向 bash 的快捷方式

        

# 查看shell
- 查看系统支持哪些shell

    `cat /etc/shells`
    
- 查看正在使用的shell

    `echo $SHELL`

        
    
# shell与终端的区别
- 终端：接收用户的输入，并传递给shell程序，接收程序输出并展示到屏幕
- shell： 接收并解析用户的命令给操作系统执行，将结果输出到终端

    

# shell快捷键描述
|快捷键描述（不区分大小写） | 说明 |
|--- |--- |
|Ctrl | control 键 |
|Shift | shift 键|
|Alt | alt 键 |
|Tab | tab 键 |
|Esc | esc 键 |
|Backspace | 退格键 |
|Enter | 回车键 |
|[Page]Up | 向上（翻页）键 |
|[Page]Down | 向下（翻页）键 |
|Left | 方向左键 |
|Right | 方向右键 |
> 快捷键后面的加号(+)或减号(-)表示组合快捷键的意思，不需要输入
  
> 类似`Ctrl + W`的形式，有时候也会表达为`C-W`的简写形式
  
> 快捷键在Mac和Linux系统上会有部分差异，需要注意


    
# shell快捷键（linux）
综合操作快捷键

|快捷键|说明|
|---|---|
|Ctrl + c | 终止程序的执行 |
|Ctrl + l | 清空屏幕 |
|Ctrl + n | 下一个历史命令。n -> next |
|Ctrl + p | 上一个历史命令。p -> previous |
|Ctrl + r | 搜索包含该字符串的命令，继续按Ctrl + r搜索上一条匹配的命令，按Ctrl + g 退出。r -> reverse search |
|Ctrl + s | 挂起当前shell，停止向屏幕输出 |
|Ctrl + q | 恢复挂起的shell，继续向屏幕删除 |
|Ctrl + v | 插入特殊字符，如Ctrl + v + Tab插入Tab字符键 |
|Alt + . | 补全上一次的最后一个参数 |
|!! | 执行上一次执行的的命令 |
|!$ | 补全上一次的最后一个参数，和Alt + .一样 |
|!* | 补全上一次的所有参数 |

移动操作快捷键

|快捷键|说明|
|---|---|
|Ctrl + a | 移动到当前行的开头。a -> first letter |
|Ctrl + e | 移动到当前行的末尾。e -> end |
|Ctrl + b | 向后移动一个字符。b -> backward |
|Ctrl + f | 向前移动一个字符。f -> forward |
|Alt + b | 移动到当前单词的开头。b -> backward |
|Alt + f | 移动到当前单词的结尾。f -> forward |


删除操作快捷键

|快捷键|说明|
|---|---|
|Ctrl + d | 删除光标所在的字符 |
|Ctrl + h | 删除光标的前一个字符 |


剪切操作快捷键

|快捷键|说明|
|---|---|
|Ctrl + u | 剪切命令行中光标所在处之前的所有字符（不包括自身）|
|Ctrl + k | 剪切命令行中光标所在处之后的所有字符（包括自身）|
|Ctrl + w | 剪切光标之前的词（以空格、标点等分隔，不包括自身）|
|Alt + d | 剪切光标之后的词（以空格、标点等分隔，包括自身）|


粘贴操作快捷键

|快捷键|说明|
|---|---|
|Ctrl + y | 粘贴刚才所删除的字符 |


撤销操作快捷键

|快捷键|说明|
|---|---|
|Ctrl + (x u) | 按住Ctrl的同时再先后按x和u，撤销刚才的操作 |


大小写操作快捷键

|快捷键|说明|
|---|---|
|Alt + u | 把光标后的词转化为大写。u -> upper |
|Alt + l | 把光标后的词转化为小写。l -> lower |
|Alt + c | 把光标后的词汇变成首字符大写。c -> capital |


 
# shell快捷键（mac）
和linux差不多，部分有区别

|快捷键|说明|
|---|---|
|Ctrl + r | 搜索包含该字符传的命令，继续按Ctrl+r搜索上一条匹配的命令，按Ctrl + s搜索下一条匹配的命令，按Ctrl + g或Ctrl + q退出。r -> reverse search |
|Ctrl + s | 正向搜索历史记录。s -> search |
|Ctrl + u | 剪切整行 |
|Ctrl + l | 会插入ls，然后回车 |



# mac下常用快捷键
|快捷键 | 说明 |
|--- |--- |
| command + q | 退出应用程序 |
| command + w | 关闭当前窗口 |
| command + r | 刷新当前页面 |
| command + t | 新建页面 |
| command + p | 打印 |
| command + a | 全选 |
| command + s | 保存 |
| command + f | 查找 |
| command + h | 隐藏当前窗口 |
| command + z | 撤销 |
| shift + command + z | 重做 |
| command + x | 前切 |
| command + c | 复制 |
| command + v | 粘贴 |
| command + m | 最小化到Dock |
| command + , | 打开设置界面（逗号）|
| command + TAB | 快速切换程序 |
| command + SPACE | 切换输入法 |
| control + SPACE | 呼出搜索框 |
| control + ← | 向左切换屏幕 |
| control + → | 向右切换屏幕 |
| control + ↑ | 显示任务管理界面 |
| control + ↓ | 显示应用程序界面 |
> `shift`一般是对`command`进行增强，`alt`则是辅助