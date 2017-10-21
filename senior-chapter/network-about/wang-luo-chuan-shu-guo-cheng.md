# 数据包传输过程
## 发送过程
1. 程序的**数据**（Data）通过Socket调用从**应用层**发送到**传输层**
2. TCP传输时，传输层为数据添加**TCP**头信息形成**数据段**（Segment），并发送到**网络层**
3. UDP传输时，传输层为数据添加**UDP**头信息形成**数据报**（Datagram），并发送到**网络层**
4. 网络层为数据段或数据报添加**IP**头信息形成**数据包**（Packet），并发送到**数据链路层**
5. 数据链路层为数据包添加**MAC**头信息形成**数据帧**（Frame），并发送到**物理层**
6. 物理层负责将数据帧转化为**比特流**（Bit Stream），并发送出去

## 接收过程
1. **物理层**负责将接收到的**比特流**（Bit Stream）化为数据帧转，并发送到**数据链路层**
2. 数据链路层去掉**数据帧**（Frame）中的**MAC**头信息形成数据包，并发送到**网络层**
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
|Message| 消息 | 应用层数据的称呼 |
|Segment | 数据段 | TCP传输时传输层数据的称呼 |
|Datagram | 数据报 | UDP传输时传输层数据的称呼 |
|Packet | 数据包 | 网络层数据的称呼 |
|Frame | 数据帧 | 数据链路层的数据的称呼 |
|MTU |（Maximum Transmission Unit）最大传输单元| 数据链路层的最大传输单元（不包含头信息）|
|MSS |（Maximum Segment Size）| 最大传输段大小 | TCP提交给IP层最大分段大小 |

通常发送请求的一方称为客户端，响应请求的一方称为服务端



# TCP传输
## 三次握手


## 四次挥手


## 分片机制


## 窗口机制


## 拥塞机制


## 失败重传


## 信息校验



# UDP传输


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