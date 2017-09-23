# 自动交互脚本
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



# 获取发行版
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



# 检查网络畅通
# ping
```
check_network_by_ping(){
    local REMOTE_SERVER_HOST=$1

    echo "Checking if ${REMOTE_SERVER_HOST} is reachable."

    if [ $(ping -c 1 ${REMOTE_SERVER_HOST} | grep "1 packets transmitted, 1 received" | wc -l) == 1 ]; then
        echo "remote host ${REMOTE_SERVER_HOST} is reachable."
    else
        echo "remote host ${REMOTE_SERVER_HOST} is not reachable via ping. maybe forbidden by firewall"
    fi
}
```


## telnet
```
check_network_by_telnet(){
    local REMOTE_HOST=$1
    local REMOTE_PORT=$2

    local telnet_output_log="/tmp/telnet_output.log"
    telnet ${REMOTE_HOST} ${REMOTE_PORT} > ${telnet_output_log} 2>&1 << EOF
        quit
EOF

    local TELNET_RESULT=
    if [[ $(grep "Connected" ${telnet_output_log} | wc -l) == 1 ]]; then
            TELNET_RESULT=0
        else
            TELNET_RESULT=1
    fi

    rm -rf ${telnet_output_log}

    return ${TELNET_RESULT}
}
```



## netcat
```
check_network_by_netcat(){
    local REMOTE_HOST=$1
    local REMOTE_PORT=$2

    local NETCAT_RESULT=
    echo test | nc -w 6 ${REMOTE_HOST} ${REMOTE_PORT} &> /dev/null && NETCAT_RESULT=0 || NETCAT_RESULT=1

    return ${NETCAT_RESULT}
}
```



# 版本比较
```
compare_version(){
    if [ -z "${1}" -o -z "${2}" ]; then
        echo "version can't be empty"
        exit 1
    fi

    typeset IFS='.'
    typeset -a v1=( $1 )
    typeset -a v2=( $2 )
    typeset n d


    local count=0
    if [ ${#v1[@]} -gt ${#v2[@]} ]; then
        count=${#v1[@]}
    else
        count=${#v2[@]}
    fi

    for (( n = 0; n < ${count}; n += 1 ))
    do
        d=$((v1[n]-v2[n]))
        if [[ ${d} != 0 ]] ; then
            [ ${d} -lt 0 ] && echo -1 || echo 1

            return
        fi
    done

    echo 0
}
```



# 检查通配文件
```
check_file_exists() {
    ! ls $1 &> /dev/null && echo "File \"${1}\" does not exist" || echo "file \"${1}\" exists"
}

check_file_wildcard() {
    [[ "$1" =~ [*?\[] ]]  && echo "FileName can't contains wildcard"
}
```


<br/>

---

# 参考

[expect - 自动交互脚本][1]  
[Why is setting a variable before a command legal in bash][2]  
[Shell Script to find the Operating System of the machine][3]  
[How can I get distribution name and version number in a simple shell script][4]  
[Check if a file exists with wildcard in shell script][5]  

[1]: http://xstarcd.github.io/wiki/shell/expect.html
[2]: https://unix.stackexchange.com/questions/126938/why-is-setting-a-variable-before-a-command-legal-in-bash
[3]: https://stackoverflow.com/questions/35236947/shell-script-to-find-the-operating-system-of-the-machine
[4]: https://unix.stackexchange.com/questions/6345/how-can-i-get-distribution-name-and-version-number-in-a-simple-shell-script
[5]: https://stackoverflow.com/questions/6363441/check-if-a-file-exists-with-wildcard-in-shell-script