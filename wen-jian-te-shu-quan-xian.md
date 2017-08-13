# 概述
简单的文件rwx权限不能满足我们对安全和便捷的需求，所以便有了SUID与SGID的特殊权限机制

# 案例
/etc/passwd文件存储着用户的相关设置，/etc/shadow存储着用户加密后的密码。/etc/passwd的拥有者是root，所属组是root，根据权限的知识普通用户应该是不能修改/etc/passwd的内容的，但是普通用户可以通过`passwd`命令修改自己的密码。这是因为`passwd`设置了suid位，让用户临时拥有了文件拥有者的权限。

```
➜  test ll /etc/passwd
-rw-r--r--. 1 root root 2609 8月   4 18:18 /etc/passwd
➜  test ll /usr/bin/passwd
-rwsr-xr-x. 1 root root 27832 6月  10 2014 /usr/bin/passwd
```

# SUID
让执行者临时拥有拥有者的权限（仅对拥有执行权限的二进制程序有效）

- 添加suid
```
chmod u+s <文件名>
```
- 去除suid
```
chmod u-s <文件名>
```


# SGID
SGID有两个功能，一个是让执行者临时拥有文件所属组的权限，另外一个是让文件下创建的文件的所属组是目录的所属组

- 添加suid
```
chmod g+s <文件名>
```
- 去除suid
```
chmod g-s <文件名>
```

