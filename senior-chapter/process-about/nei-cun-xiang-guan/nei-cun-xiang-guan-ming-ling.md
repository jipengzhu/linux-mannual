# free 
查看内存的使用情况

```
free 选项
```
|选项 | 说明 |
|--- |--- |
|-b, --bytes | 以字节（Byte）为单位显示 |
|-k, --kilo | 以千字节（）为单位显示|
|-m, --mega | 以兆字节（MegaByte）为单位显示 |
|-g, --giga | 以吉字节（GigaByte）为单位显示 |
|--tera | 以太字节（TeraByte）为单位显示 |
|-h, --human | 自动决定更友好的显示单位 |
|--si | 使用1000而不使用1024进位 |
|-t, --total | 显示总计行 |


## 输出详解
```
[root@zhujipeng /]# free -m
             total       used       free     shared    buffers     cached
Mem:          1999        268       1730        161          5        166
-/+ buffers/cache:         97       1901
Swap:         3994          0       3994
```
|输出 | 说明 |
|--- |--- |
|total	| 物理内存总数 |
|used	| 已经使用的内存数 |
|free	| 空闲的内存数 |
|shared	| 多个进程共享的内存数 |
|buffers | Buffer缓存内存数 |
|cached | Page缓存内存数 |
|-buffers/cache	| 减去`buffers/cache`后使用的内存数 |
|+buffers/cache	| 加上`buffers/cache`后剩余的内存数 |
|Swap	| 交换分区，虚拟内存 |
> `free + buffers + cached + Swap` 是实际可用的内存


<br/>

---

# 参考

[显示系统中空闲和已使用的内存][5]  
[Linux 内存 buffer 和 cache 的区别][6]  
[What is the difference between buffer vs cache memory in Linux][7]  
[Linux Swap交换分区介绍总结][8]  
[Linux 内存中Page cache和buffer cache 的区别][9]  
[linux系统缓存机制][10]  
[Linux 内核的文件 Cache 管理机制介绍][11]  
[手工释放linux内存——/proc/sys/vm/drop_cache][12]   

[5]: https://linux.cn/article-2443-1.html
[6]: http://blog.csdn.net/tianlesoftware/article/details/6459044
[7]: https://stackoverflow.com/questions/6345020/what-is-the-difference-between-buffer-vs-cache-memory-in-linux
[8]: http://www.cnblogs.com/kerrycode/p/5246383.html
[9]: http://blog.csdn.net/haiross/article/details/39478959
[10]: http://lizhenliang.blog.51cto.com/7876557/1657448
[11]: https://www.ibm.com/developerworks/cn/linux/l-cache/index.html
[12]: http://blog.csdn.net/wyzxg/article/details/7279986/
