# ps 
查看进程某一时刻的快照信息

```
ps [选项]
```

选项风格

1. UNIX 风格，选项可以组合在一起，并且选项前必须有`-`连字符
2. BSD 风格，选项可以组合在一起，但是选项前不能有`-`连字符
3. GNU 风格，长选项前有两个“-”连字符，值用空格或等号分割

## 选项详解
### 简单选择
|选项 | 说明 |
|--- |--- |
|a | 显示包含终端的所有进程，`ax`显示所有进程 |
|x | 显示当前用户的所有进程，`ax`显示所有进程 |
|-a | 显示包含终端的除了会话领导者以外的所有进程 | 
|-A | 显示所有进程 |
|-d | 显示除了会话领导者以外的所有进程 |
|-e | 显示所有进程 |
|e | 显示环境变量 |
|-N, --deselect | 反向选择进程 |
|r | 只显示正在运行的进程 |
```
[root@zhujipeng ~]# ps a -o tty | sort -u
pts/0
pts/1
TT
tty1
[root@zhujipeng ~]# ps -e -o tty | sort -u
?
pts/0
pts/1
TT
tty1

[root@mty-005 ~]# ps x -o user | sort -u
root
USER
[root@mty-005 ~]# ps -e -o user | sort -u
avahi
dbus
dig
ntp
polkitd
postfix
root
USER
zabbix
```

### 列表选择
列表的值用空格或逗号分割，形如`ps -p "1 2 3" -p 4,5,6`

|选项 | 说明 |
|--- |--- |
|-123 | 等同于`--pid 123` |
|123 | 等同于`--pid 123` |
|"1 2 3" | 等同于`-p 1 -p 2 -p 3` | 
|1,2,3 | 等同于`-p 1 -p 2 -p 3` |
|-C cmdlist | 指定命令列表 |
|-G grplist | 指定真实用户组列表 |
|-g grplist | 指定有效用户组列表 |
|--Group grplist | 等同于`-G` |
|--group grplist | 等同于`-g` |
|p pidlist | 指定进程id列表 |
|-p pidlist | 指定进程id列表 |
|--pid pidlist | 指定进程id列表 |
|--ppid pidlist | 指定父进程id列表 |
|q pidlist | 指定进程id列表（快速模式）|
|-q pidlist | 指定进程id列表（快速模式）|
|--quick-pid pidlist | 指定进程id列表（快速模式）|
|-s sesslist | 指定会话id列表 |
|--sid sesslist | 指定会话id列表 |
|t ttylist | 指定终端列表 |
|-t ttylist | 指定终端列表 |
|--tty ttylist | 指定终端列表 |
|U userlist | 指定***有效***用户列表 |
|-U userlist | 指定***真实***用户列表 |
|-u userlist | 指定***有效***用户列表 |
|--User userlist | 指定***真实***用户列表 |
|--user userlist | 指定***有效***用户列表 |
> 注意：小写的单词需要替换为实际值

### 输出控制
输出格式请参照`man ps`中的`STANDARD FORMAT SPECIFIERS`章节

|选项 | 说明 |
|--- |--- |
|-f | 显示所有列 |
|-F | 显示更多的额外列 |
|--format | 指定输出格式，等同于`-o` |
|o format | 指定输出格式 |
|o format | 指定输出格式 |
> 注意：小写的单词需要替换为实际值


### 排序输出
`--sort`可以指定排序，格式为`[+|-]key[,[+|-]key[,...]]`
> 值请参照`man ps`中的`STANDARD FORMAT SPECIFIERS`章节


## 使用详解
### 基本示例
#### 标准语法
```
[root@zhujipeng /]# ps -e
  PID TTY          TIME CMD
    1 pts/0    00:00:00 bash
   15 pts/1    00:00:00 bash
   40 pts/1    00:00:00 ps
   
[root@zhujipeng /]#  ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 09:23 pts/0    00:00:00 /bin/bash
root        15     0  0 09:23 pts/1    00:00:00 bash
root        33    15  0 10:19 pts/1    00:00:00 ps -ef

[root@zhujipeng /]#  ps -eF
UID        PID  PPID  C    SZ   RSS PSR STIME TTY          TIME CMD
root         1     0  0  3258  2776   0 09:23 pts/0    00:00:00 /bin/bash
root        15     0  0  3258  3052   1 09:23 pts/1    00:00:00 bash
root        38    15  0  3727  2252   1 10:24 pts/1    00:00:00 ps -eF
```

