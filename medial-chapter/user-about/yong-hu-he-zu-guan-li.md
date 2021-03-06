# linux用户和组管理
linux是一个多用户操作系统，多用户是指系统资源可以被不同用户各自拥有使用，即每个用户对自己的资源（例如：文件、设备）有特定的权限，互不影响



# 用户标识


## root账户
root用户拥有极高的系统所有权，能够管理系统的各项功能，如添加/删除用户，启动/关闭进程，开启/禁用硬件设备等权限。使用root用户工作时不会受到权限的控制，因此执行危险操作时很容易因为失误对系统造成危害


## UID
UID（即User IDentification的缩写）：每个用户都有对应的UID值，就像我们的身份证号码，为操作系统内部所使用。

> 帐户名称与UID保存在/etc/passwd文件中，而帐户密码则保存在/etc/shadow文件中

- 超级用户UID(0): root用户默认为0。
- 系统用户UID(1-999): 系统中系统服务由不同用户运行，更加安全，默认被限制登陆系统。
- 普通用户UID(1000+): 即管理员创建的用于日常工作而不能管理系统的普通用户。


## GID
GID(即Group IDentification的缩写)：可将多个用户加入某个组中，方便指派任务或工作，为操作系统内部所使用。

> 用户组名称与GID保存在/etc/group文件中



# 用户命令


## 用户管理
使用操作系统系统资源的用户都必须先向系统管理员申请一个账号，然后以这个账号的身份进入系统

### useradd
useradd命令用于创建新的用户

格式如下
```
useradd [选项] <用户名>
```

|选项 | 说明 |
|--- |--- |
|-b, --base-dir BASE_DIR | 指定用户家目录的基准目录（默认为/home）|
|-d, --home HOME_DIR | 指定用户的家目录（默认为/home/username）|
|-D, --defaults | 显示或修改当前的默认值 |
|-e, --expiredate EXPIRE_DATE | 帐号有效截至日期，格式：YYYY-MM-DD，空字符串表示不过期|
|-g, --gid GROUP | 指定一个初始用户组（必须已存在）|
|-G, --groups GROUP... | 指定一个或多个扩展用户组 |
|-M | 不创建用户主目录 |
|-N, --no-user-group | 不创建与用户同名的用户组 |
|-s, --shell SHELL | 指定默认的Shell |
|-u, --uid UID| 指定用户的UID |
|-U, --user-group| 创建一个和用户同名的组，并将用户添加到组中 | 

### passwd
passwd命令用于修改用户的密码

格式如下
```
passwd [选项] [用户名]
```

|选项 | 说明 |
|--- |--- |
|-l, --lock | 锁定用户禁止其登陆，只有root用户能用 |
|-u, --unlock | 解除锁定允许用户登陆，只有root用户能用 |
|--stdin | 允许从标准输入修改用户密码，如使用管道 |
|-d, --delete | 删除账号的密码 |
|-e, --expire | 强制用户下次登陆时修改密码 |
|-S, --status | 显示用户的密码状态 |

### userdel
userdel命令用于删除用户

格式如下
```
userdel [选项] <用户名>
```

|选项 | 说明 |
|--- |--- |
|-f, --force | 强制删除用户，即使用户仍然在登录状态 |
|-r, --remove | 同时删除用户，家目录与其相关文件 |

### usermod
usermod命令用于修改用户的属性

格式如下
```
usermod [选项] <用户名>
```

|选项 | 说明 |
|--- |--- |
|-c, --comment COMMENT | 填写帐号的备注信息
|-d, --home HOME_DIR | -m与-d连用，指定用户新的家目录并转移数据，否则新建家目录 |
|-e, --expiredate EXPIRE_DATE | 帐户到期时间，格式“YYYY-MM-DD” |
|-g, --gid GROUP | 变更所属用户组 |
|-G, --groups GROUP... | 变更扩展用户组 |
|-l, --login NEW_LOGIN | 修改用户名为新名字 |
|-L, --lock | 锁定用户禁止其登陆系统 |
|-U, --unlock | 解锁用户，允许其登陆系统 |
|-s, --shell SHELL | 修改默认终端 |
|-u, --uid UID | 修改用户的UID |


## 用户组管理
用户可以属于多个组，并获得相关组的权限。用户的组分为主组和附属组

### groupadd
groupadd命令用于创建群组

格式如下
```
groupadd [选项] <群组名>
```

|选项 | 说明 |
|--- |--- |
|-g, --gid GID | 为用户组指定组标识号 |
|-o, --non-unique | 与-g选项同时使用，GID可以使用系统已有用户组的GID |

### groupdel
groupdel用来删除用户组

格式如下
```
groupdel [选项] <群组名>
```

### groupmod
groupmod用来需该用户组的属性

格式如下
```
groupmod [选项] <群组名>
```

|选项 | 说明 |
|--- |--- |
|-g, --gid GID | 为用户组指定新的组标识号 |
|-o, --non-unique | 与-g选项同时使用，新的GID可以使用系统已有用户组的GID |
|-n NEW_GROUP | 将用户组的名字改为新名字 |

### newgrp
newgrp用来将用户切换到另一个组中

格式如下
```
newgrp [选项] <群组名>
```

|选项 | 说明 |
|--- |--- |
| - | 用户重新登陆 |

### groups
groups用来查看当前的用户组，和`id -gn`命令一样

格式如下
```
groups [选项] <群组名...>
```


## 默认权限（umask）
- umask命令可以查看和设置文件的默认权限
- umask设置的是权限“补码”，而chmod设置的是文件权限码
- 详情参考[这里][3]


## 密码文件
- 用户的帐户名称与UID保存在/etc/passwd文件中
- 用户的帐户密码则保存在/etc/shadow文件中
- 文件的格式详情参考[这里][1]


<br/>

---

# 参考

[linux用户和组管理详解][1]  
[LINUX UMASK详解][2]  

[1]: http://zhang789.blog.51cto.com/11045979/1845767
[2]: http://blog.csdn.net/linux7985/article/details/5993708
