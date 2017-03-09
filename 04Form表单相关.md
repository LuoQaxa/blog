#####- form表单有什么作用？有哪些常用的input 标签，分别有什么作用？
表单的作用一般是数据采集。
表单有三个基本组成部分：
1、`<form></form>`标签。它的常见属性包括action（规定当提交表单时向何处发送表单数据）、method（规定用于发送form-data的http方法）。
2、表单域：包含常用的input元素有文本字段、复选框（checkbox）、单选框（radio）、上传文件（file）。
3、表单按钮：提交按钮（submit）、复位按钮和一般按钮（button）。

#####- post 和 get 方式的区别？
1、get是从服务器端获取数据，post是向服务器提交数据
2、由于get是向url里添加数据，url的长度是受限制的，所以对数据长度是有限制的，而post是不在url里写数据的所以不受限制
3、由于get的数据是在url里的，所以比起post更加安全，因为参数不会保存在浏览器历史或者web服务器日志中。
(资料)[http://www.nowamagic.net/librarys/veda/detail/1919]

#####- 在input里，name 有什么作用？
所有主流浏览器都支持 name 属性。name 属性规定 <input> 元素的名称。name 属性用于在 JavaScript 中引用元素，或者在表单提交后引用表单数据。只有设置了 name 属性的表单元素才能在提交表单时传递它们的值。

#####- radio 如何 分组?
设置radio的name属性，相同组的name属性是相同的。

#####- placeholder 属性有什么作用?
placeholder 属性规定可描述输入字段预期值的简短的提示信息（比如：Firstname）。该提示会在用户输入值之前显示在输入字段中。placeholder 属性适用于下面的 input 类型：text、search、url、tel、email 和password。

#####- type=hidden隐藏域有什么作用? 举例说明
1、隐藏域在页面中对于用户是不可见的，在表单中插入隐藏域的目的在于收集或发送信息，以利于被处理表单的程序所使用。浏览者单击发送按钮发送表单的时候，隐藏域的信息也被一起发送到服务器。 
2、有些时候我们要给用户一信息，让他在提交表单时提交上来以确定用户身份，如sessionkey，等等．当然这些东西也能用cookie实现，但使用隐藏域就简单的多了．而且不会有浏览器不支持，用户禁用cookie的烦恼。
3、 有些时候一个form里有多个提交按钮，怎样使程序能够分清楚到底用户是按那一个按钮提交上来的呢？我们就可以写一个隐藏域，然后在每一个按钮处加上`onclick="document.form.command.value="xx""`然后我们接到数据后先检查command的值就会知道用户是按的那个按钮提交上来的。 
4、有时候一个网页中有多个form，我们知道多个form是不能同时提交的，但有时这些form确实相互作用，我们就可以在form中添加隐藏域来使它们联系起来。 
5、javascript不支持全局变量，但有时我们必须用全局变量，我们就可以把值先存在隐藏域里，它的值就不会丢失了。
6、还有个例子，比如按一个按钮弹出四个小窗口，当点击其中的一个小窗口时其他三个自动关闭．可是IE不支持小窗口相互调用，所以只有在父窗口写个隐藏域，当小窗口看到那个隐藏域的值是close时就自己关掉。 
#####- 实现如下表单,附上预览地址。其中性别和取向是单选，爱好是多选
代码地址：[jsbin](http://js.jirengu.com/kavilujezi/1/edit?html,output)
![](http://upload-images.jianshu.io/upload_images/2070541-e80e6b605faacf67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)