# id的概念
## 实际用户ID（RUID）
实际用户ID(real user id)，用于标识一个系统中用户是谁，一般是在登录之后就被唯一的确定，是登录的用户的uid


## 有效用户ID（EUID）
有效用户ID（effective user id），用于系统对进程的的访问权限进行检查，默认和实际用户ID一样


## 设置用户ID位（SUID）
用于对外的权限开放，它的作用是修改进行的有效用户ID，给进程赋予临时的特权，仅限可执行文件拥有这个标志位


## 保存的设置用户ID
是有效用户ID副本，既然是有效用户ID的副本，那么它的作用肯定是为了以后恢复有效用户ID，仅限可执行文件拥有这个标志位


## 进程的id
- 默认情况下进程的id就是启动进程时实际用户的id，权限检查时就是根据该id拥有的权限进行检查
- 有时需要修改进程的id，来提升（例如sudo和suid）或降低权限（例如nginx的worker进程和ubuntu中的rsyslog）
- 由于实际用户id是固定不变的，所以进程使用有效用户id来切换权限


# id详解
## 权限测试流程
测试的参与者是进程的有效用户id、有效组id、文件的拥有者id、文件拥有者组id

1. 进程的有效用户id是0（超级用户），则允许访问
2. 进程的有效用户id等于文件拥有者id，则按照拥有者的权限访问
3. 进程有效组id或附加组id之一等于文件拥有者组id，则按照文件拥有者组的权限访问
4. 否则，按照文件的其他用户访问权限访问
5. 如果没有权限，则提示permission denied


## 设置用户id和设置组id
1. 当文件的设置用户id位和设置组id位没有打开，进程的有效用户id和有效组id保持不变，严格按照权限测试流程测试
2. 文件的设置用户id位和设置组id位被打开，exec函数会把进程的有效用户id和有效组id设置为文件拥有者的用户id和组id，这时再进行权限测试，进程就拥有了和文件拥有者一样的访问权限
3. 保存的设置用户id会用来恢复被改变的有效用户ID

## seteuid函数
- 特权用户可以设置有效用户id为任意实际用户ID
- 非特权用户只能将有效有户ID设置为自己的实际用户ID或保存的设置用户ID



# 案例分析
1. 对于linux系统来说，用户的密码都存放在/etc/shadow文件下
```
➜  ~ ll /etc/passwd
-rw-r--r--. 1 root root 2681 8月  16 17:29 /etc/passwd
```
2. /etc/passwd属于root用户，按照权限的知识，普通用户是无法修改该文件的，但是可以却通过passwd命令修改自己的密码
```
➜  ~ ll /usr/bin/passwd
-rwsr-xr-x. 1 root root 27832 6月  10 2014 /usr/bin/passwd
```
3. passwd设置了suid位，使得进程在执行时临时改变了EUID，从而普通用户也能修改/etc/passwd文件

更多信息可以参考[这里][1]


<br/>

---

# 参考

[无死角理解保存的设置用户ID，设置用户ID位，有效用户ID，实际用户ID][1]

[1]: http://www.cnblogs.com/stemon/p/5287631.html