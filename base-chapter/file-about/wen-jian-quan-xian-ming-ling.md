# 概述
Linux系统按文件所有者、文件所有者同组用户和其他用户来规定了不同的文件访问权限
- 对于文件（目录是一种特殊的文件）来说，它都有一个特定的所有者，也就是对该文件具有所有权的用户。 
- 同时，在Linux系统中，用户是按组分类的，一个用户属于一个或多个组。 
- 文件所有者以外的用户又可以分为文件所有者的同组用户和其他用户。 


# 查看文件的权限
可以使用ls的-l选项或者ll命令（ls -l）的别名来查看
- `ls -l <文件名或目录>`
- `ll <文件名或目录>`

```   
➜  test-per ll
total 0
drwxr-xr-x  2 zhujipeng  staff    68B  8 13 15:49 test
-rw-r--r--  1 zhujipeng  staff     0B  8 13 15:52 test.txt

```
每列的含义如下
- 第1列，文件属性。由文件类型(第一个字符)＋用户权限＋组权限＋他人权限组成。
    - 文件类型
        - \- 普通文件
        - d 目录文件
        - l 链接文件
        - b 块设备
        - c 字符设备
        - p 管道
        - s 套接字
    - 文件权限
        - r 读权限
        - w 写权限
        - x 可执行权限


- 第2列，文件被引用的次数
- 第3列，文件的拥有者（owner）
- 第4列，文件的所属组（group）
- 第5列，文件的大小
- 第6-8列，文件的修改时间
- 最后一列，文件名


# 修改文件的权限（chmod）
格式如下
```
chmod [选项] <模式,模式...> <文件名...>
```

文字模式由范围＋操作符＋权限组成
- 范围
    - u 修改文件拥有者的权限 
    - g 修改文件所属组的权限
    - o 修改其他人的权限 
    - a 修改所有的权限  
- 操作符
    - ＋ 增加权限
    - \- 去掉权限
    - = 设置权限
- 权限
    - r 读权限
    - w 写权限
    - x 执行权限
    
数字模式由三个八进制数字组成。每个八进制中bit位为1代表有权限，0代表无权限
- r 100 -> 4
- w 010 -> 2
- x 001 -> 1
- rw 110 -> 6
- rx 101 -> 5
- wx 011 -> 3
- rwx 111 -> 7
            
选项如下

|选项 | 说明 |
|--- |--- |
|-f, --silent, --quiet | 忽略错误，强制执行 |
|-R, --recursive | 递归修改目录 |

> f -> force | R -> recursive

# 文件和目录的权限
linux中文件和目录的权限有所不同

- 文件的权限
    - r 可以读文件
    - w 可以写文件
    - x 可以执行文件
- 目录的权限
    - r 可以读取（cp）和查看（ls）目录的内容（即文件和目录），同时还需要可执行权限
    - w 可以在目录里创建文件（touch）和目录（mkdir）和删除文件（rm）和目录（rmdir），同时还需要可执行权限
    - x 可以进入目录（cd）和执行文件
    
实践过程

1. 创建一个目录和文件
```
➜  test-per mkdir test
➜  test-per touch test/old
➜  test-per ll
total 0
drwxr-xr-x  3 zhujipeng  staff   102B  8 13 17:56 test
```
2. 去除所有权限
```
➜  test-per chmod 0 test
➜  test-per ll
total 0
d---------  3 zhujipeng  staff   102B  8 13 17:56 test
```
3. 只添加读权限
```
➜  test-per chmod 400 test
➜  test-per ls test
ls: old: Permission denied
➜  test-per cd test
cd: permission denied: test
➜  test-per touch test/old
touch: test/old: Permission denied
➜  test-per touch test/new
touch: test/new: Permission denied
➜  test-per rm test/old
rm: test/old: Permission denied
```
4. 添加读和执行权限
```
➜  test-per chmod 500 test
➜  test-per ls test
old
➜  test-per cd test
➜  test cd ../
➜  test-per touch test/old
➜  test-per touch test/new
touch: test/new: Permission denied
➜  test-per rm test/old
rm: test/old: Permission denied
```
5. 只添加写权限
```
➜  test-per chmod 200 test
➜  test-per ls test
ls: test: Permission denied
➜  test-per cd test
cd: permission denied: test
➜  test-per touch test/old
touch: test/old: Permission denied
➜  test-per touch test/new
touch: test/new: Permission denied
➜  test-per rm test/old
rm: test/old: Permission denied
```
6. 添加写和执行权限
```
➜  test-per chmod 300 test
➜  test-per ls test
ls: test: Permission denied
➜  test-per cd test
➜  test cd ../
➜  test-per touch test/old
➜  test-per touch test/new
➜  test-per rm test/new
```
7. 只添加执行权限
```
➜  test-per chmod 100 test
➜  test-per ls test
ls: test: Permission denied
➜  test-per cd test
➜  test cd ../
➜  test-per touch test/old
➜  test-per touch test/new
touch: test/new: Permission denied
➜  test-per rm test/old
rm: test/old: Permission denied
```

总结如下
1. 如果目录只有读或写权限是不够的，还需要执行权限
2. touch目录下一个存在的文件只需要执行权限，否则需要写权限
3. ls在只有读权限和没有读权限似的错误并不相同（^_^?）
4. Tab补全只需要读权限
5. 当对文件没有写权限的时候，保存时会提示你使用!强制保存

# 强制保存文件的规则      
- 当对文件没有写权限的时候，保存时会提示你使用!强制保存
- 文件的所有者，不管对上级目录还是文件本身有何权限，都可以强制保存
- 不是文件的所有者，对上级目录有写权限，强制保存后，owner和group都会变成这个用户

    
# 更改文件的拥有者(chown)
格式如下
```
chown [选项] <拥有者名>[:所属组名] <文件名...>
```
选项如下

|选项 | 说明 |
|--- |--- |
|-R, --recursive | 递归修改目录 |

> chown -> change owner

# 更改文件的所属组(chgrp)
格式如下
```
chgrp [选项] <所属组名> <文件名...>
```
选项如下

|选项 | 说明 |
|--- |--- |
|-R, --recursive | 递归修改目录 |

> chgrp -> change group


<br/>

---

# 参考

[linux文件基本权限讲解][1]  
[Linux 文件和目录权限的区别一些简单的介绍][2]  

[1]: http://zhang789.blog.51cto.com/11045979/1846176
[2]: http://mifan6.blog.51cto.com/9954601/1659639
