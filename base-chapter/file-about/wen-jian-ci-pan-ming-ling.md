# df
df命令是用来查看***文件系统***的磁盘空间占用情况的

格式如下
```
df [选项] [文件...]
```

|选项 | 说明 |
|--- |--- |
|-a, --all | 全部文件系统的列表 |
|-B, --block-size=SIZE | 指定区块大小 |
|-h, --human-readable | 以K，M，G为单位，更加易读 |
|-H, --si | 与-h参数相同，但是K，M，G是以1000为换算单位 |
|-i, --inodes | 显示inode信息，而不是大小 |
|-k | 以KB为单位输出，等同于--block-size=1K|
|-m | 以MB为单位输出，等同于--block-size=1M|
|--no-sync | 在取得磁盘信息前，不执行sync命令 |
|--sync | 在取得磁盘信息前，先执行sync命令 |
|-t 文件系统类型 | 显示选定文件系统的磁盘信息 |
|-T, --print-type | 显示文件系统类型 |
|-x, --exclude-type=TYPE | 排除指定类型的文件系统 |
|--help | 显示帮助信息 | 
|--version | 显示版本信息 |

命令示例
- 显示磁盘使用情况    
`df`

- 列出文件系统的类型    
`df -T`

- 更易读的方式显示目前磁盘空间和使用情况  
`df -h`

- 以inode模式来显示磁盘使用情况    
`df -i`

- 显示指定类型磁盘    
`df -t ext3`


# du
du命令是用来查看***文件和目录***的磁盘空间占用情况的

格式如下
```
du [选项] [文件...]
```

|选项 | 说明 |
|--- |--- |
|-a, -all | 显示目录中文件的大小，而不仅仅是目录本身 | 
|-B, --block-size=SIZE | 指定区块大小 | 
|-b, -bytes | 显示目录或文件大小时，以byte为单位 |   
|-c, --total | 除了显示目录或文件的大小外，同时也显示所有目录和文件的总和 | 
|-D, --dereference-args  | 显示命令行中指定软链接源文件大小 |
|-d, --max-depth=N | 指定目录的最大深度 |
|-h, --human-readable | 以K，M，G为单位，更加易读 |
|-i, --inodes | 显示inode信息，而不是大小 | 
|-k | 以KB为单位输出，等同于--block-size=1K|
|-L, --dereference | 显示软链接源文件大小 |
|-l, --count-links | 重复计算硬件链接的文件 |
|-m | 以MB为单位输出，等同于--block-size=1M|
|-P, --no-dereference | 显示软链接本身的大小，是默认的选项|
|-S, --separate-dirs | 显示目录的大小时，不含其子目录的大小 |
|--si | 与-h参数相同，但是K，M，G是以1000为换算单位 |
|-s, --summarize | 仅显示总计，列出最后加总的值 |
|-X FILE, --exclude-from=FILE | 排除文件中指定目录或文件 |  
|--exclude=PATTERN | 排除指定的目录或文件 |
|-x, --one-file-xystem | 以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过 |
|--help | 显示帮助信息 | 
|--version | 显示版本信息 |


# fdisk
fdisk可以添加、删除、转换磁盘分区，指定磁盘后就会进入交互模式

格式如下
```
fdisk [选项] <设备>
fdisk -l [-u] [设备]
fdisk -p <分区...>
```

`fdisk -l`可以查看硬盘的详细信息，交互命令如下，详情参见[这里][3]

|交互命令 | 说明 |
|--- |--- |
|m | 列出帮助信息 |
|n | 创建一个分区 |
|d | 删除一个分区 |
|p | 列出分区表 |
|q | 不保存退出 |
|t | 改变分区类型 |
|w | 保存退出 |

# mount
mount命令是用来挂载设备的，详情参考[这里][4]

格式如下
```
mount [选项] <设备> <挂载点>
```

|选项 | 说明 |
|--- |--- |
|-a | 安装在/etc/fstab文件中列出的所有文件系统 |
|-f | 测试mount，检查设备和目录的而不真正挂载文件系统 |
|-n | 不把安装信息记录在/etc/mtab文件中 |
|-r, --read-only | 将文件系统安装为只读 |
|-v | 显示详细安装信息 |
|-w, --rw, --read-write | 将文件系统安装为可写，为命令默认情况 |
|-t, --types VFS_TYPE | 指定设备的文件系统类型，参见文件系统类型表 |
|-o, --options opts | 指定挂载文件系统时的选项，参见挂载选项表 |

文件系统类型表如下

|文件系统类型 | 说明 |
|--- |--- |
|ext2 | linux目前常用的文件系统 |
|etx3 | 对ext2增加日志功能后的扩展文件系统 |
|msdos | MS-DOS的fat16文件系统 |
|vfat | windows98的fat32文件系统 |
|ntfs | windows NT/2000/XP 的文件系统 |
|nfs | 网络文件系统 |
|iso9660 | CD-ROM光盘标准文件系统 |
|auto | 自动检测文件系统 |

挂载选项类表如下

|挂载选项 | 说明 |
|--- |--- |
|defaults | 使用所有选项的默认值（auto、nouser、rw、suid）|
|auto/noauto | 允许/不允许以–a选项进行安装 |
|user/nouser | 允许/不允许一般用户挂载 |
|ro | 以只读方式挂载 |
|rw | 以读写方式挂载 |
|exec/noexec | 允许/不允许执行二进制代码 |
|suid/nosuid | 确认/不确认suid和sgid位 |
|dev/nodev | 对/不对文件系统上的特殊设备进行解释 |
|codepage=XXX | 代码页 |
|iocharset=XXX | 字符集 |
|remount | 重新安装已经安装了的文件系统 |
|loop | 挂载[环回设备][5] |

挂载示例（挂载点需要先创建）

- 挂载硬盘    
`mount -t auto /dev/cdrom /mnt/cdrom`

- 挂载iso文件  
`mount -o loop linuxsetup.iso /mnt/iso1`

- 挂载u盘（假设u盘的路径是/dev/sda1）  
`mount /dev/sda1 /mnt/upan`


# unmount
unmount命令是用来卸载设备的，详情参考[这里][4]

格式如下
```
unmount [选项] <设备>
```

|选项 | 说明 |
|--- |--- |
|-l | 不马上卸载设备，空闲时再卸载 |


# /etc/fstab
fstab记录了开机启动时加载的文件系统，详情参考[这里][6]


<br/>

---

# 参考

[每天一个linux命令：df 命令][1]  
[每天一个linux命令：du 命令][2]  
[linux下使用fdisk工具快速挂载新硬盘][3]  
[linux里挂载（mount）和取消挂载（umount）命令的使用][4]  
[Linux中的loop设备][5]  
[linux之fstab文件详解][6]  
[Linux查看磁盘剩余空间方法][7]  
[玩转 Linux 之：磁盘分区、挂载知多少][8]  

[1]: http://www.cnblogs.com/peida/archive/2012/12/07/2806483.html
[2]: http://www.cnblogs.com/peida/archive/2012/12/10/2810755.html
[3]: http://yaksayoo.blog.51cto.com/510938/132809
[4]: http://blog.csdn.net/xiyangyang8/article/details/49725039
[5]: http://blog.csdn.net/scaleqiao/article/details/46777811
[6]: http://blog.csdn.net/richerg85/article/details/17917129
[7]: http://blog.sciencenet.cn/blog-2458445-999488.html
[8]: https://my.oschina.net/leejun2005/blog/290073