# inotify
一种强大的、细粒度的、异步文件系统监控机制，它满足各种各样的文件监控需要，可以监控文件系统的访问属性、读写属性、权限属性、创建、删除、移动等操作。`inotify-tools` 是一个C库和一组命令行的工作提供Linux下inotify的简单接口，`inotify-tools`安装后会得到`inotifywait`和`inotifywatch`命令


## inotifywait
监控有关文件的各种变化

```
inotifywait [-hcmrq] [-e <event> ] [-t <seconds> ] [--format <fmt> ] [--timefmt <fmt> ] <file> [ ... ]
```

|选项 | 说明 |
|--- |--- |
|--fromfile &lt; file &gt; | 指定从文件中读取排除文件列表 |
|-m, --monitor | 事件第一次发生后不退出，而是继续监听 |       
|-d, --daemon | 后台持续运行，需要配合`--outfile`指定日志输出文件 |
|-o, --outfile | 输出事件到文件中而不是标准输出 |
|-s, --syslog | 输出错误到syslog中而不是标准错误 |
|-r, --recursive | 递归监听子目录，忽略符号链接 |
|-q, --quiet | 输出少量的信息 |
|--exclude &lt; pattern &gt; | 排除指定文件，大小写敏感 |
|--excludei &lt; pattern &gt; | 排除指定文件，大小写不敏感 |
|-t &lt; seconds &gt;, --timeout &lt; seconds &gt; | 指定事件的超时时间 |
|-e &lt; event &gt;, --event &lt; event &gt; | 指定监听的时间，可使用多次 |
|-c, --csv | 输出格式为CSV格式 |
|--format &lt; fmt &gt | 指定输出的格式 |
> 输出格式的详细信息请参考 `inotifywait` 的 `man` 手册

|事件 | 说明 |
|--- |--- |
|access | 目录里的文件被读取了 |
|modify | 目录里的文件被编辑了 |
|attrib | 目录里的文件属性被改变了 |
|close_write | 写模式打开的文件被关闭了 |
|close_nowrite | 只读模式打开的文件被关闭了 |
|close | 打开的文件被关闭了 |
|open | 目录里的文件被打开了 |
|moved_to | 文件或目录被移入了监听的目录 |
|moved_from | 文件或目录被移出了监听的目录 |
|move | 有文件或目录被在监听的目录中被移动了 |
|create | 有文件或目录被在监听的目录中被创建了 |
|delete | 有文件或目录被在监听的目录中被删除了 |
|unmount | 文件所在的文件系统被卸载了 |


## inotifywatch
统计文件系统访问的次数
> `inotifywatch` 的 使用方法和 `inotifywait` 差不多



# rsync
rsync是一个远程数据同步工具，只传送两个文件的不同部分

```
Access via remote shell:
   Pull: rsync [OPTION...] [USER@]HOST:SRC... [DEST]
   Push: rsync [OPTION...] SRC... [USER@]HOST:DEST

Access via rsync daemon:
   Pull: rsync [OPTION...] [USER@]HOST::SRC... [DEST]
         rsync [OPTION...] rsync://[USER@]HOST[:PORT]/SRC... [DEST]
   Push: rsync [OPTION...] SRC... [USER@]HOST::DEST
         rsync [OPTION...] SRC... rsync://[USER@]HOST[:PORT]/DEST
```


## 工作模式
`rsync` 有2种不同的工作模式

1. `shell` 模式：使用远程shell程序（如ssh或rsh）进行连接，一个冒号时使用这种模式
2. `daemon` 模式：使用TCP直接连接rsync daemon，两个冒号或URL写法时使用这种模式

|选项 | 说明 |
|--- |--- |
|-v, --verbose | 输出更详细的信息 |
|-a, --archive | 试用归档模式，等同于`-rlptgoD` |
|-r, --recursive | 递归处理目录 |
|-u, --update | 忽略比接收端更新的文件 |
|--inplace | 替换接收端的文件 | 
|--append | 追加到接收端的文件 |
|-d, --dirs | 不递归处理目录 |
|-l, --links | 保持软链接的形式 |
|-L, --copy-links | 使用软链接对应的源文件 |
|--copy-unsafe-links | 只传输软链接的源文件不存在的文件 |
|--safe-links | 只传输软链接的源文件存在的文件 |
|-H, --hard-links | 保持硬连接 |
|-p, --perms | 保留文件的权限 |
|-E, --executability  | 保留可执行权限 |
|--chmod=CHMOD | 修改文件的权限 |
|-A, --acls | 保留访问策略 |
|-X, --xattrs | 保留额外的属性 |
|-o, --owner | 保留用户属性（只能超级用户使用）|
|-g, --group | 保留组属性 |
|-t, --times | 保留修改时间 |
|-m, --prune-empty-dirs | 忽略空的文件 |
|--exclude=PATTERN | 排除指定模式的文件 |
|--exclude-from=FILE | 从文件中读取排除模式 |
|--include=PATTERN | 包含指定模式的文件 |
|--include-from=FILE     read include patterns from FILE
             --files-from=FILE       read list of source-file names from FILE
        -h, --human-readable        output numbers in a human-readable format
            --progress              show progress during transfer
            --list-only             list the files instead of copying them
            
            -4, --ipv4                  prefer IPv4
        -6, --ipv6                  prefer IPv6
            --version               print version number
       
            --daemon                run as an rsync daemon
            

<br/>

---

# 参考

[Linux下同步工具inotify+rsync使用详解][1]  
[inotifywait命令][2]  
[rsync命令][3]  
[Inotify: 高效、实时的Linux文件系统事件监控框架][4]    
[Linux-Rsync服务器/客户端搭建实战][5]  

[1]: http://seanlook.com/2014/12/12/rsync_inotify_setup/index.html
[2]: http://man.linuxde.net/inotifywait
[3]: http://man.linuxde.net/rsync
[4]: http://www.infoq.com/cn/articles/inotify-linux-file-system-event-monitoring
[5]: http://www.cnblogs.com/JohnABC/p/6203524.html