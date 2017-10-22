# 数据包传输过程
## 发送过程
1. 程序的**数据**（Data）通过Socket调用从**应用层**发送到**传输层**
2. TCP传输时，传输层为数据添加**TCP**头信息形成**数据段**（Segment），并发送到**网络层**
3. UDP传输时，传输层为数据添加**UDP**头信息形成**数据报**（Datagram），并发送到**网络层**
4. 网络层为数据段或数据报添加**IP**头信息形成**数据包**（Packet），并发送到**数据链路层**
5. 数据链路层为数据包添加**Frame**头信息形成**数据帧**（Frame），并发送到**物理层**
6. 物理层负责将数据帧转化为**比特流**（Bit Stream），并发送出去

## 接收过程
1. **物理层**负责将接收到的**比特流**（Bit Stream）化为数据帧转，并发送到**数据链路层**
2. 数据链路层去掉**数据帧**（Frame）中的**Frame**头信息形成数据包，并发送到**网络层**
3. 网络层去掉**数据包**（Packet）中的**IP**头信息形成数据段或数据报，并发送到**传输层**
4. TCP传输时，传输层去掉**数据段**（Segment）中的TCP头信息，并返回给**应用层**
5. UDP传输时，传输层去掉**数据报**（Datagram）中的UDP头信息，并返回**给应用层**
6. 程序通过Socket调用从**应用层**获得需要的**数据**（Data）

整个过程大致是这样的，但是每一层的处理都隐含了非常多的细节

## 名词介绍
|缩写| 翻译 | 名词 |
|--- |--- |
|PDU |（Protocol Data Unit）协议数据单元 | PDU是发送机器上每层发送到接收机器上相应层的信息的称呼 |
|SDU |（Service Data Unit）服务数据单元 | SDU是在同一机器上的两层之间传送的信息的称呼 |
|Message| 报文 | 应用层数据的称呼 |
|Segment | 数据段 | TCP传输时传输层数据的称呼 |
|Datagram | 数据报 | UDP传输时传输层数据的称呼 |
|Packet | 数据包 | 网络层数据的称呼 |
|Frame | 数据帧 | 数据链路层的数据的称呼 |
|MTU |（Maximum Transmission Unit）最大传输单元| 数据链路层的最大传输单元（不包含头信息）|
|MSS |（Maximum Segment Size）| 最大传输段大小 | TCP提交给IP层最大分段大小 |



# TCP传输
tcp是面向连接的流式传输协议，具有以下特点

1. 面向连接：通信双方都需要建立连接和释放链接
2. 传输可靠：能够保证数据的完整性、顺序性、正确性
3. 流量可控：通过滑动窗口和拥塞机制来进行流量的控制

## 三次握手
三次握手是指TCP建立连接的过程
> 通常发送请求的一方称为客户端，响应请求的一方称为服务端

1. 第一次握手
    - 客户端A获得服务端B的地址后
    - 向服务端B发送连接信息，`SYN=1，seq=x（x为随机产生的值）`
    - 然后客户端A进入`SYN_SEND`状态
    
2. 第二次握手
    - 服务端B收到客户端A的连接请求，确认`SYN=1`后
    - 向客户端A发送确认信息，`SYN=1，ACK=1，ack=x+1，seq=y（y为随机产生的值）`
    - 然后服务端B从`LISTEN`状态进入到`SYN_RCVD`状态

3. 第三次握手：
    - 客户端A收到服务端B的确认消息，确认`ACK=1`后
    - 检查ack是否是第一次握手是发送的seq的值加1
    - 验证通过则向B发送确认信息，`ACK=1，ack=y+1，seq=x+1`
    - 然后客户端A从`SYN_SEND`状态进入到`ESTABLISHED`状态
    - 服务端B收到客户端A的确认信息，确认`ACK=1`后
    - 检查ack是否是第二次握手是发送的seq的值加1
    - 验证通过则从`SYN_RCVD`状态进入到`ESTABLISHED`状态

三次握手中的任何一次没有成功，都要重新发送
       
### 客户端状态变化
`None`-> `SYN_SEND` -> `ESTABLISHED`

