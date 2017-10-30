# uptime
查看系统的运行时间和平均负载

```
[root@localhost ~]# uptime
 08:10:40 up 5 min,  2 users,  load average: 0.00, 0.03, 0.03
```



# w
查看登录的用户和用户的活动

```
[root@localhost ~]# w
 08:11:54 up 6 min,  2 users,  load average: 0.00, 0.02, 0.03
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1                      08:05    6:34   0.01s  0.01s -bash
root     pts/0    192.168.8.192    08:07    2.00s  0.04s  0.03s w
```



# last
显示用户最近登录信息

```
last [-R] [-num] [ -n num ] [-adFiowx] [ -f file ] [ -t YYYYMMDDHHMMSS ] [name...]  [tty...]
lastb [-R] [-num] [ -n num ] [ -f file ] [-adFiowx] [name...]  [tty...]
```

|选项 | 说明 |
|--- |--- |
|-num | 显示行数 |
|-R | 不显示主机列 |
|-a | 在最后列显示主机名 |
|-d | 显示非本地登录的 |
|-F | 详细的登录和登出时间 |
|-i | 和`-F`大致显示，主机显示为ip |
|-w | 显示完全的用户名和域名 |
|-x | 显示关机和级别转换的信息 |



# shutdown
关闭操作系统，详情[这里][4]



# halt
关闭操作系统，详情[这里][5]



# poweroff
关闭计算机，详情参考[这里][6]



# reboot
重启操作系统，详情[这里][7]


<br/>

---

# 参考

[uptime命令][1]  
[w命令][2]  
[last命令][3]  
[shutdown命令][4]  
[halt命令][5]  
[poweroff命令][6]  
[reboot命令][7]  
[shutdown、halt、poweroff、reboot小结][8]  
[w、who、whoami和which、whereis、tty小结][9]  
[Linux中tty、pty、pts的概念区别][10]  

[1]: http://man.linuxde.net/uptime
[2]: http://man.linuxde.net/w
[3]: http://man.linuxde.net/last
[4]: http://man.linuxde.net/shutdown
[5]: http://man.linuxde.net/halt
[6]: http://man.linuxde.net/poweroff
[7]: http://man.linuxde.net/reboot
[8]: http://bluebox.blog.51cto.com/8852456/1687056
[9]: http://bluebox.blog.51cto.com/8852456/1687136
[10]: http://7056824.blog.51cto.com/69854/276610