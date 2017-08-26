# which 
查看命令文件所在的位置

格式如下
```
which [选项] <命令...>
```

# whereis
搜索包含该命令的的相关文件

> 和find相比，whereis查找的速度非常快，这是因为linux系统会将系统内的所有文件都记录在一个数据库文件中，查找时会从数据库中查找数据

格式如下
```
whereis [选项] <命令>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-b | 只搜索可执行文件 |
|-m | 只搜索帮助文件 |
|-s | 只搜索源代码文件 |
|-B list | 指定搜索可执行文件的路径 |
|-M list | 指定搜索帮助文件的路径 |
|-S list | 指定搜索源代码文件的路径 |


# locate
快速查找文件

格式如下
```
locate [选项] <文件>
```
> locate命令可以通过搜寻数据库来快速找到档案，数据库由updatedb程序来更新，updatedb是由crontab周期性调用

选项如下

|选项 | 说明 |
|--- |--- |
|-A, --all | 显示所有的匹配结果 |
|-b, --basename | 匹配文件名部分，而不是全路径 |
|-c, --count | 输出匹配个数，而不是文件名 |
|-i, --ignore-case | 匹配时忽略大小写 |
|-l, --limit, -n LIMIT | 找到足够的匹配后退出 |
|-r, --regexp REGEXP | 使用***基本正则表达式***匹配 |
|--regex | 使用***扩展正则表达式***匹配 |
|-w, --wholename| 匹配全路径，而不是文件名部分|

BRE（基本正则表达式）与ERE（扩展正则表达式）的差异参考[这里][8]


# find
Linux下find命令在目录结构中搜索文件，并执行指定的操作

格式如下
```
find [选项] <目录...> <表达式> [动作]
```

选项如下

|选项 | 说明 |
|--- |--- |
|-name | 按照文件名查找文件 |
|-perm | 按照文件权限来查找文件|
|-user | 按照文件属主来查找文件|
|-group | 按照文件所属的组来查找文件|
|-mtime [-/+]n | 按照文件的更改时间来查找文件， -n表示距现在n天以内，+n表示距现在n天以前 |
|-newer file1 ! file2| 查找更改时间比文件file1新但比文件file2旧的文件 |
|-type | 查找某一类型的文件 |
|-size | 查找文件大小的文件 |
|-amin n | 查找系统中最后N分钟访问的文件 |
|-atime n | 查找系统中最后n*24小时访问的文件 |
|-cmin n | 查找系统中最后N分钟被改变文件状态的文件 |
|-ctime n | 查找系统中最后n*24小时被改变文件状态的文件 |
|-mmin n | 查找系统中最后N分钟被改变文件数据的文件 |
|-mtime n | 查找系统中最后n*24小时被改变文件数据的文件 |

find命令非常复杂，更多参考[这里][3] 和 man文档


<br/>

___

# 参考

[每天一个linux命令 whereis 命令][1]  
[每天一个linux命令 locate 命令][2]  
[每天一个linux命令 find 命令概览][3]  
[每天一个linux命令 find命令之exec][4]
[每天一个linux命令 find命令之xargs][5]
[每天一个linux命令 find命令的参数详解][6]
[linux find -regex 使用正则表达式][7]
[BRE与ERE的差异][8]

[1]: http://www.cnblogs.com/peida/archive/2012/11/09/2761928.html
[2]: http://www.cnblogs.com/peida/archive/2012/11/12/2765750.html
[3]: http://www.cnblogs.com/peida/archive/2012/11/13/2767374.html
[4]: http://www.cnblogs.com/peida/archive/2012/11/14/2769248.html
[5]: http://www.cnblogs.com/peida/archive/2012/11/15/2770888.html
[6]: http://www.cnblogs.com/peida/archive/2012/11/16/2773289.html
[7]: http://www.cnblogs.com/jiangzhaowei/p/5451173.html
[8]: http://blog.chinaunix.net/uid-23045379-id-2562051.html