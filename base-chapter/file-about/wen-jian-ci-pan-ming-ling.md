# df
df命令的是用来查看文件系统的磁盘空间占用情况的

格式如下
```
df [选项] [文件]
```

|选项 | 说明 |
|--- |--- |
|-a | 全部文件系统列表 |
|-h | 方便阅读方式显示 |
|-H | 等于“-h”，但是计算式，1K=1000，而不是1K=1024 |
|-i | 显示inode信息 |
|-k | 区块为1k（1024字节）|
|-l | 只显示本地文件系统 |
|-m | 区块为1m（1048576字节）|
|--no-sync | 忽略sync命令 |
|--sync | 在取得磁盘信息前，先执行sync命令 |
|-P | 输出格式为POSIX |
|-T | 文件系统类型 |
|--block-size=区块大小 | 指定区块大小 |
|-t 文件系统类型 | 只显示选定文件系统的磁盘信息 |
|-x 文件系统类型 | 不显示选定文件系统的磁盘信息 |
|--help | 显示帮助信息 | 
|--version | 显示版本信息 |

> a -> all | h -> human-readable | i -> inode | k -> kilobyte | m -> megabyte | l -> local

```
[root@30bf5ac9eef2 /]# df
Filesystem     1K-blocks    Used Available Use% Mounted on
none            61896484 3261964  55467288   6% /
tmpfs            1023524       0   1023524   0% /dev
tmpfs            1023524       0   1023524   0% /sys/fs/cgroup
/dev/vda2       61896484 3261964  55467288   6% /etc/resolv.conf
/dev/vda2       61896484 3261964  55467288   6% /etc/hostname
/dev/vda2       61896484 3261964  55467288   6% /etc/hosts
shm                65536       0     65536   0% /dev/shm
tmpfs            1023524       0   1023524   0% /proc/kcore
tmpfs            1023524       0   1023524   0% /proc/timer_list
tmpfs            1023524       0   1023524   0% /proc/sched_debug
tmpfs            1023524       0   1023524   0% /sys/firmware
```