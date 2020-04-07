# AngularJS

AngularJS 通过新的属性和表达式扩展了 HTML。

AngularJS 是一个 **JavaScript 框架**。它可通过 script 标签添加到 HTML 页面。

AngularJS 通过 **指令** 扩展了 HTML，且通过 **表达式** 绑定数据到 HTML

AngularJS 可以构建一个单一页面应用程序（SPAs：Single Page Applications）。

## AngularJS 指令

### AngularJS 通过 **ng-directives** 扩展了 HTML。

**ng-app** 指令定义了 AngularJS 应用程序的 **根元素**,**ng-app** 指令在网页加载完毕时会**自动引导**（自动初始化）应用程序.

**ng-bind** 指令把应用程序数据绑定到 HTML 视图。

**ng-init** 指令初始化 AngularJS 应用程序变量,通常情况下，不使用 ng-init。您将使用一个控制器或模块来代替它。

```html
<div ng-app="" ng-init="firstName='John'">
 
     <p>在输入框中尝试输入：</p>
     <p>姓名：<input type="text" ng-model="firstName"></p>
     <p>你输入的为： {{ firstName }}</p>
 
</div>
```

**ng-repeat** 指令会重复一个 HTML 元素(**ng-repeat** 指令用在一个对象数组上)

```html
<div ng-app="" ng-init="names=[
{name:'Jani',country:'Norway'},
{name:'Hege',country:'Sweden'},
{name:'Kai',country:'Denmark'}]">
 
<p>循环对象：</p>
<ul>
  <li ng-repeat="x    in names">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>
 
</div>
```

### ng-model 指令

ng-model 指令用于绑定应用程序数据到 HTML 控制器(input, select, textarea)的值。

```js
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name">
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
});
</script>
```

**双向绑定**

```html
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name">
    <h1>你输入了: {{name}}</h1>
</div>
```

**验证用户输入**

```html
<form ng-app="" name="myForm">
    Email:
    <input type="email" name="myAddress" ng-model="text">
    <span ng-show="myForm.myAddress.$error.email">不是一个合法的邮箱地址</span>
</form>
```

**应用状态**

ng-model指令可以为应用数据提供状态值(invalid, dirty, touched, error):

```html
<form ng-app="" name="myForm" ng-init="myText = 'test@runoob.com'">
    Email:
    <input type="email" name="myAddress" ng-model="myText" required></p>
    <h1>状态</h1>
    {{myForm.myAddress.$valid}}
    {{myForm.myAddress.$dirty}}
    {{myForm.myAddress.$touched}} /*Touched: false (如果通过触屏点击则为 true)*/
</form>
```

**CSS类**

ng-model指令基于它们的状态为 HTML 元素提供了 CSS 类：

```html
<style>
input.ng-invalid {
    background-color: lightblue;
}
</style>
<body>

<form ng-app="" name="myForm">
    输入你的名字:
    <input name="myAddress" ng-model="text" required>
</form>
```



### **自定义指令**

你可以使用 **.directive** 函数来添加自定义的指令。

要调用自定义指令，HTML 元素上需要添加自定义指令名。

使用驼峰法来命名一个指令， **runoobDirective**, 但在使用它时需要以 **-** 分割, **runoob-directive**

```js
<body ng-app="myApp">

<runoob-directive></runoob-directive>

<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        template : "<h1>自定义指令!</h1>"
    };
});
</script>

</body>
```

调用自定义指令

```html
标签：<runoob-directive></runoob-directive>
属性：<div runoob-directive></div>
类名：<div class="runoob-directive"></div>
注释:<!-- directive: runoob-directive -->
```

**限制使用**

可以限制你的指令只能通过特定的方式来调用。

```js
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        restrict : "A",
        template : "<h1>自定义指令!</h1>"
    };
});
```

**restrict** 值可以是以下几种:

- `E` 作为元素名使用
- `A` 作为属性使用
- `C` 作为类名使用
- `M` 作为注释使用

**restrict** 默认值为 `EA`, 即可以通过元素名和属性名来调用指令

## AngularJS 表达式

AngularJS 表达式写在双大括号内：**{{ expression }}**。

AngularJS 表达式把数据绑定到 HTML，这与 **ng-bind** 指令有异曲同工之妙。

AngularJS 将在表达式书写的位置"输出"数据。

**AngularJS 表达式** 很像 **JavaScript 表达式**：它们可以包含文字、运算符和变量。

实例 {{ 5 + 5 }} 或 {{ firstName + " " + lastName }}

AngularJS 表达式 与 JavaScript 表达式区别:

类似于 JavaScript 表达式，AngularJS 表达式可以包含字母，操作符，变量。

与 JavaScript 表达式不同，AngularJS 表达式可以写在 HTML 中。

与 JavaScript 表达式不同，AngularJS 表达式不支持条件判断，循环及异常。

与 JavaScript 表达式不同，AngularJS 表达式支持过滤器

## AngularJS Scope(作用域)

scope(作用域) 是应用在 HTML (视图) 和 JavaScript (控制器)之间的纽带。

scope 是模型， 是一个 JavaScript 对象，带有属性和方法，这些属性和方法可以在视图和控制器中使用。

当你在 AngularJS 创建控制器时，你可以将 **$scope** 对象当作一个参数传递:

```html
<div ng-app="myApp" ng-controller="myCtrl">

<h1>{{carname}}</h1>

</div>

<script>
var app = angular.module('myApp', []);

app.controller('myCtrl', function($scope) {
    $scope.carname = "Volvo";
});
</script>
```

当在控制器中添加 **$scope** 对象时，视图 (HTML) 可以获取了这些属性。视图中，你不需要添加 **$scope** 前缀, 只需要添加属性名即可，如： **{{carname}}**。

注：所有的应用都有一个 **$rootScope**，它可以作用在 **ng-app** 指令包含的所有 HTML 元素中。

**$rootScope** 可作用于整个应用中。是各个 controller 中 scope 的桥梁。用 rootscope 定义的值，可以在各个 controller 中使用。

```html
<div ng-app="myApp" ng-controller="myCtrl">

<h1>{{lastname}} 家族成员:</h1>

<ul>
    <li ng-repeat="x in names">{{x}} {{lastname}}</li>
</ul>

</div>

<script>
var app = angular.module('myApp', []);

app.controller('myCtrl', function($scope, $rootScope) {
    $scope.names = ["Emil", "Tobias", "Linus"];
    $rootScope.lastname = "Refsnes";
});
</script>
```

## AngularJS 控制器

**控制** AngularJS 应用程序的数据,它是 **JavaScript 对象**，由标准的 JavaScript **对象的构造函数** 创建

