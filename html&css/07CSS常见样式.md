#####- 块级元素和行内元素分别有哪些？动手测试并列出4条以上的特性区别？
块级元素：div、p、ul、li、ol、h1-h6、table、th、tr、form、dd、dl、dt
行内元素：span、a、img、input、label、strong、em、bold、select、option、textarea、button。
区别：
1、块级元素是单独占据一行，行内元素是在一行内排列根据内容自适应宽高，并且不能对其设置宽高。

![](http://upload-images.jianshu.io/upload_images/2070541-bb999ca875815284.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、块级元素的margin 和 padding是横向和纵向都会生效，而行内元素的padding 和 margin只会水平方向生效。
![](http://upload-images.jianshu.io/upload_images/2070541-b8d01b210583f77a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3、块级元素居中设置margin:0 auto 加上width,而行内元素居中则直接给其父元素设置text-align:center;
4、块级元素可以包含块级元素和行内元素，而行内元素只能包含文本和行内元素.(特例如:h1~h6以及p元素是不能另外包含块元素的因为目前xhml1.0不支持这种做法，等到xhtml2.0的时候估计可以这样写.)
#####- 什么是 CSS 继承? 哪些属性能继承，哪些不能？
1、继承指的是父元素的样式会遗传给子元素，或后n辈元素.
**可继承属性**
所有元素可继承：visibility和cursor
内联元素可继承：letter-spacing、word-spacing、white-space、line-height、color、font、 font-family、font-size、font-style、font-variant、font-weight、text- ecoration、text-transform、direction
块状元素可继承：text-indent和text-align
列表元素可继承：list-style、list-style-type、list-style-position、list-style-image表格元素可继承：border-collapse
**不可继承的属性：**display、margin、border、padding、background、height、min-height、max- height、width、min-width、max-width、overflow、position、left、right、top、 bottom、z-index、float、clear、table-layout、vertical-align、page-break-after、 page-bread-before和unicode-bidi

#####- 如何让块级元素水平居中？如何让行内元素水平居中?
**块级元素居中**：
1、设置块级元素宽度并设置`margin:0 auto;`
2、将父元素设置为`position:relative`，元素设置为`position:absolute; left:50%; margin-left:-2/width`这样会造成父元素的塌陷，因为当把子元素设置为`position:absolute`的时候子元素就脱离文档流，不再能够撑开父元素了。
3、将父元素设置为`display:flex; justify-content:center;`
**行内元素**：
1、将该行内元素的父元素设置为`text-align:center`

#####- 用 CSS 实现一个三角形
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <style>
    .triangle {
      width: 0;
      height: 0;
      border-top:20px solid transparent;  
      border-bottom:20px solid transparent;  
      border-left:20px solid transparent;  
      border-right:20px solid red;  
    }
  </style>
</head>
<body>
  <div class="triangle">
  </div>

</body>
</html>
```
[原理博文](http://blog.csdn.net/huanghui8030/article/details/16984933)
#####- 单行文本溢出加 ... 如何实现?
首先要用`white-space`设置文本不自动换行，然后将超出的部分隐藏，最后设置超出的部分用省略号表示`text-overflow:ellipsis`
![](http://upload-images.jianshu.io/upload_images/2070541-444db004ae8daf65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####- px, em, rem 有什么区别？
1、像素单位，一种绝对值单位，给定文字绝对大小。
2、em的值并不是固定的，em会继承父级元素的字体大小。
3、rem是CSS3新增的一个相对单位（root em），它是相对html根元素而继承的。使用rem作为字体单位还有一个妙用：响应式！ 当屏幕大小变化时使用媒体查询，此时只要设置html根元素的大小，就可以使所有文字同时进行响应式缩放。

#####- 解释下面代码的作用?为什么要加引号? 字体里的数字符号代表什么?
```
body{ font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;}
```
答:表示字体大小为12px,行高为字体大小的1.5倍,字体名称分别有tahoma,arial,'Hiragino Sans GB’等，取字体的规则是浏览器先到电脑里查找第一个字体tahoma，有的话则用这个字体渲染，没有就再找下一个字体；如果都没有找到，那么就用浏览器默认的字体。字体中有空格的，就在名称上加上引号。为了以防中文的字体名在其他电脑上不能够被认出，就用unicode编码方式写出字体名称，即\5b8b\4f53。想要知道自己要设置的字体的unicode编码，打开控制台，输入escape(“字体名称”)，即可得到想要的字体编码，将里面的%转换成\就可以愉快的设置字体了。

#####- 代码
实现如下效果: 【[参考](http://book.jirengu.com/jrg-team/frontend-knowledge-ppt/code/hunger-ui/container.html)】
[代码](http://jsbin.com/cozitusara/edit?html,css,output)
实现如下按钮效果: 【[参考](http://book.jirengu.com/jrg-team/frontend-knowledge-ppt/code/hunger-ui/button.html)】
[代码](http://jsbin.com/tagurusiku/1/edit?html,css,output)
实现如下表格:【[参考](http://book.jirengu.com/jrg-team/frontend-knowledge-ppt/code/hunger-ui/table.html)】
[代码](http://js.jirengu.com/mecalosamo/2/edit?html,css,output)
实现如下三角形[![三角形](http://upload-images.jianshu.io/upload_images/2070541-2bc3bcf4336550f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)](http://7xnk1s.com2.z0.glb.qiniucdn.com/sanjiaoxing.png)
[代码](http://jsbin.com/nohoqugufe/edit?html,css,output)

实现如下Card: 【[参考](http://book.jirengu.com/jrg-team/frontend-knowledge-ppt/code/hunger-ui/card.html)】
[代码](http://js.jirengu.com/faxasepaji/2/edit)