##### 一、vim是什么？
简单来说就是一款十分优秀的编辑器
##### 二、vim的多种模式
从vi演生出来的Vim具有多种模式，这种独特的设计容易使初学者产生混淆。Vim和vi一样，仅仅通过键盘来在这些模式之中切换。这就使得Vim可以不用进行菜单或者鼠标操作，并且最小化组合键的操作。对文字录入员或者程序员可以大大增强速度和效率。
##### 三、3种重要的模式
Vim具有6种基本模式和5种派生模式，但是在基础入门的时候需要掌握的分别是**普通模式**、**插入模式**、**命令行模式**。
1、进入vim编辑器，在windows下打开git bash，在linux和mac下打开终端。输入下面命令：
`vim 文件名`
2、普通模式
在普通模式中，用的编辑器命令，比如移动光标，删除文本等等。这也是Vim启动后的默认模式。这正好和许多新用户期待的操作方式相反（大多数编辑器默认模式为插入模式）。
3、插入模式
从普通模式变为插入模式后就可以编辑文本了，可以使用`i`进入到插入模式，当然不只这一种方法，后面会仔细介绍。
4、命令行模式
在普通模式下输入`:`进入命令行模式，输入`w`回车，保存文档。
输入`w:文件名`可以将文档另存为其他文件名或存到其他路径下。

##### 三、退出与保存文档
1、在命令行模式下退出

![](http://upload-images.jianshu.io/upload_images/2070541-38cbdbfd0ec3ef9c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、在普通模式下退出vim
输入`shift+zz`即可保存并退出vim。

##### 四、删除文本
1、在普通模式下删除vim文本信息
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2070541-13c7844114b5cf9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
最实用的应该就是`dd`这个命令了，可以在dd前加上数字，表示一次删除多行。如`3dd`表示一次删除3行。

##### 五、文档编辑
1、执行指定次数相同的命令
在普通模式下输入  `n<command>`，例如：
- 输入`10x`，删除10个连续字符
- 输入`3dd`，删除3行文本

2、游标快速跳转
普通模式下，执行下列命令可以让光标快速跳转到指定位置，我将它分为两类：**行间跳转**和**行内跳转**
首先如果文档没有行号，可以使用`:set nu`命令为文档加上行号
- 行间跳转

![](http://upload-images.jianshu.io/upload_images/2070541-e3c8564cff7d3ac7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 行内跳转

![](http://upload-images.jianshu.io/upload_images/2070541-5196a8c87a3f2c18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 六、复制剪切及粘贴文本
1、 普通模式中使用`y`复制，`y`+参数代表不同的命令。
- 如`yy`复制游标所在整行、`3yy`复制3行

2、普通模式中使用`p`粘贴
- p(小写)代表粘贴至光标后
- P(大写)代表粘贴至光标前

3、其实`dd`删除命令就是剪切
每次`dd`删除文档内容后，便可以使用`p`来粘贴。这样就可以很快实现——交换上下行：`ddp`。

##### 七、查找替换
1、替换和Undo命令都是针对普通模式下的操作
![](http://upload-images.jianshu.io/upload_images/2070541-194cfe34b8434cb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2、调整文本位置
- 命令行模式下输入`:ce`使本行内容居中
- 命令行模式下输入`:ri`使本行内容靠右
- 命令行模式下输入`:ri`使本行内容靠左

3、查找
- 快速查找
在普通模式下输入`/`或者`?`然后键入需要查找的字符串按回车后就会进行查找，它们的区别在于一个是向下查找，一个是向上查找。进入查找之后，输入`n`和`N`可以继续查找分别继续向下查找，和反向继续查找
- 高级查找
普通模式下输入`\*`寻找游标所在处的单词，向上查找
输入`\#`同上，但是表示向下查找
输入`g\*`同`\*`，但是不是完全匹配，只需要部分符合即可。



![](http://upload-images.jianshu.io/upload_images/2070541-ed6abd4f2309933b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



##### 九、检验学习效果
- 快速定位到当前段落开头
- 快速定位到当前段落结尾
- 复制一段文本，并粘贴
- 删除几行
- 快速翻页
- 查找某个字符串

##### 十、好奇心
为什么要设置h、j、k、l来移动光标呢？一点都不方便，原来是这样因为在写VI编辑器的时候的机器是ADM-3A，这种机器的键盘如下图：

![](http://upload-images.jianshu.io/upload_images/2070541-410f7226aca032d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
具体参照 [why use h j k l](http://www.catonmat.net/blog/why-vim-uses-hjkl-as-arrow-keys/)