```html
<div ng-app="myApp" ng-controller="personCtrl">

名: <input type="text" ng-model="firstName"><br>
姓: <input type="text" ng-model="lastName"><br>
<br>
姓名: {{fullName()}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('personCtrl', function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
    $scope.fullName = function() {
        return $scope.firstName + " " + $scope.lastName;
    }
});
</script>
/*注：AngularJS 使用$scope 对象来调用控制器。
在 AngularJS 中， $scope 是一个应用对象(属于应用变量和函数)。
控制器的 $scope （相当于作用域、控制范围）用来保存AngularJS Model(模型)的对象。*/
```

**外部文件中的控制器**

```html
<div ng-app="myApp" ng-controller="personCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
<br>
Full Name: {{firstName + " " + lastName}}

</div>

<script src="personController.js"></script>
/*在大型的应用程序中，通常是把控制器存储在外部文件中。
只需要把 <script> 标签中的代码复制到名为 personController.js 的外部文件中即可：*/
```

## AngularJS 过滤器

过滤器可以使用一个管道字符（|）添加到表达式和指令中，用于转换数据

| 过滤器    | 描述                     |
| :-------- | :----------------------- |
| currency  | 格式化数字为货币格式。   |
| filter    | 从数组项中选择一个子集。 |
| lowercase | 格式化字符串为小写。     |
| orderBy   | 根据某个表达式排列数组。 |
| uppercase | 格式化字符串为大写。     |

```html
<div ng-app="myApp" ng-controller="personCtrl">
<p>姓名为 {{ lastName | uppercase }}</p>
</div>   //将字符串格式化为大写

<div ng-app="myApp" ng-controller="personCtrl">
<p>姓名为 {{ lastName | lowercase }}</p>
</div>    //将字符串格式化为小写

<div ng-app="myApp" ng-controller="costCtrl">
<input type="number" ng-model="quantity">
<input type="number" ng-model="price">
<p>总价 = {{ (quantity * price) | currency }}</p>
</div>   //将数字格式化为货币格式

<div ng-app="myApp" ng-controller="namesCtrl">
<ul>
  <li ng-repeat="x in names | orderBy:'country'">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>
</div>  //根据表达式排列数组

<div ng-app="myApp" ng-controller="namesCtrl">
<p><input type="text" ng-model="test"></p>
<ul>
  <li ng-repeat="x in names | filter:test | orderBy:'country'">
    {{ (x.name | uppercase) + ', ' + x.country }}
  </li>
</ul>
</div>
//输入过滤器可以通过一个管道字符（|）和一个过滤器添加到指令中，该过滤器后跟一个冒号和一个模型名称。filter 过滤器从数组中选择一个子集
```

**自定义过滤器**

```js
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.msg = "Runoob";
});
app.filter('reverse', function() { //可以注入依赖
    return function(text) {
        return text.split("").reverse().join("");
    }
});   //将字符串反转
```

## AngularJS 服务(Service)

###  什么是服务？

在 AngularJS 中，服务是一个函数或对象，可在你的 AngularJS 应用中使用。AngularJS 内建了30 多个服务。

###  为什么使用服务?

在很多服务中，比如 $location 服务，它可以使用 DOM 中存在的对象，类似 window.location 对象，但 window.location 对象在 AngularJS 应用中有一定的局限性。AngularJS 会一直监控应用，处理事件变化， AngularJS 使用 **$location** 服务比使用 **window.location** 对象更好。

**$location vs window.location**

|                                         | window.location                                    | $location.service                                    |
| :-------------------------------------- | :------------------------------------------------- | :--------------------------------------------------- |
| 目的                                    | 允许对当前浏览器位置进行读写操作                   | 允许对当前浏览器位置进行读写操作                     |
| API                                     | 暴露一个能被读写的对象                             | 暴露jquery风格的读写器                               |
| 是否在AngularJS应用生命周期中和应用整合 | 否                                                 | 可获取到应用生命周期内的每一个阶段，并且和$watch整合 |
| 是否和HTML5 API的无缝整合               | 否                                                 | 是（对低级浏览器优雅降级）                           |
| 和应用的上下文是否相关                  | 否，window.location.path返回"/docroot/actual/path" | 是，$location.path()返回"/actual/path"               |

###  $http 服务

**$http** 是 AngularJS 应用中最常用的服务。 服务向服务器发送请求，应用响应服务器传送过来的数据。

```js
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
    $http.get("welcome.htm").then(function (response) {
        $scope.myWelcome = response.data;
    });
});
```

###  $q

`$q`服务是AngularJS自己封装的一种对Promise的实现，使用`$q`一般有两种方式。

- $q构造方法

  `$q`的构造方法接收一个函数，该函数接收resolve和reject两个参数，分别代表成功和失败后的回调函数

  ```js
  function asyncHandle() {
             return $q(function (resolve, reject) {
                 if($scope.flag) {
                     resolve('invoke success');
                     $scope.flag = false;
                 } else {
                     reject('invoke fail');
                     $scope.flag = true;
                 }
             });
         }
  
         var promise = asyncHandle();
  
         promise.then(function (result) {
             console.log('congratulation,' + result);
         }, function (result) {
             console.log('i am sorry, ' + result);
         })
  ```

  

- $q的defer()方法

  ```js
  var defered = $q.defer();
        var promise = defered.promise;
  
        promise.then(function (result) {
            console.log('congratulation,' + result);
        }, function (result) {
            console.log('i am sorry, ' + result);
        });
  
        if($scope.flag){
            defered.resolve('invoke success');
            $scope.flag = false;
        } else {
            defered.reject('invoke fail');
            $scope.flag = true;
        }
  ```

  

###  $timeout 服务

```js
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $timeout) {
    $scope.myHeader = "Hello World!";
    $timeout(function () {
        $scope.myHeader = "How are you today?";
    }, 2000);
});
```

###  $interval 服务

```js
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $interval) {
    $scope.theTime = new Date().toLocaleTimeString();
    $interval(function () {
        $scope.theTime = new Date().toLocaleTimeString();
    }, 1000);
});
```

###  创建自定义服务

```js
app.service('hexafy', function() {
    this.myFunc = function (x) {
        return x.toString(16);
    }
});
//要使用自定义服务，需要在定义控制器的时候独立添加，设置依赖关系:
app.controller('myCtrl', function($scope, hexafy) {
    $scope.hex = hexafy.myFunc(255);
});   //将一个数字转换为16进制数
```

**过滤器中，使用自定义服务**

当你创建了自定义服务，并连接到你的应用上后，你可以在控制器，指令，过滤器或其他服务中使用它。

```js
app.filter('myFormat',['hexafy', function(hexafy) {
    return function(x) {
        return hexafy.myFunc(x);
    };
}]);    //在过滤器 myFormat 中使用服务 hexafy:
```

```html
/*在对象数组中获取值时你可以使用过滤器：*/
<ul>
<li ng-repeat="x in counts">{{x | myFormat}}</li>
</ul>
```

## AngularJS Http

**$http** 是 AngularJS 中的一个核心服务，用于读取远程服务器的数据。

