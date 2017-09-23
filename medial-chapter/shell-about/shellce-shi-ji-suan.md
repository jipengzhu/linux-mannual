# test命令
`test` 就是测试的意思，常用在流程控制语句中作为条件表达式
```
test EXPRESSION
test ! EXPRESSION
test EXPR1 && EXPR2
test EXPR1 || EXPR2
```



# 真假值
与其他语言不同，bash（包括其他Shell）中，是用0表示真，非0表示假
- 之所以用0表示成功，而不是1来表示，是因为成功的情况只有一种，而出错的可能却有许多
- 如果你有过POSIX编程经验（比如Linux下C编程），你应该会知道一个叫做`errno`的东西
- 你也会知道有大量的函数的调用结果，基本上都是返回0时表示操作成功，返回非0则出错



# [ 命令
`[` 是 `test`的命令的简写，`]` 是 `[` 命令的参数的结束标记
```
[ EXPRESSION ]
[ ! EXPRESSION ]
[ EXPR1 -a EXPR2 ]
[ EXPR1 -o EXPR2 ]
```



# [[ 命令
根据条件表达式的结果返回状态0或1，表达式部分和`[` 命令基本一样，不同如下
- `>` 和 `<` 符号不需要转移
- `==` 和 `!=` 使用正则匹配
- `AND` 和 `OR` 运算也不相同

```
[[ EXPRESSION ]
[[ ! EXPRESSION ]
[[ EXPR1 && EXPR2 ]
[[ EXPR1 || EXPR2 ]
```



# 表达式
表达式以 `[` 命令讲解，`[[` 与 `[` 的不同部分请参考 `[[`命令

### 数值比较符
|比较符 | 说明 |
|--- |--- | 
|$NUM1 -eq $NUM2 | 等于	(equal) |
|$NUM1 -ne $NUM2 | 不等于 (not equal) |
|$NUM1 -gt $NUM2 | 大于	(greater than) |
|$NUM1 -lt $NUM2 | 小于	(less than) |
|$NUM1 -ge $NUM2 | 大于等于 (greater or equal) |
|$NUM1 -le $NUM2 | 小于等于 (less or equal) |
> 数字比较不是用 `>` 和 `<` 符号，它们是重定向和字符串比较符
```
[root@zhujipeng test]# [ 2 > 3 ] && echo yes || echo no
yes
[root@zhujipeng test]# ls
3
[root@zhujipeng test]# [ 12 \> 3 ] && echo yes || echo no
no
```

### 字符串比较符
|比较符 | 说明 |
|--- |--- |
|$STR1 = $STR2  | 测试是否相等 |
|$STR1 == $STR2  | 测试是否相等 |
|$STR1 != $STR2 | 测试是否不等 |
|$STR1 \< $STR2 | 测试str1的字典序是否在小于str2 |
|$STR1 \> $STR2 | 测试str1的字典序是否在大于str2 |
|$STR1 | 总是返回0 |
|-n "$str1" | 测试是否为***空串*** | 
|-z "$str1" | 测试是否为***非空串*** |
> 注意 `[` 命令中 `<` 和 `>` 需要转义，否则是代表重定向的意思
```
[root@zhujipeng test]# [ a > b ] && echo yes || echo no
yes
[root@zhujipeng test]# ls
b
[root@zhujipeng test]# [ a \> b ] && echo yes || echo no
no
[root@zhujipeng test]# [ a < b ] && echo yes || echo no
yes
[root@zhujipeng test]# [ a < c ] && echo yes || echo no
bash: c: No such file or directory
no
```

> 注意 `[` 命令中 `-n` 和 `-z` 的值需要用双引号扩起来，否则变量未定义时就会失败
```
[root@zhujipeng test]# unset HAHA
[root@zhujipeng test]# set -u : $HAHA
bash: HAHA: unbound variable
[root@zhujipeng test]# HAHA=haha
[root@zhujipeng test]# set -u : $HAHA
[root@zhujipeng test]# unset HAHA
[root@zhujipeng test]# set -u : $HAHA
bash: HAHA: unbound variable
[root@zhujipeng test]# set +u
[root@zhujipeng test]# [ -n $HAHA ] && echo yes || echo no
yes
[root@zhujipeng test]# [ -n "$HAHA" ] && echo yes || echo no
no
[root@zhujipeng test]# export HAHA=
[root@zhujipeng test]# [ -n "$HAHA" ] && echo yes || echo no
no
[root@zhujipeng test]# unset HAHA
```

> 需要在比较符两边的元素的前面添加`x`字符，避免变量未定义导致的错误
```
[ a \> $HAHA ] && echo yes || echo no
bash: [: a: unary operator expected
no
[root@zhujipeng test]# HAHA=
[root@zhujipeng test]# [ a \> $HAHA ] && echo yes || echo no
bash: [: a: unary operator expected
no
[root@zhujipeng test]# [ xa \> x$HAHA ] && echo yes || echo no
yes
[root@zhujipeng test]# unset HAHA
```

