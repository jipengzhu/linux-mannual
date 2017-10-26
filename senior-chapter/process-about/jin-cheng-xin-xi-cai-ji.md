# vmstat
采集内存的相关信息

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


<br/>

---

# 参考

[Linux vmstat命令实战详解][1]  
[Linux IO实时监控iostat命令详解][2]  
[使用vmstat和iostat命令进行Linux性能监控][3]  

[1]: http://www.cnblogs.com/ggjucheng/archive/2012/01/05/2312625.html 
[2]: http://www.cnblogs.com/ggjucheng/archive/2013/01/13/2858810.html
[3]: https://linux.cn/article-4024-1.html