使用格式：

```js
// 简单的 GET 请求，可以改为 POST
$http({
    method: 'GET',
    url: '/someUrl'
}).then(function successCallback(response) {
        // 请求成功执行代码
    }, function errorCallback(response) {
        // 请求失败执行代码
});
```

### 简写方法

POST 与 GET 简写方法格式：

```
$http.get('/someUrl', config).then(successCallback, errorCallback);
$http.post('/someUrl', data, config).then(successCallback, errorCallback);
```

此外还有以下简写方法：

- $http.get
- $http.head
- $http.post
- $http.put
- $http.delete
- $http.jsonp
- $http.patch

### 读取 JSON 文件

以下是存储在web服务器上的 JSON 文件：

https://www.runoob.com/try/angularjs/data/sites.php

```json
{     "sites": [         {             "Name": "菜鸟教程",             "Url": "www.runoob.com",             "Country": "CN"         },         {             "Name": "Google",             "Url": "www.google.com",             "Country": "USA"         },         {             "Name": "Facebook",             "Url": "www.facebook.com",             "Country": "USA"         },         {             "Name": "微博",             "Url": "www.weibo.com",             "Country": "CN"         }     ] }
```

### AngularJS $http

AngularJS $http 是一个用于读取`web服务器`上数据的服务。

$http.get(url) 是用于读取`服务器`数据的函数。

> ### 废弃声明 (v1.5)
>
> v1.5 中`$http` 的 `success` 和 `error` 方法已废弃。使用 `then` 方法替代。

### 通用方法实例

AngularJS1.5 以上版本 - 实例

```js
app.controller('siteCtrl', function($scope, $http) {
$http({
method: 'GET',
url: 'https://www.runoob.com/try/angularjs/data/sites.php'
}).then(function successCallback(response) {
$scope.names = response.data.sites;
}, function errorCallback(response) {
// 请求失败执行代码
});
});
```

### 简写方法实例

**AngularJS1.5 以上版本 - 实例**

```html
<div ng-app="myApp" ng-controller="siteCtrl"> 
 
<ul>
  <li ng-repeat="x in names">
    {{ x.Name + ', ' + x.Country }}
  </li>
</ul>
 
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('siteCtrl', function($scope, $http) {
  $http.get("https://www.runoob.com/try/angularjs/data/sites.php")
  .then(function (response) {$scope.names = response.data.sites;});
});
</script>
```

**AngularJS1.5 以下版本 - 实例**

```html
<div ng-app="myApp" ng-controller="siteCtrl"> 
<ul>
  <li ng-repeat="x in names">
    {{ x.Name + ', ' + x.Country }}
  </li>
</ul>
</div>
<script>
var app = angular.module('myApp', []);
app.controller('siteCtrl', function($scope, $http) {
  $http.get("https://www.runoob.com/try/angularjs/data/sites.php")
  .success(function (response) {$scope.names = response.sites;});
});
</script>
```

**应用解析:**

