# epel
- EPEL的全称叫`Extra Packages for Enterprise Linux`
- 是由Fedora社区打造的为RHEL系列提供高质量软件包的项目
- 装上了EPEL之后就相当于添加了一个第三方源

```
[root@zhujipeng test]# yum search epel
Loaded plugins: fastestmirror, ovl
Loading mirror speeds from cached hostfile
 * base: mirrors.shuosc.org
 * extras: mirrors.shuosc.org
 * updates: mirrors.shuosc.org
================================================ N/S Matched: epel ================================================
epel-release.noarch : Extra Packages for Enterprise Linux repository configuration

  Name and summary matches only, use "search all" for everything.
```

详情参考 [什么是EPEL 及 Centos上安装EPEL][1]



# yum-utils
`yum-utils`以多种方式扩充`yum`的功能，从而使其功能更强大，使用更方便

```
[root@zhujipeng test]# yum search yum-utils
Loaded plugins: fastestmirror, ovl
Loading mirror speeds from cached hostfile
 * base: mirrors.shuosc.org
 * extras: mirrors.shuosc.org
 * updates: mirrors.shuosc.org
============================================= N/S Matched: yum-utils ==============================================
yum-utils.noarch : Utilities based around the yum package manager

  Name and summary matches only, use "search all" for everything.
```


详情参考 [如何安装和使用’yum-utils’来维护Yum并提高其性能][3]



# Rpmfind
[Rpmfind](http://rpmfind.net/)是一个查找和下载rpm的网站，有非常强大的搜索功能


<br/>

---

# 参考

[什么是EPEL 及 Centos上安装EPEL][1]  
[如何在CentOS 5/6上安装EPEL 源][2]  
[如何安装和使用’yum-utils’来维护Yum并提高其性能][3]  

[1]: http://blog.csdn.net/yasi_xi/article/details/11746255
[2]: https://linux.cn/article-2324-1.html
[3]: https://www.howtoing.com/linux-yum-package-management-with-yum-utils/