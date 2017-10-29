# netstat
查看系统的网络连接信息

```
netstat  [address_family_options]  [--tcp|-t]  [--udp|-u]  [--udplite|-U]   [--raw|-w]   [--listening|-l]
       [--all|-a]   [--numeric|-n]   [--numeric-hosts]   [--numeric-ports]   [--numeric-users]   [--symbolic|-N]
       [--extend|-e[--extend|-e]]  [--timers|-o]  [--program|-p]  [--verbose|-v]  [--continuous|-c]  [--wide|-W]
       [delay]

       netstat  {--route|-r}  [address_family_options]  [--extend|-e[--extend|-e]] [--verbose|-v] [--numeric|-n]
       [--numeric-hosts] [--numeric-ports] [--numeric-users] [--continuous|-c] [delay]

       netstat  {--interfaces|-I|-i}  [--all|-a]  [--extend|-e]  [--verbose|-v]  [--program|-p]   [--numeric|-n]
       [--numeric-hosts] [--numeric-ports] [--numeric-users] [--continuous|-c] [delay]

       netstat  {--groups|-g}  [--numeric|-n]  [--numeric-hosts] [--numeric-ports] [--numeric-users] [--continu‐
       ous|-c] [delay]

       netstat    {--masquerade|-M}    [--extend|-e]    [--numeric|-n]    [--numeric-hosts]    [--numeric-ports]
       [--numeric-users] [--continuous|-c] [delay]

       netstat {--statistics|-s} [--tcp|-t] [--udp|-u] [--udplite|-U] [--raw|-w] [delay]

       netstat {--version|-V}

       netstat {--help|-h}

address_family_options:

       [-4|--inet]   [-6|--inet6]   [--protocol={inet,inet6,unix,ipx,ax25,netrom,ddp,   ...   }   ]  [--unix|-x]
       [--inet|--ip|--tcpip]  [--ax25]  [--x25]  [--rose]   [--ash]   [--ipx]   [--netrom]   [--ddp|--appletalk]
       [--econet|--ec]
```

|选项 | 说明 |
|--- |--- |
|--route , -r | 显示路由表 |
|--interfaces=iface , -I=iface , -i | 指定网络接口 |
|--masquerade , -M | 显示伪装的连接 |
|--statistics , -s | 显示统计信息 |
|--verbose , -v | 显示更加详细的信息 |
|--wide , -W | 显示ip的所有部分 |
|--numeric , -n | 显示数字而不是名称 |
|--numeric-hosts | 主机部分显示为ip |
|--numeric-ports | 端口部分显示为数字 |
|--numeric-users | 用户部分显示用户id |
|--protocol=family , -A | 指定协议族 |
|-c, --continuous | 持续性的输出信息 |
|-e, --extend | 输出额外的信息 |
|-p, --program | 显示进程id |
|-l, --listening | 只显示监听的网络 |
|-a, --all | 显示所有的连接 |
|-t | 显示tcp连接协议的 |
|-u | 显示udp连接协议的 |



# ss(socket statistics)
查看系统的网络连接信息

```
ss [options] [ FILTER ]
```

|选项 | 说明 |
|--- |--- |
|-n, --numeric | 显示数字而不是名称 |
|-r, --resolve | 解析数字为名称  |
|-a, --all | 显示所有的套接字 |
|-l, --listening | 显示监听的套接字（默认不显示）|
|-o, --options | 显示时间信息 |
|-e, --extended | 显示额外的信息 |
|-m, --memory | 显示内存使用 |
|-p, --processes | 显示进程信息 |
|-i, --info | 显示内部Tcp信息 |
|-s, --summary | 显示统计信息 |
|-4, --ipv4 | 显示ipv4的套接字 |
|-6, --ipv6 | 显示ipv6的套接字 |
|-t, --tcp| 显示tcp的套接字 |
|-u, --udp| 显示udp的套接字 |
|-x, --unix | 显示Unix domain的套接字 |
|-f FAMILY, --family=FAMILY | 指定协议族 |

```
FILTER := [ state STATE-FILTER ] [ EXPRESSION ]
```

|状态 | 说明 |
|--- |--- |
|listen | 参考三次握手的状态 |
|syn-sent| 参考三次握手的状态 |
|syn-recv| 参考三次握手的状态 |
|established| 参考三次握手的状态 |
|fin-wait-1| 参考三次握手的状态 |
|fin-wait-2| 参考三次握手的状态 |
|last-ack| 参考三次握手的状态 |
|time-wait| 参考三次握手的状态 | 
|close-wait| 参考三次握手的状态 |
|closing| 参考三次握手的状态 |
|closed| 参考三次握手的状态 |
|all | 所有的状态 |
|connected | 除了`listen`和`closed`的状态 |
|synchronized| 除了`syn-sent`的`connected`状态 |

表达式部分请参考文档末尾的链接



# tcpdump
抓取网络上的数据包
```
tcpdump [ -AbdDefhHIJKlLnNOpqRStuUvxX ] [ -B buffer_size ] [ -c count ]
               [ -C file_size ] [ -G rotate_seconds ] [ -F file ]
               [ -i interface ] [ -j tstamp_type ] [ -m module ] [ -M secret ]
               [ -P in|out|inout ]
               [ -r file ] [ -V file ] [ -s snaplen ] [ -T type ] [ -w file ]
               [ -W filecount ]
               [ -E spi@ipaddr algo:secret,...  ]
               [ -y datalinktype ] [ -z postrotate-command ] [ -Z user ]
               [ expression ]
```

|选项 | 说明 |
|--- |--- |
|-A | 使用ASCII码输出 |
|-B | 指定buffer大小，单位为KB |
|-c | 达到指定大小的包后退出 |
|-D | 显示可以监听的网络接口 |
|-i | 指定监听的网络接口 |
|-n | 显示ip而不是主机名 |
|-nn | 显示主机，协议和端口的数字而不是名称 |
|-N | 不显示域名部分 |
|-v | 显示详细的输出 |
|-vv | 显示详细的输出 |
|-vvv | 显示详细的输出 |
|-S | 输出Tcp序列号的绝对值而不是相对值 |
|-x | 显示头信息 |
|-xx | 显示头信息 |
|-X | 用16进制和ASCII码显示头信息 |
|-XX | 用16进制和ASCII码显示头信息 |
> 想要监听发送到本地端口的数据包需要指定`-i lo0`

表达式部分请参考文档末尾的链接


<br/>

---

# 参考

[每天一个linux命令 netstat命令][1]  
[每天一个linux命令 ss命令][2]  
[netstat命令][3]  
[netstat 的10个基本用法][4]  
[Linux tcpdump命令详解][5]  
[tcpdump命令][6]  
[tcpdump使用技巧][7]  
[tcpdump不能抓本机程序向本机端口发送的包吗][8]  

[1]: http://www.cnblogs.com/peida/archive/2013/03/08/2949194.html
[2]: http://www.cnblogs.com/peida/archive/2013/03/11/2953420.html
[3]: http://man.linuxde.net/netstat
[4]: https://linux.cn/article-2434-1.html
[5]: http://www.cnblogs.com/ggjucheng/archive/2012/01/14/2322659.html
[6]: http://man.linuxde.net/tcpdump
[7]: https://linuxwiki.github.io/NetTools/tcpdump.html
[8]: http://bbs.chinaunix.net/thread-1589327-1-1.html