
#####- text-align: center的作用是什么，作用在什么元素上？能让什么元素水平居中
text-align作用在块级元素上，可以使块内元素的文字、图片、和行内元素水平居中。但不能使块级元素居中。注意text-align是可继承元素，所以此块级元素的子元素如果是块级元素会继承它的text-align属性，使子块级元素内的文字或图片或内联元素居中，但是子块级元素不会居中。
#####- IE 盒模型和W3C盒模型有什么区别?
IE6/7/8在不添加doctype的情况下即（怪异模式）会使用IE盒模型；
IE6、7、8在添加doctype的情况下，IE9以上和chrome使用w3c盒模型
区别：ie盒模型中width及height的数值并不是指content的width和height而是指padding+border+content（即这时候的width包括了padding和border）

#####- 以下代码的作用？兼容性？
`*{ box-sizing: border-box;}`
作用是为元素设定的任何内边距及边框均在设定的宽度和高度中进行绘制，即设置为了IE盒模型。如果是`box-sizing: content-box`就是w3c盒模型。

#####- line-height: 2和line-height: 200%有什么区别?
line-height:通常用做单行文本垂直居中，如果设置为2，那么文字的行高为它文字本身的两倍。而如果是200%则会立即计算出值为设置元素字体大小的两倍。


#####- inline-block有什么特性？如何去除缝隙？高度不一样的inline-block元素如何顶端对齐?
1、inline的特性：不占据整行，宽度由内容宽度决定
2、又具有block的特性，能设置宽高，但是有缝隙问题。
是由于两行之间有很多空白字符，浏览器都会当作一个文字。
解决方式：把html写到一起或者将父元素的`font-size`设置为0，再在inline-block元素上设置自身的`font-size`
两个inline-block元素不能对齐的问题是由于inline元素默认是基于baseline对齐的，要手动设置vertical-align为:top

#####- CSS Sprite(雪碧图|精灵图)指什么? 有什么作用？
直白点解释就是一种CSS图片合成技术即指集合网页中的小图标或背景图像到一张图片上，然后通过CSS背景定位进行选取所需的部位，这个集成的图片就是雪碧图（或叫精灵图）；其作用是可以1、减少加载图片时对服务器请求次数；2、减少页面的加载时间；3、减少鼠标划过的一些bug;


#####- 让一个元素"看不见"有几种方式？有什么区别?
隐藏或者透明
1、display：none
2、visibility：hidden,只是看不见，但是占据位置
3、opacity：0 filter:alpha(opacity=0);

[代码一](http://js.jirengu.com/rakubifusi/2/edit?html,css,output)
[代码二](http://js.jirengu.com/nubeyenuyu/2/edit?html,css,output)





#####- 如果遇到一个属性想知道兼容性，在哪查看?
可进入caniuse.com、MDN或w3school.com.cn等网站进行查询；

#####- 写一个 btn 的class， 任何 a，span,div,button 添加此class后变成如下按钮的样式(鼠标hover背景色#c14d21, 鼠标按下背景色#e25f31
<a class="btn" href="#">确定</a><span class="btn" >取消</span><div class="btn">提交</div><button class="btn"> 发送</button>
```
*{
  margin:0;
  padding:0;
}
.btn {
  display:inline-block;
  text-decoration:none;
  width: 50px;
  background-color: red;
  margin:10px;
  text-align:center;
  background-color: #f36e41;
  color:white;
  border-radius:3px;
  height:30px;
  line-height:2;
  border:none;
  font-size:14px;
  cursor:pointer;
}
.btn:hover{
  background-color: #c14d21;
}
.btn:active{
  background-color: #e25f31;
}
```