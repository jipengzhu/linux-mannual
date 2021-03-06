# 进程和线程
## 基本简介
### 指令（instruction）
计算机可以做的事情实际上非常简单，比如计算和寻址等等，这些最基础的计算机动作被称为指令

### 程序（program）
程序是指能够完成某些复杂操作和功能的指令集合

### 进程（process）
进程是一个程序关于某个数据集合的一次运行活动

### 线程（thread）
线程是系统调度的基本单元以及更加轻量级的进程

### 协程（coroutine）
协程是多入口调度的子程序以及更加轻量级的线程

 
## 区别和联系
详情参考[Linux进程与线程的区别][11]

1. 进程是分配资源的基本单位，线程是调度的基本单位
2. 进程至少有一个主线程，线程是更加轻量级的进程
3. 进程之间各自独占资源，线程之间可以共享资源

> 进程与线程的一个简单解释可以参考[这里][7]

## 线程资源
详情参考[同一进程的线程共享的资源和独有的资源][12]

### 共享的资源
- 进程代码段
- 进程的公有数据
- 进程打开的文件描述符
- 进程的当前目录
- 进程用户ID
- 进程组ID
- 信号的处理器

### 独有的资源
#### 线程ID
每个线程都有自己的线程ID并且这个ID在本进程中是唯一的

#### 寄存器的值
线程必须有自己的寄存器组来保存和恢复线程切换似的状态

#### 线程的堆栈
线程必须有自己的堆栈来保证线程之间独立运行而互不干扰

#### 错误返回码
线程必须有自己的错误返回码来避免错误被其他线程所覆盖

#### 线程优先级
线程必须有自己的优先级来表明线程间不同线程的重要程度

#### 信号屏蔽码
由于每个线程所感兴趣的信号不同，所以线程的信号屏蔽码应该由线程自己管理
> 但所有的线程都共享同样的信号处理器


# 生命周期
1. 新建（New）
2. 就绪（Runnable）
3. 运行（Running）
4. 阻塞（Blocked）
5. 死亡（Dead）

### Java线程阻塞的情况

1. 线程在请求一个被其他线程持有的锁
2. 线程调用了一个阻塞式`IO`的操作 
3. 线程调用了`sleep`方法暂停执行
4. 线程调用了`wait`方法等待唤醒
5. 线程调用了`suspend`方法挂起

> `suspend`容易导致死锁，不推荐

### Java线程死亡的情况

1. `run`方法结束，线程正常结束
2. 线程抛出一个了未被捕获的异常
3. 调用线程的`stop`方法来结束线程

> `stop`容易导致死锁，不推荐



# 进程结构
进程结构由进程控制块（PCB）（process control block）描述，详情参见[这里][8]

主要包含以下几部分

1. 进程标识信息
2. 进程调度信息
3. 进程控制信息 
4. 处理机的状态
5. 进程的数据段


## 进程标识信息
### 内部标志符 
由操作系统为每个进程生成的一个唯一的数字标识符，称为进程号（pid）（process identity descriptor）

### 外部标识符
由创建者产生的附加信息，是由字母和数字组成的字符串，例如进程名


## 进程调度信息
### 进程的状态
标识进程的当前状态（就绪、运行、阻塞）

### 进程优先级
表示进程获得处理机使用权的优先程度

### 其他的信息
为进程调度算法提供依据的其他信息
> 例如进程等待时间、进程已经获得处理器的总时间和进程占用内存的时间等


## 进程控制信息
### 程序和数据地址
组成进程的程序和数据所在内存或外存中的首地址以及相关段信息

### 进程同步和通信机制
指实现进程同步和通信时所采取的机制，如消息队列指针和信号量等

### 资源清单
列出了进程所需的全部资源及已经分配给该进程的资源，但不包括CPU



# 线程结构
详情参见[内核线程与用户线程的一点小总结][14]



# 地址空间
详情参见[浅谈进程地址空间与虚拟存储空间][15]


<br/>

---

# 参考

[操作系统 - 进程的概念][1]  
[Linux进程基础][2] 
[Linux进程关系][3]   
[Linux从程序到进程][4]  
[关于进程、线程生命周期的总结][5]  
[进程、进程组、作业、会话][6]  
[进程与线程的一个简单解释][7]  
[进程控制块、进程上下文][8]    
[数据段、代码段、堆栈段、BSS段的区别][9]  
[关于 Linux 进程你所需要知道的一切][10] 
[Linux进程与线程的区别][11]   
[Unix / Linux 线程的实质][12]  
[同一进程的线程共享的资源和独有的资源][13]  
[内核线程与用户线程的一点小总结][14]  
[浅谈进程地址空间与虚拟存储空间][15]  
[what-is-the-difference-between-a-thread-process-task][16]  
[Linux多线程与同步][17]        

[1]: http://www.cnblogs.com/tianlangshu/p/5224178.html
[2]: http://www.cnblogs.com/vamei/archive/2012/09/20/2694466.html
[3]: http://www.cnblogs.com/vamei/archive/2012/10/07/2713023.html
[4]: http://www.cnblogs.com/vamei/archive/2012/10/09/2715388.html
[5]: http://blog.csdn.net/amosilin/article/details/51077930
[6]: http://www.jianshu.com/p/f64cd61d196c
[7]: http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html
[8]: http://blog.csdn.net/cooling88/article/details/53074038
[9]: http://blog.csdn.net/jxhui23/article/details/8064766
[10]: http://mp.weixin.qq.com/s/ixDqEK1KyJs9iitxgspAww
[11]: https://my.oschina.net/cnyinlinux/blog/422207
[12]: https://my.oschina.net/cnyinlinux/blog/367910
[13]: http://www.cnblogs.com/tracylee/archive/2012/10/29/2744228.html
[14]: http://www.jianshu.com/p/5a4fc2729c17
[15]: http://blog.csdn.net/tennysonsky/article/details/45092229
[16]: https://stackoverflow.com/questions/3042717/what-is-the-difference-between-a-thread-process-task
[17]: http://www.cnblogs.com/vamei/archive/2012/10/09/2715393.html