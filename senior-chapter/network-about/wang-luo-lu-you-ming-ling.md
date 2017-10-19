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
|
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


#### 输出标志详解
|标志 | 说明 |
|--- |--- |

### 示例

#### 添加主机路由
```
route add -host 192.168.1.2 dev eth0
route add -host 10.20.30.148 gw 10.20.30.40
```

#### 添加网络路由
```
route add -net 10.20.30.40 netmask 255.255.255.248 eth0
route add -net 10.20.30.48 netmask 255.255.255.248 gw 10.20.30.41
route add -net 192.168.1.0/24 eth1
```

#### 添加默认路由
```
route add default gw 192.168.1.1
```

#### 删除主机路由
```
route del -host 192.168.1.2 dev eth0:0
route del -host 10.20.30.148 gw 10.20.30.40
```

#### 删除网络路由
```
route del -net 10.20.30.40 netmask 255.255.255.248 eth0
route del -net 10.20.30.48 netmask 255.255.255.248 gw 10.20.30.41
route del -net 192.168.1.0/24 eth1
```

#### 删除默认路由
```
route del default gw 192.168.1.1
```


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