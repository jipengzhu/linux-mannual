# 查看根目录结构
```
[root@30bf5ac9eef2 /]# ls -1 /
bin  boot dev  etc  home  lib  lib64  
lost+found  media  mnt  opt  proc  root  sbin  
selinux  srv  sys  tmp  usr  var

```


# 目录详解
- bin  
操作系统级别的命令所在的目录

- boot  
引导程序和开机启动所在的目录，通常是一个单独的分区

- dev  
设备文件所在的目录，硬盘、光驱、鼠标、键盘 都是以文件的方式放在这个目录下，/dev/null表示空设备，即丢弃输出

- etc  
内核程序配置文件所在的目录

- home  
主目录，包含各个用户的家目录

- lib  
内核程序依赖库文件所在的目录，可能有软链接指向lib64或lib32

- lib64  
64位内核程序依赖库文件所在的目录

- media  
媒体文件的挂载目录，例如CD-ROM

- mnt  
临时文件的挂载目录，例如CD-ROM，u盘

- opt  
可选软件的安装目录

- proc  
虚拟文件系统，纪录内核、进程、外部设备的状态及网络状态等信息。所有数据都是在内存中，不占任何硬盘空间

- root  
root用户的家目录

- sbin  
操作系统级别的命令所在的目录，但普通用户无权限执行

- selinux  
selinux安全配置文件目录

- srv  
网络服务的数据目录

- sys  
虚拟文件系统，主要记录与内核相关的信息，包括目前已加载的内核模块与内核检测到的硬件设备信息。所有数据都是在内存中，不占任何硬盘空间

- tmp  
临时文件目录，在系统重启时目录中文件可能不会被保留

- usr  
系统级别的目录结构，也包含bin、lib、etc等目录

- var  
运行时内容不断变化的文件所在的目录


# etc目录
- /etc/init.d  
程序开机启动脚本所在的目录

- /etc/rc.d /etc/rc*.d  
为了与以前兼容，/etc/rc*.d是指向/etc/rc.d里对应目录的软链接，/etc/rc.d里不同级别的启动脚本都是/etc/init.d的软链接

- /etc/hosts  
网络地址和域名的映射配置文件，操作系统会优先使用这个文件做dns解析

- /etc/sysconfig/network  
IP、掩码、网关、主机名配置

- /etc/resolv.conf  
DNS服务器配置

- /etc/fstab  
文件系统自动挂载配置

- /etc/inittab  
init进程对系统的设置文件

- /etc/exports  
NFS的配置文件

- /etc/profile  
系统（全局）环境变量配置文件

- /etc/issue  
发行版信息

- /etc/passwd  
用户数据库，其中的域给出了用户名、真实姓名、家目录、加密的口令和用户的其他信息

- /etc/shadow  
在安装了影子口令软件的系统上的影子口令文件。影子口令文件将/etc/passwd 文件中的加密口令移动到/etc/shadow 中，而后者只对root可读，这使破译口令更困难

- /etc/sudoers  
sudo用户的配置文件

- /etc/syslog.conf /etc/rsyslog.conf  
系统日志的配置文件

- /etc/shells  
可信任的shell列表

- /etc/xinetd.d  
如果服务器是通过xinetd模式运行的，它的脚本要放在这个目录下。有些系统没有这个目录，比如Slackware，有些老的版本也没有。在Redhat Fedora中比较新的版本中存在。

- /etc/opt/  
/opt/的配置文件


# usr目录
- /usr/doc  
Linux技术文档

- /usr/bin  
系统程序级别的命令所在的目录

- /usr/sbin  
系统程序级别的命令所在的目录

- /usr/etc  
系统程序配置文件所在的目录

- /usr/include  
开发和编译应用程序所需要的头文件

- /usr/lib  
系统程序依赖库文件所在的目录

- /usr/lib  
64位系统程序依赖库文件所在的目录

- /usr/man  
帮助文档所在的目录

- /usr/src  
Linux开放的源代码，就存在这个目录，爱好者们别放过哦

- /usr/share  
体系结构无关（共享）数据

- /usr/local  
用户级别的目录结构，也包含bin、lib、etc等目录


# var目录

- /var/log/message  
系统日志信息，按周自动轮询

- /var/spool/cron  
定时任务配置文件目录，默认按用户命名

- /var/log/secure  
记录登陆系统存取信息的文件，不管认证成功还是认证失败都会记录

