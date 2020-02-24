

##  ajax
### AJAX的应用场景
ajax是一种技术方案，它的应用场景是：在不刷新页面的情况下，去请求服务器，以获取新的数据。简称：**局部更新**
### AJAX是什么
-  中文是异步的javascript和XML
-  AJAX并不是一种新技术，而是一种成熟的解决方案。它要解决的问题是在**网页的局部更新**。
   -  A:异步的
   -  X:xml
-  浏览器通过内置对象 XMLHttpRequest 向服务器发起请求，并可以接收服务器返回给浏览器的数据，这一过程或实现这一过程的技术就是我们所说的 Ajax。
### AJAX的优点
局部更新，提升用户体验。
分离开发，提高开发效率。



##  原生ajax

### 原生ajax基本格式

- ajax的功能是由XMLHttpRequest对象实现的

- 原生ajax的格式

  ```js
  // 第一步： 新建一个XMLHttpRequest对象(xhr)
    var xhr = new XMLHttpRequest();
  
  // 第二步： 设置请求。 xhr.open(请求的方式，接口的url地址);
  xhr.open('get', 'common/getCurrentTime');
  
  // 第三步：设置回调函数。返回的数据存放在xhr.responseText中。
  xhr.onload = function() {
      console.info('从服务器返回的数据',    xhr.responseText);
  };
  // 第四步： 发送请求。
  xhr.send();
  ```

  

### 原生ajax发get请求-带参数

- get请求的参数会以**查询字符串的格式**附加在请求地址后面
  - url?参数1=值1&参数2=值2
- 在network中观察参数出现的位置。
  - 在http的请求行中可以看到
  - 在请求的地址中也可以看到

### 原生ajax发post请求

服务器上接口是post类型的，使用原生的ajax发请求时，要注意两点区别：

1. 如果有参数，则参数以查询字符串的格式附加在send()方法中；

   ```
   var p = 'userName=' + name + '&password=' + pwd;
   xhr.send(p);
   ```

- 参数
  - 可以在http协议的请求体中看到
  - 可以在network面板中看到 

2. 要设置请求头。

   ```
   xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded')
   ```

   

### get和post的区别

- 是使用get还是post完全由后端接口决定，前端调用时，只能照写；
- get传递参数，参数是请求行中
  - 在地址栏中能看见
- post传递参数，参数是在请求体中
  - 在地址栏中看不见。
  - 额外设置请求头
  - 把参数写在send()方法中

### 其它请求方式

- 接口的类型不仅只有get,post
  - put 
    - 小黑窗服务器内置一个put类型接口：
    - xhr.open('put', 'http://localhost:3005/common/putapitest');
  - delete
  - option
- **接口是什么类型，是由后端决定的**



### JSON

- json是一种特殊格式的字符串：它可以与js中的对象进行转换

  - JSON.parse(JSON字符串)  === > js中的数据
  - JSON.stringify(js中的数据) ===> JSON字符串

- 从接口中返回的数据都是字符串

  - 大多数都是JSON字符串

    

### XML

- 与json一样，是一个特殊的字符串，表示数据
- ajax,x就是xml
- 现在被json取代
  - json更简单




### 理解同步异步

同步：代码的书写顺序和执行顺序相同；
异步：代码中的书写顺序与执行顺序不相同；

### ajax中的同步异步

第三个参数是控制同异步的；

```
xhr.open(类型,地址,是否异步)
xhr.open(类型,地址,false); // 同步的方式
```

推荐使用异步的方式；



### onreadystatechange及ajax状态码

 xhr的onload是新添加的事件，ie7,8不能使用它。之前使用onreadystatechange。

```js
xhr.onreadystatechange =function(){
  if(xhr.readyState === 4){
  // console.log(xhr.responseText)
  }
}
<======>
xhr.onload =function(){
  console.log(xhr.responseText)
}
```

- xhr.readystate : 表示ajax的状态

- xhr.status:表示http响应的状态码



### get-ie浏览器缓存问题

问题：在**ie浏览器**中，如果多次**get**请求的地址都一样，则第二次之后的请求将不会发送，沿用第一次请求的结果。

解决：在请求参数中添加一个额外的参数（注意这个参数不要与接口自身的参数冲突），其作用就是让每一次的请求的地址与之前的都不一样，这样浏览器就不会缓存这个get请求了

```
url?_=时间戳；
url?a=1&b=2&_=时间戳；
```

### ajax中的异常错误处理

配合onreadystatechange和xhr.status来处理

```js
xhr.onreadystatechange = function() {
        if (xhr.readyState == 4) {
          if (xhr.status === 404) {
            alert('请联系XXX管理员。接口地址找不到');
            // .接口地址找不到
          } else if (xhr.status === 500) {
            alert('请联系XXX管理员。服务器错误');
            // .接口地址找不到
          } else if (xhr.status === 200) {
            console.log(xhr.responseText);
          }
        }
      };
```

xhr.readyState: xhr的准备状态，有5个取值（0，1，2，3，4）。

xhr.status:http响应的状态(本次请求的响应行中看到)

	- 200
	- 404
	- 301
	- 500


