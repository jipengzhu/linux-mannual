# 进程通信
有时候进程间需要协作来完成某项功能，典型的如[Master-Worker模型][1]，这时候就需要进行进程间通信



# IPC
进程间通信（Inner Process Communication）


## 进程通行方式
进程间采用的通信方式要么需要切换内核上下文，要么要与外设访问(有名管道，文件)，所以速度会比较慢

1. 共享内存（shared memory）
2. 消息队列（message queue）
3. 有名管道（named pipe）
4. 无名管道（pipe）
5. 信号量（semaphore）
6. 信号（signal）
7. 文件（file）
8. 套接字（socket）


## 线程通信方式
除了可以使用进程的通信方式，还可以使用

1. 全局变量
2. 条件变量
3. 线程信号
4. 互斥量
5. 读写锁 
6. 自旋锁



# RPC
远程过程调用（Remote Procedure Call），详情参考[这里][16]


<br/>

---

# 参考

[python使用master worker管理模型开发服务端][1]  
[并行程序设计模式--Master-Worker模式][2]  
[进程间、线程间通信方式小结][3]  
[深刻理解Linux进程间通信（IPC）][4]  
[Linux进程与线程的区别][5]  
[Linux进程间通信——使用共享内存][6]  
[Linux进程间通信——使用消息队列][7]  
[Linux进程间通信——使用命名管道][8]  
[Linux进程间通信——使用匿名管道][9]  
[Linux进程间通信——使用信号量][10]  
[Linux进程间通信——使用信号][11]  
[Linux进程间通信——使用流套接字][12]  
[浅析线程间通信一：互斥量和条件变量][13]  
[浅析线程间通信二：读写锁和自旋锁][14]  
[Linux线程编程之信号处理][15]  
[RPC综述 - PB, Thrift, Avro][16]  
[谁能用通俗的语言解释一下什么是 RPC 框架][17]  

[1]: http://xiaorui.cc/2015/07/13/python%E4%BD%BF%E7%94%A8master-worker%E7%AE%A1%E7%90%86%E6%A8%A1%E5%9E%8B%E5%BC%80%E5%8F%91%E6%9C%8D%E5%8A%A1%E7%AB%AF/
[2]: http://www.cnblogs.com/lcngu/p/5309101.html
[3]: http://blog.csdn.net/alexlee1986/article/details/21227417
[4]: https://www.ibm.com/developerworks/cn/linux/l-ipc/index.html
[5]: https://my.oschina.net/cnyinlinux/blog/422207
[6]: http://blog.csdn.net/ljianhui/article/details/10253345
[7]: http://blog.csdn.net/ljianhui/article/details/10287879
[8]: http://blog.csdn.net/ljianhui/article/details/10202699
[9]: http://blog.csdn.net/ljianhui/article/details/10168031
[10]: http://blog.csdn.net/ljianhui/article/details/10243617
[11]: http://blog.csdn.net/ljianhui/article/details/10128731
[12]: http://blog.csdn.net/ljianhui/article/details/10477427
[13]: http://blog.csdn.net/maximuszhou/article/details/42318169
[14]: http://blog.csdn.net/MaximusZhou/article/details/43938295
[15]: http://www.cnblogs.com/clover-toeic/p/4126594.html
[16]: http://www.cnblogs.com/fxjwind/archive/2013/05/16/3082219.html
[17]: https://www.zhihu.com/question/25536695