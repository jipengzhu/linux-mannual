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