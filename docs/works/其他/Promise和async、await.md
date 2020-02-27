 

 

# 1.介绍一下async和await

**async 会将其后的函数（函数表达式或 Lambda）的返回值封装成一个 Promise 对象，而 await 会等待这个 Promise 完成，并将其 resolve 的结果返回出来。**

async / await是ES7的重要特性之一，也是目前社区里公认的优秀异步解决方案。目前async / await 在 IE edge中已经可以直接使用了，但是chrome和Node.js还没有支持。幸运的是，babel已经支持async的transform了，所以我们使用的时候引入babel就行。在开始之前我们需要引入以下的package，preset-stage-3里就有我们需要的async/await的编译文件。

#  2.对ES6中Promise的理解？

​          **Promise 是异步编程的一种解决方案**，比传统的解决方案——回调函数和事件——更合理和更强大。所谓Promise，**简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。**

​          **特点：** 

​        1、自己身上有all、reject、resolve这几个方法

​        2、原型上有then、catch等方法 

​	3、一旦建立，就无法取消，这是它的缺点

 