#### BSD语法
```
[root@zhujipeng /]# ps -ax
Warning: bad syntax, perhaps a bogus '-'? See /usr/share/doc/procps-3.2.8/FAQ
  PID TTY      STAT   TIME COMMAND
    1 pts/0    Ss+    0:00 /bin/bash
   15 pts/1    Ss     0:00 bash
   36 pts/1    R+     0:00 ps -ax

[root@zhujipeng /]#  ps -aux
Warning: bad syntax, perhaps a bogus '-'? See /usr/share/doc/procps-3.2.8/FAQ
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  13032  2776 pts/0    Ss+  09:23   0:00 /bin/bash
root        15  0.0  0.1  13032  3052 pts/1    Ss   09:23   0:00 bash
root        34  0.0  0.1  14912  2260 pts/1    R+   10:20   0:00 ps -aux

[root@zhujipeng /]#  ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  13032  2776 pts/0    Ss+  09:23   0:00 /bin/bash
root        15  0.0  0.1  13032  3052 pts/1    Ss   09:23   0:00 bash
root        35  0.0  0.1  14912  2280 pts/1    R+   10:20   0:00 ps aux
```
> 注意 `-` 对 `aux`的影响不同，`-aux`代表筛选名为`x`的用户

#### 指定输出列
```
[root@zhujipeng /]# ps -eo pid,tid,class,rtprio,ni,pri,psr,pcpu,stat,wchan:14,comm
  PID   TID CLS RTPRIO  NI PRI PSR %CPU STAT WCHAN          COMMAND
    1     1 TS       -   0  19   0  0.0 Ss+  -              bash
   15    15 TS       -   0  19   1  0.0 Ss   -              bash
   48    48 TS       -   0  19   0  0.0 R+   -              ps
   
[root@zhujipeng /]# ps axo stat,euid,ruid,tty,tpgid,sess,pgrp,ppid,pid,pcpu,comm
STAT  EUID  RUID TT       TPGID  SESS  PGRP  PPID   PID %CPU COMMAND
Ss+      0     0 pts/0        1     1     1     0     1  0.0 bash
Ss       0     0 pts/1       49    15    15     0    15  0.0 bash
R+       0     0 pts/1       49    15    49    15    49  0.0 ps

[root@zhujipeng /]# ps -Ao pid,tt,user,fname,tmout,f,wchan
  PID TT       USER     COMMAND  TMOUT F WCHAN
    1 pts/0    root     bash         - 4 -
   15 pts/1    root     bash         - 4 -
   50 pts/1    root     ps           - 0 -
```

#### 指定命令名
```
[root@zhujipeng /]#  ps -C bash -o pid,cmd
  PID CMD
    1 /bin/bash
   15 bash
```

#### 指定排序列
```
[root@zhujipeng /]# ps -ef --sort=%cpu
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 13:14 pts/0    00:00:00 /bin/bash
root        16     0  0 13:14 pts/1    00:00:00 bash
root        41    16  0 13:28 pts/1    00:00:00 ps -ef --sort=%cpu
[root@zhujipeng /]# ps -ef --sort=%mem
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 13:14 pts/0    00:00:00 /bin/bash
root        16     0  0 13:14 pts/1    00:00:00 bash
root        42    16  0 13:28 pts/1    00:00:00 ps -ef --sort=%mem
[root@zhujipeng /]# ps -ef --sort -pcpu
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 13:14 pts/0    00:00:00 /bin/bash
root        16     0  0 13:14 pts/1    00:00:00 bash
root        48    16  0 13:30 pts/1    00:00:00 ps -ef --sort -pcpu
[root@zhujipeng /]# ps -ef --sort -pmem
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 13:14 pts/0    00:00:00 /bin/bash
root        16     0  0 13:14 pts/1    00:00:00 bash
root        49    16  0 13:30 pts/1    00:00:00 ps -ef --sort -pmem
```

### 输出详解
#### 列的含义
|列名 | 说明 |
|--- |--- | 
|UID | 用户id |
|PID | 进程id |
|PPID | 父进程id |
|STIME | 开始时间 |
|TTY | 终端 |
|TIME | CPU使用时间 |
|CMD| 命令 |
|%CPU | cpu使用率 |
|%MEM | 内存使用率 |
|VSZ | 虚拟内存使用大小 |
|RSS | 内存使用大小 |
|STAT| 进程的状态 |


