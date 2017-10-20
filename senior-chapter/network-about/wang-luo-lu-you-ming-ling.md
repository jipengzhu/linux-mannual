# route
查看和操作网络的路由信息


## linux的route
```
route [-CFvnNee] [-A family |-4|-6]

route  [-v] [-A family |-4|-6] add [-net|-host] target [netmask Nm] [gw Gw] [metric N] [mss M] [window W] [irtt I] [reject] [mod] [dyn] [reinstate] [[dev] If]

route  [-v] [-A family |-4|-6] del [-net|-host] target [gw Gw] [netmask Nm] [metric N [[dev] If]

route  [-V] [--version] [-h] [--help]
```

|选项 | 说明 |
|--- |--- |
|-A family | 指定协议族 |
|-n | 显示ip而不是主机名 |
|-e | 使用 `netstat` 的格式显示 |
|del | 删除路由表项 |
|add | 添加路由表项 |
|target | 目的地址 |
|-net | 目的地址是一个网络 |
|-host | 目的地址是一个主机 |
|netmask NM | 指定子网掩码（目的地址是网络时）|
|gw GW | 指定网关地址 |
|mss M | 指定最大传输单元MTU  (Maximum Transmission Unit) |
|window W | 指定TCP窗口大小 |
|irtt | 设置初始的RTT（round  trip  time）|
|dev | 指定网络设备 |

### 查看路由
```
[root@zhujipeng ~]# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         gateway         0.0.0.0         UG    0      0        0 eth1
10.0.0.0        172.16.0.1      255.0.0.0       UG    0      0        0 eth0
101.236.56.0    0.0.0.0         255.255.255.0   U     0      0        0 eth1
link-local      0.0.0.0         255.255.0.0     U     1002   0        0 eth0
link-local      0.0.0.0         255.255.0.0     U     1003   0        0 eth1
169.254.169.254 gateway         255.255.255.255 UGH   0      0        0 eth1
172.16.0.0      0.0.0.0         255.255.0.0     U     0      0        0 eth0
172.16.0.0      172.16.0.1      255.240.0.0     UG    0      0        0 eth0
198.18.0.0      172.16.0.1      255.254.0.0     UG    0      0        0 eth0
[root@zhujipeng ~]# netstat -nr
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         101.236.56.1    0.0.0.0         UG        0 0          0 eth1
10.0.0.0        172.16.0.1      255.0.0.0       UG        0 0          0 eth0
101.236.56.0    0.0.0.0         255.255.255.0   U         0 0          0 eth1
169.254.0.0     0.0.0.0         255.255.0.0     U         0 0          0 eth0
169.254.0.0     0.0.0.0         255.255.0.0     U         0 0          0 eth1
169.254.169.254 101.236.56.1    255.255.255.255 UGH       0 0          0 eth1
172.16.0.0      0.0.0.0         255.255.0.0     U         0 0          0 eth0
172.16.0.0      172.16.0.1      255.240.0.0     UG        0 0          0 eth0
198.18.0.0      172.16.0.1      255.254.0.0     UG        0 0          0 eth0
```

#### 输出格式详解
|字段 | 说明 |
|--- |--- |
|Destination | 目的地址 |
|Gateway | 网关地址 |
|Genmask | 网络掩码 |
|Flags | 路由标识 |
|Metric | 路由距离 |
|Ref | 路由表项引用的次数 |
|Use | 被路由软件查找的次数 |
|Iface | 网络接口 |
|MSS | 最大报文段长度 |
|Window | TCP窗口大小 |

#### 路由标志详解
|标志 | 说明 |
|--- |--- |
|U | 路由是活动的 |
|H | 目的地址是一个主机 |
|N | 目的地址是一个网络 |
|G | 目的地址是一个网关 |
|R | 恢复动态路由产生的表项 |
|D | 由路由的后台程序动态地安装 |
|M | 由路由的后台程序修改 |

### 示例

#### 添加主机路由
```
route add -host 10.1.0.1 dev eth0
route add -host 10.1.0.1 gw 10.2.1.128
```

#### 添加网络路由
```
route add -net 10.1.0.0 netmask 255.255.0.0 eth0
route add -net 10.1.0.0 netmask 255.255.0.0 gw 10.2.1.128
route add -net 10.1.0.0/16 eth1
```

#### 添加默认路由
```
route add default gw 10.2.1.128
```

#### 删除主机路由
```
route del -host 10.1.0.1 dev eth0
route del -host 10.1.0.1 gw 10.2.1.128
```

