# 进程管理
## 进程组
一个或多个***进程*** 的集合


## 作业
一个或多个***进程*** 的集合
- shell可以进行作业控制，可以运行一个前台作业和多个后台作业
- 如果作业中的某个进程又创建了子进程，则子进程不属于该作业
- 作业运行结束后如果前台进程不存在，shell就把自己提到前台


## 会话
一个或多个***进程组*** 的集合

- 通常一个会话开始于用户登录，终止于用户退出，在此期间该用户运行的所有进程都属于这个会话期
- 会话包括控制进程（会话首进程），一个前台进程组和任意多个后台进程组
- 一个会话只能有一个控制终端 ，控制终端上的输入和信号将发送给会话的前台进程组中的所有进程



# 进程类型
进程状态，详情参见[这里][12]

|状态 | 说明 |
|--- |--- |
|D |   Uninterruptible sleep (usually IO) |
|R |   Running or runnable (on run queue) |
|S |   Interruptible sleep (waiting for an event to  complete) |
|T |   Stopped, either by a job control signal or because it is being traced |
|W |  paging (not valid since the 2.6.xx kernel) |
|X |   dead (should never be seen) |
|Z |   Defunct ("zombie") process, terminated but not reaped by its parent |


### 前台进程
一般默认在shell中启动的进程就是前台进程

### 后台进程
脱离终端在后台执行的程序，通常以`d`结尾

### 僵尸进程
父进程没有获取子进程退出状态信息的子进程
> 详情参考 [这里][2] 和 [这里][3]



# 后台进程
使用`ctrl + z`快捷键可以将前台进程变为后台进程
```
[root@zhujipeng /]# sleep 60
^Z
[1]+  Stopped                 sleep 60
[root@zhujipeng /]# jobs
[1]+  Stopped                 sleep 60
[root@zhujipeng /]# bg
[1]+ sleep 60 &
[root@zhujipeng /]# fg
sleep 60
^C
```

命令后面使用 `&` 符号可以将进程变为后台进程
```
[root@zhujipeng /]# sleep 60 &
[1] 28
[root@zhujipeng /]# jobs
[1]+  Running                 sleep 60 &
[root@zhujipeng /]# kill -9 %1
[root@zhujipeng /]# jobs
[1]+  Killed                  sleep 60
```


## nohup
会话中前台进程会收到`SIGHUP`信号而终止，后台进程则由`huponexit`参数决定
```
[root@zhujipeng /]# shopt | grep huponexit
huponexit      	off
```

SIGHUP会在以下3种情况下被发送给相应的进程，详见[这里][9]

1. 终端关闭时，该信号被发送到session首进程以及作为job提交的进程（&提交的进程）
2. session首进程收到信号退出时，该信号被发送到该session前台进程组中的每一个进程
3. 若进程组是孤儿进程组并且有进程处于停止状态，该信号被发送到该进程组中的每一个进程

> 进程处于停止状态是收到了`SIGSTOP`或`SIGTSTP`信号


## 守护进程
守护进程是指忽略了`SIGHUP`信号的进程，启动方法参见[这里][5]和[这里][6]



# 进程信号
信号(signal)就是一种向进程传递信息的方式，详见[这里][12]

```
[root@zhujipeng /]# kill -l
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX
```

## 信号的响应

1. 中止进程(Term)
2. 忽略信号(Ign)
3. 中止进程并保存内存信息(Core)
4. 停止进程(Stop)
5. 继续运行进程(Cont)


## 常见的信号
|信号名 | 信号值 | 动作 | 说明 |
|--- |--- |--- |--- |
|SIGHUP	|1 | Term | 终止进程（可以被捕获、阻塞或忽略）|
|SIGINT	|2 | Term | 中断 (INTERRUPT) 进程（可以被捕获、阻塞或忽略）|
|SIGQUIT |3 | Core | 退出 (QUIT) 进程（可以被捕获、阻塞或忽略） |
|SIGILL	|4 | Core | 非法指令(程序错误、试图执行数据段、栈溢出等) |
|SIGABRT | 6 | Core | 调用abort函数触发 |
|SIGFPE	| 8 |Core | 算术运行错误(浮点运算错误、除数为零等) |
|SIGKILL | 9 | Term | 杀死（KILL）进程(不能被捕获、阻塞或忽略) |
|SIGSEGV | 11 | Core | 无效内存引用(试图访问不属于自己的内存空间、对只读内存空间进行写操作) |
|SIGPIPE | 13 | Term | 消息管道损坏(FIFO/Socket通信时，管道未打开而进行写操作) |
|SIGALRM | 14 | Term | 时钟定时信号 |
|SIGTERM | 15 | Term | 结束(TERMINAL)进程(可以被捕获、阻塞或忽略) |
|SIGUSR1 | 30,10,16 | Term | 用户保留 |
|SIGUSR2 | 31,12,17 | Term | 用户保留 |
|SIGCHLD | 20,17,18 | Ign | 子进程结束(由父进程接收) |
|SIGCONT | 19,18,25 | Cont | 继续执行已经停止的进程(不能被阻塞) |
|SIGSTOP | 17,19,23 | Stop | 停止进程(不能被捕获、阻塞或忽略) |
|SIGTSTP | 18,20,24 | Stop | 停止进程(可以被捕获、阻塞或忽略) |
|SIGTTIN | 21,21,26 | Stop | 后台程序从终端中读取数据时触发 |
|SIGTTOU | 22,22,27 | Stop | 后台程序向终端中写数据时触发 |


