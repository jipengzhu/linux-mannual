# expect自动交互脚本
详情参见[expect - 自动交互脚本][1]

 
登陆脚本，参数为主机和密码
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



# 执行命令前设置变量
原理参考[这里][2]



# 获取linux发行版
```
get_os() {
    # Determine OS platform
    local U_NAME=$(uname | tr "[:upper:]" "[:lower:]")

    local LINUX_DIST=""
    # If Linux, try to determine specific distribution
    if [ "$U_NAME" == "linux" ]; then
        # If available, use LSB to identify distribution
        if [ -f /etc/lsb-release -o -d /etc/lsb-release.d ]; then
            LINUX_DIST=$(lsb_release -i | cut -d: -f2 | sed s/'^\s'//)

        # If system-release is available, then try to identify the name
        elif [ -f /etc/system-release ]; then
            LINUX_DIST=$(cat /etc/system-release | awk '{print $1}')

        # /etc/issue always exit (Ubuntu, Debian, CentOS, Fedora, RHEL, Arch, OpenSUSE)
        elif [ -f /etc/issue ]; then
            LINUX_DIST=$(head -n1 /etc/issue | awk '{print $1}')

        # Otherwise, use release info file
        else
            LINUX_DIST=$(ls -d /etc/[A-Za-z]*[_-][rv]e[lr]* | grep -v "lsb" | cut -d'/' -f3 | cut -d'-' -f1 | cut -d'_' -f1)
        fi
    else
        # error "this script only supports linux"
        :
    fi

    # For everything else (or if above failed), just use generic identifier
    if [ "x$LINUX_DIST" == "x" ]; then
        LINUX_DIST=${U_NAME}
    fi

    LINUX_DIST=$(echo ${LINUX_DIST} | tr "[:upper:]" "[:lower:]")

    echo ${LINUX_DIST}
}
```


<br/>

---

# 参考

[expect - 自动交互脚本][1]  
[Why is setting a variable before a command legal in bash][2]  

[1]: http://xstarcd.github.io/wiki/shell/expect.html
[2]: https://unix.stackexchange.com/questions/126938/why-is-setting-a-variable-before-a-command-legal-in-bash