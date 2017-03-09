#####- class 和 id 的使用场景?
class是类选择器，在一个页面中可以重复使用，这样具有某一类特征的元素可以指定相同的类名从而构建相同的样式。
id选择器，在一个页面中仅能指定一个，因此需要权重高，或功能突出，或为了在低版本浏览器中方便JS调用DOM，可以使用id选择器。

#####- CSS选择器常见的有几种?
基础选择器：包括: `*`、`class`、`id`、`element`。
组合选择器：包括：多元素选择器用逗号分隔两个元素、后代选择器用空格隔开、子元素选择器用>号分隔，注意它与后代选择器的区别是：它是直接后代，而后代选择器是选择所有的内部的，不一定是直接子代 。还有毗邻元素选择器+，(注意不是内部而是同级紧跟元素)。
属性选择器
伪类选择器
伪元素选择器：`first-letter`、`first-line`、`before`、`after`。
[参考文章](http://www.cnblogs.com/webblog/archive/2009/07/07/1518274.html)

#####- 选择器的优先级是怎样的?对于复杂场景如何计算优先级？
从高到底排序如下：
在属性后面使用 !important 会覆盖页面内任何位置定义的元素样式
作为style属性写在元素标签上的内联样式
id选择器
类选择器
伪类选择器
属性选择器
标签选择器
通配符选择器
浏览器自定义

**复杂场景计算权重**
如果权重不同，则大的优先级高。比如：行内选择器1000，id选择器的权值为100，class选择器为10，标签选择器为1。
如果权重相同，则后来者居上
#####- a:link, a:hover, a:active, a:visited 的顺序是怎样的？ 为什么？
遵循LVHA原则，即：a:link - a:visited - a:hover - a:active。其原因是这4个伪类选择器因为权重一样，如果顺序不对会导致后面的伪类选择器覆盖掉前面的选择器的样式。例如：把a:visited写在最后面，那么会覆盖掉其余伪类选择器的样式，链接样式只有a:visited所定义的样式。

#####-以下选择器分别是什么意思?

`#header`
{/ 选择id值为header的元素 /}
`.header`
{/ 选择类名为header的元素 /}
`.header .logo`
{/ 选择类名为header元素的后代中类名为logo的所有元素 /}
`.header.mobile`
{/ 选择类名即含header又含mobile的元素 /}
`.header p, .header h3`
{/ 两个选择器且定义相同样式 // 选择类名为header元素后代中所有p标签 // 选择类名为header元素后代中所有的h3标签 /}
`#header .nav>li`
{/ 选择id值为header元素的后代中所有类名为nav的元素的子元素li标签 /}
`#header a:hover`
{/ 选择id值为header元素的后代中a标签并设定其伪类hover的样式，即鼠标悬停的样式 /}
`#header .logo~p`
{/ 选择id值为header元素的后代中所有类名为logo元素后的同级p标签 /}
`#header input[type=“text”]`{/ 选择id值为header元素的后代中type属性值为text的所有input标签 /}

#####- 列出你知道的伪类选择器

![伪类选择器](http://upload-images.jianshu.io/upload_images/2070541-af35f34da7c288b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####- div:first-child和div:first-of-type的作用和区别
first-child必须是其父元素的第一个子元素才能生效，也就是必须是在结构上是父元素的第一个子元素。
而div:first-of-type是选择其父元素的第一个div子元素，必不要求这个子元素结构上要在父元素的第一个子元素上。
[参考资料](http://www.cnblogs.com/xuan52rock/p/4416228.html)

#####- 运行如下代码，解析下输出样式的原因。
```
<style>
.item1:first-child{
  color: red;
}
.item1:first-of-type{
  background: blue;
}
</style>
 <div class="ct">
   <p class="item1">aa</p>
  //p的字体为红色是因为，它是第一个子元素，蓝色背景是因为它是第一个p元素
   <h3 class="item1">bb</h3>
  // 背景颜色为蓝色的原因是因为，它是第一个h3标签
   <h3 class="item1">ccc</h3>
 </div>
```