#### 进程状态
|状态 | 说明 |
|--- |--- |
|D | 不可中断的静止 | 
|R | 正在执行中 |
|S | 静止状态 |
|T | 暂停执行 | 
|Z | 不存在但暂时无法消除 | 
|W | 没有足够的记忆体分页可分配 |  
|< | 高优先序的行程 |   
|N | 低优先序的行程 |  
|L | 有记忆体分页分配并锁在记忆体内 |
|s | 会话首进程 |
|l | 多线程进程 |



# top
实时查看进程的信息

```
top [选项]
```
|选项 | 说明 |
|--- |--- |
|d | 指定每两次屏幕信息刷新之间的时间间隔，默认为5s |
|p | 通过指定监控进程ID来仅仅监控某个进程的状态 |
|q | 使top尽可能没有任何延迟的进行刷新 |
|S | 指定累计模式 |
|s | 在安全模式中运行，不支持交互 | 
|i | 不显示任何闲置或者僵死进程 |
|c | 显示整个命令行而不只是显示命令名 |


## 输出详解
```
top - 13:47:56 up  1:06,  0 users,  load average: 0.00, 0.00, 0.00
Tasks:   3 total,   1 running,   2 sleeping,   0 stopped,   0 zombie
Cpu(s):  0.2%us,  0.0%sy,  0.0%ni, 99.7%id,  0.2%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:   2047048k total,   275400k used,  1771648k free,     5144k buffers
Swap:  4090876k total,        0k used,  4090876k free,   170424k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
    1 root      20   0 13032 2776 2516 S  0.0  0.1   0:00.05 bash
   16 root      20   0 13032 3104 2732 S  0.0  0.2   0:00.11 bash
   53 root      20   0 14952 1964 1756 R  0.0  0.1   0:00.01 top
```

第一行（top）

|输出 | 说明 |
|--- |--- |
|13:47:56 | 当前时间 |
|up | 系统启动了多久 |
|users | 用户数 |
|load average | 最近1分钟前、5分钟前、15分钟前的平均负载 |

第二行（Tasks）

|输出 | 说明 |
|--- |--- |
|total | 系统总进程数 |
|running | 运行中的进程数 |
|sleeping | 睡眠中的进程数 |
|stoped | 停止的进程数 |
|zombie | 僵尸进程数 |

第三行（Cpu）

|输出 | 说明 |
|--- |--- |
|us |（user）用户空间占用CPU的百分比 |
|sy |（system）内核空间占用CPU的百分比 |
|ni |（nice）改变过优先级的进程占用CPU的百分比 |
|id |（idle）空闲CPU百分比 |
|wa |（wait）IO等待占用CPU的百分比 |
|hi |（Hardware IRQ）硬中断占用CPU的百分比 |
|si |（Software IRQ）软中断占用CPU的百分比 |
|st | 虚拟机占用百分比 | 
> IRQ全称为Interrupt Request，即是“中断请求”的意思


第四行（Mem）

|输出 | 说明 |
|--- |--- |
|total | 物理内存总量 |
|used | 已使用的内存总量 |
|free | 空闲的内存总量 |
|buffers | 缓存使用的内存量 |
> `free + buffers` 是实际可用的内存

第五行（Swap）

|输出 | 说明 |
|--- |--- |
|total| 交换区总量 |
|used | 使用的交换区总量 |
|free | 空闲交换区总量 |
|cached | 缓冲使用的交换区总量 |

第七行

|输出 | 说明 |
|--- |--- |
|PID | 进程id |
|USER | 进程所有者 |
|PR | 进程优先级 |
|NI | nice值。负值表示高优先级，正值表示低优先级 |
|VIRT | 进程使用的虚拟内存总量，单位kb |
|RES | 进程使用的未被换出的物理内存大小，单位kb |
|SHR | 共享内存大小，单位kb |
|S | 进程状态 |
|%CPU | CPU占用百分比 |
|%MEM | 物理内存百分比 |
|TIME+ | 进程使用的CPU时间总计，单位1/100秒 |
|COMMAND |  进程名称（命令名/命令行） |


## 交互命令
详情参[这里][3]或者在top中使用`h`按键



# free 


<br/>

---

# 参考

[10个重要的Linux ps命令实战][1]  
[Linux中ps命令详解][2]  
[使用top命令查看CPU负载][3] 
[Linux top命令的用法详细详解][4]

[1]: https://linux.cn/article-4743-1.html
[2]: http://blog.csdn.net/tanga842428/article/details/52742360
[3]: https://linux.cn/article-1238-1.html
[4]: http://blog.csdn.net/dxl342/article/details/53507673