### 服务端状态变化
`LISTEN`-> `SYN_RCVD` -> `ESTABLISHED`

### 为什么需要三次握手
1. 在连接时可能会出现这样的情况，客户端发送了连接请求，但是该信息在某个网络节点滞留时间过长，客户端已经连接超时释放了该连接后，该连接请求到达服务端后
2. 该信息其实是一个过时失效的信息，所以当服务端收到信息后，以为客户端需要建立连接，于是服务端会向客户端发送确认信息
3. 如果不进行第三次握手，就会出现服务端认为是连接并且建立连接，等待客户端发送数据，但是客户端并没有要求建立连接，是不会向服务端发送数据的，所以服务端就会白白的等待客户端发送数据，这样就浪费了服务端的资源

## 四次挥手
四次挥手是指TCP释放连接的过程

1. 第一次挥手
    - 主机1向主机2发起释放连接请求
    - 发送释放请求信息，`FIN=1，seq=u`
    - 然后主机1从`ESTABLISHED`状态进入到`FIN_WAIT_1`状态

2. 第二次挥手
    - 主机2收到主机1的释放连接请求后
    - 回复确认信息，`ACK=1，ack=u+1`
    - 然后主机2从`ESTABLISHED`状态进入到`CLOSE_WAIT`状态
    - 主机1收到主机2的确认信息后
    - 从`FIN_WAIT_1`状态进入到`FIN_WAIT_2`状态
 
3. 第三次挥手
    - 主机2向主机1发起释放连接请求
    - 发送释放请求信息，`FIN=1，seq=v`
    - 然后主机2从`CLOSE_WAIT`状态进入到`LAST_ACK`状态

4. 第四次挥手
    - 主机1收到主机2的释放连接请求后
    - 回复确认信息，`ACK=1，ack=v+1`
    - 然后主机1从`FIN_WAIT_2`状态进入到`TIME_WAIT`状态
    - 主机2收到主机1的确认信息后
    - 从`LAST_ACK`状态进入到`CLOSED`状态
    - 主机1经过2MSL(最大报文生存时间)后从`TIME_WAIT`状态进入到`CLOSED`状态
    
### 主机1状态变化
`ESTABLISHED`-> `FIN_WAIT_1` -> `FIN_WAIT_2` -> `TIME_WAIT` -> `CLOSED`

### 主机2状态变化
`ESTABLISHED`-> `CLOSE_WAIT` -> `LAST_ACK` -> `CLOSED`

### 为什么需要四次挥手
1. 第一次挥手
    - 主机1告诉主机2，我没有数据需要发送了或数据已全部发送完毕
    - 但是此时主机1还可以接收主机2发送的消息
    
2. 第二次挥手
    - 主机2回复确认信息，此时主机2知道主机1没有数据发送了
    - 但是主机2可能还有数据需要发送
    
3. 第三次挥手
    - 主机2告诉主机1，我也没有数据需要发送了或数据已全部发送完毕
    - 此时主机1和主机2都没有数据发送
    
4. 第四次挥手
    - 主机1回复确认信息，主机1知道了主机2也没有数据发送了
    - 但是主机1需要等待2MSL(最大报文生存时间)后才能释放连接
    
### 为什么连接需要三次握手而释放需要四次握手
第二次挥手时主机2可能还有数据要发送给，所以不能回复释放连接信息，只能回复确认信息
> 建立连接的时候服务端收到建立连接的SYN请求后，将ACK和SYN放在一个报文里发送给客户端了。而释放的时候，当收到对方的FIN报文的时候，仅仅表示对方不在发送数据了，但是还可以接收数据，而己方可能还有数据发送，所以己方可以立即close连接或者发送一些数据给对方后再发送FIN报文给对方，表示可以释放连接，所以释放的时候ACK和FIN是分开发送的，所以需要四次挥手

### 为什么需要等2MSL
1. 保证TCP的双全工连接能够可靠关闭  

