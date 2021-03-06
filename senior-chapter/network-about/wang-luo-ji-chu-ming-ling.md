# ping 
用来测试主机之间网络的连通性

```
ping [选项] <地址>
```
> 地址可以是ip，主机名（hostname），域名（domain）

|选项 | 说明 |
|--- |--- |
|-c COUNT | 指定发送请求的次数 |
|-D | 在结果前面显示unix时间戳 |
|-i INTERVAL | 指定发送请求的时间间隔 |
|-I | 指定发送使用的网络接口 |
|-n | 显示ip而不是域名 | 
|-q | 不显示中间信息 | 
|-R | 记录路由过程 |
|-v | 输出详细过程 |
|-V | 显示版本 |
> 有时候无法`ping`，有可能是被管理员或防火墙禁用了


# telnet
用于登录远程主机，对远程主机进行管理
> `telnet`因为采用明文传送报文，安全性不好，现在基本都不开放`telnet`服务，而改用更安全的`ssh`方式了

```
telnet [选项] <地址> <端口> 
```
> 地址可以是ip，主机名（hostname），域名（domain）


## telnet交互
`telnet`远程后会进入输入模式，此时无法退出，使用`Ctrl + ]` 可以切换到交互模式，输入`quit`后可以退出

```
[root@zhujipeng /]# telnet 192.168.8.192 12345
Trying 192.168.8.192...
Connected to 192.168.8.192.
Escape character is '^]'.
^]
telnet> ?
Commands may be abbreviated.  Commands are:

close   	close current connection
logout  	forcibly logout remote user and close the connection
display 	display operating parameters
mode    	try to enter line or character mode ('mode ?' for more)
open    	connect to a site
quit    	exit telnet
send    	transmit special characters ('send ?' for more)
set     	set operating parameters ('set ?' for more)
unset   	unset operating parameters ('unset ?' for more)
status  	print status information
toggle  	toggle operating parameters ('toggle ?' for more)
slc     	change state of special charaters ('slc ?' for more)
z       	suspend telnet
!       	invoke a subshell
environ 	change environment variables ('environ ?' for more)
?       	print help information
telnet> quit
Connection closed.
```



# ifconfig
查看和设置网络接口

```
ifconfig [-v] [-a] [-s] [interface]
ifconfig [-v] interface [aftype] options | address ...
```
|选项 | 说明 |
|--- |--- |
|-a | 显示所有的网络接口，包括未启用的 |
|-s | 显示简短的信息，和`netstat -i`一样 |
|-v | 显示详细的信息 |

|options | 说明 |
|--- |--- |
|up | 激活指定网口 |
|down | 关闭指定网口 |
|[-]arp | 开启或关闭arp协议 |
|[-]promisc | 开启或关闭混杂模式 |
|[-]allmulti | 开启或关闭多播模式 |
|mtu N | 设置最大传输单元 |
|netmask ADDR| 设置网络掩码 |
|add ADDR/PREFIXLEN | 添加IPv6地址到指定网口 |
|add ADDR/PREFIXLEN | 删除指定网口的IPv6地址 |


## 输出格式
```
[root@zhujipeng /]# ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:24 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:1704 (1.6 KiB)  TX bytes:0 (0.0 b)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)
```

每行的含义

1. Link - 连接信息
2. inet - 网络信息
3. 网卡状态标识
4. RX - 接收数据包情况统计
5. TX - 发送数据包情况统计
6. 网络信号冲突和传输缓冲区信息
7. 接收、发送数据字节数统计信息

|字段 | 说明 |
|--- |--- |
|eth0 | 表示第一块网卡 |
|lo | 表示主机的回环地址 |
|encap | 网络类型（encapsulation） |
|HWaddr | 物理网卡的地址（hardware address）|
|addr | 网络地址（address） |
|Bcast | 广播地址（broadcast） |
|Mask | 网络掩码 |
|UP | 启用 |
|BROADCAST | 广播 |
|MULTICAST | 多播 |
|RUNNING | 运行中 |
|MTU | 最大传输单元 |
|Metric |路由度量值，缺省值是0 |
|collisions | 网络信号冲突的情况 |
|txqueuelen | 传输缓冲区Metric大小 |



