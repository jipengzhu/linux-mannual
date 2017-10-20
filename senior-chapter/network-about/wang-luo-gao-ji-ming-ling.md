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
|-nn | 显示协议和端口的数字而不是名称 |
|-N | 不显示域名部分 |
|-v | 显示详细的输出 |
|-vv | 显示详细的输出 |
|-vvv | 显示详细的输出 |
|-x | 显示头信息 |
|-xx | 显示头信息 |
|-X | 用16进制和ASCII码显示头信息 |
|-XX | 用16进制和ASCII码显示头信息 |


# ip
ip命令和ifconfig类似，但功能更强大，详情参考[这里][8]


<br/>

---

# 参考

[每天一个linux命令 netstat命令][1]  
[netstat命令][2]  
[netstat 的10个基本用法][3]  
[Linux tcpdump命令详解][4]  
[tcpdump命令][5]  
[tcpdump使用技巧][6]  
[tcpdump不能抓本机程序向本机端口发送的包吗][7]  
[试试Linux下的ip命令，ifconfig已经过时了][8]  

[1]: http://www.cnblogs.com/peida/archive/2013/03/08/2949194.html
[2]: http://man.linuxde.net/netstat
[3]: https://linux.cn/article-2434-1.html
[4]: http://www.cnblogs.com/ggjucheng/archive/2012/01/14/2322659.html
[5]: http://man.linuxde.net/tcpdump
[6]: https://linuxwiki.github.io/NetTools/tcpdump.html
[7]: http://bbs.chinaunix.net/thread-1589327-1-1.html
[8]: https://linux.cn/article-3144-1.html