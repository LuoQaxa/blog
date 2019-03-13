- 浮动元素有什么特征？对其他浮动元素、普通元素、文字分别有什么影响?
浮动元素会脱离文档流。
1、碰到其他浮动元素其并不会忽略；
2、遇见块级元素其会完全忽略浮动元素，但遇到块级元素中的内联元素或直接的内联元素，内联元素会环绕该浮动元素；
3、遇见文字时，文字会环绕在浮动元素周围；

- 清除浮动指什么? 如何清除浮动?
清除浮动指的清除浮动元素对当前元素的影响；
清除浮动的方法
1、clear：both/right/left 可以使该元素的左/右不会有浮动元素对它造成影响。
2、overflow法
在浮动元素的父级元素上加上overflow
```
.clearfix{
	overflow:hidden;
	_zoom:1; /*for ie 6*/
}
```
3、前后缀法
```
.clearfix:before,.clearfix:after{
	content:"";
	display:block;
	clear:both;
}
```

- 有几种定位方式，分别是如何实现定位的，参考点是什么，使用场景如何？
1、static静态定位：器为文档的默认定位方法
2、absolute绝对定位：会脱离文档流，其会相对于static定位意外的第一个父元素进行定位。
3、relative相对定位
其会相对其正常位置进行定位，不会脱离文档流；
4、fixed 固定定位方式
相对窗口进行定位，其不会随着页面翻动而移动，其完全脱离文档流；
absolute相对于第一个定位父元素
relative相对于自身
fixed相当于窗口

- z-index 有什么作用? 如何使用?
其可设置各个定位元素面向用户的层次顺序；其值越大，则表明越在页面的外层；

- position:relative和负margin都可以使元素位置发生偏移?二者有什么区别？
区别是使用position:relative ，该元素原来的位置不会脱离文档流，即使用时可能会出现空白的情况，而负margin则不存在这样的情况；

- BFC 是什么？如何生成 BFC？BFC 有什么作用？举例说明
BFC就是页面上一个隔离出来了的独立容器，容器里面的子元素不会影响到外面的元素。
如何形成BFC：
浮动、绝对定位、display:inline-block/table-cells/table-captions,overflow的值不为visible，时可以创建一个新的格式化上下文。
BFC具有特性：1、阻止垂直外边距折叠：因为可以让嵌套的元素分别在不同的BFC就可以阻止它们外边就折叠了。
2、BFC不会重叠浮动元素
3、BFC可以包含浮动，可以利用这一条特性来清除浮动，设置父元素为BFC，就可以清除浮动，但是这样做都会有一些负作用，要根据实际情况选择不同的方式。

- 在什么场景下会出现外边距合并？如何合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例。
分为两种情况
1、相邻元素外边距合并：两个元素都设置外边距时，外边距不会相加，而是选择外边距的最大值。
2、嵌套元素的外边距合并
阻止嵌套元素的外边距合并形成BFC可以阻止外边柜合并或者元素上加上border或者padding。
[代码](http://js.jirengu.com/mutujoqoxa/1/edit?html,css,output)





- 代码1
https://jsbin.com/zelujexaxo/edit?html,css,output

- 代码2
https://jsbin.com/hoxalulule/1/edit?html,css,js,output

- 代码3
https://jsbin.com/lejosidawe/edit?html,css,output

- 代码4
https://jsbin.com/yeqituluwe/2/edit?html,css,js,output





- img标签和CSS背景使用图片在使用场景上有何区别？
1、img标签适合使用在图片内容可变的或者图片有实际内容的情况下。(img里可设alt对图片进行描述)；
2、背景图片适合使用在图片内容固定不变比如一些小的logo或icon等，还可以采用雪碧图的方法的情况下。
它们两的加载也不同：如果是img标签，则会等待该图片加载完后再加载后续的网页内容，如果是css背景图，则待网页内容及样式全部加载完之后再加载该图片，其不影响浏览网页全部内容。

- title和alt属性分别有什么用？
title属性的作用是给链接a标签、img标签或p标签等注明额外信息用，当元素使用title时，鼠标放在对应的元素上面，会出现提示文本。
alt属性是专门给图片进行内容描述的，这样当浏览器无法加载图片时或者当用户使用屏幕阅读器时，可以通过alt的值了解图片的内容到底是什么。另外图片使用alt也利于网站seo，便于搜索引擎爬虫识别。

- background: url(abc.png) 0 0 no-repeat;这句话是什么意思？
这句话的意思是引用abc.png这张图片，这张图片不偏移，不重复。

- background-size有什么作用? 兼容性如何? 常用的值是?
设置背景图片的大小
http://upload-images.jianshu.io/upload_images/2166980-3842393ba6f7a0ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
常用值有：数字、百分比、cover（让背景图片完全覆盖背景，图片有可能会有一部分超出背景）、content（让背景图片刚扩展至较大使得图片正好适应内容区域或者是正好被包含）

- 如何让一个div水平居中？如何让图片水平居中？
可以使用margin:数字 auto 让div水平居中；
图片水平居中可采用text-align:center; 

- 如何设置元素透明? 兼容性？
可以使用opacity设置
http://upload-images.jianshu.io/upload_images/2166980-5807dcac9a506adc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
所以`opacity = 0.5`
对IE8以下不兼容，可以用`fliter:alpha(opacity=50)`

- opacity 和 rgba都能设置透明，有什么区别？
opacity是可继承属性，而rgba不存在继承的情况。常见情况是使用opacity时元素内的文字的透明度也改变了，这个时候rgba就派上用场了。它只作用于当前元素，不会对其他产生影响。












