# 环境变量的定义
环境变量是在操作系统中一个具有特定名字的对象，它包含了一个或者多个应用程序需要使用到的信息



# 环境变量的分类
按照作用域来分
- 系统环境变量：系统环境变量对该系统中所有用户都有效
- 用户环境变量：顾名思义，这种类型的环境变量只对特定的用户有效

按照生命周期来分
- 永久的：需要用户修改相关的配置文件，变量永久生效
- 临时的：
    - 利用export命令在当前终端下导出的环境变量，Shell终端关闭就失效
    - 脚本中定义的环境变量，脚本结束就失效



# 常见的环境变量
|环境变量 | 说明 |
|--- |--- |
|PATH | 指定可执行文件的搜索路径 |
|HOME | 指定用户的主工作目录 |
|PWD | 指定当所在目录 | 
|USER | 指定当前用户名 |
|LOGNAME | 指定当前用户的登录名 |
|HOSTNAME | 指定主机的名称 |
|SHELL | 指定当前正在使用Shell |
|LANG/LANGUGE | 语言相关的环境变量，使用多种语言时可以修改此环境变量 |
|IFS | (Internal Field Seprator)，内部域分隔符，详情参考[这里][9] |
|LD\_LIBRARY_PATH | 动态库搜索路径，详情参考[这里][11] |



# 环境变量的操作
## 设置环境变量
环境的格式为`[export] 变量名=变量值:变量值...`，多个值用英文冒号分开

1. 在`/etc/profile`文件中添加变量，对所有用户生效（永久的）
2. 在`~/.bash_profile`或`~/.bashrc`文件中添加变量，对当前用户生效（永久的）
3. 在shell中使用`export 变量名=变量值`，只在当前的shell或其子shell下是有效的（临时的）

> 


## 查看环境变量
### env
显示所有环境变量，详情参考[这里][2]

格式如下
```
env [选项] [-] [变量名=变量值]... [命令 [参数]...]
```

|选项 | 说明 |
|--- |--- |
|-i, --ignore-environment | 清空以前的环境变量，从新开始 |
|-u, --unset=NAME | 移除指定的环境变量 |

### set
显示本地定义的shell变量，详情参考[这里][3]

格式如下
```
set [选项] [-o 选项名称] [--] [参数]...
```

|选项 | 说明 |
|--- |--- |
|-a | 标示已修改的变量，以供导出到环境变量 |
|-b | 让中止的后台程序立刻回报执行状态 |
|-C | 禁止重定向覆盖已存在的文件 | 
|-e | 若返回状态不等于0，则立即退出shell | 
|-f | 取消通配符匹配 |
|-h | 记录函数的所在位置 |
|-H Shell | 可利用"!"加指令编号的方式来执行history中记录的指令 |
|-k | 指令所给的参数都会被视为此指令的环境变量 |
|-m | 开启任务控制 |
|-n | 只读取指令，而不实际执行 |
|-P | 启动-P参数后，执行指令时，会以实际的文件或目录来取代符号连接 | 
|-t | 执行一条指令后退出shell |
|-u | 当执行时使用到未定义过的变量，则显示错误信息 |
|-v | 显示shell所读取的输入值 |
|-x | 执行指令后，会先显示该指令及所下的参数 |


## 清除环境变量（unset）
详情参考[这里][5]


## 只读环境变量（readonly）
详情参考[这里][6]


## 局部环境变量（local）
详情参考[这里][7]


## 声明环境变量（declare）
用于声明和显示已存在的shell变量，和`typeset`用法相同，详情参考[这里][8]

格式如下
```
declare [选项] [-p] [变量名=变量值]...
```

选项如下
> 可以使用加号“+”代替减号“-”，效果是关闭对应的属性，但是“+a”和“+r”无效。

|选项 | 说明 |
|--- |--- |
|-p | 显示每个name的属性和值，不指定name时显示相应的所有变量的 |
|-f | 用于函数，显示函数定义 |
|-F | 用于函数，只显示函数名字，不显示函数定义 |
|-a | 用于索引（下标）数组 |
|-A | 用于关联（键值对）数组 |
|-i | 用于整数，可以进行数学运算 |
|-n | 用于引用变量的值所引用的值 |
|-l | 对变量赋值时，值的大写字母全部转换为小写 |
|-u | 对变量赋值时，值的小写字母全部转换为大写 |
|-r | 声明变量只读，不能被修改，也不能unset |
|-g | 在函数中declare变量的影响范围是局部的，除非使用了“-g” |
|-x | 等效于内置命令export |
|-t | 给每个name设置trace属性 |



# 环境变量生效
## source
修改环境变量文件后需要执行`source`命令（一个点和source同义）使环境变量生效，详情参考[这里][12]

## fork and exec
fork和exec使得环境变量有不同的作用域，详情参考[这里][13]



# 环境变量的加载
详情参考[bash的环境配置文件加载原理][14]


<br/>

---

# 参考

[Linux环境变量总结][1]    
[我使用过的Linux命令之env - 显示当前用户的环境变量][2]    
[set命令][3]    
[shell的set命令][4]  
[unset命令][5]  
[readonly命令][6]  
[declare命令][7]  
[shell内建命令之declare、typeset、local][8]  
[Shell中的IFS解惑][9]  
[Shell中的 IFS][10]  
[Linux 静态库与动态库搜索路径设置][11]  
[关于Shell的source、点（.）和export][12]  
[在 Shell 脚本中调用另一脚本的三种方式][13]  
[bash的环境配置文件加载原理][14]  
[交互式shell和非交互式shell、登录shell和非登录shell的区别][15]  
[login shell与non-login shell的区别][16]  

[1]: http://www.jianshu.com/p/ac2bc0ad3d74
[2]: http://codingstandards.iteye.com/blog/994906
[3]: http://man.linuxde.net/set
[4]: https://segmentfault.com/a/1190000003005706
[5]: http://man.linuxde.net/unset
[6]: http://man.linuxde.net/readonly
[7]: http://man.linuxde.net/declare
[8]: http://blog.csdn.net/ieearth/article/details/52625644
[9]: http://blog.csdn.net/whuslei/article/details/7187639
[10]: http://skypegnu1.blog.51cto.com/8991766/1543319
[11]: http://blog.csdn.net/jaylong35/article/details/6132087
[12]: http://walkerqt.blog.51cto.com/1310630/1690202
[13]: http://liuchengxu.org/blog-cn/posts/fork-exec-source/
[14]: http://www.jianshu.com/p/3c19279661a6
[15]: http://smilejay.com/2012/10/interactive-shell-login-shell/
[16]: http://blog.sciencenet.cn/blog-3238131-1037461.html