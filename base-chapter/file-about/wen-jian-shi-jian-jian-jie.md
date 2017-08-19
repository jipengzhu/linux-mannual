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