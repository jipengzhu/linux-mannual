# kill
用于像进程发送信号，主要用于杀死进程，详情参考[这里][1]
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
> 信号可以使用上面的数字或单词去掉`SIG`的部分



# lsof
列出打开的文件（list open files），详情参考[这里][2]



# pidof
找出正在运行的程序的进程id，详情参考[这里][5]



# jps
查看Java继承信息，详情参考[这里][6]



# bg 
将后台停止的进程变为运行，详情参考[这里][8]



# fg
将后台运行的进程变为前台进程，详情参考[这里][8]



<br/>

---

# 参考

[linux kill命令详解][1]  
[Linux 命令神器：lsof 入门][2] 
[lsof在Linux中的10个例子][3]   
[lsof print numeric ports][4]  
[我使用过的Linux命令之pidof][5] 
[JVM性能调优监控工具][6]   
[jps出现– process information unavailable解决方法][7]
[Linux的bg和fg命令][8]

[1]: http://www.cnblogs.com/wangcp-2014/p/5146343.html
[2]: https://linux.cn/article-4099-1.html
[3]: http://kumu-linux.github.io/blog/2013/04/08/lsof/
[4]: https://stackoverflow.com/questions/34032299/lsof-print-numeric-ports
[5]: http://codingstandards.iteye.com/blog/841123
[6]: https://my.oschina.net/feichexia/blog/196575
[7]: http://www.ttlsa.com/linux/jps-process-information-unavailable/
[8]: http://blog.csdn.net/zh521zh/article/details/43500795