注意：以上代码的 get 请求是本站的服务器，你不能直接拷贝到你本地运行，会存在跨域问题，解决办法就是将 Customers_JSON.php 的数据拷贝到你自己的服务器上，附：[PHP Ajax 跨域问题最佳解决方案](https://www.runoob.com/w3cnote/php-ajax-cross-border.html)。

AngularJS 应用通过 **ng-app** 定义。应用在 <div> 中执行。

**ng-controller** 指令设置了 **controller 对象** 名。

函数 **customersController** 是一个标准的 JavaScript **对象构造器**。

控制器对象有一个属性: **$scope.names**。

**$http.get()** 从web服务器上读取静态 **JSON 数据**。

服务器数据文件为：  [**https://www.runoob.com/try/angularjs/data/sites.php**](https://www.runoob.com/try/angularjs/data/sites.php)。

当从服务端载入 JSON 数据时，**$scope.names** 变为一个数组。

##  AngularJS Select(选择框)

###  ng-option

在 AngularJS 中我们可以使用 **ng-option** 指令来创建一个下拉列表，列表项通过对象和数组循环输出

```html
<div ng-app="myApp" ng-controller="myCtrl"> 
<select ng-init="selectedName = names[0]" ng-model="selectedName" ng-options="x for x in names">
</select>
</div>
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.names = ["Google", "Runoob", "Taobao"];
});
</script>
```

**ng-options 与 ng-repeat**

我们也可以使用**ng-repeat** 指令来创建下拉列表,**ng-repeat** 指令是通过数组来循环 HTML 代码来创建下拉列表，但 **ng-options** 指令更适合创建下拉列表.

**ng-repeat** 有局限性，选择的值是一个字符串;使用 **ng-options** 指令，选择的值是一个对象.当选择值是一个对象时，我们就可以获取更多信息，应用也更灵活。

###  数据源为对象

前面实例我们使用了数组作为数据源，以下我们将数据对象作为数据源。

```js
$scope.sites = {
    site01 : "Google",
    site02 : "Runoob",
    site03 : "Taobao"
};
```

**ng-options** 使用对象有很大的不同，如下所示：

使用对象作为数据源, **x** 为键(key), **y** 为值(value):

```html
<select ng-model="selectedSite" ng-options="**x for (x, y) in sites**">
</select>
<h1>你选择的值是: {{selectedSite}}</h1>
```

你选择的值为在 key-**value** 对中的 **value**。**value** 在 key-**value** 对中也可以是个对象。

选择的值在 key-**value** 对的 **value** 中, 这是它是一个对象:

```js
$scope.cars = {
car01 : {brand : "Ford", model : "Mustang", color : "red"},
car02 : {brand : "Fiat", model : "500", color : "white"},
car03 : {brand : "Volvo", model : "XC90", color : "black"}
};
```

在下拉菜单也可以不使用 **key**-value 对中的 **key** , 直接使用对象的属性：

```html
<select ng-model="selectedCar" ng-options="**y.brand** for (x, y) in cars">
</select>
```

##  AngularJS 表格

###  在表格中显示数据(使用ng-repeat)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="https://cdn.bootcss.com/angular.js/1.6.3/angular.min.js"></script>
</head>
<body>
 
<div ng-app="myApp" ng-controller="customersCtrl"> 
 
<table>
  <tr ng-repeat="x in names">
    <td>{{ x.Name }}</td>
    <td>{{ x.Country }}</td>
  </tr>
</table>
 
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $http) {
    $http.get("/try/angularjs/data/Customers_JSON.php")
    .then(function (result) {
        $scope.names = result.data.records;
    });
});
</script>
```

**废弃声明**

v1.5 中`$http` 的 `success` 和 `error` 方法已废弃。使用 `then` 方法替代。

如果你使用的是 v1.5 以下版本，可以使用以下代码：

```js
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $http) {
    $http.get("/try/angularjs/data/Customers_JSON.php")
    .success(function (response) {$scope.names = response.records;});
});
```

###  使用 CSS 样式

```html
<style>
table, th , td {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd) {
  background-color: #f1f1f1;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>
```

###  使用 orderBy 过滤器

```html
<table>
  <tr ng-repeat="x in names | orderBy : 'Country'">  /*排序显示*/
    <td>{{ x.Name }}</td>
    <td>{{ x.Country }}</td>
  </tr>
</table>
```

###  使用 uppercase 过滤器

```html
<table>
  <tr ng-repeat="x in names">
    <td>{{ x.Name }}</td>
    <td>{{ x.Country | uppercase }}</td>
  </tr>
</table>
```

###  显示序号 ($index)

```html
<table>
  <tr ng-repeat="x in names">
    <td>{{ $index + 1 }}</td>
    <td>{{ x.Name }}</td>
    <td>{{ x.Country }}</td>
  </tr>
</table>
```

###  使用 $even (偶数)和 $odd（奇数）

```html
<table>
<tr ng-repeat="x in names">
<td ng-if="$odd" style="background-color:#f1f1f1">{{ x.Name }}</td>
<td ng-if="$even">{{ x.Name }}</td>
<td ng-if="$odd" style="background-color:#f1f1f1">{{ x.Country }}</td>
<td ng-if="$even">{{ x.Country }}</td>
</tr>
</table>
```

##  AngularJS HTML DOM

###  ng-disabled 指令

直接绑定应用程序数据到 HTML 的 disabled 属性。

```html
<div ng-app="" ng-init="mySwitch=true">
<p>
<button ng-disabled="mySwitch">点我!</button>
</p>
<p>
<input type="checkbox" ng-model="mySwitch">按钮
</p>
<p>
{{ mySwitch }}
</p>
</div>
/*ng-disabled 指令绑定应用程序数据 "mySwitch" 到 HTML 的 disabled 属性。
ng-model 指令绑定 "mySwitch" 到 HTML input checkbox 元素的内容（value）。如果 mySwitch 为true, 按钮将不可用*/
```

###  ng-show 指令

**ng-show** 指令隐藏或显示一个 HTML 元素。

```html
<div ng-app="">
<p ng-show="true">我是可见的。</p>
<p ng-show="false">我是不可见的。</p>
</div>
```

ng-show 指令根据 **value** 的值来显示（隐藏）HTML 元素。

你可以使用表达式来计算布尔值（ true 或 false）:

```html
<div ng-app="" ng-init="hour=13">
<p ng-show="hour > 12">我是可见的。</p>
</div>
```

###  ng-hide 指令

**ng-hide** 指令用于隐藏或显示 HTML 元素。

```html
<div ng-app="">
<p ng-hide="true">我是不可见的。</p>
<p ng-hide="false">我是可见的。</p>
</div>
```

##  AngularJS 事件

AngularJS 有自己的 HTML 事件指令。

###  ng-click 指令

```html
<div ng-app="" ng-controller="myCtrl">
<button ng-click="count = count + 1">点我！</button> /*点击事件*/
<p>{{ count }}</p>
</div>
```

###  隐藏 HTML 元素

**ng-hide** 指令用于设置应用部分是否可见。**ng-hide="true"** 设置 HTML 元素不可见。**ng-hide="false"** 设置 HTML 元素可见。

###  显示 HTML 元素

**ng-show** 指令可用于设置应用中的一部分是否**可见** 。**ng-show="false"** 可以设置 HTML 元素 **不可见**。**ng-show="true"** 可以以设置 HTML 元素可见。

##  AngularJS 模块

模块定义了一个应用程序，是应用程序中不同部分的容器，是应用控制器的容器，控制器通常属于一个模块。

###  创建模块

```html
<div ng-app="myApp">...</div>
<script>
var app = angular.module("myApp", []); /*"myApp" 参数对应执行应用的 HTML 元素。*/
</script> 
```

###  添加控制器

```html
<div ng-app="myApp" ng-controller="myCtrl">
{{ firstName + " " + lastName }}
</div>

<script>
var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
```

###  添加指令

```html
<div ng-app="myApp" runoob-directive></div>

<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        template : "我在指令构造器中创建!"
    };
});
</script>
```

###  模块和控制器包含在 JS 文件中

通常 AngularJS 应用程序将模块和控制器包含在 JavaScript 文件中。

```html
<!DOCTYPE html>
<html>
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
<body>
<div ng-app="myApp" ng-controller="myCtrl">
{{ firstName + " " + lastName }}
</div>
<script src="myApp.js"></script>   /*var app = angular.module("myApp", []);*/
<script src="myCtrl.js"></script>  /*app.controller("myCtrl", function($scope) {
                                     $scope.firstName = "John";
                                     $scope.lastName= "Doe";
                                     });*/
</body>
</html>
```

**JavaScript 中应避免使用全局函数。因为他们很容易被其他脚本文件覆盖**。

**AngularJS 模块让所有函数的作用域在该模块下，避免了该问题。**

###  什么时候载入库?

对于 HTML 应用程序，通常建议把所有的脚本都放置在 <body> 元素的最底部,这会提高网页加载速度，因为 HTML 加载不受制于脚本加载。

在我们的多个 AngularJS 实例中，您将看到 AngularJS 库是在文档的 <head> 区域被加载。

在我们的实例中，AngularJS 在 <head> 元素中被加载，因为对 angular.module 的调用只能在库加载完成后才能进行。

另一个解决方案是在 <body> 元素中加载 AngularJS 库，但是必须放置在您的 AngularJS 脚本前面：

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
</head>
<body>

<div ng-app="myApp" ng-controller="myCtrl">
{{ firstName + " " + lastName }}
</div>
<script>
var app = angular.module("myApp", []);
app.controller("myCtrl", function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
</body>
</html>
```

##  AngularJS 表单

AngularJS 表单是输入控件的集合。

## HTML 控件

以下 HTML input 元素被称为 HTML 控件:

- input 元素
- select 元素
- button 元素
- textarea 元素

###  数据绑定

Input 控件使用 ng-model 指令来实现数据绑定。

```html
<input type="text" ng-model="firstname">
```

通过以上代码应用有了一个名为 firstname 的属性。它通过 ng-model 指令来绑定到你的应用。

firstname 属性可以在 controller 中使用：

```js
var app = angular.module('myApp', []); 
app.controller('formCtrl', function($scope) {     $scope.firstname = "John"; });
```

###  Checkbox（复选框）

```html
<form>
    Check to show a header:
    <input type="checkbox" ng-model="myVar">   /*checkbox 的值为 true 或 false，可以使用 ng-model 指令绑定，它的值可以用于应用中*/
</form>
<h1 ng-show="myVar">My Header</h1>
```

###  单选框

单选框使用同一个 ng-model ，可以有不同的值，但只有被选中的单选按钮的值会被使用。注：myVar 的值可以是 dogs, tuts, 或 cars。

