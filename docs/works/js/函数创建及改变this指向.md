​		

# 函数创建及改变this指向

## 函数的定义和调用

1. 函数声明方式function 关键字(命名函数)

2. 函数表达式(匿名函数)【自调用函数】

3. ```js
    new Function()   var fn = new Function('参数1','参数2'..., '函数体')
    
    var fn = new Function('a','b','console.log(a,b);');
      
   fn(123,456);
   
   ```

4. Function 里面参数都必须是字符串格式

5. 第三种方式执行效率低，也不方便书写，因此较少使用

6. 所有函数都是Function 的实例(对象) 

7. 函数也属于对象

## 函数的调用方式

函数定义：命名函数，匿名函数

调用函数：好多种

1. 普通函数【fn()】
2. 对象的方法【对象.方法()】
3. 构造函数【new Fn()】
4. 绑定事件函数【obj.onclick = function () {}】
5. 定时器函数【window.setInterval(function () {},1000)】
6. 立即执行函数【(function () {})()】



# 改变函数内部this 指向

JavaScript 为我们专门提供了一些函数方法来帮我们更优雅的处理函数内部this的指向问题，常用的有bind()、call()、apply() 三种方法。

## call 方法

call() 方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的thi指向。

fun.call(thisArg, arg1, arg2, ...)

thisArg：在fun 函数运行时指定的this 值

arg1，arg2：传递的其他参数

返回值就是函数的返回值，因为它就是调用函数

function Father () {this}
function Son () { Father.call(this,1,2) }

因此当我们想改变this 指向，同时想调用这个函数的时候，可以使用call，比如继承

## apply 方法

```js
fun.apply(thisArg, [argsArray]):调用函数

thisArg：在fun函数运行时指定的this值

argsArray：传递的值，必须包含在数组里面

返回值就是函数的返回值，因为它就是调用函数

因此apply 主要跟数组有关系，比如使用Math.max() 求数组的最大值

var obj = {name : '张三丰'}
	function fn (arr) {
		console.log(this);
		console.log(arr);
		console.log(arr2);
	}
```




```js
//#################################################
var arr = [23,45,56,23,54];

var n = Math.max.apply(null,arr);

console.log(n); //最大值
```

## bind 方法

bind() 方法不会调用函数。但是能改变函数内部this 指向

fun.bind(thisArg, arg1, arg2, ...)

thisArg：在fun 函数运行时指定的this 值

arg1，arg2：传递的其他参数

返回由指定的this 值和初始化参数改造的原函数拷贝

因此当我们只是想改变this 指向，并且不想调用这个函数的时候，可以使用bind

```
var btn = document.querySelector('input');
```

```js
	btn.onclick = function () {
		this.disabled = true;
		window.setTimeout(function () {
			this.disabled = false;
		}.bind(btn),2000);
}
```

## call  apply  bind 总结


```js
fun.call(obj,arg1,arg2......);
fun.apply(obj,[a,b,c])
fun.bind(obj,arg1,arg2......);

```
相同点:  都可以改变函数内部的this指向.

区别点:  
1.call 和apply  会调用函数, 并且改变函数内部this指向.
2.call 和apply 传递的参数不一样, call 传递参数aru1, aru2..形式apply 必须数组形式[arg]
3.bind  不会调用函数, 可以改变函数内部this指向

主要应用场景:  
1.call 经常做继承. 
2.apply 经常跟数组有关系.比如借助于数学对象实现数组最大值最小值
3.bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向

继承：

​	ES5：组合继承，构造函数 + 原型对象

​	构造函数：call

​	原型对象：父类的实例对象赋值给子类的原型对象，constructor指回构造函数

​	数组遍历方法：forEach，filter，some

​	字符串方法：trim

​	this：指向

​	改变this指向：call，apply，bind


