# 相关命令
## uname
显示系统内核相关信息

```
uname [OPTION]...
```

|选项 | 说明 |
|--- |--- |
|-a, --all | 显示所有信息 |
|-s, --kernel-name | 显示内核名称 |
|-n, --nodename | 显示主机名 |
|-r, --kernel-release | 显示内核发行信息 |
|-v, --kernel-version | 显示内核版本 |
|-m, --machine | 显示机器名 |
|-p, --processor | 显示cpu |
|-i, --hardware-platform | 显示硬件平台 |
|-o, --operating-system | 显示操作系统 |


## lscpu
查看cpu相关的信息


## lsblk
查看块设备相关的信息


## lsscsi
查看控制器相关的信息


## lsmod
显示内核中的模块的状态信息


## lsb_release
查看linux的发行版本信息



# 查看cpu
总核数 = 物理CPU个数 X 每颗物理CPU的核数

总逻辑CPU数 = 物理CPU个数 X 每颗物理CPU的核数 X 超线程数

## 查看物理CPU的个数
```
cat /proc/cpuinfo| grep "physical id"| sort -u | wc -l
```


## 查看每个CPU的核数
```
cat /proc/cpuinfo| grep "cpu cores"| uniq
```


## 查看逻辑CPU的个数
```
cat /proc/cpuinfo| grep "processor"| wc -l
```

## 查看CPU的型号
```
cat /proc/cpuinfo | grep name | cut -f2 -d:
```

## 查看CPU的频率
```
cat /proc/cpuinfo | grep MHz | cut -f2 -d:
```



# 查看内存
```
[root@localhost ~]# cat /proc/meminfo
MemTotal:        1016232 kB
MemFree:          762864 kB
MemAvailable:     749112 kB
Buffers:            2108 kB
Cached:           101048 kB
SwapCached:            0 kB
Active:           104772 kB
Inactive:          76760 kB
Active(anon):      78672 kB
Inactive(anon):     6408 kB
Active(file):      26100 kB
Inactive(file):    70352 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       2097148 kB
SwapFree:        2097148 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:         78408 kB
Mapped:            22852 kB
Shmem:              6704 kB
Slab:              41240 kB
SReclaimable:      18988 kB
SUnreclaim:        22252 kB
KernelStack:        1584 kB
PageTables:         3828 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     2605264 kB
Committed_AS:     292864 kB
VmallocTotal:   34359738367 kB
VmallocUsed:        5944 kB
VmallocChunk:   34359729728 kB
HardwareCorrupted:     0 kB
AnonHugePages:     12288 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       57280 kB
DirectMap2M:      991232 kB
```


<br/>

---

# 参考

[uname命令][1]  
[Linux下lshw,lsscsi,lscpu,lsusb,lsblk硬件查看命令][2] 
[lsmod命令][3]  
[查看linux版本及lsb_release安装及一些想法][4]  
[Debian 拋弃 Linux 标准规范（LSB）][5]  
[Linux查看物理CPU个数、核数、逻辑CPU个数][6]  

[1]: http://man.linuxde.net/uname
[2]: http://www.cnblogs.com/clphp/p/6399119.html
[3]: http://man.linuxde.net/lsmod
[4]: http://blog.csdn.net/darkdragonking/article/details/61194308
[5]: https://linux.cn/article-6387-1.html
[6]: http://www.cnblogs.com/emanlee/p/3587571.html