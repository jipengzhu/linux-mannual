# 任务调度
Linux下的任务调度分为两类

1. 系统任务调度
2. 用户任务调度

## 系统任务调度
系统任务的调度信息位于`/etc/crontab`，需要通过修改文件来添加

```
[root@localhost ~]# cat /etc/crontab
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed
```

|字段 | 说明 |
|--- |--- |
|SHELL | 运行时使用的shell |
|PATH | 命令的搜索路径 |
|MAILTO | 接收电子邮件的用户 |


|列 | 说明 |
|--- |--- |
|minute | 指定分钟(0 - 59) |
|hour | 指定小时(0 - 23) |
|day of month| 指定一月中的第几天(1 - 31) |
|month | 指定月份(1 - 12) |
|day of week | 指定星期几(0 - 6) |
|user-name| 指定用户名 |
|command to be executed | 需要执行的命令 |


## 用户任务调度
用户任务的调度信息位于`/var/spool/cron`，文件名为用户名，可以通过`crontab`命令来配置

```
crontab [-u user] file
crontab [-u user] [-l | -r | -e] [-i] [-s]  
```

> 注意：`crontab`指定文件时会覆盖原来的定时任务

|选项 | 说明 |
|--- |--- |
|-u | 指定用户 |
|-l | 显示定时任务 |
|-r | 清空定时任务 |
|-e | 编辑定时任务 |
|-i | 提示用户选择 |

`crontab`每行的语法和系统任务调度一样，只是没有用户列


## 时间格式
定时任务的时间除了使用数字，还可以使用以下特殊字符

- *： 该时间字段的所有值
- ,： 指定列表范围
- -： 指定连续范围
- /： 指定时间频率


## 时间示例
每小时的第1分钟执行一次
```
1 * * * *
```

每天的0点第1分钟执行一次
```
1 0 * * *
```

每1分钟执行一次
```
* * * * *
```

每15分钟执行一次
```
*/15 * * * *
```

每小时的第7分和13分执行一次
```
7,13 * * * *
```

每天的第8点到第12点第7分和13分执行一次
```
7,13 8-12 * * *
```

每3个小时的第7分和13分执行一次
```
7,13 */3 * * *
```

每周六的第7分和13分执行一次
```
7,13 * * * 6
```

每季度的周六的第7分和13分执行一次
```
7,13 * * */3 6
```


## 周期执行
可以将脚本放到`/etc`中`crontab`相关的目录下执行

```
[root@localhost ~]# ls /etc/cron.d /etc/cron*ly -d -1
/etc/cron.d
/etc/cron.daily
/etc/cron.hourly
/etc/cron.monthly
/etc/cron.weekly
```

比如`logrotate`的定时任务文件

```
[root@localhost ~]# cat /etc/cron.daily/logrotate
#!/bin/sh

/usr/sbin/logrotate -s /var/lib/logrotate/logrotate.status /etc/logrotate.conf
EXITVALUE=$?
if [ $EXITVALUE != 0 ]; then
    /usr/bin/logger -t logrotate "ALERT exited abnormally with [$EXITVALUE]"
fi
exit 0
```

上面的`cron`相关的文件下面的文件中被调度的

```
[root@localhost ~]# cat /etc/cron.d/0hourly
# Run the hourly jobs
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
01 * * * * root run-parts /etc/cron.hourly

[root@localhost ~]# cat  /etc/anacrontab
# /etc/anacrontab: configuration file for anacron

# See anacron(8) and anacrontab(5) for details.

SHELL=/bin/sh
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
# the maximal random delay added to the base delay of the jobs
RANDOM_DELAY=45
# the jobs will be started during the following hours only
START_HOURS_RANGE=3-22

#period in days   delay in minutes   job-identifier   command
1	5	cron.daily		nice run-parts /etc/cron.daily
7	25	cron.weekly		nice run-parts /etc/cron.weekly
@monthly 45	cron.monthly		nice run-parts /etc/cron.monthly
```


## 时间冲突
`crontab`表达式中，前面4项的关系之间为`与`的关系，需要同时满足才执行，星期列跟其他是`或`的关系


## 脚本添加
可以通过脚本将定时任务追加到`/var/spool/cron`下对应用户的文件中去


<br/>

---

# 参考

[crontab命令][1]  
[每天一个linux命令：crontab命令][2]  
[请问centos系统/etc/cron.daily/下的脚本，是在哪里设置的定时执行呢][3]  
[crontab 如果日期和星期冲突时,会如何执行][4]  
[linux下利用shell脚本实现添加crontab任务][5]  

[1]: http://man.linuxde.net/crontab
[2]: http://www.cnblogs.com/peida/archive/2013/01/08/2850483.html
[3]: http://bbs.chinaunix.net/thread-4146297-1-1.html
[4]: https://segmentfault.com/q/1010000010790162/
[5]: http://www.cnblogs.com/wangfantasy/p/3447601.html