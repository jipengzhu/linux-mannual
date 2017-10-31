# 用户登录
## ssh
远程登录和数据转发

```
ssh [-1246AaCfgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec] [-D [bind_address:]port] [-E log_file]
         [-e escape_char] [-F configfile] [-I pkcs11] [-i identity_file] [-L [bind_address:]port:host:hostport]
         [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
         [-Q cipher | cipher-auth | mac | kex | key] [-R [bind_address:]port:host:hostport] [-S ctl_path]
         [-W host:port] [-w local_tun[:remote_tun]] [user@]hostname [command]
```

```
➜  ~ ssh root@192.168.8.238
root@192.168.8.238's password:
Last login: Sun Oct 29 05:06:33 2017 from 192.168.8.192
[root@localhost ~]#
```

ssh登录部分不复杂，复杂的部分在于数据转发，详情参见[这里][2]

```
ssh -NL 0.0.0.0:3000:127.0.0.1:3001 root@101.236.56.121
```
上述命令代表将发送到`101.236.56.121`的`3000`端口的数据转发到本机（`127.0.0.1`）的`3001`端口


## sshpass
可以指定密码的远程登录工具，需要额外安装，详情参见[这里][5]


## expect  
登陆脚本如下，参数为主机和密码，用户名按需修改，配合`item2`的`profile`非常不错
```
#! /usr/bin/expect

set host [ lindex $argv 0 ]
set pass [ lindex $argv 1 ]
set timeout 10

spawn ssh -o ServerAliveInterval=60 root@$host
expect {
	"*yes/no" { send "yes\r"; exp_continue}
	"*password" {send "${pass}\r"}
}
interact
``` 



# 免密登录
每次登陆都需要输入密码很麻烦，可以通过免密来解决，详情参考[这里][7]
> `ssh-copy-id`命令可以简化拷贝过程


# 用户切换
## su
切换用户

格式如下
```
su [选项] [用户名]
```

|选项 | 说明 |
|--- |--- |
|-c command, --command=command | 切换时执行命令 |
|-, -l, --login | 切换时使用登陆模式，重新读取环境变量 |
|-m, -p|切换时保留环境变量，如果使用了－l选项，忽略该选项|
|-s SHELL, --shell=SHELL| 切换时指定使用的shell |


## sudo
提升普通用户的权限
> su命令允许普通用户完全变更为root用户身份
> 但这也无疑会暴露了超级管理员的密码，使得系统增添很多的安全隐患
> 因此我们需要使用sudo程序来仅将特定命令的执行权限赋予给指定的用户

格式如下
```
sudo [选项] [用户名]
```

|选项 | 说明 |
|--- |--- |
|-b | 在后台执行指定的命令 |
|-k | 清空安全时间，下次执行sudo时需要再次密码验证 |
|-l | 列出当前用户可执行的命令 | 
|-u user | 用户名或UID值 以指定的用户身份执行命令 |
|-p prompt | 更改询问密码的提示语 |

> l -> list | b -> background

sudo相关配置文件和visudo命令可以参考[这里][2]


## runuser
使用指定用户执行命令，详情参见[这里][14]


<br/> 

---

# 参考

[Linux 下 SSH 命令实例指南][1]  
[基于SSH协议的端口转发][2]  
[通过 SSH 实现 TCP / IP 隧道（端口转发）][3]  
[动态端口转发：安装带有 SSH 的 SOCKS 服务器][4]  
[sshpass：一个很棒的免交互 SSH 登录工具][5]  
[expect - 自动交互脚本][6] 
[如何在 CentOS / RHEL 上设置 SSH 免密码登录][7]
[Linux使用ssh公钥实现免密码登录Linux][8]  
[ssh 免密码设置失败原因总结][9]  
[KNOWN_HOSTS处理][10]  
[实战演练su命令与sudo服务][11]    
[Linux 下以其他用户身份运行程序—— su、sudo、runuser][12]  
[linux 切换用户身份、su、sudo、/etc/sudoers][13]
[linux 常用命令： runuser][14]

[1]: https://linux.cn/article-3858-1.html
[2]: http://www.cnblogs.com/sting2me/p/5167730.html
[3]: https://linux.cn/article-8945-1.html
[4]: https://linux.cn/article-8947-1.html
[5]: https://linux.cn/article-8086-1.html
[6]: http://xstarcd.github.io/wiki/shell/expect.html
[7]: https://linux.cn/article-6901-1.html
[8]: http://www.cnblogs.com/Percy_Lee/p/5698603.html
[9]: http://www.cnblogs.com/yjmyzz/p/4481720.html
[10]: https://yq.aliyun.com/articles/6827
[11]: http://zhang789.blog.51cto.com/11045979/1846231
[12]: http://blog.chopmoon.com/favorites/219.html
[13]: http://desert3.iteye.com/blog/1663995
[14]: http://www.cnblogs.com/doscho/p/6498148.html