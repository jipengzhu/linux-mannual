# gzip
gzip是指GNU zip，压缩和解压文件，后缀名为gz。
- 只能压缩文件，不能压缩目录
- 压缩之后不能保留原文件
- 如需打包，需要配合`tar`命令

格式如下
```
gzip [选项] <文件名...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-c --stdout --to-stdout | 将压缩结果输出到标准输出，通常是屏幕 |
|-d --decompress --uncompress | 解压缩文件 |
|-l --list | 列出压缩文件的信息 |
|-r --recursive | 递归压缩目录里的文件 |
|-v --verbose | 压缩时输出详细信息 |
|-# --fast --best | 指定压缩级别，1-9，默认为6 |


# gunzip
解压gz文件

格式如下
```
gunzip [选项] <文件名...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-c --stdout --to-stdout | 将解压结果输出到标准输出，通常是屏幕 |


# bzip2
bzip2是gzip的升级版，后缀名为bz2

格式如下
```
bzip2 [选项] <文件名...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-k, --keep | 保留原文件 |


# bunzip2
bunzip2是gunzip的升级版

格式如下
```
bunzip2 [选项] <文件名...>
```


# zip
压缩和解压文件，用的最多的压缩命令
- 压缩之后保留原文件
- 不自动产生后缀名，通常自行指定为zip
- linux和windows都支持的格式

格式如下
```
zip [选项] <zip文件名> <文件名...>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-c, --entry-comments | 替每个被压缩的文件加上注释 |   
|-d, --delete | 从压缩文件内删除指定的文件 |       
|-f | 更新或者添加文件 |      
|-F | 尝试修复已损坏的压缩文件 |       
|-g | 将文件压缩后附加在既有的压缩文件之后，不另行建立新的压缩文件 |       
|-i, --include FILES | 只压缩符合条件的文件 |       
|-j | 只保存文件名称及其内容，而不存放任何目录名称 |      
|-J | 删除压缩文件前面不必要的数据 |     
|-k | 使用MS-DOS兼容格式的文件名称 |       
|-l | 压缩文件时，把LF字符置换成LF+CR字符 |     
|-ll | 压缩文件时，把LF+CR字符置换成LF字符 |       
|-L, --license | 显示版权信息 |     
|-m, --move | 将文件压缩并加入压缩文件后，删除原始文件，即把文件移到压缩文件中  |
|-n, -suffixes SUFFIXES | 不压缩具有以特定字符串结尾的文件 |       
|-o,--latest-time | 压缩时间以压缩文件内拥有最新更改时间的文件为准 |     
|-q, --quiet | 不显示指令执行过程 |      
|-r, --recurse-paths | 递归处理，将指定目录下的所有文件和子目录一并处理 |       
|-S | 包含系统和隐藏文件 |     
|-t --from-date | 把压缩文件的日期设成指定的日期 |      
|-T | 检查备份文件内的每个文件是否正确无误 |      
|-u | 更换较新的文件到压缩文件内 |       
|-v | 显示指令执行过程或显示版本信息 |       
|-V | 保存VMS操作系统的文件属性 |      
|-w | 在文件名称里假如版本编号，本参数仅在VMS操作系统下有效 |     
|-x, --exclude FILES | 压缩时排除符合条件的文件 |      
|-X | 不保存额外的文件属性 |       
|-y | 直接保存符号连接，而非该连接所指向的文件，本参数仅在UNIX之类的系统下有效 |       
|-z | 替压缩文件加上注释 |     
|-$ | 保存第一个被压缩文件所在磁盘的卷册名称 |      
|-# | 指定压缩效率，压缩效率是一个介于1-9的数值 |


## unzip
解压zip文件

格式如下
```
unzip [选项] <文件名>
```

选项如下

|选项 | 说明 |
|--- |--- |
|-o | 覆盖存在的文件 |

# tar
打包文件，后缀名为tar，配合-z选项时，后缀名为tar.gz或tgz

格式如下
```
tar [选项] <文件名...>
```
选项如下

|选项 | 说明 |
|--- |--- |
|-c, --create | 建立一个tar包 |
|-C, --directory=DIR | 指定解压文件到指定目录 |
|--delete | 从tar包中删除文件 |
|-f, --file=ARCHIVE | 指定压缩文件名 |
|-r, --append | 追加文件到tar包中 |
|-t, --list | 列出tar包中的文件和目录 |
|-u, --update | 更新文件 |
|-x | 解压文件 |
|-z, --gzip | 使用gzip压缩 |
|-k, --keep-old-files | 解压时如果文件已存在，报错 |
|--overwrite | 覆盖已存在的文件 |
|-v | 输出进度 |


<br/>

___

# 参考

[Linux常用命令之压缩打包篇（gzip、gunzip、tar、zip、bzip2）][1]  
[Linux文档的压缩与打包][2]  
[Linux下zip包的压缩与解压][3]  
[Linux常见压缩格式Tar、Zip和Gz格式之不同][4]  
[rar tar gz zip 7z 有什么区别][5]  

[1]: http://blog.csdn.net/yiliumu/article/details/20656597
[2]: http://zhang789.blog.51cto.com/11045979/1846484
[3]: https://www.cnblogs.com/chinareny2k/archive/2010/01/05/1639468.html
[4]: https://www.sysgeek.cn/tar-vs-zip-vs-gz/
[5]: https://www.zhihu.com/question/26026741