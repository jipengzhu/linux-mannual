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


# yum仓库
yum仓库里存放了软件包的下载源和缓存等相关信息

```
[root@zhujipeng test]# ls /etc/yum
yum/         yum.conf     yum.repos.d/
[root@zhujipeng test]# ls /etc/yum.repos.d/
CentOS-Base.repo  CentOS-Debuginfo.repo  CentOS-Media.repo
CentOS-Vault.repo  CentOS-fasttrack.repo
```


## repo文件格式
```
[root@zhujipeng test]# cat /etc/yum.repos.d/CentOS-Media.repo
# CentOS-Media.repo
#
#  This repo can be used with mounted DVD media, verify the mount point for
#  CentOS-6.  You can use this repo and yum to install items directly off the
#  DVD ISO that we release.
#
# To use this repo, put in your DVD and use it with the other repos too:
#  yum --enablerepo=c6-media [command]
#
# or for ONLY the media repo, do this:
#
#  yum --disablerepo=\* --enablerepo=c6-media [command]

[c6-media]
name=CentOS-$releasever - Media
baseurl=file:///media/CentOS/
        file:///media/cdrom/
        file:///media/cdrecorder/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
```

参数如下

|参数 | 说明 |
|--- |--- |
|[...] | 仓库的名称，不能重复|
|name | 仓库的描述，必须参数 |
|baseurl | 配置仓库的路径，指定一个url |
|mirrorlist | 指向一个镜像列表，指定多个url |
|enabled | 是否启用当前仓库，值为1或0，默认为1 |
|gpgcheck | 是否需要`gpg`校验，值为1或0，默认为1 |
|gpgkey | 验证RPM包的密钥文件路径，可以在远处服务器上也可以在本地 |
|cost | 仓库优先级的配置，值越低表示访问的代价越低，也即优先使用 |

baseurl可以是本地目录，光盘，ftp，http形式的，值可以使用变量

|变量 | 说明 |
|--- |--- |
|$releasever | 当前操作系统的主版本号。若CentOS6.4 该值为6 |
|$basearch | 当前平台的基本架构。x86_64 或 i386 |
|$arch | 当前平台版本架构。x86_64 或 i386/i586/i686等 |
> 详情请参考[这里][6]


## yum仓库搭建
### 使用目录
详情参考[createrepo：创建本地源][7]

### 使用ISO
详情参考[RedHat/CentOS利用iso镜像做本地yum源][8]



<br/>

---

# 参考

[深入理解yum工作原理][1] 
[rpm包制作][2]   
[使用RPM安装、卸载、查询、升级和校验软件包][3]  
[yum的工作原理以及如何建立yum仓库][4]  
[Linux软件包管理工具yum详解][5]  
[yum中$releasever、 $basearch等变量含义][6]  
[createrepo：创建本地源][7]    
[RedHat/CentOS利用iso镜像做本地yum源][8]  

[1]: http://www.firefoxbug.com/index.php/archives/2777/
[2]: http://www.firefoxbug.com/index.php/archives/2776/
[3]: http://wuyelan.blog.51cto.com/6118147/1546305
[4]: http://wuyelan.blog.51cto.com/6118147/1546674
[5]: http://zhang789.blog.51cto.com/11045979/1846643
[6]: http://blog.csdn.net/taiyang1987912/article/details/46890997
[7]: http://blog.csdn.net/iloveyin/article/details/7766848
[8]: https://linux.cn/article-1017-1.html