- /var/log/wtmp    
记录登陆者信息的文件，last,who,w 命令信息来源于此

- /var/spool/clientmqueue    
当邮件服务未开启时，所有应发给系统管理员的邮件都将保留在此

- /var/spool/mail    
邮件目录

- /var/tmp   
比/tmp 允许的大或需要存在较长时间的临时文件(虽然系统管理员可能不允许/var/tmp有很旧的文件) 

- /var/lib     
系统正常运行时要改变的文件 

- /var/local     
/usr/local中安装的程序的可变数据(即系统管理员安装的程序)存放的目录。注意，如果必要，即使本地安装的程序也会使用其他/var目录，例如/var/lock。
 
- /var/lock    
锁定文件目录。许多程序遵循在/var/lock中产生一个锁定文件的约定，以支持他们正在使用某个特定的设备或文件。其他程序注意到这个锁定文件，将不试图使用这个设备或文件。

- /var/log  
各种程序的Log文件，特别是login（/var/log/wtmp log所有到系统的登录和注销）和syslog（/var/log/messages 里存储所有核心和系统程序信息）。/var/log 里的文件经常不确定地增长，应该定期清除。 

- /var/run    
保存到下次引导前有效的关于系统的信息文件。例如/var/run/utmp包含当前登录的用户的信息。

- /var/cache  
应用程序缓存数据。这些数据是在本地生成的一个耗时的I/O或计算结果。应用程序必须能够再生或恢复数据。缓存的文件可以被删除而不导致数据丢失。


# proc目录
- /proc/meminfo  
内存信息

- /proc/loadavg  
还记得 top 以及 uptime 吧？没错！上头的三个平均数值就是记录在此！

- /proc/uptime  
就是用 uptime 的时候，会出现的资讯啦！

- /proc/cpuinfo  
关于处理器的信息，如类型、厂家、型号和性能等。

- /proc/cmdline  
加载 kernel 时所下达的相关参数！查阅此文件，可了解系统是如何启动的！

- /proc/filesystems    
目前系统已经加载的文件系统！

- /proc/interrupts  
目前系统上面的 IRQ 分配状态。

- /proc/ioports  
目前系统上面各个装置所配置的 I/O 位址。

- /proc/kcore  
这个就是内存的大小啦！好大对吧！但是不要读他啦！

- /proc/modules   
目前我们的 Linux 已经加载的模块列表，也可以想成是驱动程序啦！

- /proc/mounts  
系统已经挂载的设备，就是用 mount 这个命令呼叫出来的数据啦！

- /proc/swaps   
到底系统挂加载的内存在哪里？呵呵！使用掉的 partition 就记录在此啦！

- /proc/partitions   
使用 fdisk -l 会出现目前所有的 partition 吧？在这个文件当中也有纪录喔！

- /proc/pci   
在 PCI 汇流排上面，每个装置的详细情况！可用 lspci 来查阅！

- /proc/version   
核心的版本，就是用 uname -a 显示的内容啦！

- /proc/bus/*    
一些汇流排的装置，还有 U盘的装置也记录在此喔！

# dev目录
- /dev/hd[a-t]
IDE设备

- /dev/sd[a-z]
SCSI设备

- /dev/fd[0-7]
标准软驱

- /dev/md[0-31]
软raid设备

- /dev/loop[0-7]
本地回环设备

- /dev/ram[0-15]
内存

- /dev/null
无限数据接收设备,相当于黑洞

- /dev/zero
无限零资源

- /dev/tty[0-63]
虚拟终端

- /dev/ttyS[0-3]
串口

- /dev/lp[0-3]
并口

- /dev/console
控制台

- /dev/fb[0-31]
framebuffer

- /dev/cdrom 
=> /dev/hdc

- /dev/modem
=> /dev/ttyS[0-9]

- /dev/pilot 
=> /dev/ttyS[0-9]

- /dev/random
随机数设备

- /dev/urandom
随机数设备


# /bin、/usr/bin、/usr/local/bin的区别
etc，lib和bin类似，参见[这里][2]
- /bin 
对应于操作系统级别的命令

- /usr/bin
对应于系统软件级别的命令

- /usr/bin
对应于用户（可选）软件级别的命令


<br/>

---
# 参考


[linux目录结构详细介绍][1]

[1]: http://yangrong.blog.51cto.com/6945369/1288072
[2]: https://unix.stackexchange.com/questions/74646/difference-between-lib-lib32-lib64-libx32-and-libexec

