# rm命令
当变量未定义时，`rm`很可能会删掉你不想删掉的文件，`-f` 选项很危险

# 赋值语句
shell中`=`两边不能有空格，和编程语言不一样
```
[root@zhujipeng test]# HAHA = haha
bash: HAHA: command not found
```

# 条件测试
## `[`和空格
`[` 和表达式之间要有空格
```
[root@zhujipeng test]# [ -n haha ] && echo yes || echo no
yes
[root@zhujipeng test]# [-n haha ] && echo yes || echo no
bash: [-n: command not found
no
[root@zhujipeng test]# [ -n haha] && echo yes || echo no
bash: [: missing `]'
no
```


## `[` 中的比较符号
```
[root@zhujipeng test]# [ 1 -gt 2 ] && echo yes || echo no
no
[root@zhujipeng test]# ll
total 0
[root@zhujipeng test]# [ 1 > 2 ] && echo yes || echo no
yes
[root@zhujipeng test]# ll
total 0
-rw-r--r-- 1 root root 0 Sep 23 09:07 2
```


## `[[` 中的比较符号
```
[root@zhujipeng test]# [[ 1 -gt 2 ]] && echo yes || echo no
no
[root@zhujipeng test]# [[ 1 > 2 ]] && echo yes || echo no
no
```


## `[` 中的逻辑符号
```
[root@zhujipeng test]# [ -n haha -a -n hehe ] && echo yes || echo no
yes
[root@zhujipeng test]# [ -n haha && -n hehe ] && echo yes || echo no
bash: [: missing `]'
no
```

## `[[` 中的逻辑符号
```
[root@zhujipeng test]# [[ -n haha -a -n hehe ]] && echo yes || echo no
bash: syntax error in conditional expression
bash: syntax error near `-a'
[root@zhujipeng test]# [[ -n haha && -n hehe ]] && echo yes || echo no
yes
```

## 变量未定义
`-n` 和 `-z` 的值需要用双引号扩起来，否则变量未定义时就会失败

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

<br/>

---

# 参考

[shell 语句出错自动退出][1]  
[linux shell 中判断字符串为空的正确方法][2]  
[Bash空格的那点事][3]  
[Bash引号的那点事][4]  
[shell中的括号（小括号，中括号，大括号）及单引号、 双引号，反引号][5]

[1]: http://blog.csdn.net/drbinzhao/article/details/8281645
[2]: http://blog.csdn.net/q_l_s/article/details/51435939
[3]: http://www.igigo.net/post/archives/152#main
[4]: http://www.igigo.net/post/archives/128
[5]: http://www.cnblogs.com/kex1n/p/6678286.html