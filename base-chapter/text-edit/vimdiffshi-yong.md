# 差异比较
- 源程序文件（通常是纯文本文件）的比较和合并工具一直是软件开发过程中比较重要的组成部分
- 现在市场上很多功能很强大的专用比较和合并工具，比如 BeyondCompare
- 很多IDE 或者软件配置管理系统（比如Eclipse）都提供了内建的功能来支持文件的比较和合并


# vimdiff
vimdif可以比较两个文件的差异，并且进行编辑和合并差异

```
vimdiff  FILE_LEFT  FILE_RIGHT
vim -d  FILE_LEFT  FILE_RIGHT
```
或者在vim编辑器中
```
:vim FILE_LEFT
```

如果希望交换两个窗口的位置，或者希望改变窗口的分割方式

|快捷键 | 说明 |
|--- |--- |
|Ctrl-w + K | 把当前窗口移到最上边 |
|Ctrl-w + H | 把当前窗口移到最左边 |
|Ctrl-w + J | 把当前窗口移到最下边 |
|Ctrl-w + L | 把当前窗口移到最右边 |
