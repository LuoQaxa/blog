#####- CSS的全称是什么?
css是层叠样式表（cascade style sheet），定义HTML元素的样式表现。

#####- CSS有几种引入方式? link 和@import 有什么区别?
1、**行内式**：直接在标签中写style=""
缺点：HTML页面不纯净，文件体积大，不利于蜘蛛爬行，后期维护不方便。
2、**内嵌式**：将css代码写在style标签内。
优缺点：页面使用公共CSS代码，也是每个页面都要定义的，如果一个网站有很多页面，每个文件都会变大，后期维护难度也大，如果文件很少，CSS代码也不多，这种样式还是很不错的。
3、**外链式**：利用link标签链接外部样式表
如：<link type=“text/css” rel=“stylesheet” href=“style.css” />优缺点：实现了页面框架代码与表现CSS代码的完全分离，使得前期制作和后期维护都十分方便。
4、**导入样式**（不建议使用）导入样式和链接样式比较相似，采用@import样式导入CSS样式表，在HTML初始化时，会被导入到HTML或者CSS文件中，成为文件的一部分，类似第二种内嵌样式。分为在html中导入和css中导入：
在html中使用，如下：
```
<style type=“text/css”>
@import url(style.css);
</style>
```

在CSS中使用，如下：
`@import url(style.css);`
四种CSS引入方式的优先级
1.就近原则
2.理论上：行内>内嵌>链接>导入
3.实际上：内嵌、链接、导入在同一个文件头部，谁离相应的代码近，谁的优先级高

**区别**：
1、使用上，link是html的一个标签，可以放在html的任何地方；@import是css的一个语法，放在<style>标签里面，或者放在任何样式文件(例如index.css)里面。切忌@import不能放在html里面（样式文件、style标签外面）。
2、加载顺序，当一个页面被加载的时候，link引用的CSS会同时被加载，而@import引用的CSS 会等到页面全部被下载完再被加载。

##### -以下这几种文件路径分别用在什么地方，代表什么意思?
`css/a.css`:当前路径css文件夹下的a.css文件
`./css/a.css`:当前目录css文件夹下的a.css文件
`b.css`:当前路径下的b.css文件
`../imgs/a.png`：上级目录下的a.png文件
`/Users/hunger/project/css/a.css`:这是一个绝对路径
`/static/css/a.css`：网络路径，表示主域名下，static文件夹下的css文件夹里的a.css文件。即主域名加上/static/css/a.css就是文件路径。


#####- 如果我想在js.jirengu.com上展示一个图片，需要怎么操作?
1、把本地图片上传到网上，生成一个网址（URL），然后通过引用此地址，来加载使用图片。
2、图片上传到jirengu服务器项目文件中的图片文件上，通过相对路径引用图片。

#####- 列出5条以上html和 css 的书写规范
语法不区分大小写，但是建议统一写小写
不使用关联的style属性定义样式
id和class使用有意义的单词，分隔号建议使用-
有可能就是用缩写
属性值是0的省略单位
块内容缩进
属性名冒号后面添加一个空格

#####- 截图介绍 chrome 开发者工具的功能区


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2070541-105a91aac16690f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Elements:查找网页源代码HTML中的任一元素,手动修改任一元素的属性和样式且能实时在浏览器里面得到反馈。
Console:记录开发者开发过程中的日志信息，且可以作为与JS进行交互的命令行Shell。
Sources:断点调试JS。
Network:从发起网页页面请求Request后分析HTTP请求后得到的各个请求资源信息（包括状态、资源类型、大小、所用时间等），可以根据这个进行网络性能优化。
Timeline:记录并分析在网站的生命周期内所发生的各类事件，以此可以提高网页的运行时间的性能。
Profiles:如果你需要Timeline所能提供的更多信息时，可以尝试一下Profiles,比如记录JS CPU执行时间细节、显示JS对象和相关的DOM节点的内存消耗、记录内存的分配细节。
Application:记录网站加载的所有资源信息，包括存储数据（Local Storage、Session Storage、IndexedDB、Web SQL、Cookies）、缓存数据、字体、图片、脚本、样式表等。
Security:判断当前网页是否安全。
Audits:对当前网页进行网络利用情况、网页性能方面的诊断，并给出一些优化建议。比如列出所有没有用到的CSS文件等。

[参考](http://web.jobbole.com/83571/)