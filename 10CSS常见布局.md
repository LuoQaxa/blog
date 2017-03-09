- 文档流的概念指什么？有哪种方式可以让元素脱离文档流?
文档流指的是将窗口分成一行一行，元素按从左至右或从上至下的顺序摆放即为文档流。
1、浮动，2、绝对定位


- 如何让一个固定宽高的元素在页面上垂直水平居中?
可采用绝对定位再使用负margin的方式


- 代码题
1、https://jsbin.com/xocoguhode/1/edit?html,css,output
2、

布局
https://jsbin.com/jizuzadafo/1/edit?html,css,output

- 单列布局
http://js.jirengu.com/kicogeqane/1/edit?html,css,output
单列布局可以用一个ComWidth来控制头部内容和尾部的宽度。

- 双列布局，侧边栏固定，主栏目自适应
主要是这两栏的父元素的宽度是不固定的，是自适应的比如是body。侧边栏左浮动，主栏目
设置margin-left为侧边栏的宽度+margin值。那么它的宽度就是自适应的了
http://js.jirengu.com/yukutivoli/2/edit

- 三列布局：左右是固定宽度，中间是自适应宽度
http://js.jirengu.com/jesonofoci/1/edit?html,css,output
需要注意的html的顺序
```
<div class="aside">左边栏</div>
<div class="aside1">右边栏</div>
<div class="main">内容</div>
```
为什么要写在后面呢？如果写在后面的时候因为浮动元素脱离文档流，所以main会在侧边栏下面，再加上margin值就能达到效果。
如果是写在中间，会先渲染main元素，main元素是块级元素，所以会独占一行，下一个浮动元素就会掉下去。所以必须将main写在最后

- 圣杯布局：也是三列布局，两边固定宽度，中间自适应。但是需要把中间内容元素在DOM元素次序中放到最前面。
三个都是浮动元素，设置两个边栏为固定宽度。中间的内容宽度为100%，这个时候目录与侧栏都会被挤到下一行。要想把侧边栏放到上面去，可以分别设置两个的margin-left:-100%和margin-left:-本身的宽度。
然后清除浮动，因为三个都是浮动的元素，然后设置main与侧边栏的距离
http://js.jirengu.com/nakatabipe/1/edit?html,css,output

- 双飞翼布局：为了解决圣杯布局，当.aside的宽度大于.main的宽度时就会出现错乱。
双飞翼布局就能够让.main永远不会比.aside小。
http://js.jirengu.com/jipihoyake/1/edit?html,css,output

- 布局图片展示列表：利用负margin
http://js.jirengu.com/kemiqaqela/1/edit?html,css,output