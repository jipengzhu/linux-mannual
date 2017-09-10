# 差异比较
- 源程序文件（通常是纯文本文件）的比较和合并工具一直是软件开发过程中比较重要的组成部分
- 现在市场上很多功能很强大的专用比较和合并工具，比如 BeyondCompare
- 很多IDE 或者软件配置管理系统（比如Eclipse）都提供了内建的功能来支持文件的比较和合并


# vimdiff
vimdif可以比较两个文件的差异，并且进行编辑和合并差异

## 打开方法
```
vimdiff  FILE_LEFT  FILE_RIGHT
vim -d  FILE_LEFT  FILE_RIGHT
```
或者在vim编辑器中
```
:vim FILE_LEFT
```


## 交换窗口
如果希望交换两个窗口的位置，或者希望改变窗口的分割方式

|快捷键 | 说明 |
|--- |--- |
|Ctrl-w + K | 把当前窗口移到最上边 |
|Ctrl-w + H | 把当前窗口移到最左边 |
|Ctrl-w + J | 把当前窗口移到最下边 |
|Ctrl-w + L | 把当前窗口移到最右边 |


## 快速移动
默认左右两侧的屏幕滚动是同步的，如果不想要通过以下命令可以设置
`:set noscrollbind`

|快捷键 | 说明 |
|--- |--- |
|]c | 跳转到下一个差异点 |
|[c | 跳转到下一个差异点 |
> 在命令前加上数字可以移动相应的次数，默认为1次


## 文件合并
文件比较的最终目的之一就是合并，以消除差异。

|命令 | 说明 |
|--- |--- |
|dp | 将正在编辑中的文件的差异应用到另一个文件中(diff put) |
|do | 将另一个文件中的差异应用到正在编辑的文件中(diff get) |
|:diffupdate | 当自动刷新失败时强制刷新比较结果|
> diff "get"，之所以不用dg，是因为dg已经被另一个命令占用了


## 折叠展开
- 比较和合并文件时经常需要结合上下文来确定最终要采取的操作
- vimdiff缺省是会把不同之处上下各 6 行的文本都显示出来
- 其他的相同的文本行被自动折叠，可使用`zo`命令展开

|命令 | 说明 |
|--- |--- |
|zo |（folding open） 展开折叠 |
|zc |（folding close）使用折叠 |
|:set diffopt=context:3| 设置上下文行数为3 |
> 之所以用z这个字母，是因为它看上去比较像折叠着的纸


## 批量操作
|命令 | 说明 |
|--- |--- |
|:qa |（quit all）退出全部文件 |
|:wa |（write all）保存全部文件 |
|:wqa |（write, then quit all）保存全部文件，然后退出 |
|:qa! |（force to quit all）都不保存，然后退出 |


<br/>

---

# 参考

[技巧：Vimdiff 使用][1]  
[linux-vimdiff,diff,patch,cmp:文件比较][2]  
[读懂diff][3]  

[1]: https://www.ibm.com/developerworks/cn/linux/l-vimdiff/index.html
[2]: http://blog.csdn.net/gexiaobaoHelloWorld/article/details/7783686
[3]: http://www.ruanyifeng.com/blog/2012/08/how_to_read_diff.html