```html
<form>
    选择一个选项:
    <input type="radio" ng-model="myVar" value="dogs">Dogs
    <input type="radio" ng-model="myVar" value="tuts">Tutorials
    <input type="radio" ng-model="myVar" value="cars">Cars
</form>
```

###  下拉菜单

使用 ng-model 指令可以将下拉菜单绑定到你的应用中。ng-model 属性的值为你在下拉菜单选中的选项：

```html
<form>
选择一个选项:
<select ng-model="myVar">
    <option value="">
    <option value="dogs">Dogs
    <option value="tuts">Tutorials
    <option value="cars">Cars
</select>
</form>
```

###  表单实例

```html
<div ng-app="myApp" ng-controller="formCtrl">
  <form novalidate>  /*novalidate 属性是在 HTML5 中新增的。禁用了使用浏览器的默认验证*/
    First Name:<br>
    <input type="text" ng-model="user.firstName"><br>
    Last Name:<br>
    <input type="text" ng-model="user.lastName">
    <br><br>
    <button ng-click="reset()">RESET</button>
  </form>
  <p>form = {{user}}</p>
  <p>master = {{master}}</p>
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('formCtrl', function($scope) {
    $scope.master = {firstName: "John", lastName: "Doe"};
    $scope.reset = function() {
        $scope.user = angular.copy($scope.master);
    };
    $scope.reset();
});
</script>

```

##  AngularJS 输入验证

AngularJS 表单和控件可以验证输入的数据。

###  输入验证

AngularJS 表单和控件可以提供验证功能，并对用户输入的非法数据进行警告。

客户端的验证不能确保用户输入数据的安全，所以服务端的数据验证也是必须的。

```html
<!DOCTYPE html>
<html>
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
<body>

<h2>Validation Example</h2>

<form  ng-app="myApp"  ng-controller="validateCtrl"
name="myForm" novalidate>

<p>用户名:<br>
  <input type="text" name="user" ng-model="user" required>
  <span style="color:red" ng-show="myForm.user.$dirty && myForm.user.$invalid">
  <span ng-show="myForm.user.$error.required">用户名是必须的。</span>
  </span>
</p>

<p>邮箱:<br>
  <input type="email" name="email" ng-model="email" required>
  <span style="color:red" ng-show="myForm.email.$dirty && myForm.email.$invalid">
  <span ng-show="myForm.email.$error.required">邮箱是必须的。</span>
  <span ng-show="myForm.email.$error.email">非法的邮箱。</span>
  </span>
</p>

<p>
  <input type="submit"
  ng-disabled="myForm.user.$dirty && myForm.user.$invalid ||
  myForm.email.$dirty && myForm.email.$invalid">
</p>

</form>

<script>
var app = angular.module('myApp', []);
app.controller('validateCtrl', function($scope) {
    $scope.user = 'John Doe';
    $scope.email = 'john.doe@gmail.com';
});
</script>

</body>
</html>

```

| 属性      | 描述             |
| :-------- | :--------------- |
| $dirty    | 表单有填写记录   |
| $valid    | 字段内容合法的   |
| $invalid  | 字段内容是非法的 |
| $pristine | 表单没有填写记录 |

AngularJS **ng-model** 指令用于绑定输入元素到模型中。

模型对象有两个属性： **user** 和 **email**。我们使用了 **ng-show**指令， **color:red** 在邮件的 **$dirty** 或 **$invalid** 都为 true 时才显示。

`20200325`

## AngularJS API

**A**pplication **P**rogramming **I**nterface（应用程序编程接口）

###  AngularJS 全局 API

AngularJS 全局 API 用于执行常见任务的 JavaScript 函数集合，如：

- 比较对象
- 迭代对象
- 转换对象

全局 API 函数使用 angular 对象进行访问。

以下列出了一些通用的 API 函数：