# lsof
查看所有打开的文件，也可查看网络的信息，详情参考[这里][8]
> linux下一切皆文件，网络也用文件表示

## 显示连接信息
### 显示所有连接
```
lsof -i 
```

### 仅获取IPv6流量
```
lsof -i 6
```

### 仅显示TCP/UDP连接
```
lsof -iTCP
lsof -iUDP
```

### 显示指定端口的连接
```
lsof -i:22
lsof -i :22
```

### 显示指定主机的连接
```
lsof -i@172.16.12.5
```

### 显示指定主机和端口的连接
```
lsof -i@172.16.12.5:22
```

### 显示监听端口
```
lsof -i -sTCP:LISTEN
lsof -i | grep -i LISTEN
```



# hostname
显示和设置主机名
```
hostname [选项] [主机名]
```

|选项 | 说明 |
|--- |--- |
|-a, --alias | 显示主机别名 |
|-A, --all-fqdns | 显示完全限定名FQDN（Fully Qualified Domain Name）和主机名 |
|--d, --domain | 显示域名部分 |
|-f, --fqdn, --long | 显示完全限定名FQDN（Fully Qualified Domain Name）|
|-i, --ip-address | 显示主机对应的ip |
|-I, --all-ip-addresses | 显示主机对应的所有ip |
|-s, --short | 显示主机名在第一个点号前面的部分 |
> 关于如何修改主机名请参考[这里][10]，FQDN的知识参考[这里][11]



# nslookup
查询DNS，详情参考[这里][13]



# dig
查询DNS，详情参考[这里][15]



# arp
操作主机的arp缓冲区，详情参考[这里][18]


# ip
ip命令和ifconfig类似，但功能更强大，详情参考[这里][19]


<br/>

---

# 参考

[每天一个linux命令 ping命令][1]  
[配置Linux禁止ping和请允许ping][2]  
[Linux禁止ping以及开启ping的方法][3]  
[每天一个linux命令 telnet命令][4]  
[linux下怎么退出telnet][5]  
[Centos 开启telnet-service服务][6]  
[每天一个linux命令 ifconfig命令][7]  
[Linux 命令神器：lsof 入门][8]  
[hostname命令][9]  
[深入理解Linux修改hostname][10]  
[FQDN 是什么][11]  
[Linux设置FQDN][12]  
[nslookup命令][13]  
[linux下DNS解析（nslookup、dig、host）][14]  
[Linux命令：使用dig命令解析域名][15]  
[域名解析中A记录、CNAME、MX记录、NS记录的区别和联系][16]  
[常用域名记录解释][17]  
[arp命令][18]  
[试试Linux下的ip命令，ifconfig已经过时了][19]  

[1]: http://www.cnblogs.com/peida/archive/2013/03/06/2945407.html
[2]: http://sky9896.blog.51cto.com/2330653/1886609
[3]: http://www.cnblogs.com/chenshoubiao/p/4781016.html
[4]: http://www.cnblogs.com/peida/archive/2013/03/13/2956992.html
[5]: http://blog.csdn.net/love__coder/article/details/6733307
[6]: http://www.cnblogs.com/xlmeng1988/archive/2012/04/24/telnet-server.html
[7]: http://www.cnblogs.com/peida/archive/2013/02/27/2934525.html
[8]: https://linux.cn/article-4099-1.html
[9]: http://man.linuxde.net/hostname
[10]: http://www.cnblogs.com/kerrycode/p/3595724.html
[11]: http://blog.csdn.net/u012842205/article/details/51931017
[12]: http://www.cnblogs.com/zhenyuyaodidiao/p/4947930.html
[13]: http://man.linuxde.net/nslookup
[14]: http://122269875.blog.51cto.com/1660536/1713947
[15]: http://blog.csdn.net/reyleon/article/details/12976889
[16]: http://blog.csdn.net/crazw/article/details/8986581
[17]: https://www.ezloo.com/2011/04/a_mx_cname_txt_aaaa_ns.html
[18]: http://man.linuxde.net/arp
[19]: https://linux.cn/article-3144-1.html