### 文件比较符
|比较符 | 说明 |
|--- |--- |
|-e FILENAME | 是否存在 |
|-d FILENAME | 是否为目录 |
|-f FILENAME | 是否为普通文件 |
|-h FILENAME | 是否为软链接文件 |
|-L FILENAME | 是否为软链接文件 |
|-r FILENAME | 是否有读权限 |
|-w FILENAME | 是否写读权限 |
|-x FILENAME | 是否有执行权限 |
|-s FILENAME | 文件大小是否大于0 |
|-c FILENAME | 是否为字符设备文件 |
|-b FILENAME | 是否为块设备文件 |
|FILENAME1 -nt FILENAME2| 文件1是否比文件2***新*** |
|FILENAME1 -ot FILENAME2| 文件1是否比文件2***旧*** |
> `-e` 检测的是链接文件的源文件是否存在
```
[root@zhujipeng test]# ll
total 0
lrwxrwxrwx 1 root root 5 Sep 20 12:49 test1.link -> test1
[root@zhujipeng test]# [ -e test1 ] && echo yes || echo no
no
[root@zhujipeng test]# [ -e test1.link ] && echo yes || echo no
no
[root@zhujipeng test]# [ -h test1.link ] && echo yes || echo no
yes
```

### 模糊比较
`[` 会做路径展开（file globbing）和单词分割（word splitting），而 `[[` 不会

```
[root@zhujipeng test]# ls
a.log  a.txt
[root@zhujipeng test]# A='a.*'
[root@zhujipeng test]# echo $A
a.log a.txt
[root@zhujipeng test]# echo "$A"
a.*

[root@zhujipeng test]# [ $A == a* ] && echo yes || echo no
bash: [: too many arguments
no
[root@zhujipeng test]# [ "$A" == a* ] && echo yes || echo no
bash: [: too many arguments
no
[root@zhujipeng test]# [ $A == "a*" ] && echo yes || echo no
bash: [: too many arguments
no
[root@zhujipeng test]# [ "$A" == "a*" ] && echo yes || echo no
no
[root@zhujipeng test]# [ "$A" == "a.*" ] && echo yes || echo no
yes

[root@zhujipeng test]# [[ $A == a* ]] && echo yes || echo no
yes
[root@zhujipeng test]# [[ "$A" == a* ]] && echo yes || echo no
yes
[root@zhujipeng test]# [[ $A == "a*" ]] && echo yes || echo no
no
[root@zhujipeng test]# [[ "$A" == "a*" ]] && echo yes || echo no
no
[root@zhujipeng test]# [[ "$A" == "a.*" ]] && echo yes || echo no
yes
```



# 数值运算
## 整数运算
## [] 运算符
```
[root@zhujipeng test]# echo $[ 1 * 3 ]
3
```

## (( )) 运算符
```
[root@zhujipeng test]# echo $(( 1 * 3 ))
3
```

## expr命令
```
[root@zhujipeng test]# echo `expr 1 \* 3`
3
```

## let命令
```
[root@zhujipeng test]# let a=1+2 && echo $a
3
[root@zhujipeng test]# a=1 && let a++ && echo $a
2
[root@zhujipeng test]# a=2 && let a+=1 && echo $a
3
```


## 浮点数运算(bc)
除法运算的时候，默认是取整的，即没有小数部分，需要使用`scale`设置精度

### 常规运算
```
[root@zhujipeng test]# echo '3.0 - 1.0' | bc
2.0
[root@zhujipeng test]# echo '2.0/3' | bc
0
[root@zhujipeng test]# echo 'scale=3;2.0/3' | bc
.666
```

### 进制转换
不指定进制时默认是10进制

```
[root@zhujipeng test]# echo 'ibase=8;755' | bc
493
[root@zhujipeng test]# echo 'obase=2;ibase=8;755' | bc
111101101
[root@zhujipeng test]# echo 'obase=8;ibase=2;111101101' | bc
755
```


<br/>

---

# 参考

[玩转Bash脚本：test测试语句][1]  
[Linux 之 shell 比较运算符][2]   
[Linux-shell-算术运算{expr、bc、dc、(( ))和[ ]}][3]  
[Why do shell script comparisons often use x$VAR = xyes?][4]    
[linux shell 中判断字符串为空的正确方法][5]

[1]: https://www.kancloud.cn/digest/wanbash/119000
[2]: http://blog.csdn.net/ithomer/article/details/6836382
[3]: http://www.cnblogs.com/snowsolf/p/3325235.html
[4]: https://stackoverflow.com/questions/174119/why-do-shell-script-comparisons-often-use-xvar-xyes
[5]: http://blog.csdn.net/q_l_s/article/details/51435939