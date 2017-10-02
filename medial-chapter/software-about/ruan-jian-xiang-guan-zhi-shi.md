# 安装方式
linu下的软件包有三种安装方式

Redhat系列

- 源码安装
- rpm安装
- yum安装

Debian系列

- 源码安装
- dpkg安装
- apt-get安装



# 源码安装
相对于二进制软件包，源码安装配置和编译比较繁琐，但是可移植性却好得多

源码包通常包含以下字样

- `src`：源码包标识，相对于`bin`
- `.tar.gz`：压缩包格式 
- `.tgz`：`tar.gz`的缩写

二进制包通常包含以下字样

- `bin`：二进制包格式，相对于`src`
- `.rpm`：Redhat系列二进制包
- `.deb`：Debian系列二进制包

源码安装通常有以下几步
> 通常我们会执行`--prefix`参数将软件安装到指定位置以便维护

1. 生成Makefile：`./configure --prefix=/opt/XXX`
2. 编译源文件：`make`
3. 安装软件包：`make install`

> `./configre --help`可以查看帮助信息来获得更多的设置选项
> `make clean`（不一定有）可以清除编译连接过程中的临时文件
> `make uninstall`（不一定有）可以根据Makefile文件来删除软件



# rpm
```
rpm [选项] <软件包>
``` 

通用选项如下

|选项 | 说明 |
|--- |--- |
|-v | 显示详细信息（通用选项） |
|-vv | 显示调试信息（通用选项） |


## 安装
```
rpm -ivh <安装包> 
```

选项如下

|选项 | 说明 |
|--- |--- |
|-i, --install | 安装（通常与vh选项一起使用）|
|-h, --hash | 以#显示进度信息 |
|--force  | 强制进行安装 |
|--nodeps | 忽略依赖关系 |
|--test | 只测试，不实际执行 |
|--replacepkgs | 重新安装软件包 |
|--oldpackage | 允许安装低版本的包 |
> 出错后可以使用`--force`和`--nodeps`（no dependency）强制进行安装


## 升级
```
rpm -Uvh <安装包> 
```

|选项 | 说明 |
|--- |--- |
|-U, --upgrade | 升级（如果没有安装则安装）|
|-F, --freshen | 升级（软件包要事先安装过）|
|-h, --hash | 以#进度显示进度信息 |
|--force  | 强制进行升级 |
|--nodeps | 忽略依赖关系 |
|--test | 只测试，不实际执行 |


## 查询
```
rpm -q[其他选项] [参数]
```

|选项 | 说明 |
|--- |--- |
|-q, --query | 查询单个软件包 |
|-qa | 查看所有已安装软件包 |
|-qi | 查看软件包摘要信息 |
|-ql | 查看软件包生成的文件列表 |
|-qd | 查看软件包生成的帮助文件 |
|-qf | 查看文件是由哪个软件包安装的 |
|-qR | 查看软件包的依赖关系 |
|-q –scripts | 查看软件包安装脚本 |
|-p, package | 指定查询时使用的本地软件包 |

> `-p` 参数的影响如下
```
[root@zhujipeng test]# rpm -q telnet
telnet-0.17-48.el6.x86_64
[root@zhujipeng test]# rpm -q telnet-0.17-48.el6.x86_64.rpm
package telnet-0.17-48.el6.x86_64.rpm is not installed
[root@zhujipeng test]# rpm -qp telnet-0.17-48.el6.x86_64.rpm
telnet-0.17-48.el6.x86_64
```


## 删除
```
rpm -e <安装包> 
```

|选项 | 说明 |
|--- |--- |
|-e, --erase | 移除软件包 |
|--nodeps | 忽略依赖关系 |
|--test | 只测试，不实际执行 |
|--allmatches | 移除所有匹配的版本 |



# yum安装
```
yum [选项] [子命令] [软件包]...
```

通用选项如下

|选项 | 说明 |
|--- |--- |
|-y, --assumeyes | 所有的询问回答yes |
|--assumeno | 所有的询问回答no |
|-q, --quiet | 不显示输出 |


## 安装
> 初始安装软件包

```
yum install [软件包]...
```

> 初始安装软件包

```
yum localinstall [软件包]...
```

> 重新安装软件包

```
yum reinstall [软件包]...
```

选项如下

|选项 | 说明 |
|--- |--- |
|--nogpgcheck | 不检查GPG签名 |
|--downloadonly | 只下载不安装 |
|--downloaddir=directory | 指定下载的目录 |


## 升级
> 升级软件包

```
yum update [软件包]...
```

> 升级软件包

```
yum localupdate [软件包]...
```

> 检查软件更新

```
yum check-update [软件包]...
```

选项如下

|选项 | 说明 |
|--- |--- |
|--nogpgcheck | 不检查GPG签名 |
|--downloadonly | 只下载不安装 |
|--downloaddir=directory | 指定下载的目录 |


## 降级
> 降级安装软件包

```
yum downgrade [软件包]...
```


## 查询
> 列出安装包

```
yum list [软件包]...
```

> 列出可更新安装包

```
yum list updates
```

> 列出已安装安装包

```
yum list installed
```

> 模糊查找软件包

```
yum search [软件包]...
```

> 查看软件包信息

```
yum info [软件包]...
```

> 查询软件包的提供方

```
yum provides [软件包]...
```

> 查询文件所在的安装包

```
yum resolvedep [文件]...
```

> 查询软件包的依赖

```
yum deplist [软件包]...
```


## 删除
> 删除软件包

```
yum erase [软件包]...
```

> 删除软件包

```
yum remove [软件包]...
```


## 软件包组
> 显示所有软件包组

```
yum grouplist [软件包]...
```

> 显示组包含的软件包

```
yum groupinfo [软件包]...
```

> 安装RPM软件包组

```
yum groupinstall [软件包]...
```

> 更新RPM软件包组

```
yum groupupdate [软件包]...
```

> 删除RPM软件包组

```
yum groupremove [软件包]...
```


## 软件仓库
### 仓库
> 查看所有的yum仓库

```
yum repolist all
```

> 查看启用的的yum仓库

```
yum repolist enabled
```

> 查看禁用的yum仓库

```
yum repolist disabled
```

### 缓存
> 清除缓存

```
yum clean <缓存范围>
```

|缓存范围 | 说明 |
|--- |--- |
|headers | 软件包头信息 |
|packages | 软件包缓存 |
|metadata | 元数据缓存 |
|expire-cache | 过期信息缓存 |
|dbcache | 数据库信息缓存 |
|plugins | 插件缓存 | 
|all | 所有缓存 |


> 建立缓存

```
yum makecache
```


## 历史记录
> 列出yum历史操作命令

```
yum history
```


## 查看帮助
> 查看子命令的帮助信息

```
yum help <子命令>
```


</br>

---

# 参考

[rpm、tar及yum使用详解][1]  

[1]: http://502245466.blog.51cto.com/7559397/1259949