| API                                                          | 描述                                          |
| :----------------------------------------------------------- | :-------------------------------------------- |
| angular.lowercase (<angular1.7） angular.$$lowercase()（angular1.7+） | 转换字符串为小写                              |
| angular.uppercase() (<angular1.7） angular.$$uppercase()（angular1.7+） | 转换字符串为大写                              |
| angular.isString()                                           | 判断给定的对象是否为字符串，如果是返回 true。 |
| angular.isNumber()                                           | 判断给定的对象是否为数字，如果是返回 true。   |

**注意：**自 AngularJS 1.7 之后移除 angular.lowercase 和 angular.uppercase 方法, 改为 angular.$$lowercase 和 angular.$$uppercase

###  angular.lowercase()

```html
<div ng-app="myApp" ng-controller="myCtrl">
<p>{{ x1 }}</p>
<p>{{ x2 }}</p>
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.x1 = "RUNOOB";
    $scope.x2 = angular.$$lowercase($scope.x1);
});
</script>
```

###  angular.uppercase()

```html
<div ng-app="myApp" ng-controller="myCtrl">
<p>{{ x1 }}</p>
<p>{{ x2 }}</p>
</div>
​
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.x1 = "runoob";
    $scope.x2 = angular.$$uppercase($scope.x1);
});
</script>
```

### angular.isString()

```html
<div ng-app="myApp" ng-controller="myCtrl">
<p>{{ x1 }}</p>
<p>{{ x2 }}</p>
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
$scope.x1 = "RUNOOB";
$scope.x2 = angular.isString($scope.x1);
});
</script>
```

###  angular.isNumber()

```html
<div ng-app="myApp" ng-controller="myCtrl">
<p>{{ x1 }}</p>
<p>{{ x2 }}</p>
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
$scope.x1 = "RUNOOB";
$scope.x2 = angular.isNumber($scope.x1);
});
</script>
```

##  AngularJS Bootstrap

###  Bootstrap

AngularJS 的首选样式表是 Twitter Bootstrap,你可以在你的 AngularJS 应用中加入 Twitter Bootstrap，你可以在你的 <head>元素中添加如下代码:

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css">
```

如果站点在国内，建议使用百度静态资源库的Bootstrap，代码如下：

```html
<link rel="stylesheet" href="//apps.bdimg.com/libs/bootstrap/3.3.4/css/bootstrap.min.css">
```

```html
<!DOCTYPE html>
<html>
<link rel="stylesheet" href="http://apps.bdimg.com/libs/bootstrap/3.3.4/css/bootstrap.min.css">
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
<body ng-app="myApp" ng-controller="userCtrl">

<div class="container">

<h3>Users</h3>

<table class="table table-striped">
  <thead><tr>
    <th>Edit</th>
    <th>First Name</th>
    <th>Last Name</th>
  </tr></thead>
  <tbody><tr ng-repeat="user in users">
    <td>
      <button class="btn" ng-click="editUser(user.id)">
      <span class="glyphicon glyphicon-pencil"></span>&nbsp;&nbsp;Edit
      </button>
    </td>
    <td>{{ user.fName }}</td>
    <td>{{ user.lName }}</td>
  </tr></tbody>
</table>

<hr>
<button class="btn btn-success" ng-click="editUser('new')">
  <span class="glyphicon glyphicon-user"></span> Create New User
</button>
<hr>

<h3 ng-show="edit">Create New User:</h3>
<h3 ng-hide="edit">Edit User:</h3>

<form class="form-horizontal">
<div class="form-group">
  <label class="col-sm-2 control-label">First Name:</label>
  <div class="col-sm-10">
    <input type="text" ng-model="fName" ng-disabled="!edit" placeholder="First Name">
  </div>
</div>
<div class="form-group">
  <label class="col-sm-2 control-label">Last Name:</label>
  <div class="col-sm-10">
    <input type="text" ng-model="lName" ng-disabled="!edit" placeholder="Last Name">
  </div>
</div>
<div class="form-group">
  <label class="col-sm-2 control-label">Password:</label>
  <div class="col-sm-10">
    <input type="password" ng-model="passw1" placeholder="Password">
  </div>
</div>
<div class="form-group">
  <label class="col-sm-2 control-label">Repeat:</label>
  <div class="col-sm-10">
    <input type="password" ng-model="passw2" placeholder="Repeat Password">
  </div>
</div>
</form>

<hr>
<button class="btn btn-success" ng-disabled="error || incomplete">
  <span class="glyphicon glyphicon-save"></span> Save Changes
</button>
</div>

<script src = "myUsers.js"></script>
</body>
</html>
```

## 指令解析

| AngularJS 指令      | 描述                                                  |
| :------------------ | :---------------------------------------------------- |
| <html ng-app        | 为 <html> 元素定义一个应用(未命名)                    |
| <body ng-controller | 为 <body> 元素定义一个控制器                          |
| <tr ng-repeat       | 循环 users 对象数组，每个 user 对象放在 <tr> 元素中。 |
| <button ng-click    | 当点击 <button> 元素时调用函数 editUser()             |
| <h3 ng-show         | 如果 edit = true 显示 <h3> 元素                       |
| <h3 ng-hide         | 如果 edit = true 隐藏 <h3> 元素                       |
| <input ng-model     | 为应用程序绑定 <input> 元素                           |
| <button ng-disabled | 如果发生错误或者 incomplete = true 禁用 <button> 元素 |

------

## Bootstrap 类解析

| 元素     | Bootstrap 类     | 定义             |
| :------- | :--------------- | :--------------- |
| <div>    | container        | 内容容器         |
| <table>  | table            | 表格             |
| <table>  | table-striped    | 带条纹背景的表格 |
| <button> | btn              | 按钮             |
| <button> | btn-success      | 成功按钮         |
| <span>   | glyphicon        | 字形图标         |
| <span>   | glyphicon-pencil | 铅笔图标         |
| <span>   | glyphicon-user   | 用户图标         |
| <span>   | glyphicon-save   | 保存图标         |
| <form>   | form-horizontal  | 水平表格         |
| <div>    | form-group       | 表单组           |
| <label>  | control-label    | 控制器标签       |
| <label>  | col-sm-2         | 跨越 2 列        |
| <div>    | col-sm-10        | 跨越 10 列       |

```js
angular.module('myApp', []).controller('userCtrl', function($scope) {
$scope.fName = '';
$scope.lName = '';
$scope.passw1 = '';
$scope.passw2 = '';
$scope.users = [
{id:1, fName:'Hege', lName:"Pege" },
{id:2, fName:'Kim',  lName:"Pim" },
{id:3, fName:'Sal',  lName:"Smith" },
{id:4, fName:'Jack', lName:"Jones" },
{id:5, fName:'John', lName:"Doe" },
{id:6, fName:'Peter',lName:"Pan" }
];
$scope.edit = true;
$scope.error = false;
$scope.incomplete = false;

$scope.editUser = function(id) {
  if (id == 'new') {
    $scope.edit = true;
    $scope.incomplete = true;
    $scope.fName = '';
    $scope.lName = '';
    } else {
    $scope.edit = false;
    $scope.fName = $scope.users[id-1].fName;
    $scope.lName = $scope.users[id-1].lName;
  }
};

$scope.$watch('passw1',function() {$scope.test();});
$scope.$watch('passw2',function() {$scope.test();});
$scope.$watch('fName', function() {$scope.test();});
$scope.$watch('lName', function() {$scope.test();});

$scope.test = function() {
  if ($scope.passw1 !== $scope.passw2) {
    $scope.error = true;
    } else {
    $scope.error = false;
  }
  $scope.incomplete = false;
  if ($scope.edit && (!$scope.fName.length ||
  !$scope.lName.length ||
  !$scope.passw1.length || !$scope.passw2.length)) {
     $scope.incomplete = true;
  }
};

});
```

## JavaScript 代码解析

| Scope 属性        | 用途                                      |
| :---------------- | :---------------------------------------- |
| $scope.fName      | 模型变量 (用户名)                         |
| $scope.lName      | 模型变量 (用户姓)                         |
| $scope.passw1     | 模型变量 (用户密码 1)                     |
| $scope.passw2     | 模型变量 (用户密码 2)                     |
| $scope.users      | 模型变量 (用户的数组)                     |
| $scope.edit       | 当用户点击创建用户时设置为true。          |
| $scope.error      | 如果 passw1 不等于 passw2 设置为 true     |
| $scope.incomplete | 如果每个字段都为空(length = 0)设置为 true |
| $scope.editUser   | 设置模型变量                              |
| $scope.watch      | 监控模型变量                              |
| $scope.test       | 验证模型变量的错误和完整性                |

##  AngularJS 包含

###  在 HTML 中,目前还不包含 HTML 文件

###  服务端包含

大多服务端脚本都支持包含文件功能 (**SSI**： Server Side Includes)。

使用 SSI, 你可在 HTML 中包含 HTML 文件，并发送到客户端浏览器。

```php
<?php require("navigation.php"); ?>
```

###  客户端包含

通过 JavaScript 有很多种方式可以在 HTML 中包含 HTML 文件。

通常我们使用 http 请求 (**AJAX**) 从服务端获取数据，返回的数据我们可以通过 使用 **innerHTML** 写入到 HTML 元素中。

###  AngularJS 包含(**ng-include** )

**包含html内容**

```html
<body ng-app=""> 
 
<div ng-include="'runoob.html'"></div>  /*你可以使用 ng-include 指令来包含 HTML 内容:*/

</body>
```

**包含 AngularJS 代码**

```html
<div ng-app="myApp" ng-controller="sitesCtrl"> 
  <div ng-include="'sites.htm'"></div>
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('sitesCtrl', function($scope, $http) {
    $http.get("sites.php").then(function (response) {
        $scope.names = response.data.records;
    });
});
</script>

```

```html
/*sites.htm代码，包含了angularjs代码*/
<table>
<tr ng-repeat="x in names">
<td>{{ x.Name }}</td>
<td>{{ x.Url }}</td>
</tr>
</table>
```

###  跨域包含

**默认情况下， ng-include 指令不允许包含其他域名的文件。**

**如果你需要包含其他域名的文件，你需要设置域名访问白名单：**

```html
<body ng-app="myApp">
 
<div ng-include="'https://c.runoob.com/runoobtest/angular_include.php'"></div>
 
<script>
var app = angular.module('myApp', [])
app.config(function($sceDelegateProvider) {
    $sceDelegateProvider.resourceUrlWhitelist([
        'https://c.runoob.com/runoobtest/**'
    ]);   
});
</script>
 
</body>
```

此外，你还需要设置服务端允许跨域访问，

```php+HTML
<?php
// 允许所有域名可以访问
header('Access-Control-Allow-Origin:*');
 
echo '<b style="color:red">我是跨域的内容</b>';
?>
```

##  AngularJS 动画

AngularJS 提供了动画效果，可以配合 CSS 使用。AngularJS 使用动画需要引入 angular-animate.min.js 库

```html
<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular-animate.min.js"></script>
```

还需在应用中使用模型 ngAnimate：

```html
<body ng-app="ngAnimate">
```

###  什么是动画？

动画是通过改变 HTML 元素产生的动态变化效果。

应用中动画不宜太多，但合适的使用动画可以增加页面的丰富性，也可以更易让用户理解。

```html
<body ng-app="ngAnimate">

隐藏 DIV: <input type="checkbox" ng-model="myCheck">

<div ng-hide="myCheck"></div>
    
<script>
var app = angular.module('myApp', ['ngAnimate']);  //如果我们应用已经设置了应用名，可以把 ngAnimate 直接添加在模型中：
</script>
    
</body>
```

###  ngAnimate 做了什么?

ngAnimate 模型可以添加或移除 class 。

ngAnimate 模型并不能使 HTML 元素产生动画，但是 ngAnimate 会监测事件，类似隐藏显示 HTML 元素 ，如果事件发生 ngAnimate 就会使用预定义的 class 来设置 HTML 元素的动画。

AngularJS 添加/移除 class 的指令:

- `ng-show`
- `ng-hide`
- `ng-class`
- `ng-view`
- `ng-include`
- `ng-repeat`
- `ng-if`
- `ng-switch`

`ng-show` 和 `ng-hide` 指令用于添加或移除 `ng-hide` class 的值。

其他指令会在进入 DOM 会添加 `ng-enter` 类，移除 DOM 会添加 `ng-leave` 属性。

当 HTML 元素位置改变时，`ng-repeat` 指令同样可以添加 `ng-move` 类 。

此外， 在动画完成后，HTML 元素的类集合将被移除。例如： `ng-hide` 指令会添加以下类：

- `ng-animate`
- `ng-hide-animate`
- `ng-hide-add` (如果元素将被隐藏)
- `ng-hide-remove` (如果元素将显示)
- `ng-hide-add-active` (如果元素将隐藏)
- `ng-hide-remove-active` (如果元素将显示)

###  使用 CSS 动画

我们可以使用 CSS transition(过渡) 或 CSS 动画让 HTML 元素产生动画效果

####  CSS 过渡

CSS 过渡可以让我们平滑的将一个 CSS 属性值修改为另外一个：

```html
<style>
div {
    transition: all linear 0.5s;
    background-color: lightblue;
    height: 100px;     
    /*在 DIV 元素设置了 .ng-hide 类时，过渡需要花费 0.5 秒，高度从 100px 变为 0:*/
}
.ng-hide {
    height: 0;
}
</style>

```

####  CSS 动画

CSS 动画允许你平滑的修改 CSS 属性值:

```html
<style>
@keyframes myChange {
    from {
        height: 100px;
    } to {
        height: 0;
    }
}
div {
    height: 100px;
    background-color: lightblue;
}
div.ng-hide {
    animation: 0.5s myChange;
}
</style>
```

##  AngularJS 依赖注入

###  什么是依赖注入

wiki 上的解释是：依赖注入（Dependency Injection，简称DI）是一种软件设计模式，在这种模式下，一个或更多的依赖（或服务）被注入（或者通过引用传递）到一个独立的对象（或客户端）中，然后成为了该客户端状态的一部分。

该模式分离了客户端依赖本身行为的创建，这使得程序设计变得松耦合，并遵循了依赖反转和单一职责原则。与服务定位器模式形成直接对比的是，它允许客户端了解客户端如何使用该系统找到依赖 .  **一句话 --- 没事你不要来找我，有事我会去找你。**

AngularJS 提供很好的依赖注入机制。以下5个核心组件用来作为依赖注入：value factory service provider constant

###  value

Value 是一个简单的 javascript 对象，用于向控制器传递值（配置阶段）：

```js
// 定义一个模块
var mainApp = angular.module("mainApp", []);

// 创建 value 对象 "defaultInput" 并传递数据
mainApp.value("defaultInput", 5);
...

// 将 "defaultInput" 注入到控制器
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
   $scope.number = defaultInput;
   $scope.result = CalcService.square($scope.number);
   
   $scope.square = function() {
      $scope.result = CalcService.square($scope.number);
   }
});
```



###  factory

factory 是一个函数,用于返回值。在 service 和 controller 需要时创建。通常我们使用 factory 函数来计算或返回值。

```js
// 定义一个模块
var mainApp = angular.module("mainApp", []);

