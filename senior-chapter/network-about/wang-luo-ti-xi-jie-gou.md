# 体系结构
计算机网络的各层及其协议的集合，称为网络的体系结构


## 网络协议
为进行网络中的数据交换而建立的规则、标准或约定称为网络协议

网络协议主要由以下三要素组成：

1. 语法，即数据与控制信息的结构或格式
2. 语义，即需要发出何种控制信息，完成何种动作以及做出何种相应
3. 同步，即事件实现顺序的详细说明 

网络协议的主要模型为以下两种：

1. OSI模型（7层）
2. TCP/IP模型（5层）


## 网络模型
### OSI模型
OSI模型主要由7层组成

- 应用层（Application Layer）
- 表示层（Presentation Layer）
- 会话层（Session Layer）
- 传输层（Transport Layer）
- 网络层（Network Layer）
- 数据链路层（Data Link Layer）
- 物理层（Pyhsical Layer）

> 传输层也叫运输层，我个人觉得传输层比较顺口

### TCP/IP模型
- 应用层
- 传输层
- 网络层
- 数据链路层
- 物理层

> 网络层也叫网际层，数据链路层和物理层有时也合称为网络接口层

### TCP/IP模型和OSI模型的对应关系
1. 应用层对应OSI模型的应用层、表示层、会话层
2. 传输层对应OSI模型的传输层
3. 网际层对应OSI模型的网络层
4. 网络接口层对应OSI模型的数据链路层、物理层

### 各层的作用和协议
#### 应用层
解决进程之间的消息传递

|协议或应用 | 说明 |
|--- |--- |
|FTP（21)|文件传输协议（File Transfer Protocol）|
|SSH （22）| 远程会话协议（Secure Shell）|
|SMTP（25）| 简单邮件协议（Simple Mail Transfer Protocol）|
|DNS（53）| 域名解析系统（Domain Name System）|
|DHCP（68）| 动态主机配置协议（Dynamic Host Configuration Protocol）|
|TFTP（69）| 简单文件传输协议（Trivial File Transfer Protocol）|
|HTTP（80）| 超文本传输协议（HyperText Transfer Protocol）|
|POP3（110）| 邮局管理协议（Post Office Protocol 3）|
|SFTP（115）| 安全文件传送协议（Secure File Transfer Protocol）
|IMAP4（143）| 邮件访问协议（Internet Message Access Protocol 4）|
|SNMP（161）| 简单网络管理协议（Simple Network Management Protocol）|
|LDAP（389）| 轻型目录访问协议（Lightweight Directory Access Protocol）|
|HTTPS（443）| 加密的超文本传输协议（Hyper Text Transfer Protocol over Secure Socket Layer）|

#### 传输层
解决主机之间的消息传递

|协议或应用 | 说明 |
|--- |--- |
|TCP | 传输控制协议（Transmission Control Protocol）|
|UDP | 用户数据报协议（User Datagram Protocol）|

#### 网络层
解决主机之间的发现识别

|协议或应用 | 说明 |
|--- |--- |
|IP | 网络互联协议（Internet Protocol）|
|ICMP | 网络控制报文协议（Internet Control Message Protocol）|
|IGMP | 网络组组管理协议（Internet Group Management Protocol）|
|IGP | 内部网关协议（Interior Gateway Protocol）|
|RIP | 路由信息协议（Routing Information Protocol）|
|OSFP |开放式最短路径优先（Open Shortest Path First） |
|BGP | 边界网关协议（Border Gateway Protocol）|

#### 数据链路层 
解决网络传输相关的问题

|协议或应用 | 说明 |
|--- |--- |
|ARP | 地址解析协议（Address Resolution Protocol）|
|RARP | 逆地址解析协议（Reverse Address Resolution Protocol）|
|SLIP| 串行线路网际协议（Serial Line Internet Protocol）|
|CSLIP| 压缩的串行线路网际协议（Compressed Serial Line Internet Protocol）|
|PPP| 点对点协议（Point to Point Protocol）|

#### 物理层
解决比特流的传输和电平信号等问题


### 网络分层的好处
1. 功能分工：分层之后各层逻辑清晰以便实现、维护和问题排查
2. 服务复用：避免上一层的每一种协议都得去实现下一层的功能
3. 统一透明：上层不用关心下层是如何实现的和不同实现的细节


<br/>

---

# 参考

[计算机网络体系结构详解（图文）][1]  
[计算机网络之路由协议详解][2]  
[OSI网络体系结构][3]  
[TCP/UDP 常用端口列表][4]  
[FTP主动模式和被动模式的比较][5]  
[SMTP、IMAP和POP3的区别和联系][6]  
[DHCP协议详解][7]  
[SNMP原理与实战详解][8]  
[ldap介绍][9]  
[DHCP原理及配置][10]  
[ICMP协议详解][11]  
[DHCP协议详解][12]  

[1]: http://blog.csdn.net/songkai320/article/details/51754433
[2]: http://blog.csdn.net/songkai320/article/details/51770377
[3]: http://www.cnblogs.com/panjun-Donet/p/3650467.html
[4]: http://blog.csdn.net/joyous/article/details/41806771
[5]: http://jackiechen.blog.51cto.com/196075/193883/
[6]: http://www.jianshu.com/p/fc15b2546ef8
[7]: http://blog.csdn.net/windeal3203/article/details/50677166
[8]: http://freeloda.blog.51cto.com/2033581/1306743/
[9]: http://407711169.blog.51cto.com/6616996/1439543
[10]: http://minux.blog.51cto.com/8994862/1714849
[11]: http://blog.csdn.net/snlying/article/details/4211396
[12]: http://blog.csdn.net/windeal3203/article/details/50677166