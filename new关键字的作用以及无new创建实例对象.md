#### new关键字的作用
1. 参考方神的文章[JS 的 new 到底是干什么的？](https://zhuanlan.zhihu.com/p/23987456?refer=study-fe)
总结起来js中利用了原型链解决了重复创建对象和继承的问题。假如说我们没有使用new关键字，代码就如下

```
function 士兵(ID){
  var 临时对象 = {}
  //绑定实例对象的原型
  临时对象.__proto__ = 士兵.原型
 
  临时对象.ID = ID
  临时对象.生命值 = 42
  //返回实例对象
  return 临时对象
}

士兵.原型 = {
  兵种:"美国大兵",
  攻击力:5,
  行走:function(){ /*走俩步的代码*/}，
  奔跑:function(){ /*狂奔的代码*/  },
  死亡:function(){ /*Go die*/    },
  攻击:function(){ /*糊他熊脸*/   },
  防御:function(){ /*护脸*/       }
}

var 士兵ID = 士兵(ID)
```
2. new关键字帮我们做了四件事：
不用创建临时对象，因为 new 会帮你做（你使用「this」就可以访问到临时对象）；
不用绑定原型，因为 new 会帮你做（new 为了知道原型在哪，所以指定原型的名字为 prototype）；
不用 return 临时对象，因为 new 会帮你做；
不要给原型想名字了，因为 new 指定名字为 prototype。

#### 丢掉new来创建对象
既然知道new帮你做了这些事情，我们来尝试不用new这个语法糖来创建对象
1. 创建临时对象，并返回临时对象
```
var Shape = function(width, height) {
    var self = {}
    self.area = function() {
        return width * height;
    }
    return self;
};

var shape = Shape(20, 30);
shape.area();
```
但是这样没有利用到构造函数的原型对象，不能动态添加方法。
但是直接尝试给_proto_赋值是没有效果的。
2. 类似jquery的无new创建对象
```
var Person = function(name,age){
	//借用另外一个构造函数的new来隔离不同的作用域
   return new init(name,age); 
}
Person.prototype = {
   constructor: Person,
   version    : "1.0.0"
}
// new init()先执行init这个构造函数，既然是要创建Person的实例，即创建的对象的_proto_属性是要指向Person.prototype的。
// 也就是说实例对象要能访问到Person.prototype上的属性和方法。

var init = function(name,age){
  this.name = name;
  this.age = age;
}
// 那就是最关键的一步，将Person.prototype赋值给init.prototype
init.prototype = Person.prototype;



var Person = function(name,age){
   return new Person.prototype.init(name,age); 
}
Person.prototype = {
   constructor : Person,
   version     : "1.0.0"
}
var init = Person.prototype.init = function(name,age){

  this.name = name;
  this.age = age;
  
  // return this; // 加不加都一样
}
init.prototype = Person.prototype; // 最关键的一句
```
3. 最常见的无new创建
```
function Shape(width, height) {
  if (!(this instanceof Shape)) {
    return new Shape(width, height);
  }
  this.width = width;
  this.height = height;
}
Shape.prototype.area = function() {
  return this.width * this.height
};
var shape = Shape(20, 30);
console.log(shape.area());
```
