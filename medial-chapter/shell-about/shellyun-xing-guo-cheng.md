# shell运算过程
1. 将命令分割成tokens
2. 检查token是不是关键字
3. 检查token是不是别名
4. 花括号（{}）展开
5. 波浪号（~）展开
6. 变量替换
7. 命令替换
8. 算术替换
9. 单词分割（word splitting）
10. 路径匹配（path globbing）


#  花括号展开
在花括号内，可以是以逗号分隔的字符串，或者是一个序列表达式
```
[root@zhujipeng test]# echo a{b,c,d}e
abe ace ade
[root@zhujipeng test]# echo a{b..d}e
abe ace ade
[root@zhujipeng test]# echo a{b..f..2}e
abe ade afe
[root@zhujipeng test]# echo a{1..3}e
a1e a2e a3e
[root@zhujipeng test]# echo a{001..3}e
a001e a002e a003e
[root@zhujipeng test]# echo a{1..7..3}e
a1e a4e a7e
```

# 波浪线展开
如果一个单词以未被引号包括的 '~' 开头，则
- 这个单词所有到斜线 '/'(如果有得话) 之间的字符被认为是一个波浪线前缀字符串（TILDE-PREFIX）
- 如果波浪线前缀对应的登录名是无效的，或者波浪线展开失败，则保留原样
- 如果波浪线前缀是 '~+'，则被替换为 'PWD' 变量的值
- 如果波浪线前缀是 '~-'，则被替换为 'OLDPWD' 变量的值(如果存在的话)

```
[root@zhujipeng test]# echo ~
/root
[root@zhujipeng test]# echo ~root/.bashrc
/root/.bashrc
[root@zhujipeng test]# echo "~root/.bashrc"
~root/.bashrc
[root@zhujipeng test]# echo ~guest
~guest
[root@zhujipeng test]# echo ~-
/root
[root@zhujipeng test]# cd /tmp
[root@zhujipeng tmp]# cd -
/root/test
[root@zhujipeng test]# echo ~+
/root/test
[root@zhujipeng test]# echo ~-
/tmp
```



# 变量替换
- 变量替换的基本的形式是 ${PARAMETER}
- 如果 PARAMETER 的第一个字符是 "!"，会进行“间接变量展开”
- 但是 ${!PREFIX*} 和 ${!NAME[@]} 是例外，在下面会介绍

## 安全替换
使用下面表格中的的形式，bash 会测试 
- PARAMETER 是否是未定义（unset）
- PARAMETER 是否是空字符串（null）

在下面的表格中，VAR 可进行 
- “波浪线展开”
- “变量替换”
- “命令替换” 
- “算术替换”

如果 VAR 是字符串，就不会做展开

> 如果删除冒号 ':'，只会测试 PARAMETER 是否是 unset(是否存在)


|变量 | 说明 |
|--- |--- |
|${PARAMETER:-VAR} | 如果 PARAMETER 是 unset 或者 null，最终将返回***变量 VAR***的展开结果 |
|${PARAMETER:=VAR} | 如果 PARAMETER 是 unset 或者 null，最终将***变量 VAR***的展开结果赋值给PARAMETER |
|${PARAMETER:?VAR} | 如果 PARAMETER 是 unset 或者 null，最终将***变量 VAR***的展开结果（如果未给出 WORD，会有一条消息）写入标准错误输出以及 shell，如果 shell 是非交互式的，就退出 shel |
|${PARAMETER:+VAR} | 如果 PARAMETER 是 unset 或者 null，最终结果是 nothing |

```
[root@zhujipeng test]# echo ${PARAMETER:-VAR} && echo ${PARAMETER}
VAR

[root@zhujipeng test]# echo ${PARAMETER:-${VAR}} && echo ${PARAMETER}


[root@zhujipeng test]# echo ${PARAMETER:=${VAR}} && echo ${PARAMETER}


[root@zhujipeng test]# echo ${PARAMETER:?${VAR}} && echo ${PARAMETER}
bash: PARAMETER:
[root@zhujipeng test]# echo ${PARAMETER:+${VAR}} && echo ${PARAMETER}


[root@zhujipeng test]# VAR=haha
[root@zhujipeng test]# unset PARAMETER && echo ${PARAMETER:-${VAR}} && echo ${PARAMETER}
haha

[root@zhujipeng test]# unset PARAMETER && echo ${PARAMETER:=${VAR}} && echo ${PARAMETER}
haha
haha
[root@zhujipeng test]# unset PARAMETER && echo ${PARAMETER:?${VAR}} && echo ${PARAMETER}
bash: PARAMETER: haha
[root@zhujipeng test]# unset PARAMETER && echo ${PARAMETER:+${VAR}} && echo ${PARAMETER}


[root@zhujipeng test]# unset VAR && unset PARAMETER
```


