# vmstat
采集进程的相关信息

```
vmstat [options] [delay [count]]
```

|选项 | 说明 |
|--- |--- |
|-n, --one-header | 只显示一次头部信息 |
|-s, --stats | 显示统计信息 |
|-S, --unit &lt; character &gt; | 指定k或m来更友好的显示 | 


## 输出格式
```
[root@zhujipeng /]# vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 3  0 2253612 2016736 256864 8466484    0    1    27   230    0    1  5  1 94  0  0
```

|字段 | 说明 |
|--- |--- |
|r | 处于运行态和就绪态的进程 |
|b | 处于阻塞态的进程 |
|swpd | 交换内存已使用的大小 |
|free | 空闲的物理内存的大小 |
|buff | 系统的缓存内存 |
|cache | 文件的缓存内存 |
|si | 每秒从磁盘读入虚拟内存的大小 |
|so | 每秒从虚拟内存写入磁盘的大小 |
|bi | 块设备每秒接收的块数量 |
|bo | 块设备每秒发送的块数量 |
|in | 每秒CPU的中断次数 |
|cs | 每秒上下文切换次数 |
|us | 用户CPU时间 |
|sy | 系统CPU时间 |
|id | 空闲CPU时间 |
|wa | 等待IO完成的CPU时间 |



# iostat
采集磁盘的统计信息

```
iostat [ -c ] [ -d ] [ -h ] [ -k | -m ] [ -N ] [ -t ] [ -V ] [ -x ] [ -y ] [ -z ] [ -j {  ID  |  LABEL  |
       PATH  |  UUID  | ... } ] [ [ -T ] -g group_name ] [ -p [ device [,...] | ALL ] ] [ device [...] | ALL ] [
       interval [ count ] ]
```

|选项 | 说明 |
|--- |--- |
|-c | 显示cpu相关的信息 |
|-d | 显示设备相关的信息 |
|-h | 设备信息的显示结果对人类更友好 |
|-k | 以千字节为单位显示 |
|-m | 以兆字节为单位显示 |
|-t | 输出时间信息 |
|-x | 显示额外的信息 |
|-z | 不显示不活跃的设备的信息 |


## 输出格式
```
[root@zhujipeng /]# iostat -m
Linux 3.10.0-327.36.3.el7.x86_64 (zhujipeng) 	2017年10月25日 	_x86_64_	(12 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           5.14    0.00    0.90    0.29    0.03   93.64

Device:            tps    MB_read/s    MB_wrtn/s    MB_read    MB_wrtn
vda               2.50         0.01         0.02      46194     101982
vdb               0.20         0.00         0.01      15674      33398
vdc              71.84         0.30         2.62    1476509   12934514

[root@zhujipeng /]# iostat -x
Linux 3.10.0-327.36.3.el7.x86_64 (mty-004) 	2017年10月25日 	_x86_64_	(12 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           5.14    0.00    0.90    0.29    0.03   93.64

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
vda               0.00     0.07    0.22    2.29     9.57    21.13    24.54     0.00    1.32    1.94    1.26   0.48   0.12
vdb               0.69     1.64    0.12    0.09     3.25     6.92    99.77     0.01   35.71    0.48   83.86   0.92   0.02
vdc               0.00   104.90   13.16   58.68   305.90  2680.04    83.12     0.49    6.81    1.52    7.99   0.31   2.26
```

|字段 | 说明 |
|--- |--- |
|%user | 用户cpu时间百分比 |
|%nice | 改变过优先级的进程的占用CPU的百分比 |
|%system | 系统cpu时间百分比 |
|%iowait | 等待IO完成cpu时间百分比 |
|%steal | `Hypervisor`分配给运行在其它虚拟机上的任务的实际cpu时间 |
|%idle| 空闲cpu时间百分比 |
|tps | io吞吐量 |
|MB_read/s| 每秒读取速度（本例中单位为兆）|
|MB_wrtn/s| 每秒写入速度（本例中单位为兆）|
|MB_read| 已读取的数据大小（本例中单位为兆）|
|MB_wrtn| 已写入的数据大小（本例中单位为兆）|
|rrqm/s | 每秒读请求被文件系统合并的数量 |
|wrqm/s | 每秒写请求被文件系统合并的数量 |
|r/s | 每秒读请求的数量 |
|w/s | 每秒写请求的数量 |
|rkB/s | 每秒读取数据的大小（单位为千字节）|
|wkB/s | 每秒写入数据的大小（单位为千字节）|
|avgrq-sz | 请求扇区的平均大小 |
|avgqu-sz | 请求队列的平均长度 |
|await | IO请求响应的平均时间（单位是毫秒）|
|r_await | IO读请求响应的平均时间（单位是毫秒）|
|w_await | IO写请求响应的平均时间（单位是毫秒）|
|svctm | 每次设备I/O操作的服务时间（单位是毫秒） |
|%util| 统计时间内所有处理IO时间比率 |
> `%util` 暗示了设备的繁忙程度，如果是多磁盘，即使%util是100%，磁盘使用未必就到了瓶颈



# sar(System Activity Reporter)
监控Linux系统的活动状况，详情参见[这里][19]

<br/>

---

# 参考

[Linux vmstat命令实战详解][1]  
[Linux CPU实时监控mpstat命令详解][2]  
[Linux IO实时监控iostat命令详解][3]  
[Linux 运行进程实时监控pidstat命令详解][4]  
[使用vmstat和iostat命令进行Linux性能监控][5]  
[剖析 Linux hypervisor][6]  
[虚拟化 - KVM 和 Xen 比较][7]  
[对比Xen和KVM：Linux虚拟化技术选择][8]  
[KVM详解，太详细太深入了，经典][9]  
[LXC(Linux containers)快速入门][10]  
[谈谈 OpenStack 与 Docker 的落地方案选择][11]
[Docker学习笔记 — Docker与LXC的区别][12]  
[Docker学习笔记1——为啥要用Docker][13]    
[Docker学习笔记2——Docker Toolbox是啥][14]  
[Docker学习笔记3——Docker vs KVM][15]  
[Docker学习笔记4——Docker Volume][16]   
[Docker Toolbox利器让你更愉快地使用容器][17]  
[Docker Machine、Swarm、Compose][18]  
[Linux使用sar进行性能分析][19]

[1]: http://www.cnblogs.com/ggjucheng/archive/2012/01/05/2312625.html 
[2]: http://www.cnblogs.com/ggjucheng/archive/2013/01/13/2858775.html
[3]: http://www.cnblogs.com/ggjucheng/archive/2013/01/13/2858810.html
[4]: http://www.cnblogs.com/ggjucheng/archive/2013/01/13/2858874.html
[5]: https://linux.cn/article-4024-1.html
[6]: https://www.ibm.com/developerworks/cn/linux/l-hypervisor/
[7]: http://www.cnblogs.com/sammyliu/articles/4389981.html
[8]: http://blog.chinaunix.net/uid-30022178-id-5749329.html
[9]: http://blog.csdn.net/qq_2632356095/article/details/24668979
[10]: http://www.cnblogs.com/lisperl/archive/2012/04/15/2450183.html
[11]: http://dockone.io/article/1690
[12]: http://blog.csdn.net/wangtaoking1/article/details/45043523
[13]: http://www.jianshu.com/p/0e598643334b
[14]: http://www.jianshu.com/p/d248ba49ec3e
[15]: http://www.jianshu.com/p/ca7d5438ce1e
[16]: http://www.jianshu.com/p/3507f262081e
[17]: http://www.ywnds.com/?p=9146
[18]: http://dockone.io/question/160
[19]: http://blog.csdn.net/xusensen/article/details/54606401