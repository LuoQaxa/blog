遍历数组并对数组的每一项进行操作，常用的方法有for循环，forEach，for of，它们各自有什么区别，分别适用于什么时候，这是本文要讨论的。
#### for循环
```js
const arr = [1,2,3,null,4,5]
//普通的for循环
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i])
}

// 传说中性能较高的for循环
for (let i = 0; len = arr.length; i < len; i++) {
    console.log(arr[i])
}
```
其实第二种for循环在chrome浏览器中的表现并不像人们说的不用每次取长度值，提高了效率。而实际运行结果和普通的for循环没有太大区别，因为v8引擎对对象属性操作做了很大的优化，length做为数组的属性，并不需要每次都重新计算数组的长度。

#### forEach
mdn描述：forEach 方法按升序为数组中含**有效值**的每一项执行一次callback 函数，那些**已删除**或者**未初始化的项**将被跳过。

语法：`arr.forEach(callback[, thisArg])`,
返回值： undefined

1. 将for循环改写为forEach
```js
arr.forEach((item) => {
    console.log(item)
})
```
可以看出对比for循环，`forEach`不用去维护一个索引值，但是`forEach`也有缺点：没有办法跳出`forEach`循环

2. 不建议在`forEach`中操作数组，因为结果可能不符合你的预期
```js
var a = [1, 2, 3, 1, 2, 3];
a.forEach((item, index) => {
    console.log(index, item);
    if (item === 1) {
    	a.splice(index, 1);
    }
});
// 输出
// 0 1
// 1 3
// 2 1
// 3 3



var a = [1, 2, 3, 1, 2, 3];
a.forEach((item, index) => {
    console.log(index, item);
    if (item === 1) {
    	a.push(1);
    }
});
// 输出
// 0 1
// 1 2
// 2 3
// 3 1
// 4 2
// 5 3
```
为什么第一个输出4次，第二个输出不是8次呢？
答案可以在mdn中找到：
forEach 遍历的范围在第一次调用 callback 前就会确定。调用 forEach 后添加到数组中的项不会被 callback 访问到。如果已经存在的值被改变，则传递给 callback 的值是 forEach 遍历到他们那一刻的值。已删除的项不会被遍历到。如果已访问的元素在迭代时被删除了（例如使用 shift()），之后的元素将被跳过。

3. 模拟实现forEach
```js
if (!Array.prototype.forEach) {
  Array.prototype.forEach = function (callback, thisArgs) {
    // forEach 遍历的范围在第一次调用 callback 前就会确定
    const originData = this;
    const l = originData.length;
    for (let i = 0; i < l; i++) {
    // 删除之后的元素会被跳过
      if (this[i]) {
        thisArgs ? callback.call(thisArgs, this[i], i, originData) : callback(this[i], i, originData);
      }
    }
  }
}
```
   
#### for of
为了减小多重循环的复杂度，es6提供了可迭代对象和`for of`循环共同解决这个问题

1. 可迭代对象: 
  >>> js中一些内置类型都是内置的可迭代类型并且有默认的迭代行为, 比如 Array or Map, 另一些类型则不是 (比如Object) 。如果普通对象想要成为可迭代对象必须实现@@iterator方法，意思是这个对象（或者它原型链 prototype chain 上的某个对象）必须有一个名字是 Symbol.iterator 的属性。这个属性会在for of循环的每一次迭代中被调用，这个函数返回一个迭代器
  
  - 内置的可迭代类型的`prototype`上有`Symbol(Symbol.iterator)`属性
  ```js
  Object.getOwnPropertySymbols(Map.prototype) //[Symbol(Symbol.toStringTag), Symbol(Symbol.iterator)]
  Object.getOwnPropertySymbols(Array.prototype) //[Symbol(Symbol.iterator), Symbol(Symbol.unscopables)]
  ```
  - 普通对象转化为可迭代对象
  ```js
  function *gen() {
    yield 1;
    yield 2;
  }
  const iterator = gen();
  var obj = {
    a: 1
  }

  obj[Symbol.iterator] = function() {
    return iterator
  }

  for (let item of obj) {
    console.log(item);
  }
  // 1, 2
  ```
  可以发现`for of`实际上是遍历的对象的`Symbol.iterator`属性

2. for of循环的适用场景
 - 它扩展了迭代循环的应用对象，包括：数组，Set/Map，类数组对象，如 arguments 对象、DOM NodeList 对象，Generator 对象，字符串
 - 适用于只需要遍历对象中的元素
 - 在性能方面的优势：可以随时跳出



参考：<br>
[JS数组循环的性能和效率分析（for、while、forEach、map、for of）](https://juejin.im/post/5b645f536fb9a04fc9376882#heading-0)<br>
[Array.prototype.forEach(callback) 的 callback 到底执行了几次?](https://juejin.im/post/5ab229a96fb9a028de4496a3#comment)<br>
[一文彻底弄懂 for forEach for-in for-of 的区别](https://juejin.im/post/5c778c96e51d453eeb067374)<br>
[ES6 系列之迭代器与 for of ](https://github.com/mqyqingfeng/Blog/issues/90)<br>
