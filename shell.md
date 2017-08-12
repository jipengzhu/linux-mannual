# shell
在计算机科学中，Shell俗称外壳（用来区别于内核），它类似于Windows的DOS，够接收用户的命令并翻译给操作系统执行，是用户与操作系统（内核）之间的桥梁。


# shell的分类
1. bash
    - 现在大多数linux系统默认使用的shell。
    - 是 Bourne shell（最早的Unix shell）的一个免费版本。
    - 可以通过help命令来查看帮助

2. csh
    - C shell 使用的是“类C”语法，具有C语言风格
    - 目前使用的并不多，已经被/bin/tcsh所取代
    - 内部有52个命令，较为庞大

3. ksh
    - Korn shell 的语法与 Bourne shell 相同
    - 同时具备了 C shell 的易用特点。许多安装脚本都使用 ksh 
    - 内部有42条命令
    
4. tcsh
    - tcsh是csh的增强版，与 C shell 完全兼容
      
5. zsh
    - 传说中的[终极shell](https://zhuanlan.zhihu.com/p/19556676?columnSlug=mactalk)
    
6. sh
    - sh 通常是指向 bash 的快捷方式
    

# 查看系统的shell
- 查看系统支持哪些shell

    `cat /etc/shells`
    
- 查看正在使用的shell

    `echo $SHELL`
 