// 创建 factory "MathService" 用于两数的乘积 provides a method multiply to return multiplication of two numbers
mainApp.factory('MathService', function() {
   var factory = {};
   
   factory.multiply = function(a, b) {
      return a * b
   }
   return factory;
}); 

// 在 service 中注入 factory "MathService"
mainApp.service('CalcService', function(MathService){
   this.square = function(a) {
      return MathService.multiply(a,a);
   }
});
...
```



###  provider

`AngularJS 中通过 provider 创建一个 service、factory等(配置阶段)。Provider 中提供了一个 factory 方法 get()，它用于返回 value/service/factory。`

```js
// 定义一个模块
var mainApp = angular.module("mainApp", []);
...

// 使用 provider 创建 service 定义一个方法用于计算两数乘积
mainApp.config(function($provide) {
   $provide.provider('MathService', function() {
      this.$get = function() {
         var factory = {};  
         
         factory.multiply = function(a, b) {
            return a * b; 
         }
         return factory;
      };
   });
});
```



###  constant

constant(常量)用来在配置阶段传递数值，注意这个常量在配置阶段是不可用的。

```js
mainApp.constant("configParam", "constant value");
```

###  实例

```js
//AngularJS 实例 - factory
var mainApp = angular.module("mainApp", []);
mainApp.value("defaultInput", 5);
 
mainApp.factory('MathService', function() {
    var factory = {};
 
    factory.multiply = function(a, b) {
        return a * b;
    }
    return factory;
});
 