## 变量展开
`*` 和 `@` 的区别请参考`shell脚本基础`章节 

```
${!PREFIX*}
${!PREFIX@}
```
> 展开结果为所有以 PREFIX 为前缀的变量的名字

```
${!NAME[@]}
${!NAME[*]}
```
> 如果 NAME 是数组变量，展开为数组索引(key)的列表
> 如果 NAME 不是数组变量，当变量存在时展开为0


## 参数的长度
```
${#PARAMETER}
```
> 位置参数是参数的个数，数组变量时数组的长度 


## 子串截取
```
${PARAMETER:OFFSET}
${PARAMETER:OFFSET:LENGTH}
```
> OFFSET: 截取的开始位置，为负时从尾部向前截取
> LENGTH: 截取的长度，没有则截取到末尾


1. 当 PARAMETER 是普通变量时，以字符为单位对参数做截取
2. 当 PARAMETER 是位置参数时，表示从OFFSET处开始的LENGTH个位置参数
3. 当 PARAMETER 是数组变量时，表示从OFFSET处开始的LENGTH个数组变量


1. 对于字符串值，索引从 0 开始(0-based)
2. 对于位置参数，索引从 1 开始(1-based)
3. 对于数组变量，索引从 0 开始(0-based)


## 删除匹配
```
${PARAMETER#PATTERN}
${PARAMETER##PATTERN}
${PARAMETER%PATTERN}
${PARAMETER%%PATTERN}
```
> \#代表从左向右匹配，%代表从右向左
> 一个代表最小匹配，两个代表最大匹配

```
[root@zhujipeng test]# cat test.sh
HAHA='var/log/messages'
echo ${HAHA#*a}
echo ${HAHA##*a}
echo ${HAHA%a*}
echo ${HAHA%%a*}
[root@zhujipeng test]# sh test.sh
r/log/messages
ges
var/log/mess
v
```

## 正则替换
```
${PARAMETER/PATTERN/STRING}
${PARAMETER//PATTERN/STRING}
```
> 一个斜杠替换第一个匹配，两个斜杠替换所有匹配
> 如果参数是“*”或者“@”，对每个位置参数做上面的操作

```
[root@zhujipeng test]# cat test.sh
HAHA='var/log/messages'
echo ${HAHA/a/b}
echo ${HAHA//a/b}
[root@zhujipeng test]# sh test.sh
vbr/log/messages
vbr/log/messbges
```

## 大小写转换
```
${PARAMETER^PATTERN}
${PARAMETER^^PATTERN}
${PARAMETER,PATTERN}
${PARAMETER,,PATTERN}
```
> 一个替换第一个匹配，两个替换所有匹配
> 但是实际测试却是一个不生效，两个生效
> 如果参数是“*”或者“@”，对每个位置参数做上面的操作

```
[root@zhujipeng test]# cat test.sh
HAHA='var/log/messages'
echo ${HAHA^a}
echo ${HAHA^^a}

HAHA='vAr/log/messAges'
echo ${HAHA,A}
echo ${HAHA,,A}
[root@zhujipeng test]# sh test.sh
var/log/messages
vAr/log/messAges
vAr/log/messAges
var/log/messages
```


# 命令替换
```
$(COMMAND)
`COMMAND`
```


# 算术替换
```
$(( EXPRESSION ))
```


# 单词分割
shell会对对未被引号引用的展开进行单词分割
> 分割符由`IFS` 变量决定

```
[root@zhujipeng test]# cat test.sh
HAHA='haha /var/log/*yum*.log'
for i in ${HAHA}
do
	echo $i
done
echo ------
for i in "${HAHA}"
do
        echo $i
done
[root@zhujipeng test]# sh test.sh
haha
/var/log/anaconda.yum.log
/var/log/yum.log
------
haha /var/log/anaconda.yum.log /var/log/yum.log
```

# 路径匹配
shell会对展开的结果进行路径匹配
```
[root@zhujipeng test]# cat test.sh
HAHA='haha /var/log/*yum*.log'
for i in ${HAHA}
do
	echo $i
done
echo ------
for i in "${HAHA}"
do
        echo $i
done
[root@zhujipeng test]# sh test.sh
haha
/var/log/anaconda.yum.log
/var/log/yum.log
------
haha /var/log/anaconda.yum.log /var/log/yum.log
```


<br/>

---

# 参考

[shell 基本特性之~ shell展开详解][1]  
[Shell中的 IFS][2]  


[1]: http://www.jianshu.com/p/403f3554e2c1
[2]: http://skypegnu1.blog.51cto.com/8991766/1543319