> 如果直接进入CLOSE状态，由于IP协议的不可靠性或者因为网络原因，主机2没有收到主机1最后回复的ACK，在超时后主机2会继续发送FIN，因为主机1已经没有了与之相对应的连接，最后主机2就会收到RST而不是ACK，主机2会将问题报告给上层处理。虽然这样不会造成数据的丢失，但是这不符合TCP的可靠性要求，所以需要等待，此时主机1进入TIME_WAIT状态，当再次收到FIN的时候，确保主机2能够收到ACK，最后正常的关闭连接


2. 保证这个连接的重复数据在网络中消失

> 如果直接进入了CLOSE状态，然后有向服务端发送新的连接请求。因为不能保证两次连接请求的端口是否一样。如果出现特殊情况，两次端口都一样，旧的连接数据还存在网络中，新的连接建立后，就连接的数据到达服务端，服务端会将其视为新连接传输的数据，这就导致新旧连接的数据混淆了。所以需要等待2MSL的时间，这样才能保证数据从网络中消失

### TIME_WAIT和CLOSE_WAIT
#### TIME_WAIT
- TIME_WAIT是主动关闭连接的一方保持的状态
- 服务器保持大量TIME_WAIT状态，这种情况比较常见
- 一些爬虫服务器，没有做内核优化的话经常会遇到这个问题
- 爬虫服务器本质上就是一个客户端，任务后会主动的关闭连接

#### CLOSE_WAIT
- CLOSE_WAIT是被动关闭连接的一方保持的状态
- 是对方主动关闭连接后服务器没有发出FIN信号导致的
- 应该是程序没有检测对方的关闭请求到或者忘记了关闭连接
- 这种情况无法通过调节内核参数解决，只能查代码然后关闭连接

#### 举例说明
- 服务器A是一台爬虫服务器
- 它使用简单的HttpClient去请求资源服务器B上面的apache获取文件资源
- 正常情况下如果请求成功，那么在抓取完资源后服务器A会主动发出关闭连接的请求
- 这个时候就是主动关闭连接，服务器A的连接状态就是TIME_WAIT
- 如果一旦发生异常呢 ？
- 假设请求的资源服务器B上并不存在
- 那么这个时候就会由服务器B发出关闭连接的请求，服务器A就是被动的关闭了连接
- 如果程序员忘了让HttpClient释放连接，那就会造成CLOSE_WAIT的状态了


## 分片机制
### MTU
在以太网上，由于电气限制，一帧不能超过1518字节，除去以太网帧头14字节（mac地址等）和帧尾4字节校验，还剩1500字节，这个大小称为MTU（最大传输单元）

> 而1492的MTU值的来源，是因为PPPoE协议（TCP/IP以太网无此功能）
PPPoE协议是宽带运营商用于对用户认证计费而设计的
PPPoE头尾一共8字节，所以有效载荷实际为1492

### IP分片
如果你的IP包大于1500字节，IP层就会分片了，详见[这里][6]

### TCP分片
MSS是TCP每次能够传输的最大数据分段，不能超过1460（1500 - 20 - 20），如果数据段大于MSS就会进行TCP分片，所以TCP传输通常不会进行IP分片
> TCP和IP的头信息都是20字节，详情参见[这里][17]

### UDP分片
UDP不会分片，如果数据报大于1472（1500 - 20 - 8），就会进行IP分片，由于UDP是不可靠的传输协议，如果分片丢失就会导致重组失败和数据包被丢弃
> UDP的头信息都是8字节，详情参见[这里][17]


## 窗口机制
详情参见[这里][18]


## 拥塞机制
详情参见[这里][18]


## 失败重传
详情参见[这里][19]


## 信息校验
详情参见[这里][20]


# UDP传输
udp是面向无连接的报文传输协议，具有以下特点

1. 面向无连接：通信双方不需要建立连接和释放链接
2. 不可靠传输：只管将数据发送出去和尽最大努力交付数据
3. 有大小限制：UDP协议规定UDP能够发送最大数据包是64K



# 消息边界
详情参见[这里][8]



# UDP缓冲
详情参见[这里][25]


<br/>

---

# 参考

