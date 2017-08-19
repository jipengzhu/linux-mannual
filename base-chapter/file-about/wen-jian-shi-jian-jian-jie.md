# 文件的三个时间
- Windows
- 创建时间（create time）
- 修改时间（modify time）
- 访问时间（access time）

- Linux
- 访问时间（access time）
- 修改时间（modify time）
- 状态时间（change time）


# 文件的时间详解
在windows下，一个文件有：创建时间、修改时间、访问时间。
而在Linux下，一个文件也有三种时间：访问时间、修改时间、状态时间

- 修改时间：文件的内容最后一次修改的时间，`ls -l`命令显示时间就是这个时间，对文件进行编辑之后保存，mtime就会改变。
- 访问时间：对文件进行一次读操作就会改变，例如cat、more、less等操作，但是像stat、ls等不访问文件内容的命令对atime是不会有影响的。
- 状态时间：当文件的状态被改变的时候就会改变，例如当使用chmod、chown等改变文件属性的命令就会改变文件的ctime


# 查看文件时间
- 查看所有时间
`stat <文件名>`

- 查看修改时间
`ls -l <文件名>`

- 查看访问时间
`ls -lu <文件名>`

- 查看状态时间
`ls -lc <文件名>`


# 修改文件时间示例
```
[root@30bf5ac9eef2 file-time]# touch test.txt
[root@30bf5ac9eef2 file-time]# stat test.txt
  File: `test.txt'
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: 2dh/45d	Inode: 571         Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2017-08-19 17:36:23.513744773 +0000
Modify: 2017-08-19 17:36:23.513744773 +0000
Change: 2017-08-19 17:36:23.513744773 +0000
[root@30bf5ac9eef2 file-time]# echo haha >> test.txt
[root@30bf5ac9eef2 file-time]# stat test.txt
  File: `test.txt'
  Size: 5         	Blocks: 8          IO Block: 4096   regular file
Device: 2dh/45d	Inode: 571         Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2017-08-19 17:36:23.513744773 +0000
Modify: 2017-08-19 17:37:31.957587082 +0000
Change: 2017-08-19 17:37:31.957587082 +0000
[root@30bf5ac9eef2 file-time]# cat test.txt
haha
[root@30bf5ac9eef2 file-time]# stat test.txt
  File: `test.txt'
  Size: 5         	Blocks: 8          IO Block: 4096   regular file
Device: 2dh/45d	Inode: 571         Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2017-08-19 17:37:58.459710303 +0000
Modify: 2017-08-19 17:37:31.957587082 +0000
Change: 2017-08-19 17:37:31.957587082 +0000
[root@30bf5ac9eef2 file-time]# chmod a+x test.txt
[root@30bf5ac9eef2 file-time]# stat test.txt
  File: `test.txt'
  Size: 5         	Blocks: 8          IO Block: 4096   regular file
Device: 2dh/45d	Inode: 571         Links: 1
Access: (0755/-rwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2017-08-19 17:37:58.459710303 +0000
Modify: 2017-08-19 17:37:31.957587082 +0000
Change: 2017-08-19 17:49:29.153883697 +0000
```