## 信号快捷键
```
[root@zhujipeng /]# stty -a
speed 38400 baud; rows 26; columns 115; line = 0;
intr = ^C; quit = ^\; erase = ^?; kill = ^U; eof = ^D; eol = <undef>; eol2 = <undef>; swtch = <undef>; start = ^Q;
stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; flush = ^O; min = 1; time = 0;
-parenb -parodd cs8 -hupcl -cstopb cread -clocal -crtscts -cdtrdsr
-ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff -iuclc -ixany -imaxbel -iutf8
opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0
isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke
```

|信号 | 快捷键 |
|--- |--- |
|SIGINT | CTRL+C |
|SIGQUIT | CTRL+\ |
|SIGTSTP | CRTL+Z |
> `CRTL+D` 是发送特殊的 `EOF` 字符



# 进程信息
`/proc`下存在一些以进程id命名的文件，详情参见[这里][15]

```
[root@zhujipeng /]# ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 12:03 pts/0    00:00:00 /bin/bash
root       235     0  0 13:14 ?        00:00:00 /sbin/udevd -d
root       248     0  0 13:16 pts/2    00:00:00 bash
root       288   248  0 14:38 pts/2    00:00:00 ps -ef
[root@zhujipeng /]# ls /proc/1
attr        comm             fd         maps        ns             projid_map  smaps    task
autogroup   coredump_filter  fdinfo     mem         oom_adj        root        stack    timers
auxv        cpuset           gid_map    mountinfo   oom_score      sched       stat     timerslack_ns
cgroup      cwd              limits     mounts      oom_score_adj  schedstat   statm    uid_map
clear_refs  environ          loginuid   mountstats  pagemap        sessionid   status   wchan
cmdline     exe              map_files  net         personality    setgroups   syscall
```


# fork
由fork创建的新进程被称为子进程（child process），详情见[fork出的子进程和父进程][16]


<br/>

---

# 参考

[进程、进程组、作业、会话][1]  
[戏说守护、僵尸、孤儿进程][2]  
[孤儿进程与僵尸进程][3] 
[Linux后台任务的运行、查看和关闭][4]   
[Linux 守护进程的启动方法][5]  
[让进程在后台可靠运行的几种方法][6]  
[Linux 守护进程的实现][7]  
[Linux ssh exit，启动的后台进程不会停止][8]  
[SIGHUP信号与控制终端][9]  
[Linux信号基础][10] 
[linux内核中异步通知机制--信号处理机制][11]  
[Linux信号处理机制][12]   
[Linux中ctrl-c, ctrl-z, ctrl-d 区别][13]  
[Linux进程的Uninterruptible sleep][14]  
[Linux查看进程的启动和运行相关的文件][15]  
[fork出的子进程和父进程][16] 
[shell中的fork、source和exec总结][17]   

[1]: http://www.jianshu.com/p/f64cd61d196c
[2]: https://zhuanlan.zhihu.com/p/21250530
[3]: http://www.cnblogs.com/Anker/p/3271773.html
[4]: http://blog.zhengyi.one/linux-jobs.html
[5]: http://www.ruanyifeng.com/blog/2016/02/linux-daemon.html
[6]: https://www.ibm.com/developerworks/cn/linux/l-cn-nohup/index.html
[7]: http://alfred-sun.github.io/blog/2015/06/18/daemon-implementation/
[8]: http://www.linuxdiyf.com/linux/14117.html
[9]: http://blog.csdn.net/cugxueyu/article/details/2046565
[10]: http://www.cnblogs.com/vamei/archive/2012/10/04/2711818.html
[11]: http://abcdxyzk.github.io/blog/2015/02/11/kernel-sched-signal/
[12]: http://hutaow.com/blog/2013/10/19/linux-signal/
[13]: http://blog.csdn.net/mylizh/article/details/38385739
[14]: http://dangzhiqiang.blog.51cto.com/7961271/1721396
[15]: http://www.netpc.com.cn/2240.html
[16]: http://blog.csdn.net/theone10211024/article/details/13774669
[17]: http://www.cnblogs.com/balaamwe/archive/2012/01/16/2323727.html