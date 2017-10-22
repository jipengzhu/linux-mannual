# IP
IP是32位二进制数据，通常以十进制表示，并以“.”分隔，用来标识网络中一个个主机


## IP地址类
早期的IP是按网络号和主机号来划分的，把所有IP地址分为五类

|类别 | 开始位 | 网络号 | 主机号 | 范围 | 主机个数 |
|--- |--- |--- |--- |
|A | 0 | 7 | 24 | 0.0.0.0 - 127.255.255.255| 16777214(2<sup>24</sup> - 2) |
|B | 10 | 14 | 16 | 128.0.0.0 - 191.255.255.255 | 65534(2<sup>16</sup> - 2) |
|C | 110 | 21 | 8 | 192.0.0.0 - 223.255.255.255 | 254(2<sup>8</sup> - 2)|1
> 主机号全为0表示某网络的网络地址，全为1表示某网络的广播地址

|类别 | 开始位 | 剩余位 | 剩余位说明  | 范围 |
|--- |--- |--- |--- |--- |
|D | 1110 |  28 | 多播组号 | 224.0.0.0 - 239.255.255.255 |
|E | 11110 | 27  | 留待后用 | 240.0.0.0 - 255.255.255.255 |

### 分类地址的缺点
随着Internet的飞速发展，分类地址方案的局限性很快显现出

1. C类主机太少，大多数组织都申请B类网络地址，导致B类地址很快就分配完了
2. A类的网络位数较少，生成的网络地址不够用，主机地址却很，多造成了浪费
3. 大量C类网络的出现，路由器需要检索的路由表越来越庞大，负担越来越重


## CIDR（Classless Inter-Domain Routing）
CIDR，无类别域间路由，是一种通过子网掩码来划分网络的技术
> IP地址与子网掩码做与运算能够得到网络地址


## 私有IP
私有IP地址仅用于内部网络使用，不能通过公网访问

|类别 | 范围 |
|--- |--- |
|A | 10.0.0.0 - 10.255.255.255 |
|B | 172.16.0.0 - 172.31.255.255 |
|C | 192.168.0.0 - 192.168.255.255 |
> 小的局域网通常都是`192.168`开头的，详情见[这里][10]


## 广播地址
详情参见[这里][3]


## MAC地址
MAC地址，也称作硬件地址，烧录在NIC(网卡)之中，永远不会变

有了IP地址，为什么还要用MAC地址

1. IP地址是动态的，可以给任何一张网卡用，只有IP地址无法确定到主机
2. MAC地址是固定的，烧录到了网卡之中，永远不会变，可以确定到主机
3. IP地址用于表示同意逻辑上的目标，MAC地址则是标识物理上的目标

> IP地址和MAC地址的关系类似于内存中的虚拟地址和物理地址关系



# 子网掩码
详情参见[这里][4]



# NAT转换
详情参见[这里][19]



# 更多知识
更多的知识请参考末尾的链接


<br/>

[IP地址，子网掩码，默认网关，DNS服务器详解][1]  
[IP地址与路由][2]  
[单播、广播和多播IP地址][3]  
[子网掩码][4]  
[MAC地址表、ARP缓存表以及路由表][5]  
[IP地址和MAC地址的区别和联系是什么][6]  
[有了IP地址，为什么还要用MAC地址][7]  
[同一网段内的两台主机通信是否需要路由器][8]   
[内网和外网之间的通信][9]  
[为什么局域网的IP普遍是192.168开头][10]  
[UNIX网络编程][11]  
[socket绑定INADDR_ANY，那会怎样][12]  
[想了解下数据是如何分发到子进程的][13]  
[中继器、集线器(HUB)、网桥、交换机、路由器比较][14]  
[localhost、127.0.0.1 和 本机IP 三者的区别][15]  
[IP地址，子网掩码，子网划分][16]  
[看完后，搞懂ARP的工作原理，其实并不难][17]  
[MAC地址详解][18]  
[网络地址转换NAT原理及其作用][19]

[1]: http://www.cnblogs.com/JuneWang/p/3917697.html
[2]: https://akaedu.github.io/book/ch36s05.html
[3]: http://www.cnblogs.com/therock/articles/2798653.html
[4]: http://www.cnblogs.com/chaikefusibushiji/p/4284302.html
[5]: http://dengqi.blog.51cto.com/5685776/1223132
[6]: https://www.zhihu.com/question/49335649
[7]: https://www.zhihu.com/question/21546408
[8]: https://www.zhihu.com/question/41496681
[9]: http://blog.csdn.net/tennysonsky/article/details/45226275
[10]: https://www.zhihu.com/question/19813460
[11]: https://yuyang0.github.io/notes/unp.html
[12]: http://www.cnblogs.com/youngforever/articles/3312234.html
[13]: http://wenda.workerman.net/?/question/1281
[14]: http://www.cnblogs.com/sddai/p/5480002.html
[15]: https://www.zhihu.com/question/23940717
[16]: http://www.jianshu.com/p/66bd9c1e08d8
[17]: http://blog.csdn.net/engineer_along/article/details/51835319
[18]: http://blog.csdn.net/hello_hwc/article/details/40953003
[19]: http://www.cnblogs.com/wbxjiayou/p/5150753.html