#### 删除网络路由
```
route del -net 10.1.0.0 netmask 255.255.0.0 eth0
route del -net 10.1.0.0 netmask 255.255.0.0 gw 10.2.1.128
route del -net 10.1.0.0/16 eth1
```

#### 删除默认路由
```
route del default gw 10.2.1.128
```

## mac的路由
```
route [-dnqtv] command [[modifiers] args]
route add [ host | network ] %s: gateway %s flags %x
route delete [ host | network ] %s: gateway %s flags %x
```

|选项 | 说明 |
|--- |--- |
|-d | 使用调试模式，不实际修改 | 
|-t | 使用测试模式 |
|-v | 输出详细信息 |
|-q | 禁止所有输出 |

|命令 | 说明 |
|--- |--- |
|add | 添加路由 |
|flush | 清空路由 |
|delete | 删除指定路由 |
|change | 改变路由规则 |
|get | 显示路由规则 |
|monitor | 监视路由变化 |


### 查看路由
```
➜  Downloads netstat -nr
Routing tables

Internet:
Destination        Gateway            Flags        Refs      Use   Netif Expire
default            192.168.9.254      UGSc           20        0     en0
127                127.0.0.1          UCS             0        0     lo0
127.0.0.1          127.0.0.1          UH             38 11175096     lo0
169.254            link#4             UCS             0        0     en0
192.168.8/23       link#4             UCS             6        0     en0
192.168.8.68       b4:b:44:b5:ff:1b   UHLWI           0        2     en0
192.168.8.79       f4:f:24:3f:c9:ad   UHLWI           0        0     en0    675
192.168.8.192/32   link#4             UCS             0        0     en0
192.168.8.206      34:36:3b:c8:90:3e  UHLWI           0       18     en0   1144
192.168.8.254      c:d6:bd:47:27:be   UHLWI           0        0     en0    239
192.168.9.23       50:68:a:d1:80:38   UHLWI           0        0     en0    293
192.168.9.254/32   link#4             UCS             1        0     en0
192.168.9.254      3c:8c:40:2:f:4c    UHLWIir        22       24     en0   1162

Internet6:
Destination                             Gateway                         Flags         Netif Expire
::1                                     ::1                             UHL             lo0
fe80::%lo0/64                           fe80::1%lo0                     UcI             lo0
fe80::1%lo0                             link#1                          UHLI            lo0
fe80::%en0/64                           link#4                          UCI             en0
fe80::3636:3bff:fec6:4144%en0           34:36:3b:c6:41:44               UHLI            lo0
fe80::%awdl0/64                         link#9                          UCI           awdl0
fe80::50b8:92ff:fe08:7c3b%awdl0         52:b8:92:8:7c:3b                UHLI            lo0
ff01::%lo0/32                           ::1                             UmCI            lo0
ff01::%en0/32                           link#4                          UmCI            en0
ff01::%awdl0/32                         link#9                          UmCI          awdl0
ff02::%lo0/32                           ::1                             UmCI            lo0
ff02::%en0/32                           link#4                          UmCI            en0
ff02::%awdl0/32                         link#9                          UmCI          awdl0
```

### 示例

#### 添加主机路由
```
route add 10.1.0.1 10.2.1.128
route add -host 10.1.0.1 10.2.1.128
```

#### 添加网络路由
```
route add -net 10.1.0.0 10.2.1.128 255.255.0.0
route add -net 10.1.0.0/16 10.2.1.128
```

#### 添加默认路由
```
route add default 10.2.1.128
```

#### 删除主机路由
```
route delete 10.1.0.1 10.2.1.128
route delete -host 10.1.0.1 10.2.1.128
```

#### 删除网络路由
```
route delete -net 10.1.0.0 10.2.1.128 255.255.0.0
route delete -net 10.1.0.0/16 10.2.1.128
```

#### 删除默认路由
```
route delete default 10.2.1.128
```


# windows的路由
详情参见[这里][5]


<br/>

---

# 参考

[route route命令][1]  
[traceroute命令][2]  
[linux 多网卡路由问题][3]  
[mac osx修改mac地址和管理路由表的方法][4]  
[windows route 命令详解][5]    

[1]: http://man.linuxde.net/route
[2]: http://man.linuxde.net/traceroute
[3]: http://blog.csdn.net/yuanbinquan/article/details/51468886
[4]: http://www.huilog.com/?p=660
[5]: http://cwfsxlove.blog.51cto.com/43997/50389