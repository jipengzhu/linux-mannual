# who
显示登陆的用户

```
who [OPTION]... [ FILE | ARG1 ARG2 ] 
```

|选项 | 说明 |
|--- |--- |
|-a, --all | 显示所有的用户 |
|-b, --boot | 系统最后一次的启动时间 |
|-d, --dead | 显示死亡的进程 |
|-H, --heading | 显示头信息 |
|-l, --login | 显示登录的进程 |
|--lookup | 对主机做DNS查询 |
|-m | 只显示主机和用户名 |
|-p, --process | 显示init进程的子进程 |
|-q, --count | 所有的登录名和总数 |
|-r, --runlevel | 显示运行级别 |
|-s, --short | 显示简短的信息 |
|-t, --time | 显示最后的时钟信息 |
|-T, -w, --mesg | 显示用户的信息 |
|-u, --users | 显示登录的用户 |

```
[root@zhujipeng /]# who
root     pts/0        2017-10-29 14:27 (111.207.151.80)
[root@zhujipeng /]$ whoami
root
[root@zhujipeng /]# su - dig
上一次登录：四 10月 19 16:58:38 CST 2017pts/4 上
[dig@zhujipeng /]$ who
root     pts/0        2017-10-29 14:27 (111.207.151.80)
[dig@zhujipeng /]$ whoami
dig
```



# whoami
查看正在使用的用户名

```
whoami [OPTION]...
```

```
[root@zhujipeng /]# who
root     pts/0        2017-10-29 14:27 (111.207.151.80)
[root@zhujipeng /]$ whoami
root
[root@zhujipeng /]# su - dig
上一次登录：四 10月 19 16:58:38 CST 2017pts/4 上
[dig@zhujipeng /]$ who
root     pts/0        2017-10-29 14:27 (111.207.151.80)
[dig@zhujipeng /]$ whoami
dig
```



# id
显示用户id信息

```
id [OPTION]... [USER]
```
|选项 | 说明 |
|--- |--- |
|-Z, --context | 显示SELinux的安全策略 |
|-g, --group | 显示有效用户组的id |
|-G, --groups | 显示所有用户组的id |
|-n, --name | 显示名称而不是id，配合`-ugG` |
|-r, --real | 显示实际id而不是有效用户id，配合`，配合`-ugG`` |
|-u, --user | 显示有效用户id |


<br/>

---

# 参考

[who、whoami命令 和 who am i 命令的区别][1]  
[id命令][2]  
[linux下进程的实际用户ID（有效组）和有效用户ID（有效组ID）][3]  

[1]: http://www.cnblogs.com/aqxin/archive/2011/05/20/2052075.html
[2]: http://man.linuxde.net/id
[3]: http://www.cnblogs.com/wmllz/p/5040123.html