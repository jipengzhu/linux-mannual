# 前言
熟练掌握shell编程和调试是成为一名优秀的unix/linux开发者和系统管理员的必经之路

常用的调试手段
- 分析输出的错误信息
- 在脚本中加入调试语句，输出调试信息
- 利用调试工具


但与其它高级语言相比，shell解释器缺乏相应的调试机制和调试工具的支持，其输出的错误信息又往往很不明确



# 调试方法
## trap命令
```
trap <command> <signal>
```

系统信号
```
[root@zhujipeng test]# kill -l
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

|系统信号 | 说明|
|--- |--- |
|SIGHUP | 用户终端连接(正常或非正常)结束时发出 |
|SIGINT | 进程终止(interrupt)信号， 结束前台进程 |
|SIGTERM | 进程终止(terminate)信号，进程平稳结束 |
|SIGKILL | 进程终止(kill)信号，进程立即结束，不能被捕获 |
|SIGUSR1 | 留给用户使用 |
|SIGUSR2 | 留给用户使用 |
> SIGTERM、SIGKILL、SIGINT和SIGQUIT的区别参考[这里][2]


|伪信号 | 说明 |
|--- |--- |
|EXIT | 从一个函数中退出或整个脚本执行完毕发出 |
|ERR | 当一条命令返回非零状态时(代表命令执行不成功)发出 |
|DEBUG | 脚本中每一条命令执行之前发出 |
> “伪信号”是因为这三个信号是由shell产生的

```
[root@zhujipeng test]# cat test.sh
error_trap() {
  echo "[Line $1] Error: command or function exited with status $?"
}

exit_trap() {
  echo "[Line $1] INFO: exit method"
}

foo() {
  false
}

bar() {
  for i in {1..10}
  do
    sleep 1
  done
}

trap 'error_trap $LINENO' ERR
trap 'exit_trap $LINENO' EXIT
trap 'echo abort by user $USER; exit 1' INT

abc
foo
bar
[root@zhujipeng test]# sh test.sh
test.sh: line 24: abc: command not found
[Line 24] Error: command or function exited with status 127
[Line 10] Error: command or function exited with status 1
^Cabort by user
[Line 1] INFO: exit method
```


## tee命令
管道的中间结果并不会显示在屏幕上，需要使用 `tee` 命令输出到文件观察

```
[root@zhujipeng test]# cat test.sh
ifconfig | grep 'inet addr:' | grep -v '127.0.0.1'
ifconfig | grep 'inet addr:' | tee /tmp/test.txt | grep -v '127.0.0.1'

echo 'content of test.txt'
cat /tmp/test.txt
[root@zhujipeng test]# sh test.sh
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
content of test.txt
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet addr:127.0.0.1  Mask:255.0.0.0
```


## 勾子函数
```
[root@zhujipeng test]# cat test.sh
debug() {
  [ x"$DEBUG" = x"true" ] && echo $*
}

echo debug
debug haha hehe
[root@zhujipeng test]# sh test.sh
debug
[root@zhujipeng test]# DEBUG='true' && sh test.sh
debug
```


## 调试开关
`shell` 命令有一些选项可以帮助调试

|选项 | 说明 |
|-n | 只读取脚本，但不实际执行，用于检查是否有语法错误 |
|-x | 显示每一条命令的执行过程，是调试脚本的强有力工具 |
|-c | 从字符串中读取命令并执行，用来临时测试一小段脚本 |

当脚本非常庞大时，`-x` 的输出会很多，这时可以使用 `set -x`命令 
```
[root@zhujipeng test]# cat test.sh
foo() {
  echo haha
}

echo call foo
foo
echo

echo debug foo
set -x
foo
set +x
echo

echo call foo
foo
[root@zhujipeng test]# sh test.sh
call foo
haha

debug foo
+ foo
+ echo haha
haha
+ set +x

call foo
haha
```

## 脚本变量
对于复杂的shell脚本的调试来说，需要输出行号和函数等相关信息

|变量 | 说明 |
|--- |--- |
|LINENO | 当前行号，类似于C语言中的内置宏`__LINE__` |
|FUNCNAME | 函数名称，类似于C语言中的内置宏`__func__` |
|PS4 | 调试时输出的前缀，缺省的$PS4的值是"+"号 |
> 不是所有的shell都支持这些变量

```
[root@zhujipeng test]# cat test.sh
PS4="[+$LINENO:${FUNCNAME[0]}]"
echo haha
[root@zhujipeng test]# sh -x test.sh
+ PS4='[+1:]'
[+1:]echo haha
haha
```






<br/>

---

# 参考

[Shell脚本调试技术][1]  
[SIGTERM、SIGKILL、SIGINT和SIGQUIT的区别][2]  

[1]: https://www.ibm.com/developerworks/cn/linux/l-cn-shell-debug/index.html
[2]: http://blog.csdn.net/dai_xiangjun/article/details/41871647