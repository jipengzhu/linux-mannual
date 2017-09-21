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

## 检测替换
使用下面表格中的的形式，bash 会测试 
- PARAMETER 是否是未定义（unset）
- PARAMETER 是否是空字符串（null）

在下面的表格中，VAR 可进行 
- “波浪线展开”
- “变量替换”
- “命令替换” 
- “算术展开”

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
