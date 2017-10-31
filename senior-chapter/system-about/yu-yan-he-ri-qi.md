# locale
显示地区和语言

```
[root@localhost ~]# locale
LANG=zh_CN.UTF-8
LC_CTYPE=zh_CN.UTF-8
LC_NUMERIC="zh_CN.UTF-8"
LC_TIME="zh_CN.UTF-8"
LC_COLLATE="zh_CN.UTF-8"
LC_MONETARY="zh_CN.UTF-8"
LC_MESSAGES="zh_CN.UTF-8"
LC_PAPER="zh_CN.UTF-8"
LC_NAME="zh_CN.UTF-8"
LC_ADDRESS="zh_CN.UTF-8"
LC_TELEPHONE="zh_CN.UTF-8"
LC_MEASUREMENT="zh_CN.UTF-8"
LC_IDENTIFICATION="zh_CN.UTF-8"
LC_ALL=
```

|字段 | 说明 |
|--- |--- |
|LC_CTYPE | 语言符号分类 |
|LC_NUMERIC | 数字显示格式 |
|LC_TIME | 时间显示格式 |
|LC_COLLATE | 排序比较习惯 |
|LC_MONETARY | 货币基本单位 |
|LC_MESSAGES | 提示信息格式 |
|LC_PAPER | 默认纸张大小 |
|LC_NAME | 姓名书写方式 |
|LC_ADDRESS | 地址书写方式 |
|LC_TELEPHONE | 电话书写方式 |
|LC_MEASUREMENT | 度量计算方式 |
|LC_IDENTIFICATION | 自身包含信息的概述 |
|LC_ALL | 其他选项的默认设置 |
> 字段的优先级顺序为 `LC_ALL > LC_* >LANG`

`locale`就是某一个地域内的人们的语言习惯和思维方式的表现，系统支持的`locale`可使用如下命令查看

```
ls /usr/share/i18n/locales
```
> `zh_CN` 就是简体中文的意识 

`locale`显示地区和语言，`local`则是用来定义局部变量的

```
[root@localhost ~]# local
-bash: local: 只能在函数中使用
```



# date
显示和修改时间

```
date [OPTION]... [+FORMAT]
date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
```

|选项 | 说明 |
|--- |--- |
|-d, --date=STRING | 指定显示格式 |
|-f, --file=DATEFILE | 从文件中读取显示格式 |
|-I[TIMESPEC], --iso-8601[=TIMESPEC] | 以`ISO 8601`格式显示 |
|-r, --reference=FILE | 显示文件的最后修改时间 |
|-R, --rfc-2822 | 以`RFC 2822`格式显示 |
|--rfc-3339=TIMESPEC | 以`RFC 3339`格式显示 |
|-s, --set=STRING | 设置时间 |
|-u, --utc, --universal | 显示`UTC`时间 |

输出格式控制符

|控制符 | 说明 |
|--- |--- |
|%% | 转义百分号 |
|%a | 简写的星期名 |
|%A | 完整的星期名 |
|%b | 简写的月份名 |
|%B | 完整的月份名 |
|%c | 本地日期和时间 |
|%C | 年份的前两位（世纪） |
|%d | 一月中的第几天 |
|%D | 同`%m/%d/%y` |
|%F | 同`%Y-%m-%d` |
|%g | 一年中的第几个星期时的年份后两位，参考`%G` |
|%g | 一年中的第几个星期时的年份，配合`%V`|
|%h | 同`%b` |
|%H | 24小时制 |
|%I | 12小时制 |
|%j | 一年中的第几天 |
|%m | 月份 |
|%M | 分钟 |
|%n | 换行符 |
|%N | 纳秒 |
|%p | 显示`AM`或`PM`|
|%P | 显示`am`或`pm`|
|%s | `1970-01-01 00:00:00`以来的秒数 |
|%S | 秒 |
|%t | `TAB`符号 |
|%T | 同`%H:%M:%S` |
|%u | 一周中的第几天（1..7），***1是星期一*** |
|%U | 一年中的第几周（00..53），***星期天***是一周的的第一天 |
|%V | `ISO`标准中的一周中的第几周（00..53），***星期一***是一周的的第一天 |
|%w | 一周中的第几天（0..6），***0是星期天*** |
|%W | 一年中的第几周（00..53），***星期一***是一周的的第一天|
|%y | 年份的后两位 |
|%Y | 完整的年份 |
|%z | 显示时区 |



