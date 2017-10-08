# 基本格式
Shell脚本的文件名后缀通常是.sh （当然也可以使用其他后缀或者没有后缀，`.sh`只是为了规范） 

```
#!/bin/bash  
# 注释使用#号
# 第一行是Shebang
# 告诉系统使用bash程序执行这个文件
```



# 执行方法
## 使用路径名
为文件添加可执行权限
`chmod u+x test.sh`
然后使用路径名执行
`./test.sh`



# 变量
变量不需要声明，初始化不需要指定类型，变量值默认当作字符串处理

1. 只能使用数字，字母和下划线，且不能以数字开头
2. 变量名区分大小写
3. 变量名要通俗易懂

变量赋值是通过等号(=)进行赋值
> ***注意***： 在变量、等号和值之间不能出现空格


## 变量分类
Shell变量有这几类：本地变量、环境变量、局部变量、位置变量、特殊变量

### 本地变量
对当前shell进程有效的，对当前进程的子shell进程和其它shell进程无效

1. 定义：VAR_NAME=VALUE
2. 变量引用：${VAR_NAME} 或者 $VAR_NAME
3. 取消变量：unset VAR_NAME

### 环境变量
对当前shell进程及其子shell进程有效，对其它的shell进程无效

1. 定义：export VAR_NAME=VALUE

> 要想对所有shell进程都有效需要配置到配置文件中

### 局部变量
在函数中调用，函数执行结束，变量就会消失

1. 定义：local VAR_NAME=VALUE

### 位置变量
$0表示脚本名，$1-9表示第1到9个参数

### 特殊变量
|变量 | 说明 |
|--- |--- |
|$? | 上一条命令的返回状态码， 返回状态码在0-255之间 |
|$# | 参数个数 |
|$* | 所有的参数 |
|$@ | 所有的参数 |
|$_ | 最后一个参数 |
|$$ | 当前shell的进程号（PID）|
|$! | 后台执行的最后一个命令的进程号（PID） |

> \$\$ 可以实现脚本自杀，或者使用exit命令直接退出，也可以使用exit [num]

### $* 和 $@的区别
1. 不带双引号时，$* 和 $@一样，都会对参数进行展开
2. 带双引号时，$* 会将输入参数合并为一个参数
3. 带双引号时，$@ 会保留输入参数的结构

```
[root@zhujipeng /]# cat test.sh
echo 'print param from $*'
for var in $*
do
  echo $var
done

echo 'print param from $@'
for var in $@
do
  echo $var
done

echo 'print param from "$*"'
for var in "$*"
do
  echo $var
done

echo 'print param from "$@"'
for var in "$@"
do
  echo $var
done
[root@zhujipeng /]# sh test.sh a 'b c'
print param from $*
a
b
c
print param from $@
a
b
c
print param from "$*"
a b c
print param from "$@"
a
b c
```


## 引号
Shell编程中有三类引号：单引号、双引号、反引号

1. ''单引号不解析变量
2. ""双引号会解析变量
3. ``反引号获取命令的结果

> 反引号是执行并引用一个命令的执行结果，类似于$(...)


## 函数
```
function FUNCTION_NAME(){  
  ...  
}  

```
1. 引用自定义函数文件时，使用 `source func.sh` 命令
2. 函数可以可以通过 `$n` 获取参数来使用
3. 函数的返回值，只能是数字

## 函数返回值
Shell函数返回值，一般有3种方式
- `return`
- `echo`
- `global argv`

### return语句
return语句只能返回 `0-255`，且使用 `$?` 来访问

```
[root@zhujipeng test]# cat test.sh
func(){
  return 7
}

func
echo $?
[root@zhujipeng test]# sh test.sh
7
```

### echo语句
```
[root@zhujipeng test]# cat test.sh
func(){
  echo 7
}

echo `func`
[root@zhujipeng test]# sh test.sh
7
```

### 全局变量
```
[root@zhujipeng test]# cat test.sh
ret_val=
func(){
  ret_val=7
}

func
echo $ret_val
[root@zhujipeng test]# sh test.sh
7
```
```
[root@zhujipeng test]# cat test.sh
ret_val=
func(){
  ret_val=7
  echo "inner ${ret_val}"
}

echo haha | func
echo "outer ${ret_val}"
[root@zhujipeng test]# sh test.sh
inner 7
outer
```
> 在管道中修改全局变量并没有用，因为子进程的修改无法反映到父进程

## read
接收标准输入（键盘）或者其他文件描述符的输入，并将数据放入一个变量中

1. 输出提示字符串
```
read -p "Enter your name:" VAR_NAME 
```

