# 查看文件的权限
可以使用ls的-l选项或者ll命令（ls -l）的别名来查看
- `ls -l <文件名或目录>`
- `ll <文件名或目录>`

```   
➜  test ll
total 0
drwxr-xr-x  2 zhujipeng  staff    68B  8 13 15:49 test
-rw-r--r--  1 zhujipeng  staff     0B  8 13 15:52 test.txt

```
每列的含义如下
- 第1列，文件属性。由文件类型(第一个字符)＋用户权限＋组权限＋他人权限组成。
    - 文件类型
        - \- 代表文件
        - d 代表目录
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
- 第3列，文件的拥有者
- 第4列，文件的所属组
- 第5列，文件的大小
- 第6-8列，文件的修改时间
- 最后一列，文件名


# 修改文件的权限（chmod）
格式如下
```
chmod [选项] <模式...> <文件...>
```
模式由范围＋操作符＋权限组成或八进制数字
- 范围
    - u 修改文件拥有者的权限 
    - g 修改文件所属组的权限
    - o 修改其他人的权限 
    - a 修改所有的权限
    
- 操作符
    - ＋ 增加权限
    - \- 去掉权限
    - = 设置权限
            
选项如下

|选项 | 说明 |
|--- |--- |
|-f | 忽略错误，则强制执行 |
|-R | 递归修改目录的权限 |


# 文件和目录的权限
linux中文件和目录的权限有所不同

- 文件的权限
    - r 可以读文件
    - w 可以写文件
    - x 可以执行文件
- 目录的权限
    - r 可以读（cp）和查看（ls）目录的内容（即文件和目录），同时还需要可执行权限。Tab补全只需要读权限。
    - w 可以在目录里创建文件（touch）和目录（mkdir)和删除文件（rm)和目录(rmdir)，同时还需要可执行权限。
    - x 可以进入目录（cd）和执行文件
    
实践过程

1. 创建一个目录和文件
```
➜  test-per mkdir test
➜  test-per touch test/test.txt
➜  test-per ll
total 0
drwxr-xr-x  3 zhujipeng  staff   102B  8 13 17:06 test
```
2. 去除所有权限
```
➜  test-per chmod 0 test
➜  test-per ll
total 0
d---------  3 zhujipeng  staff   102B  8 13 17:06 test 
```
3. 只添加读权限
```
➜  test-per chmod 400 test
➜  test-per ls test
ls: test.txt: Permission denied
➜  test-per cd test
cd: permission denied: test
➜  test-per touch test/test.txt
touch: test/test.txt: Permission denied
➜  test-per rm test/test.txt
rm: test/test.txt: Permission denied
```
4. 添加读和执行权限
```
➜  test-per chmod 500 test
➜  test-per ll
total 0
dr-x------  3 zhujipeng  staff   102B  8 13 17:06 test
➜  test-per ls test
test.txt
➜  test-per cd test/
➜  test cd ../
➜  test-per touch test/test.txt
➜  test-per rm test/test.txt
rm: test/test.txt: Permission denied
```
5. 只添加写权限
```
➜  test-per chmod 200 test
➜  test-per ll
total 0
d-w-------  3 zhujipeng  staff   102B  8 13 17:06 test
➜  test-per ls test
ls: test: Permission denied
➜  test-per cd test
cd: permission denied: test
➜  test-per touch test/test.txt
touch: test/test.txt: Permission denied
➜  test-per rm test/test.txt
rm: test/test.txt: Permission denied
```
6. 添加写和执行权限
```
➜  test-per chmod 300 test
➜  test-per ll
total 0
d-wx------  3 zhujipeng  staff   102B  8 13 17:06 test
➜  test-per ls test
ls: test: Permission denied
➜  test-per cd test
➜  test cd ../
➜  test-per touch test/test.txt
➜  test-per rm test/test.txt
```
7. 只添加执行权限
```
➜  test-per touch test/test.txt
➜  test-per chmod 100 test
➜  test-per ll
total 0
d--x------  3 zhujipeng  staff   102B  8 13 17:06 test
➜  test-per ls test
ls: test: Permission denied
➜  test-per cd test
➜  test cd ../
➜  test-per touch test/test.txt
➜  test-per rm test/test.txt
rm: test/test.txt: Permission denied
```

强制保存文件的规则      
- 当用户对文件没有写权限的时候，保存时会提示你使用!强制保存
- 文件的所有者，不管对上级目录还是文件本身有何权限，都可以强制保存
- 不是文件的所有者，对上级目录有写权限，强制保存后，owner和group变成这个用户

    


