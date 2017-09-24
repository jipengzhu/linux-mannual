# Linux介绍
- Linux是一套能够免费使用和自由传播的类Unix操作系统，由一个基于POSIX和UNIX的多用户、多任务、支持多线程和多CPU的操作系统内核和众多开源软件组成。
- 它能运行主要的UNIX工具软件、应用程序和网络协议，可以运行于32位和64位硬件之上。
- Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。


# Linux历史
- Unix一开始是开源的，后来AT&T收回版权，并且宣布不再公开源代码。
- Unix是用90%的C语言和10%汇编语言混合编写的，移植到不同硬件平台时需要更改代码，因此各个公司都推出了针对自家机型的Unix系统。
- AT&T System V 第七版时，终于推出了针对X86的Unix，因此能够在个人计算机上安装Unix了，但有一条规定：“不能向学生公开源代码”。
- 为了教学，Tanebaum教授编写了兼容Unix的针对X86的Minix操作系统。因为Minix只是教学使用，因此功能并不强。
- 后来Linus Torvalds用GNU的bash当做开发环境，gcc当做编译工具，编写了Linux内核。
- 一开始Linux内核并不能兼容Unix，即Unix上跑的应用程序不能不加修改的在Linux上跑，因为Unix应用程序与Linux内核之间的接口并不一致。
- 因为Unix是遵循POSIX（Portable Operating System Interface）规范的，后来Torvalds修改了Linux内核，遵循了POSIX规范。
- 一开始Linux只适用于386，后来经过全世界的网友的帮助，最终能够兼容多种硬件。


## GNU计划
- 70年代出现了两位针锋相对的领袖人物，来自哈佛大学的比尔·盖茨（Bill Gates）和 同样来自哈佛大学的理查德·斯托曼（Richard M.Stallman）。
- 前者宣布了版权（Copyright）时代的到来，并构建了辉煌的微软帝国。后者创立自由软件体系GNU（GNU is Not Unix），拟定了GNU通用公共许可协议（General Public License，简称GPL）。
- 所有GPL协议下的自由软件都遵循着Richard M. Stallman的非版权（Copyleft）原则：即自由软件允许用户自由拷贝、修改和销售，但是对其源代码的任何修改都必须向所有用户公开。
- GNU计划和自由软件基金会FSF(the Free Software Foundation)是由Richard M. Stallman于1984年一手创办的，旨在开发一个类似UNIX并且是自由软件的完整操作系统：GNU系统（GNU 是"GNU's Not Unix"的递归缩写，它的发音为"guh-NEW"）。
- 各种使用Linux作为核心的GNU操作系统正在被广泛的使用，虽然这些系统通常被称作"Linux"，但是Stallman认为：严格地说，它们应该被称为GNU/Linux系统。
- 到上世纪90 年代初，GNU项目已经开发出许多高质量的免费软件，其中包括有名的emacs编辑系统、bash shell程序、gcc 系列编译程序、gdb 调试程序等等。这些软件为Linux操作系统的开发创造了一个合适的环境。
- GNU计划是Linux操作系统能够诞生的基础之一，以至于目前许多人都将Linux操作系统称为“GNU/Linux”操作系统


## Linux史上的重要人物
1. Ken Thompson：C语言之父和Unix之父
2. Dennis Ritchie：C语言之父和Unix之父
3. Stallman：著名黑客，GNU创始人
4. Bill Joy：BSD开发者
5. Tanenbaum：Minix开发者
6. Linus Torvalds：Linux之父


## Linux发行版
- Linux内核和众多开源软件一起构成了Linux操作系统。
- Linux发行版本是指软件发行商提供的包含linux内核和众多软件的集成套件。
- Linux的发行版本可以大体分为两类，一类是商业公司维护的发行版本，一类是社区组织维护的发行版本。
- 前者以著名的Redhat（RHEL）为代表，后者以Debian为代表。
- Redhat，应该称为Redhat系列，包括RHEL(Redhat Enterprise Linux，也就是所谓的Redhat Advance Server，收费)、Fedora Core(由原来的Redhat桌面版本发展而来的，免费)、CentOS(RHEL的社区克隆版本，免费)
- Debian，或者称Debian系列，包括Debian和Ubuntu等。Debian是社区类Linux的典范，是迄今为止最遵循GNU规范的Linux系统
- 对于个人用户，一般服务器操作系统选择centos，桌面操作系统选择ubuntu


## 软件授权模式
1. Open Source：开放源代码；
2. Close Source：不开放源代码；
  - Freeware：免费但不开源；
  - Shareware：一开始免费试用，经过一段时间后收费；


## Linux内核的功能
* 进程管理
* 内存管理
* 文件管理
* 设备管理
* 网络管理


## Linux内核版本号
查看命令：`uname -r`

版本：3.2.0-23 
组成：主版本.次版本.释放版本-修订版本

Linux的内核版本分为稳定版本和开发版本。
* 次版本如果是偶数，则为稳定版本，如果是奇数，则为开发版本。
* 释放版本为对次版本的改动，即加入一些功能。
* 修改版本为编译的次数，每次加一。


## Linux相关概念
* 类Unix操作系统：
Unix Like，类Unix的操作系统是指借鉴Unix发展而来的操作系统，例如mac操作系统和linux操作系统

* POSIX规范:
Portable Operating System Interface，可移植操作系统接口，是对应用程序和系统调用之间的接口的规范

* SELinux
Security-Enhanced Linux，美国国家安全局（NSA）对于强制访问控制的实现，是 Linux历史上最杰出的新安全子系统


<br/>

---

# 参考

[Linux发行版：CentOS、Ubuntu、RedHat、Android、Tizen、MeeGo][1]  
[Linux各发行版介绍][2]  
[Linux下查看系统版本号信息的方法][3]  

[1]: http://blog.csdn.net/ithomer/article/details/9729933
[2]: http://weibo.com/ttarticle/p/show?id=2309404113611055322504
[3]: http://blog.csdn.net/alexander_phper/article/details/53010225