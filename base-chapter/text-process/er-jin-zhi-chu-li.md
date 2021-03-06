# hexdump
hexdump命令一般用来查看“二进制”文件的十六进制编码，但实际上它能查看任何文件，而不只限于二进制文件

```
hexdump [选项] [文件]...
```

|选项 | 说明 |
|--- |--- |
|-n length | 只格式化文件的前length个字节 |
|-C | 输出规范的十六进制和ASCII码 |
|-b | 单字节八进制显示 |
|-c | 单字节字符显示 |
|-d | 双字节十进制显示 |
|-o | 双字节八进制显示 | 
|-x | 双字节十六进制显示 | 
|-s | 从偏移量开始输出 |
|-e | 指定格式字符串 |

格式字符串包含在一对单引号中，形如：'a/b "format1" "format2"'
- 每个格式字符串由三部分组成，每部分之间由空格分隔
- b表示对每b个输入字节应用format1格式
- a表示对每a个输入字节应用format2格式
- 一般a > b，a、b应用的格式与输入的顺序相反
- b只能为1，2，4，a可以省略，省略则a=1

|格式 | 说明 |
|--- |--- |
|%02d | 两位十进制  |
|%03x | 三位十六进制 |
|%02o | 两位八进制 |
|%c | 单个字符 |
|%_ad | 标记下一个输出字节的序号，用十进制表示 |
|%_ax | 标记下一个输出字节的序号，用十六进制表示 |
|%_ao | 标记下一个输出字节的序号，用八进制表示 |
|%_p | 对不能以常规字符显示的用 . 代替 |
> 同一行如果要显示多个格式字符串，则可以跟多个-e选项



# od
od命令用于输出文件的八进制、十六进制或其它格式编码的字节
> 通常用于显示或查看文件中不能直接显示在终端的字符

```
od [选项] [文件]...
```

|选项 | 说明 |
|--- |--- |
|-A, --address-radix=RADIX | 选择以何种基数计算字码 |
|-a | 此参数的效果和同时指定“-t a”参数相同 | 
|-b | 此参数的效果和同时指定“-t o1”参数相同 | 
|-c | 此参数的效果和同时指定“-t c”参数相同 |
|-d | 此参数的效果和同时指定“-t u2”参数相同 | 
|-f | 此参数的效果和同时指定“-t fF”参数相同 |
|-h | 此参数的效果和同时指定“-t x2”参数相同 | 
|-i | 此参数的效果和同时指定“-t dI”参数相同 | 
|-j, --skip-bytes=BYTES | 略过指定的字符数目 | 
|-l | 此参数的效果和同时指定“-t dL”参数相同 |
|-N, --read-bytes=BYTES | 到指定的字符数目为止 |
|-o | 此参数的效果和同时指定“-t o2”参数相同 |
|-s | 此参数的效果和同时指定“-t d2”参数相同 |
|-S BYTES, --strings[=BYTES] | 只显示符合指定的字节目的字符串 |
|-t, --format=TYPE | 设置输出格式 | 
|-v, --output-duplicates | 输出时不省略重复的数据 | 
|-w[BYTES], --width[=BYTES] | 设置每列的最大字符数 | 
|-x | 此参数的效果和同时指定“-h”参数相同 |
|--help | 在线帮助 |
|--version | 显示版本信息 |


# xdd
详情参考 [在Linux下使用vim配合xxd查看并编辑二进制文件][4] 和 [linux 命令 xxd linux下查看二进制文件][5]


</br>

---

# 参考

[hexdump命令][1]  
[Linux命令学习总结：hexdump][2]  
[od命令][3]  
[Linux之od命令详解][4]  
[在Linux下使用vim配合xxd查看并编辑二进制文件][5]  
[linux 命令 xxd linux下查看二进制文件][6]  

[1]: http://man.linuxde.net/hexdump
[2]: http://www.cnblogs.com/kerrycode/p/5077687.html
[3]: http://man.linuxde.net/od
[4]: http://www.cnblogs.com/hdk1993/p/4395574.html
[5]: 在Linux下使用vim配合xxd查看并编辑二进制文件
[6]: http://fancyxinyu.blog.163.com/blog/static/18232136620111183019942/