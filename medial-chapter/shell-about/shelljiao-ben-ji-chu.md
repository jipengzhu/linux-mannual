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


<br/>

---

# 参考

[Shell编程详解][1]

[1]: http://blog.csdn.net/u011204847/article/details/51184883