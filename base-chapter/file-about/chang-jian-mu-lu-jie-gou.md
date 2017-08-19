# 查看根目录结构
```
[root@30bf5ac9eef2 /]# ls -1 /
bin
dev
etc
home
lib
lib64
lost+found
media
mnt
opt
proc
root
sbin
selinux
srv
sys
tmp
usr
var

```

# 目录详解
- bin
普通命令所在的目录

- dev
设备文件所在的目录，/dev/null表示空设备，即丢弃输出

- etc
配置文件所在的目录

- home
主目录，包含各个用户的家目录

- lib
库文件所在的目录，可能有软链接指向lib64或lib32

- lib64
64位库文件所在的目录

- media
媒体文件的挂载目录，例如CD-ROM

- mnt
临时文件的挂载目录，例如CD-ROM，u盘

- opt
可选软件的安装目录

- proc
虚拟文件系统，对应内核的状态信息，只读不能修改

- root
root用户的家目录

- sbin
系统命令所在的目录，不同用户无权限执行

- selinux
selinux安全相关目录

- srv
- sys
- tmp
- usr
- var