# cal
显示日历

```
cal [options] [[[day] month] year]
```

|选项 | 说明 |
|--- |--- |
|-1, --one | 只显示当前月 |
|-3, --three | 显示当前月和上下两个月 |
|-s, --sunday | 星期天为一周的第一天 |
|-m, --monday | 星期一为一周的第一天 |
|-j, --julian | 显示一年中的第几天 |
|-y, --year | 显示年份 |

```
[root@localhost ~]# cal -s
      十月 2017
日 一 二 三 四 五 六
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31

[root@localhost ~]# cal -m
      十月 2017
一 二 三 四 五 六 日
                   1
 2  3  4  5  6  7  8
 9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
```
> `-s`和`-m`并不会影响某一天的星期，只是影响展示效果


<br/> 

---

# 参考

[locale的设定及LANG、LC_CTYPE、LC_ALL环境变量][1]  
[每个国家对应的语言Locale和国家代码对照表][2]  
[linux系统locale的设定][3]  
[十分钟搞清字符集和字符编码][4]  
[字符串，那些你不知道的事][5]  
[VIM 文件编码识别与乱码处理][6]  
[Python字符编码详解][7]  
[PYTHON-进阶-编码处理小结][8]  
[Python2 中的编码问题][9]  
[立即停止使用setdefaultencoding('utf-8')，以及为什么][10]  
[每天一个linux命令：date命令][11]  
[date命令][12]  
[使用beego/go mysql /JavaScript 遇到的时间坑以及ISO-8601标准][13]
[UTC 和ISO 8601时间格式的一些疑问][14]  
[关于“时间”的一次探索][15]  
[一周的第一天是周一还是周日？由来是什么][16]  
[JAVA Calendar类setFirstDayOfWeek和setMinimalDaysInFirstWeek][17]  
[每天一个linux命令（38）：cal 命令][18]  
[cal命令][19]  
[日历查询的算法 如何计算某一天是星期几][20]  
[历史上第一个星期一是从哪天开始的,为什么是那一天][21]  

[1]: http://www.cnblogs.com/xlmeng1988/archive/2013/01/16/locale.html
[2]: http://www.cnblogs.com/jacksoft/p/5771130.html
[3]: http://www.cnblogs.com/markjiao/archive/2008/05/20/1203316.html
[4]: http://cenalulu.github.io/linux/character-encoding/
[5]: http://liujiacai.net/blog/2015/11/20/strings/
[6]: http://edyfox.codecarver.org/html/vim_fileencodings_detection.html
[7]: http://www.cnblogs.com/huxi/articles/1897271.html
[8]: http://wklken.me/posts/2013/08/31/python-extra-coding-intro.html
[9]: http://liujiacai.net/blog/2016/06/30/python2-encoding/
[10]: https://blog.ernest.me/post/python-setdefaultencoding-unicode-bytes
[11]: http://www.cnblogs.com/peida/archive/2012/12/13/2815687.html
[12]: http://man.linuxde.net/date
[13]: http://www.enjoydiy.com/3400.html
[14]: https://segmentfault.com/q/1010000004333145/a-1020000004333293
[15]: https://segmentfault.com/a/1190000004292140
[16]: https://www.zhihu.com/question/20162291
[17]: http://blog.csdn.net/okyoung188/article/details/53487888
[18]: http://www.cnblogs.com/peida/archive/2012/12/14/2817473.html
[19]: http://man.linuxde.net/cal
[20]: http://www.cnblogs.com/carekee/articles/4529720.html
[21]: https://zhidao.baidu.com/question/52338886.html