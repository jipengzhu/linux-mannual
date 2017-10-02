# yum简介
yum（Yellow dogUpdater, Modified）是一个RPM包的前端管理工具，能够自动解决软件包的依赖关系



# yum运行原理
yum的工作需要两部分来合作，分别是yum服务器和yum客户端


## yum服务端
- 所有要发行的rpm包都放在yum服务器上以提供别人来下载
- rpm包是根据kernel的版本号和cpu的版本号来进行编译发布的
- 包含了rpm包对应的版本号，conf文件，binary信息，及依赖信息


## yum客户端
- client每次都会去解析/etc/yum.repos.d下面所有以.repo结尾的配置文件
- yum会定期去"更新"yum服务器上的rpm包"清单"，并保存到自己的cache里面
- 下载的rpm软件包默认缓存到`/var/cache/yum`，需要设置`keepcache`参数开启


## yum仓库
yum仓库里存放了软件包的下载源和缓存等相关信息

```
[root@zhujipeng test]# ls /etc/yum
yum/         yum.conf     yum.repos.d/
[root@zhujipeng test]# ls /etc/yum.repos.d/
CentOS-Base.repo  CentOS-Debuginfo.repo  CentOS-Media.repo
CentOS-Vault.repo  CentOS-fasttrack.repo
```




</br>

---

# 参考

[深入理解yum工作原理][1] 
[rpm包制作][2]   
[使用RPM安装、卸载、查询、升级和校验软件包][3]  
[yum的工作原理以及如何建立yum仓库][4]    

[1]:http://www.firefoxbug.com/index.php/archives/2777/
[2]:http://www.firefoxbug.com/index.php/archives/2776/
[3]:http://wuyelan.blog.51cto.com/6118147/1546305
[4]:http://wuyelan.blog.51cto.com/6118147/1546674