[细说OSI七层协议模型及OSI参考模型中的数据封装过程][1]  
[Socket与HTTP解析][2]  
[TCP、UDP、IP 协议分析][3]  
[数据帧frame，数据包packet，数据报datagram和数据段segment][4]  
[TCP、UDP区别以及TCP传输原理、拥塞避免、连接建立、连接释放总结][5]  
[TCP分段与IP分片][6]  
[TCP粘包/拆包问题][7] 
[TCP和UDP的"保护消息边界"][8]   
[TCP、UDP数据包大小的限制][9]  
[MTU、MSS、缓存区大小][10]  
[理解TCP序列号（Sequence Number）和确认号（Acknowledgment Number)][11]  
[TCP三次握手四次挥手详解][12]  
[TCP协议中的三次握手和四次挥手(图解)][13]  
[简析TCP的三次握手与四次分手][14]  
[处于CLOSE_WAIT和TIME_WAIT状态连接的原因及解决][15]  
[HTTP TCP UDP Socket 关系][16]  
[ip头、tcp头、udp头详解及定义][17]  
[计算机网络【七】：可靠传输的实现][18]  
[TCP错误恢复特性之一TCP重传][19]  
[TCP新手误区--数据校验的意义][20]  
[TCP的可靠性有多高][21]  
[UDP 和 TCP 的 socket 分别一般用在什么地方][22]  
[TCP与UDP的不同接包处理方式][23]  
[浅谈UDP(数据包长度，收包能力，丢包及进程结构选择)][24] 
[告知你不为人知的UDP-疑难杂症和使用][25]   
[又见CLOSE_WAIT][26]  
[什么是TCP Window][27]  
[IP数据报分片——Fragmentation和重组][28]  
[TCP 的那些事儿（上）][29]  
[TCP 的那些事儿（下）][30]  
[浅谈TCP/IP网络编程中socket的行为][31]  
[计算机网络信道复用技术][32]  

[1]: http://blog.csdn.net/qq_14935437/article/details/71081546
[2]: http://blog.csdn.net/study_zhxu/article/details/55212006
[3]: http://892848153.iteye.com/blog/2200650
[4]: http://blog.csdn.net/rationalgo/article/details/8664453
[5]: http://blog.csdn.net/jeasn168/article/details/39099365
[6]: http://blog.csdn.net/ns_code/article/details/30109789
[7]: http://www.cnblogs.com/wade-luffy/p/6165671.html
[8]: http://blog.csdn.net/zhangxinrun/article/details/6721427
[9]: http://www.cnblogs.com/findumars/p/5356095.html
[10]: https://www.zhihu.com/question/48454744
[11]: http://blog.csdn.net/zhanghuaichao/article/details/52396550
[12]: http://www.cnblogs.com/zmlctt/p/3690998.html
[13]: http://blog.csdn.net/whuslei/article/details/6667471/
[14]: http://www.jellythink.com/archives/705
[15]: http://jschu.blog.51cto.com/5594807/1732414
[16]: http://www.cnblogs.com/ghj1976/p/4295346.html
[17]: http://www.cnblogs.com/shenpengyan/p/5912567.html
[18]: http://blog.chinaunix.net/uid-26275986-id-4109679.html
[19]: http://www.cnblogs.com/huangchaosong/p/7154177.html
[20]: http://blog.csdn.net/bjrxyz/article/details/75194716
[21]: http://www.cnblogs.com/my_life/articles/5367814.html
[22]: https://www.zhihu.com/question/20060141
[23]: http://www.cnblogs.com/thankgoodness/articles/3146069.html
[24]: http://www.cnblogs.com/linuxbug/p/4906000.html
[25]: http://www.cnblogs.com/purpleraintear/p/6403053.html
[26]: http://mp.weixin.qq.com/s?__biz=MzI4MjA4ODU0Ng==&mid=402163560&idx=1&sn=5269044286ce1d142cca1b5fed3efab1&3rd=MzA3MDU4NTYzMw==&scene=6#rd
[27]: http://www.cnblogs.com/awpatp/archive/2013/02/17/2914152.html
[28]: https://my.oschina.net/xinxingegeya/blog/483138
[29]: https://coolshell.cn/articles/11564.html
[30]: https://coolshell.cn/articles/11564.html
[31]: http://www.cnblogs.com/promise6522/archive/2012/03/03/2377935.html
[32]: http://www.itdadao.com/articles/c15a851445p0.html