2. 等待指定的时间
```
read -t 5 -p "Enter your name:" VAR_NAME
```

3. 键入密码不显示
```
read  -s  -p "Enter your password: " PASSWORD 
```

## declare
限定变量的属性

|选项 | 说明 |
|--- |--- |
|-r | 只读 |
|-i | 整数 |
|-a | 数组 |
> 某些算术计算允许在被声明为整数的变量中完成，而不需要特别使用 `expr`或 `let` 来完成

<br/>


## 数组
`declare -a` 表示定义普通数组

1. 支持稀疏格式
2. 仅支持一维数组

### 数组赋值
1. 一次对一个元素赋值 `a[0]=$RANDOM`
2. 一次对多个元素赋值 `a=(a b c d)`
3. 按索引进行赋值 `a=([0]=a [3]=b [1]=c)`

### 查看元素
1. ${ARRAY[index]}：查看数组指定角标的元素  
2. ${ARRAY}：查看数组的第一个元素  
3. ${ARRAY[*]}或者${ARRAY[@]}：查看数组的所有元素


### 数组长度
1. ${#ARRAY[*]}  
2. ${#ARRAY[@]}

### 元素大小
```
${#ARRAY[index]} 
```
> ${#ARRAY[0]}表示获取数组中的第一个元素的长度，等于${#ARRAY}

### 数组区间
```
${ARRAY[@]:offset[:length]}  
```
1. offset：偏移的元素个数
2. length：取出的元素的个数
3. 省略length取出数组中偏移量后的所有元素

### 删除元素
```
unset ARRAY[index]
```

## 重定向
标准输入、输出、错误可以使用文件描述符0、1、2引用

重定向输入
```
COMMAND < FILE
```

重定向输出
```
COMMAND [FILE_DESCRIPTOR]> FILE
```
> 可以使用 `&` 后面接文件描述符来代表文件

|文件描述符 | 说明 |
|--- |--- |
|0 | 标准输入 |
|1 | 标准输出 |
|2 | 错误输出 |
> 可以使用 `&` 符号同时代表标准输出和错误输出

字符串重定向
```
COMMAND <<< STRING
```


## true 和 false
true命令啥都不做，只设置退出码为0，false设置为非0，详见[这里][10]


## here document
详情参照[这里][5]

```
[root@zhujipeng test]# cat << EOF
> hi
> here
> EOF
hi
here
[root@zhujipeng test]# cat << EOF > /tmp/test.txt
> hi
> here
> EOF
[root@zhujipeng test]# cat /tmp/test.txt
hi
here
```



# xargs命令
xargs命令是给其他命令传递参数的一个过滤器，详情参见[xargs命令][16]

# shell中的括号
详情参照[这里][6]


<br/>

---

# 参考

[Shell编程详解][1]  
[Linux Shell函数返回值][2]  
[Linux中重定向及管道][3]    
[What does <<< mean][4]  
[linux shell的here document用法(cat << EOF)][5]  
[shell中的括号][6]    
[linux shell中的单引号与双引号的区别][7]   
[linux shell的here document用法(cat << EOF)][8]    
[1>/dev/null 2>&1的含义][9]  
[我使用过的Linux命令之true][10]  
[我使用过的Linux命令之:（冒号）][11]  
[我使用过的Linux命令系列总目录][12]   
[关于Shell的source、点（.）和export][13]   
[sh/bash/csh/Tcsh/ksh/pdksh等shell本质区别][14]         
[csh输出重定向][15]  
[[xargs命令][16]  

[1]: http://blog.csdn.net/u011204847/article/details/51184883
[2]: http://blog.csdn.net/ithomer/article/details/7954577
[3]: http://blog.csdn.net/songyang516/article/details/6758256
[4]: https://unix.stackexchange.com/questions/80362/what-does-mean
[5]: http://blog.csdn.net/wangjunjun2008/article/details/24351045
[6]: http://www.cnblogs.com/kex1n/p/6678286.html
[7]: http://lspgyy.blog.51cto.com/5264172/1282107
[8]: http://blog.csdn.net/wangjunjun2008/article/details/24351045
[9]: http://dongwei.iteye.com/blog/322702
[10]: http://codingstandards.iteye.com/blog/833338
[11]: http://codingstandards.iteye.com/blog/1160298
[12]: http://codingstandards.iteye.com/blog/1112967
[13]: http://walkerqt.blog.51cto.com/1310630/1690202
[14]: http://blog.csdn.net/dream_an/article/details/50548936
[15]: http://blog.itpub.net/14710393/viewspace-2106342/
[16]: http://man.linuxde.net/xargs