# ping 
用来测试主机之间网络的连通性

```
ping [选项] <地址>
```
> 地址可以是ip，主机名（hostname），域名（domain）

|选项 | 说明 |
|--- |--- |
|-c COUNT | 指定发送请求的次数 |
|-D | 在结果前面显示unix时间戳 |
|-i INTERVAL | 指定发送请求的时间间隔 |
|-I | 指定发送使用的网络接口 |
|-n | 显示ip而不是域名 | 
|-q | 不显示中间信息 | 
|-R | 记录路由过程 |
|-v | 输出详细过程 |
|-V | 显示版本 |
> 有时候无法`ping`，有可能是被管理员或防火墙禁用了


# telnet
用于登录远程主机，对远程主机进行管理
> `telnet`因为采用明文传送报文，安全性不好，现在基本都不开放`telnet`服务，而改用更安全的`ssh`方式了

```
telnet [选项] <地址> <端口> 
```
> 地址可以是ip，主机名（hostname），域名（domain）

## telnet交互
`telnet`远程后会进入输入模式，此时无法退出，使用`Ctrl + ]` 可以切换到交互模式，输入`quit`后可以退出

```
[root@zhujipeng /]# telnet 192.168.8.192 12345
Trying 192.168.8.192...
Connected to 192.168.8.192.
Escape character is '^]'.
^]
telnet> ?
Commands may be abbreviated.  Commands are:

close   	close current connection
logout  	forcibly logout remote user and close the connection
display 	display operating parameters
mode    	try to enter line or character mode ('mode ?' for more)
open    	connect to a site
quit    	exit telnet
send    	transmit special characters ('send ?' for more)
set     	set operating parameters ('set ?' for more)
unset   	unset operating parameters ('unset ?' for more)
status  	print status information
toggle  	toggle operating parameters ('toggle ?' for more)
slc     	change state of special charaters ('slc ?' for more)
z       	suspend telnet
!       	invoke a subshell
environ 	change environment variables ('environ ?' for more)
?       	print help information
telnet> quit
Connection closed.
```



<br/>

---

# 参考

[每天一个linux命令 ping命令][1]  
[配置Linux禁止ping和请允许ping][2]  
[Linux禁止ping以及开启ping的方法][3]  
[每天一个linux命令 telnet命令][4]  
[linux下怎么退出telnet][5]  
[Centos 开启telnet-service服务][6]  

[1]: http://www.cnblogs.com/peida/archive/2013/03/06/2945407.html
[2]: http://sky9896.blog.51cto.com/2330653/1886609
[3]: http://www.cnblogs.com/chenshoubiao/p/4781016.html
[4]: http://www.cnblogs.com/peida/archive/2013/03/13/2956992.html
[5]: http://blog.csdn.net/love__coder/article/details/6733307
[6]: http://www.cnblogs.com/xlmeng1988/archive/2012/04/24/telnet-server.html