mainApp.service('CalcService', function(MathService){
    this.square = function(a) {
        return MathService.multiply(a,a);
    }
});
 
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
    $scope.number = defaultInput;
    $scope.result = CalcService.square($scope.number);
 
    $scope.square = function() {
        $scope.result = CalcService.square($scope.number);
    }
});
```

```js
//AngularJS 实例 - provider
var mainApp = angular.module("mainApp", []);
         
mainApp.config(function($provide) {
    $provide.provider('MathService', function() {
        this.$get = function() {
            var factory = {};
 
            factory.multiply = function(a, b) {
                return a * b;
            }
            return factory;
        };
    });
});
            
mainApp.value("defaultInput", 5);
         
mainApp.service('CalcService', function(MathService){
    this.square = function(a) {
        return MathService.multiply(a,a);
    }
});
         
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
    $scope.number = defaultInput;
    $scope.result = CalcService.square($scope.number);
 
    $scope.square = function() {
        $scope.result = CalcService.square($scope.number);
    }
});
```

##  AngularJS 路由

AngularJS 路由允许我们通过不同的 URL 访问不同的内容。

通过 AngularJS 可以实现多视图的单页 Web 应用（single page web application，SPA）。

通常我们的 URL 形式为 **http://runoob.com/first/page**，但在单页 Web 应用中 AngularJS 通过 **#! + 标记** 实现，例如：

```http
http://runoob.com/#!/first
http://runoob.com/#!/second
http://runoob.com/#!/third
```

***注意 Angular1.6 之前的版本是通过* # + 标记 *实现路由**

当我们点击以上的任意一个链接时，向服务端请的地址都是一样的 (http://runoob.com/)。 因为 #! 号之后的内容在向服务端请求时会被浏览器忽略掉。 所以我们就需要在客户端实现 #! 号后面内容的功能实现。 AngularJS 路由就通过 **#! + 标记** 帮助我们区分不同的逻辑页面并将不同的页面绑定到对应的控制器上。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>AngularJS 路由实例 - 菜鸟教程</title>
<script src="https://cdn.bootcss.com/angular.js/1.7.0/angular.min.js"></script>
<script src="https://cdn.bootcss.com/angular.js/1.7.0/angular-route.min.js"></script>
</head>
<body ng-app='routingDemoApp'>
 
    <h2>AngularJS 路由应用</h2>
    <ul>
        <li><a href="#!/">首页</a></li>
        <li><a href="#!/computers">电脑</a></li>
        <li><a href="#!/printers">打印机</a></li>
        <li><a href="#!/blabla">其他</a></li>
    </ul>
     
    <div ng-view></div>
    <script>
        angular.module('routingDemoApp',['ngRoute'])
        .config(['$routeProvider', function($routeProvider){
            $routeProvider
            .when('/',{template:'这是首页页面'})
            .when('/computers',{template:'这是电脑分类页面'})
            .when('/printers',{template:'这是打印机页面'})
            .otherwise({redirectTo:'/'});
        }]);
    </script>
</body>
</html>
```

实例解析：

- 1、载入了实现路由的 js 文件：angular-route.js。

- 2、包含了 ngRoute 模块作为主应用模块的依赖模块。

  ```
  angular.module('routingDemoApp',['ngRoute'])
  ```

- 3、使用 ngView 指令。

  ```
  <div ng-view></div>
  ```

  该 div 内的 HTML 内容会根据路由的变化而变化。

- 4、配置 $routeProvider，AngularJS $routeProvider 用来定义路由规则。

  ```
  module.config(['$routeProvider', function($routeProvider){
      $routeProvider
          .when('/',{template:'这是首页页面'})
          .when('/computers',{template:'这是电脑分类页面'})
          .when('/printers',{template:'这是打印机页面'})
          .otherwise({redirectTo:'/'});
  }]);
  ```

AngularJS 模块的 config 函数用于配置路由规则。通过使用 configAPI，我们请求把$routeProvider注入到我们的配置函数并且使用$routeProvider.whenAPI来定义我们的路由规则。

$routeProvider 为我们提供了 when(path,object) & otherwise(object) 函数按顺序定义所有路由，函数包含两个参数:

- 第一个参数是 URL 或者 URL 正则规则。
- 第二个参数是路由配置对象。

###  路由设置对象

AngularJS 路由也可以通过不同的模板来实现。

$routeProvider.when 函数的第一个参数是 URL 或者 URL 正则规则，第二个参数为路由配置对象。

路由配置对象语法规则如下：

```js
$routeProvider.when(url, {
    template: string,
    templateUrl: string,
    controller: string, function 或 array,
    controllerAs: string,
    redirectTo: string, function,
    resolve: object<key, function>
});
```

参数说明：

- **template:**

  如果我们只需要在 ng-view 中插入简单的 HTML 内容，则使用该参数：

  ```
  .when('/computers',{template:'这是电脑分类页面'})
  ```

- **templateUrl:**

  如果我们只需要在 ng-view 中插入 HTML 模板文件，则使用该参数：

  ```
  $routeProvider.when('/computers', {
      templateUrl: 'views/computers.html',
  });
  ```

  以上代码会从服务端获取 views/computers.html 文件内容插入到 ng-view 中。

- **controller:**

  function、string或数组类型，在当前模板上执行的controller函数，生成新的scope。

- **controllerAs:**

  string类型，为controller指定别名。

- **redirectTo:**

  重定向的地址。

- **resolve:**

  指定当前controller所依赖的其他模块。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>AngularJS 路由实例 - 菜鸟教程</title>
<script src="https://cdn.bootcss.com/angular.js/1.7.0/angular.min.js"></script>
<script src="https://cdn.bootcss.com/angular.js/1.7.0/angular-route.min.js"></script>
<script type="text/javascript">
angular.module('ngRouteExample', ['ngRoute'])
.controller('HomeController', function ($scope, $route) { $scope.$route = $route;})
.controller('AboutController', function ($scope, $route) { $scope.$route = $route;})
.config(function ($routeProvider) {
    $routeProvider.
    when('/home', {
        templateUrl: 'embedded.home.html',
        controller: 'HomeController'
    }).
    when('/about', {
        templateUrl: 'embedded.about.html',
        controller: 'AboutController'
    }).
    otherwise({
        redirectTo: '/home'
    });
});
</script>
 
  
</head>
 
<body ng-app="ngRouteExample" class="ng-scope">
  <script type="text/ng-template" id="embedded.home.html">
      <h1> Home </h1>
  </script>
 
  <script type="text/ng-template" id="embedded.about.html">
      <h1> About </h1>
  </script>
 
  <div> 
    <div id="navigation">  
      <a href="#!/home">Home</a>
      <a href="#!/about">About</a>
    </div>
      
    <div ng-view="">
    </div>
  </div>
</body>
</html>
```

