# gdb
GDB是一个由GNU开源组织发布的、UNIX/LINUX操作系统下的、基于命令行的、功能强大的程序调试工具

```
gdb [选项] <program>
gdb [选项] <program> <core>
gdb [选项] <program> <PID>
```
> program也就是你的执行文件，一般在当前目录下

|选项 | 说明 |
|--- |--- |
|-s FILE | 指定符号表 |
|-symbols=FILE | 指定符号表 |
|-c FILE | 指定`core dump`文件 |
|-core=FILE | 指定`core dump`文件 |
|-d DIRECTORY | 指定源文件搜索目录 |
|-directory=DIRECTORY | 指定源文件搜索目录 |

gdb交互命令请参考[用GDB调试程序][1]


<br/>

---

# 参考

[用GDB调试程序][1]  
[使用truss、strace或ltrace诊断软件的"疑难杂症"][2]  
[使用 gdb 调试运行中的 Python 进程][3]  

[1]: https://wiki.ubuntu.com.cn/%E7%94%A8GDB%E8%B0%83%E8%AF%95%E7%A8%8B%E5%BA%8F
[2]: https://www.ibm.com/developerworks/cn/linux/l-tsl/index.html
[3]: https://mozillazg.github.io/2017/07/debug-running-python-process-with-gdb.html