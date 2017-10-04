# 进程管理
## 进程组
一个或多个***进程***的集合


## 作业
一个或多个***进程***的集合
- shell可以进行作业控制，可以运行一个前台作业和多个后台作业
- 如果作业中的某个进程又创建了子进程，则子进程不属于该作业
- 作业运行结束后如果前台进程不存在，shell就把自己提到前台


## 会话
一个或多个***进程组***的集合

- 通常一个会话开始于用户登录，终止于用户退出，在此期间该用户运行的所有进程都属于这个会话期
- 会话包括控制进程（会话首进程），一个前台进程组和任意多个后台进程组
- 一个会话只能有一个控制终端 ，控制终端上的输入和信号将发送给会话的前台进程组中的所有进程



# 进程类型
## 前台进程
一般默认在shell中启动的进程就是前台进程

## 后台进程
脱离终端在后台执行的程序，通常以`d`结尾

## 僵尸进程
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



# nohup
会话中前台进程会收到`SIGHUP`信号而终止，后台进程则由`huponexit`参数决定
```
[root@zhujipeng /]# shopt | grep huponexit
huponexit      	off
```

SIGHUP会在以下3种情况下被发送给相应的进程，详见[这里][9]

1. 终端关闭时，该信号被发送到session首进程以及作为job提交的进程（即用 & 符号提交的进程）
2. session首进程退出时，该信号被发送到该session中的前台进程组中的每一个进程
3. 若父进程退出导致进程组成为孤儿进程组，且该进程组中有进程处于停止状态（收到SIGSTOP或SIGTSTP信号），该信号会被发送到该进程组中的每一个进程


守护进程的启动方法的启动方法参见[这里][5]和[这里][6]


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

[1]: http://www.jianshu.com/p/f64cd61d196c
[2]: https://zhuanlan.zhihu.com/p/21250530
[3]: http://www.cnblogs.com/Anker/p/3271773.html
[4]: http://blog.zhengyi.one/linux-jobs.html
[5]: http://www.ruanyifeng.com/blog/2016/02/linux-daemon.html
[6]: https://www.ibm.com/developerworks/cn/linux/l-cn-nohup/index.html
[7]: http://alfred-sun.github.io/blog/2015/06/18/daemon-implementation/
[8]: http://www.linuxdiyf.com/linux/14117.html
[9]: http://blog.csdn.net/cugxueyu/article/details/2046565