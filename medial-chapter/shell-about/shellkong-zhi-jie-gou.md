# if选择结构
c语言中的`else if`在shell中写作`elif`，`elif`语句可以有多个
```
if <条件1>
then
  <命令>
elif <条件2>
then
  <命令>
else
  <命令>
fi
```
```
if <条件1>; then <命令>; elif <条件2>; then <命令>; else <命令>; fi

```
> 注意if和[]之间要有空格，[]和内容之间也有空格



# for循环结构
shell写法
```
for <变量> in 取值列表
do
    <命令>
done
```
```
for <变量> in <取值列表> ; do <命令> ;done
```
c语言写法
```
for((i = 0; i < 7; i++))
do
  echo $i
done
```

## 迭代元素
### 普通枚举
```
for i in 'fruit' 'meat' 'sleep'
do
    echo I like $i
done
```

### 命令替换
```
for var in `ls /var/log/*.log`
do
    echo $var
done
```

### 变量展开
```
sum=0
for i in {1..100}
do
    let sum+=$i
done
echo $sum
```
```
sum=0
for i in {1..100..2}
do
    let sum+=$i
done
echo $sum
```
```
for i in ｛a..z｝
do
    letters="${letters}${ch}"
done
echo $letters
```


## seq命令
```
seq <初始值> [增量] <结束值>
```

用脚本ping一下局域网ip
```
PREFIX=192.168.1.
for i in `seq 100 110`
do
    echo -n "${PREFIX}$i "
    ping -c5  ${PREFIX}${i} >/dev/null 2>&1
    if [ "$?" -eq 0 ];then
        echo "OK"
    else
        echo "Failed"
    fi
done
```



# while循环结构
```
while <条件>
do
    <循环体>
done
```
```
while 条件;do <循环体>; done
```

## 死循环
```
while :
do
    echo I love you forever
done
```
> 这是一个死循环，执行之后请用按组合键Ctrl + C来终止它

```
while true
do
    echo I love you forever
done
```
> `true` 和 `false` 都是shell中的一个命令，不是关键字

## 重定向
### 输入重定向
将文件内容逐行传递给while后面的命令(类似管道)，然后再执行循环体

```
while <命令>
do
    <循环体>
done < <文件名>
``` 

从/etc/passwd文件中读取用户名并输出
```
OLD_IFS=$IFS # IFS是文件内部分隔符
IFS=":"     # 设置分隔符为:
while read username var # var变量不可少
do
    echo "用户名:$username"
done < /etc/passwd 
IFS=$OLD_IFS

echo "$IFS"| od -b
```

### 输出重定向
会将命令的输出，以及循环体中的标准输出都重定向到指定的文件中

```
while <命令>
do
    <循环体>
done > <文件名>
```

每隔1分钟，ping一下局域网内主机192.168.1.101
```
while date
do
    ping -c5 192.168.1.101 >/dev/null 2>&1 
    if [ $? = 0 ];then
        echo OK
    else
        echo FAIL
    fi
    sleep 60 # 60秒是1分钟
done > ping.txt
```

### 遍历文件
```
while read line
do
    echo $line
done < test.txt
```
```
cat test.txt | while read line
do
    echo $line
done
```
```
for line in `cat test.txt`
do
    echo $line
done
```

while遍历和for遍历是有区别的，while按行分割，for按字段分割
```
[root@zhujipeng /]# cat test.txt
1
2 3
[root@zhujipeng /]# cat test.txt | while read line; do echo $line; done
1
2 3
[root@zhujipeng /]# for line in `cat test.txt`; do echo $line; done
1
2
3
```


# case分支结构
case匹配可以使用通配符`*`（任意多个字符）、`?`（一个字符）和`[]`（字符集）

```
case VAR in
    VAR1) <命令>;;
    VAR2) <命令>;;
    VAR3) <命令>;;
    ...
    *) <命令>
esac
```

输出带颜色的文字
```
str="is good "
read -p "你喜欢什么颜色：" color
case $color in
    red) echo -e "\e[1;31m$color $str \e[0m";;
    green) echo -e "\e[1;32m$color $str \e[0m";;
    yellow) echo -e "\e[1;33m$color $str \e[0m";;
    blue) echo -e "\e[1;34m$color $str \e[0m";;
    *) echo -e "\e[1;30m这是什么颜色?\e[0m";;
esac
```

<br/>

---

# 参考
[玩转Bash脚本：test测试语句][1]  
[玩转Bash脚本：选择结构之if][2]  
[玩转Bash脚本：循环结构之for循环][3]  
[玩转Bash脚本：循环结构之while循环][4]  
[玩转Bash脚本：选择结构之case][5]  

[1]: https://www.kancloud.cn/digest/wanbash/119000
[2]: https://www.kancloud.cn/digest/wanbash/119002
[3]: https://www.kancloud.cn/digest/wanbash/119006
[4]: https://www.kancloud.cn/digest/wanbash/119007
[5]: https://www.kancloud.cn/digest/wanbash/119004