# pc头条

https://github.com/shuiruohanyu/90heimatoutiao

# 移动端头条

https://github.com/lipengzhou/topline-m



# 黑马头条PC第1天

## 反馈

| ***  | 作用域插槽的用法可以理解为子传父的另一种方法吗？面试的时候被问到组件间通信-子传父的话，可以说作用域插槽的知识吗？ |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

## 复习

- 插槽 

- 匿名插槽 => <slot></slot>  =>  没有name 就认为一个匿名插槽  => <child>  插槽内容</child>

- 具名插槽  =>  <slot name></slot> => 有name  认为是一个具名插槽 => <child>  插槽内容 => slot =>指向给哪个插槽</child>

- 插槽后备内容 =>  <slot>  后备备份内容</slot>  =>备份内容 =>当没有插槽内容传入时 .备份内容会显示

- 作用域插槽 =>  <slot title="张三" ></slot> => <child>  <span slot-scope="obj">  {{ obj.title }}</child>  

- ```html
  <child>
      必须在子组件的标签内部才可以接受到 slot-scope
  </child>
  
  <child></child>
  <child></child>
  ```

- 作用域插槽 => elementIUI =>table => 作用域插槽

## 黑马头条PC-初始化项目-VueCli4.0配置项目

**`目标-任务`** 通过vue-cli4.0初始化一个黑马头条项目  

- 注意: 前期只是为了展示和快速开发,我们基本采用了默认设置,这节课我们来进行一下个性化配置

1. 初始化一个项目(4.0)

   ```bash
   $ vue create toutiao-81 
   ```

2. 创建之后会得到如下图形

3. ![1565167797626](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565167797626.png) 

`default（babel，eslint）`：默认的配置

`Manually select features`：手动选择功能特性配置项

> 我们这里选择第2种，支持更多的自定义选项。

![1565168348755](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168348755.png)

使用键盘上下箭头进行移动，使用空格切换选中与否。

`Babel`：将 ECMAScript  6 转 ECMAScript 5用的一个工具

`Router`：Vue Router 路由

`CSS Pre-processors`：CSS预处理器（SASS、Less、Stylus。。。。）

`Linter / Formatter`：代码校验和格式化

勾选好以后，回车进入下一步。

![1565168419189](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168419189.png)

选择路由模式

路由路径有两种模式：

- hash锚点模式：`http://协议:端口号/path路径/#/路由路径`
  - 简单，兼容好
- history模式：`http://协议:端口号/路由路径`
  - url简洁
  - 兼容差，需要额外的服务器配置

我们这里输入 `n` ,使用默认的路由模式。 回车进入下一步

![1565168480673](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168480673.png)

选择 CSS 预处理器

这里我们选择使用熟悉的 Less 预处理器。回车下一步

![1565168591190](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168591190.png)

选择代码格式校验风格

JavaScript 代码风格不是固定的，社区中有几种比较推荐的格式。

Airbnb 制定的 JavaScript Style

[JavaScript Standard Style](<https://standardjs.com/readme-zhcn.html>)

这里我们选择 `ESLint + Standard config` 模式。

![1565168637110](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168637110.png)

选择代码格式校验方式

`Lint on save`：每当代码文件保存的时候进行格式校验。

`Lint and fix on commit`：当执行 git commit 代码提交的时候进行校验和尝试自动修复校验失败的语法格式，如果校验失败并且自动修复也失败，就无法完成代码提交。你需要手动解决了代码格式问题然后重新提交，这样就确保版本历史中的代码一定没有代码格式问题。

![1565168763310](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168763310.png)

VueCLI 会在项目中生成一些工具的配置文件。配置文件可以存储在两个地方：

`In dedicated config files`：生成独立的配置文件，推荐，维护方便

`In package.json` 混到 package.json 文件中，不推荐，维护麻烦

这里我们选择第1种，将这些工具的配置文件保存到独立的配置文件中，方便查看和修改。

![1565168819556](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565168819556.png)

你可以把你刚才那些选择配置项保存为一个模板，下次使用 `vue create` 创建项目的时候它会提示你是否可以使用这个选择模板直接创建你的项目。

如果你需要，就输入 `y`，然后它会让你给这个模板起个名字，下次就可以直接使用；

如果不需要，就输入 `n`，继续下一步。

这里我们不需要，输入 `n` 继续下一步。

![1565169110413](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565169110413.png)

> 到这里，自定义配置项就完成了，Vue CLI 开始根据你的选择创建项目并安装项目依赖的第三方包。

![1565169240661](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565169240661.png)

> 安装结束，根据在终端中的提示执行以下命令：
>
> ```bash
> $ cd 项目目录
> $ npm run serve
> ```
>
> ![1565169593965](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565169593965.png)

> 启动成功

按照给出的地址，在浏览器中访问测试。

![1565169642554](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565169642554.png)



**`任务`** 根据以上步骤完成 黑马头条项目的初始化

## 黑马头条PC-知识补充-ESlint

- **`目标`**了解什么是ESlint 如何在VSCode中配置ESlint

- ESlint**：是用来统一**JavaScript**代码风格的工具，**不包含css、html等**。

  我们项目中使用的是 [JavaScript Standard Style](<https://standardjs.com/readme-zhcn.html>) 代码风格。下面是它的一些具体规则要求：

  - **使用两个空格** – 进行缩进 

  - **字符串使用单引号** – 需要转义的地方除外

  - ```js
    var a = 'hello world'
    ```

  - **不能有未使用的变量**    

  - **代码结尾无分号无空格**

  - **关键字后加空格** `if (condition) { ... }`

  - **函数名后加空格** `function name (arg) { ... }`

  - 对象 **成员名称******冒号**** 与 **值** 之间需要有一个空格   {name: '张三'}

  - 坚持使用全等 `===` 摒弃 `==` 一但在需要检查 `null || undefined` 时可以使用 `obj == null`。

    .....

  

说了那么多，看看[这个遵循了 Standard 规范的示例文件](https://github.com/expressjs/body-parser/blob/master/index.js) 中的代码吧。或者，这里还有[一大波使用了此规范的项目](https://raw.githubusercontent.com/standard/standard-packages/master/all.json) 代码可供参考。

如果你不认识命令行中的语法报错是什么意思，你可以根据错误代号去 ESLint 规则列表中查找其具体含义。

### 如何应用ESlint

**`目标`** 在vscode中应用eslint

 目前有两种方式 应用eslint  

- 一种是**`编辑器`**中可以加入ESLint插件,在编写代码时 进行检查 并且自动修正 (辅助工具)

  - 一种是在各种框架的**`脚手架`**上 加入了 **`eslint`**检查  一般用于**`代码检查`**和**`提交校验`**

- 如何在VSCode中配置ESlint

- **第一步** 在VSCode插件中 查找ESLint插件 **`安装`**并启用

- ![1565161712465](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565161712465.png)

- **第二步**  打开vscode配置文件 settings.json  (by File-> Preferences->Settings)

  在最末尾如下内容

  ```json
  "eslint.enable": true,
  "eslint.autoFixOnSave": true,
  "eslint.run": "onType",
  "eslint.options": {
      "extensions": [".js",".vue"]
  },
  "eslint.validate": [
      { "language": "html", "autoFix": true },
      { "language": "javascript", "autoFix": true },
      { "language": "vue", "autoFix": true }
  ]
  ```

- 前提是 项目中 支持eslint=>vuecli创建项目时 选择了eslint

## 黑马头条PC-初始化项目-项目目录介绍

**`目标`**初始化项目的目录进行简单认识

```
│  .browserslistrc 该文件会被 Babel 和 Autoprefix 用来根据浏览器的版本确定需要转译的 JavaScript 特性和 CSS 浏览器前缀
│  .editorconfig 编辑器配置文件，编辑器会根据该文件选择编辑格式
│  .eslintrc.js ESLint配置文件
│  .gitignore Git忽略配置文件
│  babel.config.js Babel转码工具配置文件
│  package-lock.json 包管理工具的锁定文件
│  package.json	包说明文件
│  postcss.config.js	postcss配置文件
│  README.md 说明文档
│  
├─node_modules 第三方包
├─public 公共资源目录
│      favicon.ico
│      index.html
│      
└─src 源码目录
    │  App.vue 根组件
    │  main.js 入口模块
    │  router.js 路由模块
    │  
    ├─assets 静态资源目录
    │      logo.png
    │      
    ├─components 非路由组件目录
    │      HelloWorld.vue
    │      
    └─views 路由组件目录
            About.vue
            Home.vue
```

通过代码发现 main.js为整个项目的总入口文件

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
// 在这里完成了 Vue的实例化 并且已经挂载了路由 
```

**`注意`**这里的app.vue实际上为整个项目的根组件 

```xml
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
```

我们发现根组件中放入了导航和路由的承载容器 接着我们查看路由的配置文件

```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/about',
      name: 'about',
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
    }
  ]
})


```

我们发现了一种**`新的组件引用方式`**  



```js
component: () => import(/* webpackChunkName: "about" */ './views/About.vue')

```

**`注意`**: 我们曾经说过spa首屏渲染时会将所有模板的代码都**`一次性`**加载到页面上造成**`首屏加载缓慢`**, 并且提到了一种**`按需加载`**的引用方式,OK,上面这种方式就是**`按需加载`**,只有用到该组件的时候,该组件模块才会被加载到页面上,节省了多余的资源

按需加载 => 只有需要访问的时候 才进行js的请求,否则不请求

**`任务`**查阅以上模块内容,理解以上代码行为.

## 黑马头条PC-初始化项目-git管理

- **`目标-任务`**在github建立一个远程仓库,并将新建的代码推到远程仓库上

- - 真正的项目开发都是采用git管理的  
  - 以后每天的模块增加 修改 删除 都会以git提交的方式 推送给同学们

  - 老师 仓库 => 每天提交内容 到仓库  => 远程仓库地址给 同学们 =>同学们只能拉取代码 ,更新代码
  - 同学 建立自己的远程仓库 => 按照小节敲代码  => 推送 给自己的仓库

1. 新建git远程仓库 

- 首先需要有一个github的账号 然后登陆github官网 进行新建远程仓库操作

2. 完成初始提交

```bash
$ git remote add origin 远程仓库地址
$ git push -u origin master  // -u 的意思是 记录当前的推送信息

```

之后开发的过程如果需要提交历史记录：

```bash
$ git add .  # 工作区修改到暂存
$ git commit -m "log日志" # 暂存区到本地仓库

```

推送的时候如果不改变远程仓库和分支的话就直接：

```bash
$ git push  

```



![image-20191112161411695](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/image-20191112161411695.png)

## 黑马头条PC-初始化项目-安装ElementUI

- **`目标-任务`**在新建的项目中 安装elementUI 并提交git

- 安装

  - ```bash
    $ npm install element-ui --save
    
    ```

  - 在main.js文件中引入elementui模块和注册

    ```js
    import Vue from 'vue'
    import App from './App.vue'
    import router from './router'
    import ElementUI from 'element-ui'  // 引入UI
    import 'element-ui/lib/theme-chalk/index.css' // 引入样式
    Vue.config.productionTip = false
    Vue.use(ElementUI)
    new Vue({
    router,
    render: h => h(App)
    }).$mount('#app')
    
    ```

## 黑马头条PC-初始化项目-整理目录-准备资源

- **`目标-任务`** 清理项目中无用的文件,并导入图片资源 到assets目录下  初始化引入一个index.less文件 
- views一般放置 **`路由级组件`**,就是直接挂到路由表的component的组件,相当于我们原来**`一个个页面`**
- 路由级组件里面 **`引用的其他组件`**一般放在components下 ,这样更规范
- 1. 清理无用的*.vue文件 
- 2. 导入准备好的图片资源
- 3. 在main.js中引入 一个index.less此样式文件的意义是 对于全局样式的设置 例如 margin padding的初始化配置
- 4. 提交git

结论: 此步骤的目的是准备好 开发资源 下一步做好准备

## 黑马头条PC-初始化项目-页面分析-新建登录和主页

- **`目标-任务`** 对具体的页面模块路由进行分析,并在路由中加入新建登录页面 +
- ![1567219836575](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1567219836575.png)
- ![1568772011942](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1568772011942.png)
- 我们访问第一次会进入登录页面  得出 **`登录页`**是**`整个项目的入口页面`**, 登录页肯定属于一级路由
- 进入主页后 我们发现 页面出现了**`三个区域`**  其中中间区域的内容切换菜单时 会发生变化,所以判断 主页存在**`二级路由`**

**`结论`**:通过以上得出结论,  **`登录页`** 和 **`主页`**都为一级路由,主页下 存在**`二级路由`**

根据一级路由和二级路由关系设计以下路由表

| path           | 功能     | 备注           |
| -------------- | -------- | -------------- |
| /login         | 登录     | **`一级路由`** |
| /home          | 首页     | **`一级路由`** |
| /home/publish  | 发布文章 | 二级路由       |
| /home/articles | 文章列表 | 二级路由       |
| /home/comment  | 评论     | 二级路由       |
| /home/material | 素材     | 二级路由       |
| //home/fans    | 粉丝     | 二级路由       |
| /home/account  | 个人设置 | 二级路由       |

- 新建一个login组件和home组件,并配置路由表,在页面显示,提交git
- import login from './login ' //简写模式
- import login from './login/index.vue ' // 完整模式

## 黑马头条PC-登录模块-页面布局及样式

- **`目标-任务`**完成登录页的布局及开发
- **`注意`**千人千面,每个前端程序员对于样式的实现方式都不一样,手法和手段各有不同,但是目标都是写出精美的页面. 
  - 既然我们选择使用elementUI框架,那么任何样式布局的东西都可以先在element中寻找是否有适合的
- 登录实际是个表单 我们可以在ElementUI提供的表单类组件中寻找可使用的组件
- 表单 => 提交数据 ,校验数据 => elementUI表单

**`补充知识点`** 

在单文件组件中,如果需要在style标签中使用 诸如 **less** **scss**  需要在style标签上 给lang属性赋值 如图

**scoped属性**

默认情况下，vue单文件组件的style样式是[全局的]()，

如果在一个应用中使用了**多个**单文件组件，它们使用<span style="background-color:yellow;">相同选择器</span>为相同的元素设置了style样式，那么只有一个会起作用(**后者会覆盖前者**)

**解决方法**：

如果加了**`scoped`**属性,那么当前组件的样式 **`只对当前自己的html`**起作用

给每个style标签都设置一个`scoped`属性，这样各个单文件组件的html标签解析出来后都会带有一个与其他单组件标签不同的`data-v-xxx`的唯一属性，style样式设定也会自动与本身组件的`data-v-xxx`联系起来，这样就使得style样式只针对自己的组件起作用了

登录页实际采用组件

表单 => 采集数据 ,校验数据

- **`el-form`**是表单的容器 ,如果要放置表单, 需要放置在**`el-form`**里面
- 如果 要放置一个input组件到表单 =>  需要放置在**`el-form-item`**里面

- [el-card](https://element.eleme.cn/#/zh-CN/component/card)
- [el-form](https://element.eleme.cn/#/zh-CN/component/form)
- [el-form-item](https://element.eleme.cn/#/zh-CN/component/form)
- el-button
- el-input
- el-checkbox
- 页面内容

```xml
<div class="login">
    <!-- 放置一个el-card组件 -->
    <el-card class='login-card'>
      <!-- 放置标题图片 -->
      <div class='title'>
        <img src="../../assets/img/logo_index.png" alt="">
      </div>
      <!-- 放置表单 -->
      <el-form>
        <!-- 表单域 里面   放置 input/select/checkbox 相当于一行-->
        <el-form-item>
           <el-input placeholder="请输入手机号"></el-input>
        </el-form-item>
        <!-- 表单域 -->
        <el-form-item>
          <el-input style="width:65%" placeholder="验证码"></el-input>
            <el-button style="float:right" plain>发送验证码</el-button>
        </el-form-item>
        <el-form-item>
          <!-- 复选框 -->
          <el-checkbox>我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" style="width:100%">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>

```

页面样式

```less
.login  {
    background-image: url('../../assets/img/back.jpg');
    height: 100vh;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    .login-card {
      width: 440px;
      height: 350px;
      .title {
        text-align: center;
        margin-bottom: 30px;
        img {
          height: 45px;
        }
      }
    }
  }

```

最终实现效果

![image-20191218171710250](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/image-20191218171710250.png)

## 黑马头条PC-登录模块-数据绑定及校验

**`目标-任务`**完成登录模块的表单数据绑定及数据校验-实现点击登录对手机号和验证码的验证

- 表单校验-两种-**`自动校验`**(校验单个表单数据)-**`手动校验`**-提交整个表单时,校验整个表单数据
- 数据校验 => el-form组件绑定 **`model`**属性 => 数据对象  给el-form绑定**`rules`**规则  给form-item配置**`prop`**,prop是校验的字段名(只写字段名)
- 通过采用elementUI的组件进行页面的渲染 绑定数据同样需要根据elementUI要求
- Form 组件提供了表单验证的功能，只需要通过 `rules` 属性传入约定的验证规则，并将 Form-Item 的 `prop` 属性设置为需校验的字段名即可。校验规则参见 [async-validator](https://github.com/yiminghe/async-validator)
- **el-form** 中的 **`model`**属性绑定表单数据对象
- **el-form** 中的 **`rules`**属性绑定数据的校验规则
- **el-form-item** 中的**`prop`**属性 写上 下面表单组件的字段名
- 数据的双向绑定 => v-model 
- required只校验 null  '' undefined 和空字符串 ,但是不校验false/true

| 规则            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| type(可不填)    | 指定要检验的字段的类型                                       |
| **`required`**  | 必填项,如果不填 就无法通过校验/如果为true,就表示该字段必填   |
| **`validator`** | **`自定义校验函数`**                                         |
| **`message`**   | 当不满足设置的规则时的提示信息                               |
| **`pattern`**   | 正则表达式                                                   |
| range           | 使用min和max属性定义范围。对于字符串和数组类型，将根据长度进行比较，对于数字类型，数字不得小于min，也不得大于max。 |
| len             | 要验证字段的确切长度，请指定len属性。对于字符串和数组类型，对length属性执行比较，对于数字类型，此属性指示数字的完全匹配，即，它可能仅严格等于len。如果len属性与最小和最大范围属性组合，则len优先。 |
| enum            | 要从可能值列表中验证值，请使用带枚举属性的枚举类型，列出该字段的有效值，例如： var descriptor = {   role: {type: "enum", enum: ['admin', 'user', 'guest']} } |

如果数据校验不满足 还可以自定义校验函数 **`validator`**

**`validator`**是一个函数, 其中有三个参数 (**`rule`**(当前规则),`value`(当前值),**`callback`**(回调函数))

```js
var  func = function (rule, value, callback) {
    // 根据value进行进行校验 
    // 如果一切ok  
    // 直接执行callback
    callback() // 一切ok 请继续
    // 如果不ok 
    callback(new Error("错误信息"))
}

```



最终模板代码

```xml
 <div class='login'>
      <!-- 使用elementUI组件 el-card -->
     <el-card class="login-card">
         <!-- 匿名插槽 -->
         <div  class='title'>
             <img src="../../assets/img/logo_index.png" alt="">
         </div>
         <!-- 表单 => el-form包裹 -->
         <!-- 数据校验 => el-form绑定 model ,绑定rules规则 -->
         <el-form ref="myForm" :model="loginForm" :rules="loginRules" style="margin-top:20px">
             <!-- 每一个表单域由一个 Form-Item 组件构成 -->
             <!-- form-item  prop属性 绑定 下面表单组件的 字段名 -->
             <el-form-item prop="mobile">
                 <!-- 表单域中可以放置各种类型的表单控件，包括 Input、Select、Checkbox、Radio、Switch、DatePicker、TimePicker -->
                 <!-- 手机号 绑定 v-model -->
                 <el-input v-model="loginForm.mobile" placeholder="请输入手机号"></el-input>
             </el-form-item>
             <el-form-item prop="code">
                 <!-- 验证码 -->
                 <el-input v-model="loginForm.code" placeholder="请输入验证码" style="width:65%"></el-input>
                 <!-- 发送验证码 -->
                 <el-button  style="float:right">发送验证码</el-button>
             </el-form-item>
             <el-form-item prop="agree">
                 <!-- 同意选项 -->
                 <el-checkbox v-model="loginForm.agree">我已阅读并同意用户协议和隐私条款</el-checkbox>
             </el-form-item>
              <el-form-item>
                  <!-- 登录按钮 -->
                  <!-- 注册点击事件 -->
                  <el-button @click="login"  type="primary" style="width:100%">登录</el-button>
              </el-form-item>
         </el-form>
     </el-card>
  </div>

```

最终js代码

```js
export default {
  data () {
    let validator = function (rule, value, callBack) {
      // rule当前规则
      // value当前表单项的值
      // callback 回调函数
      // 正常写法
    //   if (value) {
    //     // 正确 勾选了协议
    //     callBack() // 一切OK请继续
    //   } else {
    //     // 不对 没勾选协议
    //     callBack(new Error('您必须同意无条件被我们蒙骗'))
    //   }
      value ? callBack() : callBack(new Error('您必须同意无条件被我们蒙骗')) // 炫技模式
    }
    return {
      // 表单数据 是一个对象
      loginForm: {
        mobile: '', // 手机号
        code: '', // 验证码
        agree: false // 是否同意协议
      },
      loginRules: {
        //   决定着校验规则  key(字段名):value(对象数组) => 一个对象就是一个校验规则
        // required 为true 就表示该字段必填 如果不填 就会提示消息
        mobile: [{ required: true, message: '请输入您的手机号' },
          { pattern: /^1[3456789]\d{9}$/, message: '请输入合法的手机号' }],
        code: [{ required: true, message: '请输入您的验证码' },
          { pattern: /^\d{6}$/, message: '验证码为6位数字' }],
        agree: [{ validator }]
      } // 登录规则集合对象
      // 自定义形式去校验
    }
  },
  methods: {
    login () {
      // 校验整个表单的规则
      // validate 是一个方法 => 方法中传入的一个函数 两个校验参数  是否校验成功/未校验成功的字段
      this.$refs.myForm.validate(function (isOK) {
        if (isOK) {
          console.log('校验成功')
        }
      })
    }
  }
}

```

结论: 用到的**正则表达式**

手机号: **/^1[3456789]\d{9}$/**

6位数字:**/^\d{6}$/**

- el-form  需要绑定model,需要规则rules 
- el-form-item 需要prop属性 需要绑定校验的字段 
- rules规则 => required必填 pattern正则表达式 message 提示信息 
- 自定义校验函数 validator  => rule,value,callback =>  callBack() / callBack(new Error(错误信息))

## 黑马头条PC-登录模块-安装axios-配置全局使用

**`目标-任务`** 将axios安装在当前项目中,并将其赋值给全局对象,在任何位置都可以访问 并配置baseUrl

- 登录需要接口访问,访问工具推荐 axios

- axios 安装到运行依赖

  ```bash 
  $ npm i axios -S
  or 
  $ npm install axios --save
  
  ```

- 引入axios 配置baseUrl

- 在main.js中引用 并赋值给Vue的原型属性

- ![1565191964151](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565191964151.png)

## 黑马头条PC-登录模块-登录请求-返回值中token解析

**`目标-任务`** 通过axios调用登录接口,得到登录返回值 分析返回值意义

```js
     this.$http
        .post('/authorizations', this.formData)
        .then(result => {
            console.log(result)
        })

```

**得到的数据结果**:

<table>
  <thead class="ant-table-thead">
    <tr>
      <th key=name>名称</th><th key=type>类型</th><th key=required>是否必须</th><th key=default>默认值</th><th key=desc>备注</th><th key=sub>其他信息</th>
    </tr>
  </thead><tbody className="ant-table-tbody"><tr key=0-0><td key=0><span style="padding-left: 0px"><span style="color: #8c8a8a"></span> message</span></td><td key=1><span>string</span></td><td key=2>必须</td><td key=3></td><td key=4><span>消息提示</span></td><td key=5></td></tr><tr key=0-1><td key=0><span style="padding-left: 0px"><span style="color: #8c8a8a"></span> data</span></td><td key=1><span>object</span></td><td key=2>非必须</td><td key=3></td><td key=4><span>数据</span></td><td key=5></td></tr><tr key=0-1-0><td key=0><span style="padding-left: 20px"><span style="color: #8c8a8a">├─</span> token</span></td><td key=1><span>string</span></td><td key=2>必须</td><td key=3></td><td key=4><span>用户token令牌</span></td><td key=5></td></tr><tr key=0-1-1><td key=0><span style="padding-left: 20px"><span style="color: #8c8a8a">├─</span> refresh_token</span></td><td key=1><span>string</span></td><td key=2>必须</td><td key=3></td><td key=4><span>用于刷新token的令牌</span></td><td key=5></td></tr><tr key=0-1-2><td key=0><span style="padding-left: 20px"><span style="color: #8c8a8a">├─</span> id</span></td><td key=1><span>integer</span></td><td key=2>必须</td><td key=3></td><td key=4><span>用户id</span></td><td key=5></td></tr><tr key=0-1-3><td key=0><span style="padding-left: 20px"><span style="color: #8c8a8a">├─</span> name</span></td><td key=1><span>string</span></td><td key=2>必须</td><td key=3></td><td key=4><span>用户昵称</span></td><td key=5></td></tr><tr key=0-1-4><td key=0><span style="padding-left: 20px"><span style="color: #8c8a8a">├─</span> photo</span></td><td key=1><span>string</span></td><td key=2>必须</td><td key=3></td><td key=4><span>用户头像</span></td><td key=5></td></tr>
               </tbody>
              </table>

我们需要重点分析一下上面传给我们的**token(令牌)**

- **token令牌** 是**`前后分离`**时代的产物
- 传统模式 采用的是**session**和**cookie** 
- ![1565191558467](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565191558467.png)

![1565191796203](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1565191796203.png)

## 黑马头条PC-登录模块-登录请求-token存储问题

**`目标-任务`**对token令牌进行前端存储,以便后续接口访问使用

- 上个小节中我们发现 token会被频繁用到,不可能每次请求接口之前先去后端登录获取一下token,所以token要在前端进行持久化

**`前端持久化`** 可以直接采用 **`localStorage`** localStorage和session没关系

**注意**设置数据时,由于我们设置的用户信息是个对象 需要先将对象转化成字符串  

```js
JSON.stringify(obj)

```

实际代码

```js
 this.$http.post('/authorizations', this.formData).then(result => {
         window.localStorage.setItem('user-token',result.data.data.token)
 })

```

## 黑马头条PC-登录模块-登录成功及失败处理

**`目标-任务`** 对登录成功或者失败时进行不同的处理

- 登录成功时 需要跳转 到主页
- 登录失败时 提示信息

实际代码

```js
          this.$axios({
            url: '/authorizations',
            method: 'post',
            data: this.loginForm
          }).then(result => {
            // console.log(result.data.data.token)
            // 放到前端的缓存中
            window.localStorage.setItem('user-token', result.data.data.token)
            // 编程式导航
            this.$router.push('/') // 登录成功 跳转到home页
          }).catch(() => {
            this.$message({
              message: '手机号或者验证码错误',
              type: 'warning'
            })
          })


```

## 黑马头条PC-主页模块-页面布局

**`思路-步骤`** 实现以下布局

![1568793370086](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1218%E9%A1%B9%E7%9B%AE%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0/assets/1568793370086.png)

- elementUI组件 是否有支持类似效果的

- el-container => 大容器

- 左侧 =>  el-aside 

- 右侧 => el-container =>  el-header- el-main

- ```xml
  <!-- 先定义一个大容器 -->
    <el-container>
      <!-- 先放置一个左侧 -->
      <el-aside>左侧内容</el-aside>
      <!-- 右侧大容器 -->
      <el-container>
        <!-- 头部 -->
        <el-header>头部</el-header>
        <!-- 中部区域 -->
        <el-main>
          <!-- 二级路由容器 -->
           <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  
  ```

  

## 黑马头条PC-主页模块-左侧导航菜单

**`思路-步骤`**

- 左侧菜单背景色 #323745
- 菜单上部图片背景色  #2e2f32
- 导航背景色 #353b4e
- 导航字体颜色 #adafb5
- 导航字体激活颜色  #ffd04b

- 左侧导航=> 抽提一个新的组件 => components(普通组件)

- 导航组件=> el-menu => el-menu-item =>  不折叠的=>不带二级菜单的

- el-menu=> 二级菜单=> el-submenu => el-menu-item  => el-submenu 显示内容 => title插槽决定 => 

- ```xml
  <div class='layout-aside'>
       <div class='title'>
           <img src="../../assets/img/logo_admin.png" alt="">
       </div>
       <el-menu
        style="width:201px"
        background-color="#353b4e"
        text-color="#adafb5"
        active-text-color="#ffd04b">
        <!-- 首页 -->
         <el-menu-item index="4">
             <!-- 图标 -->
          <i class="el-icon-s-home"></i>
          <span slot="title">首页</span>
        </el-menu-item>
        <!-- 内容管理 二级菜单 el-submenu => el-menu-item-->
        <el-submenu index="1">
            <!-- el-submenu 插槽 title =>  一级显示内容 -->
          <template slot="title">
            <i class="el-icon-document"></i>
            <span>内容管理</span>
          </template>
            <!-- 二级内容 -->
            <el-menu-item index="1-1">发布文章</el-menu-item>
            <el-menu-item index="1-2">内容列表</el-menu-item>
            <el-menu-item index="1-3">评论列表</el-menu-item>
            <el-menu-item index="1-3">素材管理</el-menu-item>
        </el-submenu>
        <el-submenu>
            <!-- title插槽时submenu 中显示的一级内容 -->
            <template slot='title'>
                <i class='el-icon-s-custom'></i>
                <span>粉丝管理</span>
            </template>
            <!-- 二级内容 -->
           <el-menu-item>图文数据</el-menu-item>
           <el-menu-item>粉丝概况</el-menu-item>
           <el-menu-item>粉丝画像</el-menu-item>
           <el-menu-item>粉丝列表</el-menu-item>
  
        </el-submenu>
        <el-menu-item index="3" >
          <i class="el-icon-s-tools"></i>
          <span slot="title">账户信息</span>
        </el-menu-item>
  
      </el-menu>
    </div>
  
  ```

## 总结

- 登录校验

- vue-cli 4.0 创建了一个项目 

- babel/router/css-processers/lint-formatter  => 个性化配置

- 安装了elementUI  

- 整理了目录 导入了图片,删除了没用的文件

- git  管理 => 建立远程仓库 ,   

- ```bash
  $  git remote  add origin  远程地址
  $  git  push  -u origin master 
  
  ```

- 登录页面分析  => 登录/主页 一级路由  => 二级路由

- 登录 => 布局 =>  div => el-card => el-form 

- el-form ==> el-form-item => el-input 

- el-form  model => 表单数据对象

- el-form  rules =>  校验规则对象

- el-form-item => prop => 绑定校验的字段名

- el-input => v-model

- required  必填 message 提示信息  pattern  正则表达式  validator (自定义校验函数)

- validator => funtion(rule,value,callback) =>  通过  callback()  不通过 callback(new Error())

- 手动校验表单

- el-form => ref属性

- this.$refs.ref属性 => validate(function(isOK){}) => isOK true => 校验成功 ,否则不成功

## 黑马头条PC-主页模块-头部结构及下拉菜单

**`思路-步骤`**

![image-20191219163207234](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1219/%E7%AC%94%E8%AE%B0/assets/image-20191219163207234.png)

elementUI => flex =>el-row/ el-col

```html
 <el-row class='layout-header' type='flex' align="middle">
      <!-- 先定义一行 -->
     <el-col class='left' :span="12">
         <i class='el-icon-s-fold'></i>
         <span>江苏传智播客教育科技股份有限公司</span>
     </el-col>
     <el-col class='right' :span="12">
         <el-row type='flex' justify="end" align="middle">
             <img src="../../assets/img/header.jpg" alt="">
             <!-- 下拉菜单 -->
             <el-dropdown>
                 <!-- 匿名插槽  下拉菜单显示的元素内容 -->
                 <span>水若寒宇</span>
                 <el-dropdown-menu slot="dropdown">
                     <el-dropdown-item>个人信息</el-dropdown-item>
                     <el-dropdown-item>git地址</el-dropdown-item>
                     <el-dropdown-item>退出</el-dropdown-item>
                 </el-dropdown-menu>
             </el-dropdown>
         </el-row>
     </el-col>

  </el-row>
```



## 黑马头条PC-统一全局注册插件的使用方式Vue.use

**`思路-步骤`**实现 像elementUI一样 ,直接use ,然后就随便用

- elementUI里面 导出了一个对象=> Vue.use就会调用对象中的方法 =>install(Vue)

- ```js
  export default { 
    install(Vue){
        Vue.component()
        Vue.component()
        Vue.component()
        Vue.component()
        Vue.component()
        Vue.proptotype.$message = ''
    }
  }
  // elementUI导出的方法
  ```

- Vue.use(对象) => Vue框架 会调用 对象中的方法 **`install方法`**

- 调用insall方法时, 会传入Vue对象

- elementUI的install方法 里面 拿到了Vue对象, **`Vue.component()`** // 注册 组件

- 要实现类似elementUI的效果 => 定义对象  => install方法 =>  全局注册组件

- ```js
  import layoutAside from './home/layout-aside'
  import layoutHeader from './home/layout-header'
  
  // 所有自定义组件的插件
  export default {
    install: function (Vue) {
      Vue.component('layout-aside', layoutAside) // 注册 左侧导航组件
      Vue.component('layout-header', layoutHeader) // 注册头部组件
    }
  }
  
  ```

  

## 黑马头条PC-主页模块-头部信息查询

**`思路-步骤`**

![image-20191219171348086](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1219/%E7%AC%94%E8%AE%B0/assets/image-20191219171348086.png)

- 调用接口 =>查询 用户信息  => 用户信息 展示到 页面上
- img => 固定地址的话  =>  代码编译时 ,会将 img 的图片 编译成base64字符串 => 可以预览
- img => 动态变量  => 给一个相对地址 不能够让图片显示
- 如果想显示 => 需要先将图片变化成变量 => 动态展示
- 图片 地址 => 动态变量时  => require(地址) => 变量 => 去做逻辑判断

## 黑马头条PC-主页模块-头部退出系统

**`思路-步骤`**

- 退出 => 登录页, 删除掉令牌

- ```js
      //   点击菜单项时触发
      clickMenu (command) {
        if (command === 'info') {
  
        } else if (command === 'git') {
          //   跳转到git地址
          window.location.href = 'https://github.com/shuiruohanyu/90heimatoutiao'
        } else {
          //    退出
          window.localStorage.removeItem('user-token') // 删除令牌
          this.$router.push('/login') // 回到登录页
        }
      }
  ```

  



## 黑马头条PC-主页模块-左侧导航配置路由

**`思路-步骤`**

- el-menu  => 左侧导航 => 导航路由? 

- router-link => to => 跳转地址

- el-menu => router => true  => 使用 vue-router 的模式，启用该模式会在激活导航时以 index 作为 path 进行路由跳转

- :router="true" => 设置router 为true的完整写法

- router  =>  等价于 :router="true"

- | path           | 功能     | 备注           |
  | -------------- | -------- | -------------- |
  | /login         | 登录     | **`一级路由`** |
  | /home          | 首页     | **`一级路由`** |
  | /home/publish  | 发布文章 | 二级路由       |
  | /home/articles | 文章列表 | 二级路由       |
  | /home/comment  | 评论     | 二级路由       |
  | /home/material | 素材     | 二级路由       |
  | //home/fans    | 粉丝     | 二级路由       |
  | /home/account  | 个人设置 | 二级路由       |

## 黑马头条PC-主页模块-默认导航

**`思路-步骤`**

![1568951095742](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1219/%E7%AC%94%E8%AE%B0/assets/1568951095742.png)

- 二级路由的path  什么都不写 代表 二级路由的默认组件

## 黑马头条PC-登录模块-主页-权限思考

**`思路-步骤`**  

- 不论登录与否 =>都可以直接进入主页 => **`不对`**!!!!

- 如果没登录 => 不能进入主页 =>  没token就不能进入主页

- 进入主页 => 有token => 放行

- 拦截 => 路由改变瞬间 => 判断有无token => 有token  继续 =>没token 就回登录

- 路由改变瞬间 => 导航守卫 => 路由改变时  => 页面拦截

  

## 黑马头条PC-主页模块-导航守卫

**`思路-步骤`**

- router.beforeEach  => 全局前置守卫 => 在每一个路由发生改变之前 会触发这个事件

  ```js
  router.beforeEach(function(to,from,next){})
  ```

  login => home

  this.$route.path

  **to: Route**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)

  **from: Route**: 当前导航正要离开的路由

  **next: Function**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。

  ```js
  new Promise(function(resolve,reject){   }).then
  ```

  - next函数必须执行 =>不执行 就会死在跳转的位置
  - 如果直接执行next() => 表示一切正常 login => home 可以正常走   类似 callback()
  - **next(false)** => 中断当前的导航 =>  login => home 不能正常走  停在login
  - **next(地址)** => 强制将login=>home =>另一个地址 

  ```js
  import router from './router'
  // 全局前置守卫
  router.beforeEach(function (to, from, next) {
    // 判断 拦截的范围
    if (to.path.startsWith('/home')) {
      // 进入到了拦截范围
      // 判断是否登录 有token 就登录 没token就没登录
      let token = window.localStorage.getItem('user-token') // 获取token
      if (token) {
        // 如果有token
        next()
      } else {
        next('/login') // 没有token 就跳转到登录页
      }
    } else {
      next() // 放行
    }
  })
  // 先导出
  export default router
  ```

  

## 黑马头条PC-接口访问-token统一处理思考

**`思路-步骤`**

- token是令牌, 调用接口时 基本都要携带令牌,携带令牌的方式 各个接口 自己找自己的,这种方式不统一!!! 不好!!!!

班里有50个同学,要去食堂吃饭,但是吃饭每个人需要**`证件(token)`**,现在教室里每个人的证件都在讲台上,大家去吃饭先要去讲台上**`拿证件(取token)`**才能吃饭,50个人要分别上50次讲台,**`每个人独自取自己的token`**,现在有个方案,在大家出门前,老师自动把**`证件(统一注入token)`**放到每个人的兜里,大家不再需要上讲台拿证件,直接去食堂,很爽!!!!!

- 统一处理携带的令牌 => token => 携带参数  => axios =>headers=>Authorization
- axios拦截器 
- 请求拦截

## 黑马头条PC-接口访问-axios拦截器-统一处理请求token

**`思路-步骤`**

- 请求拦截 => **`请求之前`**拦截 =>  **`请求到达后台之前`**拦截
- **`请求到达后台之前`** => 将token塞进去,token格式一致
- 
- 响应拦截 => 别人返回的数据 拦截

```js
// 负责对axios进行处理
import axios from 'axios'
axios.interceptors.request.use(function (config) {
  // 在发起请求请做一些业务处理
  // config是要发送请求的配置信息
  let token = window.localStorage.getItem('user-token') // 获取token
  config.headers['Authorization'] = `Bearer ${token}` // 统一注入token 到headers属性 因为所有接口要求的token格式是一样的
  return config
}, function (error) {
  // 对请求失败做处理
  return Promise.reject(error)
})
export default axios
```

- config 的选项对象  axios默认选项

  ```json
  {
     // `url` 是用于请求的服务器 URL
    url: '/user',
  
    // `method` 是创建请求时使用的方法
    method: 'get', // default
  
    // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
    // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
    baseURL: 'https://some-domain.com/api/',
  
    // `transformRequest` 允许在向服务器发送前，修改请求数据
    // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
    // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
    transformRequest: [function (data, headers) {
      // 对 data 进行任意转换处理
      return data;
    }],
  
    // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
    transformResponse: [function (data) {
      // 对 data 进行任意转换处理
      return data;
    }],
  
    // `headers` 是即将被发送的自定义请求头
    headers: {'X-Requested-With': 'XMLHttpRequest'},
  
    // `params` 是即将与请求一起发送的 URL 参数
    // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
    params: {
      ID: 12345
    },
  
     // `paramsSerializer` 是一个负责 `params` 序列化的函数
    // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
    paramsSerializer: function(params) {
      return Qs.stringify(params, {arrayFormat: 'brackets'})
    },
  
    // `data` 是作为请求主体被发送的数据
    // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
    // 在没有设置 `transformRequest` 时，必须是以下类型之一：
    // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
    // - 浏览器专属：FormData, File, Blob
    // - Node 专属： Stream
    data: {
      firstName: 'Fred'
    },
  
    // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
    // 如果请求话费了超过 `timeout` 的时间，请求将被中断
    timeout: 1000,
  
     // `withCredentials` 表示跨域请求时是否需要使用凭证
    withCredentials: false, // default
  
    // `adapter` 允许自定义处理请求，以使测试更轻松
    // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
    adapter: function (config) {
      /* ... */
    },
  
   // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
    // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
    auth: {
      username: 'janedoe',
      password: 's00pers3cret'
    },
  
     // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
    responseType: 'json', // default
  
    // `responseEncoding` indicates encoding to use for decoding responses
    // Note: Ignored for `responseType` of 'stream' or client-side requests
    responseEncoding: 'utf8', // default
  
     // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
    xsrfCookieName: 'XSRF-TOKEN', // default
  
    // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
    xsrfHeaderName: 'X-XSRF-TOKEN', // default
  
     // `onUploadProgress` 允许为上传处理进度事件
    onUploadProgress: function (progressEvent) {
      // Do whatever you want with the native progress event
    },
  
    // `onDownloadProgress` 允许为下载处理进度事件
    onDownloadProgress: function (progressEvent) {
      // 对原生进度事件的处理
    },
  
     // `maxContentLength` 定义允许的响应内容的最大尺寸
    maxContentLength: 2000,
  
    // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
    validateStatus: function (status) {
      return status >= 200 && status < 300; // default
    },
  
    // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
    // 如果设置为0，将不会 follow 任何重定向
    maxRedirects: 5, // default
  
    // `socketPath` defines a UNIX Socket to be used in node.js.
    // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
    // Only either `socketPath` or `proxy` can be specified.
    // If both are specified, `socketPath` is used.
    socketPath: null, // default
  
    // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
    // `keepAlive` 默认没有启用
    httpAgent: new http.Agent({ keepAlive: true }),
    httpsAgent: new https.Agent({ keepAlive: true }),
  
    // 'proxy' 定义代理服务器的主机名称和端口
    // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
    // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
    proxy: {
      host: '127.0.0.1',
      port: 9000,
      auth: {
        username: 'mikeymike',
        password: 'rapunz3l'
      }
    },
  
    // `cancelToken` 指定用于取消请求的 cancel token
    // （查看后面的 Cancellation 这节了解更多）
    cancelToken: new CancelToken(function (cancel) {
    })
  }
  ```

  

## 黑马头条PC--接口访问-axios拦截器-统一处理响应数据

**`思路-步骤`** 

- 响应拦截  =>数据响应回来   **`到达then之前(响应拦截)`**=> then

 在axios 请求的响应数据 **`then`**执行之前也可以拦截 响应拦截器

return response =>  response =>  then(result)

处理返回响应数据 => resutlt.data.data =>  result.data

```js
axios.interceptors.response.use(function (response) {
    // 对响应数据做处理
    return response;
  }, function (error) {
    // 对响应错误做处理
    return Promise.reject(error);
  });
```

```js
// 响应拦截 响应数据 回来 到达then方法之前
axios.interceptors.response.use(function (response) {
  // 对响应数据做处理 执行成功时进入
  return response.data ? response.data : {}
}, function () {
  // 执行失败时执行
})
```



## 黑马头条PC--接口访问-axios拦截器-统一处理异常数据

**`思路-步骤`**

- 只有状态码 OK时 才会进入then=>状态码 200/201  否则 catch

- axios => then(成功),catch(失败)

- 统一处理失败 => 拦截器里统一处理失败 => 响应拦截器 => 响应拦截器中有状态码

- ```js
  // 响应拦截 响应数据 回来 到达then方法之前
  axios.interceptors.response.use(function (response) {
    // 对响应数据做处理 执行成功时进入
    return response.data ? response.data : {}
  }, function (error) {
    // 执行失败时执行
    let status = error.response.status // 获取失败的状态码
    let message = '未知错误'
    switch (status) {
      case 400:
        message = '请求参数错误'
        break
      case 403:
        message = '403 refresh_token未携带或已过期'
        break
      case 507:
        message = '服务器数据库异常'
        break
      case 401:
        message = 'token过期或未出'
        window.localStorage.clear() // 清空缓存
        router.push('/login') // this.$router.push()
        break
      case 404:
        message = '手机号不正确'
        break
      default:
        break
    }
    Message({ message })
    //   希望 在异常处理函数中将所有的错误都处理完毕 不再进入catch  终止错误
    return new Promise(function () {}) // 终止当前的错误
  })
  ```

  ## 黑马头条PC-主页模块-导航守卫

  **`思路-步骤`**

  - **`next()`** =>表示 resolve => 表示放过当前的请求

  - **`next(false)`**: 中断当前的导航

  - **`next(地址)`** 拦截即将要去的地方 转到另外一个地址

  - router.beforeEach  => 全局前置守卫 => 在每一个路由发生改变之前 会触发这个事件

    ```js
    router.beforeEach(function(to,from,next){})
    ```

    login => home

    this.$route.path

    **to: Route**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)

    **from: Route**: 当前导航正要离开的路由

    **next: Function**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。

    ```js
    new Promise(function(resolve,reject){   }).then
    ```

    - next函数必须执行 =>不执行 就会死在跳转的位置
    - 如果直接执行next() => 表示一切正常 login => home 可以正常走   类似 callback()
    - **next(false)** => 中断当前的导航 =>  login => home 不能正常走  停在login
    - **next(地址)** => 强制将login=>home =>另一个地址 

    ```js
    // 处理路由拦截器 导航守卫
    import router from '../router'
    
    // 全局前置守卫  当 路由发生变化时 这个方法里的回调函数就会执行
    router.beforeEach(function (to, from, next) {
      // 权限拦截 认为有token 让过去 没token不让过
      if (to.path.startsWith('/home')) {
        //   确定要去检查的范围
        let token = window.localStorage.getItem('user-token')
        if (token) {
          next() // 放过
        } else {
          next('/login') // 跳转到登录页
        }
      } else {
        next() // 直接放过
      }
    })
    
    ```

    

  - 

  ## 黑马头条PC-面包屑组件封装

  **`思路-步骤`**

  - ![image-20191221165126872](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1221/%E7%AC%94%E8%AE%B0/assets/image-20191221165126872.png)

    ```html
    <el-breadcrumb separator=">">
      <el-breadcrumb-item to="/home">首页</el-breadcrumb-item>
      <el-breadcrumb-item>
          <!-- 定义一个具名插槽 -->
          <slot name='title'></slot>
      </el-breadcrumb-item>
     </el-breadcrumb>
    ```

  

  ## 黑马头条PC-评论列表-新建页面-挂载路由

  **`思路-步骤`**

  - 二级路由组件 评论管理 => 路由级组件

  - 挂载到路由表上

  - ```json
    {
         path: 'comment', // 完整 相对
         component: () => import('../views/comment')
       }
    ```

    

  ## 黑马头条PC-评论列表-页面结构-table

  **`思路-步骤`**

  - 完成整个页面的结构和布局

  - 回顾插槽

  - ```html
    <div>hello world <slot name="title"></slot></div>  => child
    ```

  - ```html
    <child>
        张三
    </child>
    ```

  - ```html
    <child>
        <p slot="title">1</p>
        <p slot="title">2</p>
        <p slot="title">3</p>
    </child>
    ```

  - ```html
    <!-- 卡片组件 -->
    <el-card>
        <bread-crumb slot="header">
          <!-- 插槽内容 -->
           <template slot="title">
               评论管理
           </template>
        </bread-crumb>
        <!-- el-table -->
        <!-- 表格 -->
        <el-table>
            <!-- 放置列组件 -->
            <el-table-column width="600" label="标题"></el-table-column>
            <el-table-column label="评论状态"></el-table-column>
            <el-table-column label="总评论数"></el-table-column>
            <el-table-column label="粉丝评论数"></el-table-column>
            <el-table-column label="操作"></el-table-column>
      
        </el-table>
    </el-card>
    ```

  - 

  ## 黑马头条PC-评论列表-评论数据加载到页面及状态过滤

  **`步骤-思路`**  

  - 接口  => 有!
  - 工具 => axios
  - el-table  => 不显示布尔值

  ```html
  <div>
    <slot row="张三" column="" $index  store></slot>  => el-table-column
  </div>
  ```

  ```html
  <el-table-column>
      <template slot-scope="obj">{{ obj.row }}</template>
  </el-table-column>
  ```

  el-table-column => formatter => 格式化数据

  el-table-column => 作用域插槽

  ## 黑马头条PC-评论列表-打开和关闭评论

  - 接口
  - 工具

  ```js
        this.$confirm(`您是否确定要${mess}评论吗`, '提示').then(() => {
          // 调用接口
          this.$axios({
            method: 'put',
            url: '/comments/status',
            params: { article_id: row.id },
            data: { allow_comment: !row.comment_status } // 因为当前如果是打开 ,就要关闭 如果是关闭 就要打开
          }).then(result => {
            //  表示执行成功
            this.getComment() // 重新拉取评论管理数据
          })
        })
  ```

  ## 黑马头条PC-统一处理大数字类型

  **`步骤-思路`**

  [js数据精度](https://juejin.im/post/5af3f84bf265da0b7c074be6)

  - 在JavaScript处理整数的时候会遇到某些特别奇怪的问题,比如后台给你返回了一个超长的数字,然后js在计算的时候突然发现计算不对,不是后面为0就是计算得不到想要的结果.这里涉及到一个很简单的知识 也就是NUMBER的安全整数.

  - javascript => 计算数字的时候 =>安全范围 => 如果超过了一定的数字大小 => 计算就会失真=>就会不正确

  - 安全范围=> 最大安全整数 => 最大安全数字=> 如果超过了最大安全数字  => 计算就会有问题

  - ```js
    Number.MAX_SAFE_INTEGER // 9007199254740991
    9007199254740991+2 // 9007199254740992
    ```

  - 后端 => 前端 => 字符串 =>对象 => JSON.parse() => 如果超出了最大安全数字 => 计算偏差 =>JSON.parse不精确(一旦超过最大安全整数)  =>  axios 自动调用的  => 转化方法 =>json.parse()

  - json.parse =>处理大数字的时候 => 计算偏差  => 找出替代方案 => 第三方的转化包 => 保证数字的不丢,计算正常

  - js的数字有  最大安全数值

    - 2的53次方

    - Number.MAX_SAFE_INTEGER

    - 在运算 或 json对象转换的时候会有误差

    - 运算的时候：![1566433920292](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1222/%E7%AC%94%E8%AE%B0/assets/1566433920292.png)

      

    - json对象转换的时候：

      ![1566433999504](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1222/%E7%AC%94%E8%AE%B0/assets/1566433999504.png)

  - json-bigint  npm的包

    - 看文档 
    - **`npm i json-bigint`**
    - import JSONBig from 'json-bigint'
    - JSONBig .parse('json数据')

  - 在哪里使用：

    - 原来 是axios默认转换的数据  **`JSON.parse`**()
    - 现在 使用自定义的方式来转换数据

  ```js
   // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
    transformResponse: [function (data) {
      // 对 data 进行任意转换处理
  
      return data;
    }],
  ```

  **`结论`**后端传会的id数字超过了前端的**`最大安全数字`**的限制,导致JSON.parse以及其他运算失败.需要第三方的转化包,

  **`json-bigint`**, => 调用接口  => OK

  ```js
  axios.defaults.transformResponse = [function (data) {
  // data 是响应回来的字符串
    return jsonBigInt.parse(data)
  }]
  ```

  JSON.parse  => JSONbig.parse()

  ## 黑马头条PC-评论列表-列表分页及请求

  **`步骤-思路`**

  放置一个分页组件

  ```html
   <el-row type='flex' justify="center" align="middle" style="height:80px">
        <!-- 分页组件 total 总页码  每页多少条-->
        <el-pagination background layout="prev, pager, next"
         :current-page="page.currentPage"
         :page-size="page.pageSize"
         :total="page.total"
         @current-change="changePage"
         ></el-pagination>
      </el-row>
  ```

  - total  => 总条数 

  - page-size => 每页多少条

  - current-page => 当前页码

  - @current-change => 当前页码改变触发的事件 => 将最新页码 赋值给当前页码 => 请求数据

  - ```js
        // 页码改变事件
        changePage (newPage) {
          this.page.currentPage = newPage // 最新的页码
          this.getComment()
        },
    ```

  ## 黑马头条PC-评论列表-加载状态

  **`步骤-思路`** 

  - v-loading ="变量"

  - 通过变量 布尔值  => 进度条打开还是关闭

  - ```js
        getComment () {
          this.loading = true // 打开进度条
          this.$axios({
            url: '/articles',
            params: { response_type: 'comment', page: this.page.currentPage, per_page: this.page.pageSize }
          }).then(result => {
            this.list = result.data.results
            this.page.total = result.data.total_count // 总条数
            this.loading = false
            // setTimeout(() => { this.loading = false }, 300) // 关闭
          })
        },
    ```

  - 

  ## 黑马头条PC-素材列表-新建页面-挂载路由

  **`步骤-思路`**

  ```html
  <template>
    <el-card>
        <!-- 头部内容 -->
        <bread-crumb slot="header">
          <template slot="title">
             素材管理
          </template>
        </bread-crumb>
    </el-card>
  </template>
  
  <script>
  export default {
  
  }
  </script>
  
  <style>
  
  </style>
  
  ```

  

  ## 黑马头条PC-素材列表-页面结构-tab

  **`步骤-思路`**

  ```html
        <el-tabs v-model="activeName">
            <!-- 标签 -->
            <el-tab-pane label="全部图片" name="all">全部</el-tab-pane>
            <el-tab-pane label="收藏图片" name="collect">收藏</el-tab-pane>
        </el-tabs>
  ```

  

  ## 黑马头条PC-素材列表-数据加载

  **`步骤-思路`**

  - 收藏 和全部 要公用一个list数据

  - 由于当前只能看到一个页签 ,所以当点击页签时 ,就去加载点击页签的数据,就可以保证数据的正确

  - ```js
    export default {
      data () {
        return {
          activeName: 'all', // 当前选中的标签
          list: [] // 接收素材数据
        }
      },
      methods: {
        // 切换页签方法
        changeTab () {
          this.getMaterial() // 调用获取数据方法
        },
        // 获取素材的方法
        getMaterial () {
          this.$axios({
            url: '/user/images',
            params: {
              collect: this.activeName === 'collect' // 传false是获取所有的数据 传true是获取收藏数据
            }
          }).then(result => {
            this.list = result.data.results // 获取图片数据 有可能是 全部 也由可能是收藏
          })
        }
      },
      created () {
        this.getMaterial()
      }
    }
    ```

    

  ## 黑马头条PC-素材列表-分页组件及请求

  **`步骤-思路`**

  - 收藏 =>  全部 公用了一个list

  - 切换tab页  =>  根据tab页name去查询对应的分类数据 =>  total_count(总数)

  - ```html
    <!-- 公共分页组件 -->
            <el-row type="flex" justify="center">
               <el-pagination
                   :current-page="page.currentPage"
                   :page-size="page.pageSize"
                   :total="page.total"
                   @current-change="changePage"
                   background
                   layout="prev, pager, next"
                  >
               </el-pagination>
             </el-row>
    ```

  - ```js
    export default {
      data () {
        return {
          activeName: 'all', // 当前选中的标签
          list: [], // 接收素材数据
          page: {
            currentPage: 1,
            pageSize: 8,
            total: 0
          }
        }
      },
      methods: {
        // 改变页码方法
        changePage (newPage) {
          this.page.currentPage = newPage
          this.getMaterial()
        },
        // 切换页签方法
        changeTab () {
          this.page.currentPage = 1 // 重置回第一页
          this.getMaterial() // 调用获取数据方法
        },
        // 获取素材的方法
        getMaterial () {
          this.$axios({
            url: '/user/images',
            params: {
              page: this.page.currentPage,
              per_page: this.page.pageSize,
              collect: this.activeName === 'collect' // 传false是获取所有的数据 传true是获取收藏数据
            }
          }).then(result => {
            this.list = result.data.results // 获取图片数据 有可能是 全部 也由可能是收藏
            this.page.total = result.data.total_count // 总条数
          })
        }
      },
      created () {
        this.getMaterial()
      }
    }
    ```

  - 全部 /收藏 共用了list,共用了分页组件

  - 切换页签 => 将页码重置到了第一页

  - 切换页码 =>  将最新页码 赋值给了当前页

  ## 黑马头条PC-素材列表-素材的上传

  **`步骤-思路`**

  - 上传接口 => 接口 formdata类型

  - 上传组件 => elementUI => upload

  - ```js
    // 上传图片方法
        uploadImg (params) {
          this.loading = true // 先弹个层
          let data = new FormData()
          data.append('image', params.file) // 文件加入到参数中
          this.$axios({
            method: 'post',
            url: '/user/images',
            data
          }).then(result => {
            this.loading = false // 关闭弹层
            this.getMaterial() // 直接调用拉取数据的方法
          })
        },
    ```

    

  ## 黑马头条PC-素材列表-素材的收藏和删除

  **`步骤-思路`**

  ```js
     // 取消或者收藏
      collectOrCancel (item) {
        // item.iscollected true => 取消收藏 ? 收藏
        this.$axios({
          method: 'put',
          url: `/user/images/${item.id}`,
          data: {
            collect: !item.is_collected // 取反 因为 收藏  =>取消收藏
          }
        }).then(result => {
          this.getMaterial() // 重新拉取数据
        })
      },
  ```

  ```js
   // 删除用户图片素材
      delMaterial (id) {
        this.$confirm('你确定要删除此图片吗?').then(() => {
          this.$axios({
            method: 'delete',
            url: `/user/images/${id}`
          }).then(() => {
            this.getMaterial() // 重新拉取数据
          })
        })
      },
  ```

  ## 总结

  - 评论管理

  - - 打开/关闭评论  => js  处理大数字 => 第三方包 json-bigint
    - 分页
    - 放置一个分页组件  
    - total 
    - page-size 
    - current-page 
    - @current-change => 获取最新页码 给当前页赋值 => 请求最新页码数据

  - 素材管理

  - 全部素材 

  - 全部素材  / 收藏素材  一个接口 => tab页切换 => activeName === 'all'  'collect'

  - 全部素材 / 收藏素材   共用一份数据 => 因为当前用户只能看到一份数据

  - 共用一个分页组件 => 获取接口里 返回的总条数 是变化的

  - 素材的上传和收藏/删除 => 成功  =>  重新拉取数据

  - ## 复习

    - 搭建vue-cli4.0 项目 
    - 登录页 =>  表单校验 => 登录验证 => 存储token =>主页 (导航守卫解决没有token的人不进入主页)
    - 主页 => 左侧 /头部 =>主页二级默认组件 => axios拦截器 
    - axios请求拦截器  => 可以改变请求配置信息 => 配置信息中注入token
    - axios 响应拦截器  => 成功 => 进行了数据的解构 => result.data.data => result.data
    - axios 响应拦截器  => 失败 => 处理各种错误 =>  return Promise.reject(error) => catch
    - 评论管理 => 加载数据  => 加载到页面 => 表格 => el-table =>el-table-column
    - 素材管理 => 加载数据 => 全部素材 / 收藏素材 => 一个接口 => el-tabs => 当前选中的tab页 => activeName 
    - activeName => all =>全部素材  
    - activeName => collect =>收藏素材
    - 分页 => 放置一个分页组件 =>el-pagination 
    - el-pagination  => total  => 总页数 current-page => 当前页码  page-size => 每页多少条数据
    - @current-change => 页码改变事件 => 请求新的数据

    ## 黑马头条PC-内容列表-新建页面-挂载路由

    **`思路-步骤`**

    - 新建一个路由级组件 
    - 挂载到二级路由上 => 按需加载

    ## 黑马头条PC-内容列表-页面结构-搜索工具栏

    **`思路-步骤`**

    - 表单容器 => model   rules => el-form => 这些属性是校验时必须写的,一般的绑定不需要写

    - ```html
      <el-form style="padding-left:50px">
              <el-form-item label="文章状态:">
                  <!-- 放置一个单选组  文章状态，0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除，不传为全部-->
                  <el-radio-group v-model="searchForm.status">
                      <!-- label -->
                      <el-radio :label="5">全部</el-radio>
                      <el-radio :label="0">草稿</el-radio>
                      <el-radio :label="1">待审核</el-radio>
                      <el-radio :label="2">审核通过</el-radio>
                      <el-radio :label="3">审核失败</el-radio>
                  </el-radio-group>
              </el-form-item>
              <el-form-item label="频道列表:">
                  <el-select placeholder="请选择频道" v-model="searchForm.channel_id">
                      <!-- el-option label是显示值 value是存储值 -->
                      <el-option v-for="item in channels" :key="item.id" :label="item.name" :value="item.id"></el-option>
                  </el-select>
              </el-form-item>
              <el-form-item label="时间选择:">
                  <!-- 日期选择器 日期范围-->
                  <el-date-picker v-model="searchForm.dateRange" type="daterange"></el-date-picker>
              </el-form-item>
          </el-form>
      ```

      

    ## 黑马头条PC-内容列表-页面主体结构

    **`思路-步骤`**

    - 手写的方式 实现页面的主题结构

    - ```html
      <el-card class='articles'>
            <bread-crumb slot='header'>
               <template slot='title'>文章列表</template>
            </bread-crumb>
            <!-- 表单容器 -->
            <el-form style="padding-left:50px">
                <el-form-item label="文章状态:">
                    <!-- 放置一个单选组  文章状态，0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除，不传为全部-->
                    <el-radio-group v-model="searchForm.status">
                        <!-- label -->
                        <el-radio :label="5">全部</el-radio>
                        <el-radio :label="0">草稿</el-radio>
                        <el-radio :label="1">待审核</el-radio>
                        <el-radio :label="2">审核通过</el-radio>
                        <el-radio :label="3">审核失败</el-radio>
                    </el-radio-group>
                </el-form-item>
                <el-form-item label="频道列表:">
                    <el-select placeholder="请选择频道" v-model="searchForm.channel_id">
                        <!-- el-option label是显示值 value是存储值 -->
                        <el-option v-for="item in channels" :key="item.id" :label="item.name" :value="item.id"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="时间选择:">
                    <!-- 日期选择器 日期范围-->
                    <el-date-picker v-model="searchForm.dateRange" type="daterange"></el-date-picker>
                </el-form-item>
            </el-form>
            <el-row class='total' type='flex' align="middle">
                <span>
                    共找到10000条符合条件的内容
                </span>
            </el-row>
            <div class='article-item' v-for="item in 100" :key="item">
                <!-- 左侧 -->
                <div class='left'>
                    <img src="../../assets/img/default.jpg" alt="">
                    <div class='info'>
                        <span>90期的弟弟们，哈哈哈啊哈哈哈嗝</span>
                        <el-tag class='tag'>标签一</el-tag>
                        <span class='date'>2019-12-24 15:07:01</span>
                    </div>
                </div>
                <!-- 右侧 -->
                <div class='right'>
                    <span><i class="el-icon-edit"></i>修改</span>
                    <span><i class="el-icon-delete"></i>删除</span>
                </div>
            </div>
        </el-card>
      ```

      

    ## 黑马头条PC-内容列表-请求数据

    **`思路-步骤`**

    - 调用接口 =>先不做筛选,不做分页

    - 过滤器 不但可以用在插值表达式 

    - 还可以用在 v-bind表达式

    - ```html
          <div class='article-item' v-for="item in list" :key="item.id.toString()">
              <!-- 左侧 -->
              <div class='left'>
                  <img :src="item.cover.images.length ? item.cover.images[0] : defaultImg" alt="">
                  <div class='info'>
                      <span>{{ item.title }}</span>
                      <!-- 文章状态 0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除 -->
                      <el-tag :type="item.status | filterType" class='tag'>{{ item.status | filterStatus }}</el-tag>
                      <span class='date'>{{ item.pubdate }}</span>
                  </div>
              </div>
              <!-- 右侧 -->
              <div class='right'>
                  <span><i class="el-icon-edit"></i>修改</span>
                  <span><i class="el-icon-delete"></i>删除</span>
              </div>
          </div>
      ```

    - ```js
          getArticles () {
            this.$axios({
              url: '/articles'
            }).then(result => {
              this.list = result.data.results // 获取文章列表数据
            })
          }
      ```

    - 

    ## 黑马头条PC-内容列表-页面结构-搜索筛选

    **`思路-步骤`**

    - 条件 => 组合条件 => 不论谁的数据发生变化 =>先组装条件  => 统一发送请求

    - 第一种做法=>监听每个组件的change事件

    - ```js
      changeCondition () {
         let params = {
           status: this.searchForm.status === 5 ? null : this.searchForm.status, // 因为5是前端定义的一个标识, 如果等于5 表示查全部, 全部应该什么都不传 直接传null
           channel_id: this.searchForm.channel_id,
           begin_pubdate: this.searchForm.dateRange.length ? this.searchForm.dateRange[0] : null, // 开始时间
           end_pubdate: this.searchForm.dateRange.length > 1 ? this.searchForm.dateRange[1] : null // 截止时间
         }
         this.getArticles(params)
       }
      ```

    - 第二种做法 => watch 去监听数据变化

    - ```js
      watch: {
          name: function(newValue,oldValue){
              
          }
      }
      // 传统模式  a: { b:{c:'123'} }
      watch:{
         "a.b.c":function(){}
      }
      watch: {
          a:{
              handler:function(){
                  // this指向当前实例
              } // handler是一个固定写法 默认对象中任何的变化都会触发该函数
              deep: true // deep 深度检测 不论嵌套多少层 都可以监听到改变
          }
      }
      ```

    - 

    ## 黑马头条PC-内容列表-分页请求

    **`思路-步骤`**

    ```js
        //   改变页码方法
        changePage (newPage) {
          this.page.currentPage = newPage // 最新页码
          this.getConditionArticle() // 调用获取文章数据
        },
        //   改变条件
        changeCondition () {
          this.page.currentPage = 1 // 强制将页码重置第一页
          this.getConditionArticle() // 调用获取文章数据
        },
        getConditionArticle () {
          let params = {
            page: this.page.currentPage,
            per_page: this.page.pageSize,
            status: this.searchForm.status === 5 ? null : this.searchForm.status, // 因为5是前端定义的一个标识, 如果等于5 表示查全部, 全部应该什么都不传 直接传null
            channel_id: this.searchForm.channel_id,
            begin_pubdate: this.searchForm.dateRange.length ? this.searchForm.dateRange[0] : null, // 开始时间
            end_pubdate: this.searchForm.dateRange.length > 1 ? this.searchForm.dateRange[1] : null // 截止时间
          }
          this.getArticles(params)
        }
    ```

    - 页码改变时 => 设置最新页码 => 收集原来的条件参数 => 组合 =>查询
    - 条件改变时 => 强制页码到第一页 => 收集参数  =>组合 =>查询

    ## 黑马头条PC-内容列表-页面结构-删除内容

    **`思路-步骤`**

    - 删除内容 => 只能删除 草稿 => 不能删除 已发表的

    - 注册删除的事件

    - ```js
          delMaterial (id) {
            this.$confirm('是否要删除该文章?').then(() => {
              // 调用删除接口
              this.$axios({
                method: 'delete',
                url: `/articles/${id.toString()}`
              }).then(result => {
                // 提示
                this.$message({
                  type: 'success',
                  message: '删除成功'
                })
                // 重新拉取数据
                // this.page.currentPage = 1 // 根据业务 处理 如果删除了数据 是否回到第一页根据具体业务而定
                this.getConditionArticle()
              })
            })
          }
      ```

    - 

    ## 黑马头条PC-发表文章-新建页面-挂载路由

    **`思路-步骤`**

    - 路由级组件
    - 挂载二级路由  => 按需加载

    ## 黑马头条PC-发表文章-页面结构-简单实现

    **`思路-步骤`**

    ```html
    <el-card>
          <bread-crumb slot='header'>
            <template slot='title'>
                发布文章
            </template>
          </bread-crumb>
          <!-- 容器 -->
          <el-form style="margin-left:50px" label-width="100px">
              <el-form-item label="标题">
                  <el-input style="width:60%"></el-input>
              </el-form-item>
              <el-form-item label="内容">
                     <el-input
                     type="textarea"
                    :rows="4"></el-input>
              </el-form-item>
              <el-form-item label="封面">
                  <el-radio-group>
                      <el-radio>单图</el-radio>
                      <el-radio>三图</el-radio>
                      <el-radio>无图</el-radio>
                      <el-radio>自动</el-radio>
                  </el-radio-group>
              </el-form-item>
              <el-form-item label="频道">
                  <el-select></el-select>
              </el-form-item>
              <el-form-item>
                  <el-button type='primary'>发布</el-button>
                  <el-button>存入草稿</el-button>
    
              </el-form-item>
          </el-form>
      </el-card>
    ```

    

    ## 黑马头条PC-发表文章-频道数据加载

    **`思路-步骤`**

    - 定义channels

    - 获取数据给channels

    - v-for循环生成el-option

    - ```html
          <el-select>
                        <el-option v-for="item in channels" :value="item.id" :label="item.name" :key="item.id"></el-option>
                    </el-select>
      ```

    - ```js
      export default {
        data () {
          return {
            channels: [] // 接收频道数据
          }
        },
        methods: {
          //   获取所有的频道
          getChannels () {
            this.$axios({
              url: '/channels'
            }).then(result => {
              this.channels = result.data.channels
            })
          }
        },
        created () {
          this.getChannels()
        }
      }
      ```

    - 

    ## 黑马头条PC-发表文章-发布文章校验逻辑实现

    **`思路-步骤`**

    - 表单 el-form => **`model`**(表单数据对象)  rules(校验规则对象)

    - el-form-item => prop => 要校验的字段

    - el-input =>v-model双向绑定

    - 手动校验 => 获取el-form 组件的实例 => validate => function(isOK,fields){}

    - 标题  =>长度在5-30字符之间

    - min => 字符串 如果校验的值是字符串,min指的是字符串的最短长度

    - min =>数字 如果校验的值是数字,min指的是数字的最小值

    - max=> 字符串 如果校验的值是字符串,min指的是字符串的最大长度

    - max=>数字 如果校验的值是数字,min指的是数字的最大值

    - ```js
      data () {
        return {
          channels: [], // 接收频道数据
          formData: {
            title: '', // 文章标题
            content: '', // 文章内容
            cover: {
              type: 0, // 封面类型 -1:自动，0-无图，1-1张，3-3张
              images: [] // 放置封面地址的数组
            },
            channel_id: null // 频道id
          },
          publishRules: {
            //   校验规则 title/content/channel_id 必填项
            title: [{ required: true, message: '文章标题不能为空' }, {
              min: 5,
              max: 30,
              message: '标题的长度在5到30个字符之间'
            }],
            content: [{ required: true, message: '文章内容不能为空' }],
            channel_id: [{ required: true, message: '文章频道不能为空' }]
          }
        }
      ```

    - ```js
          // 发布文章
          publishArticle () {
            this.$refs.publishForm.validate(isOK => {
              if (isOK) {
                console.log('校验通过')
              }
            })
          }
      ```

    - ```html
      <el-form ref="publishForm" :model="formData" :rules="publishRules" style="margin-left:50px" label-width="100px">
              <el-form-item prop="title" label="标题">
                  <el-input v-model="formData.title" style="width:60%"></el-input>
              </el-form-item>
              <el-form-item prop="content" label="内容">
                    <el-input
                    v-model="formData.content"
                     type="textarea"
                    :rows="4"></el-input>
              </el-form-item>
              <el-form-item  prop="cover" label="封面">
                  <el-radio-group v-model="formData.cover.type">
                      <!-- // 封面类型 -1:自动，0-无图，1-1张，3-3张 -->
                      <el-radio :label="1">单图</el-radio>
                      <el-radio :label="3">三图</el-radio>
                      <el-radio :label="0">无图</el-radio>
                      <el-radio :label="-1">自动</el-radio>
                  </el-radio-group>
              </el-form-item>
              <el-form-item prop="channel_id" label="频道">
                  <el-select v-model="formData.channel_id">
                      <el-option v-for="item in channels" :value="item.id" :label="item.name" :key="item.id"></el-option>
                  </el-select>
              </el-form-item>
              <el-form-item>
                  <el-button @click="publishArticle" type='primary'>发布</el-button>
                  <el-button @click="publishArticle">存入草稿</el-button>
        
              </el-form-item>
          </el-form>
      ```

    - 

    ## 黑马头条PC-发表文章-发布文章-简单发布文章

    **`思路-步骤`**

    - 先不做 封面,也不做富文本编辑器

    - @事件名="方法名"  @事件名="方法名()"

    - 鲁棒性测试

    - ```js
          // 发布文章 发布到草稿 /正式文章
          publishArticle (draft) {
            this.$refs.publishForm.validate(isOK => {
              if (isOK) {
                // 调用发布接口
                this.$axios({
                  url: '/articles',
                  method: 'post',
                  params: { draft }, // 查询参数
                  data: this.formData // 请求体参数
                }).then(() => {
                  this.$message({
                    type: 'success',
                    message: '保存成功'
                  })
                  // 跳转到文章列表页
                  this.$router.push('/home/articles')
                })
              }
            })
          }
      ```

    - 

    ## 黑马头条PC-发表文章-修改文章-简单模式跳转

    **`思路-步骤`**

    - 点击修改 => 发布文章

    - 动态路由 => 定义路由参数 => 路由规则地址 =>  /publish/:参数名

    - 传入参数

    - 取参数 =>$route.params.参数名

    - 当两个不同的路由的地址 对应同一个组件的时候,如果相互切换,组件实例并不会销毁,也就是不会执行钩子函数的一系列操作

    - ```js
      watch: {
        // 处理 两个地址对应同一个组件跳转的时候 组件不销毁 但是数据没有重置的问题
        $route: function (to, from) {
          if (to.params.articleId) {
            // 是修改
          } else {
            // 是发布
            this.formData = {
              title: '', // 文章标题
              content: '', // 文章内容
              cover: {
                type: 0, // 封面类型 -1:自动，0-无图，1-1张，3-3张
                images: [] // 放置封面地址的数组
              },
              channel_id: null // 频道id
            }
          }
        }
      }
      ```

    - ```js
          // 通过id查询文章数据
          getArticleById (articleId) {
            this.$axios({
              url: `/articles/${articleId}`
            }).then(result => {
              this.formData = result.data // 将数据赋值data
            })
          }
      ```

    - 

    ## 黑马头条PC-发表文章-修改文章-提交数据修改

    **`思路-步骤`**

    - **`leetcode`**

    - ```js
          publishArticle (draft) {
            this.$refs.publishForm.validate(isOK => {
              if (isOK) {
                // 判断是修改还是发布文章
                let { articleId } = this.$route.params // 获取动态路由参数
                this.$axios({
                  url: articleId ? `/articles/${articleId}` : '/articles',
                  method: articleId ? 'put' : 'post',
                  params: { draft }, // 查询参数
                  data: this.formData // 请求体参数
                }).then(result => {
                  this.$message({
                    type: 'success',
                    message: '保存成功'
                  })
                  // 跳转到文章列表页
                  this.$router.push('/home/articles')
                })
                // if (articleId) {
                //   // 修改文章接口
                //   this.$axios({
                //     url: `/articles/${articleId}`,
                //     params: { draft }, // 查询参数
                //     data: this.formData // 请求体参数
                //   }).then(result => {
                //     this.$message({
                //       type: 'success',
                //       message: '保存成功'
                //     })
                //     // 跳转到文章列表页
                //     this.$router.push('/home/articles')
                //   })
                // } else {
                //   // 调用发布接口
                //   this.$axios({
                //     url: '/articles',
                //     method: 'post',
                //     params: { draft }, // 查询参数
                //     data: this.formData // 请求体参数
                //   }).then(() => {
                //     this.$message({
                //       type: 'success',
                //       message: '保存成功'
                //     })
                //     // 跳转到文章列表页
                //     this.$router.push('/home/articles')
                //   })
                // }
              }
            })
          }
      ```

    - 

    ## 黑马头条PC-发布文章-注册富文本编辑器并使用

    **`思路-步骤`**

    [quill编辑器](https://www.jianshu.com/p/8e6eeefcc588)

    - 安装富文本编辑器

    - ```bash
      $ npm i vue-quill-editor -S # 运行时依赖
      ```

    - ![image-20191225170252095](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1225/%E7%AC%94%E8%AE%B0/assets/image-20191225170252095.png)

    - 使用quill-editor => 直接替代 el-input即可,支持v-model指令

    ## 黑马头条PC-发布文章-封面功能设计

    **`思路-步骤`**

    - el-radio-group => 绑定formData.cover.type => 变化 => 改变formData.cover.images

    - type => 0或者 -1 => images => []

    - type =>1=> images => ['']

    - type =>3=> images => ['','','']

    - 第一种做法 => el-radio-group => change => 监听type的变化

    - 第二种方法 => watch => 

    - ```js
      a:{
          b: {
              c:'name'
          }
      }
      watch:{
          "a.b.c":function(){},
             "a":{
                 deep:true,
                     handler:function(){
                         
                     }
             } 
      }
      ```

    - ```js
      // 监听 封面类型的改变
        'formData.cover.type': function () {
          if (this.formData.cover.type === 0 || this.formData.cover.type === -1) {
            this.formData.cover.images = [] // 无图或者自动
          } else if (this.formData.cover.type === 1) {
            this.formData.cover.images = [''] // 单图
          } else if (this.formData.cover.type === 3) {
            this.formData.cover.images = ['', '', ''] // 3图
          }
        }
      ```

    ## 黑马头条PC-发布文章-封面功能组件实现

    **`思路-步骤`**

    - 新建一个封面组件 **`cover-image`**

    - props传递父=> 子

    - 对images => 循环展示 

    - ![image-20191225180707882](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1225/%E7%AC%94%E8%AE%B0/assets/image-20191225180707882.png)

    - 还差 点击图片时 => 弹出层 => 嵌套组件 => 管理素材并且返回选择的图片地址 => 封面组件 => 

    - **`最难点`**!!!!! => 子传父 => 子传父

    - ```html
      <div class='cover-image'>
         <div @click="openDialog" v-for="(item,index) in list" :key="index" class='cover-image-item'>
           <img :src="item ? item : defaultImg" alt="">
         </div>
         <!-- 放置一个对话框 -->
         <el-dialog :visible="dialogVisible" @close="closeDialog" title="选择封面图片">
               <!-- 放置另外一个组件 素材库组件 和上传组件 -->
         </el-dialog>
       </div>
      ```

      ```js
      export default {
        props: ['list'],
        data () {
          return {
            defaultImg: require('../../assets/img/pic_bg.png'),
            dialogVisible: false // 用来控制弹层的开关
          }
        },
        methods: {
          openDialog () {
            this.dialogVisible = true // 打开弹层
          },
          closeDialog () {
            this.dialogVisible = false // 关闭弹层
          }
        }
      }
      ```

      ```css
       .cover-image {
           margin: 20px 100px;
           display: flex;
           .cover-image-item {
             border: 1px solid #ccc;
             width: 250px;
             height: 250px;
             padding: 20px;
             img {
               width: 100%;
               height: 100%;
             }
           }
         }
      ```

      

    ## 黑马头条PC-发布文章-封面图片选择组件封装及使用

    **`思路-步骤`**

    ## 黑马头条PC-发布文章-封面图片选择组件上传

    **`思路-步骤`**

    ## 总结

    - 发布 => 修改 => 公用一个组件  => 切换路由  => 组件实例并没有销毁 =>watch => 监听 $route => params.参数
    - 有参数 => 修改
    - 没参数 => 发布
    - watch => 监听了封面类型 => 一旦数据改变 =>就会触发
    - 获取文章详情 => 赋值给data =>  造成数据变化  => watch执行 => 一直都是空字符串  => 继续判断有没有图片地址
    - 用el-radio-group => change => 只会在点击的时候触发 => 可以解决这个问题
    - 封装了一个封面组件 => cover-image => 父 => 子
    - props => 1 定义属性 2 接收属性 3  this 或者 {{ props属性 }} 
    - 点击图片 => 弹层 => dialog => visible => 显示或者隐藏 => 关闭  => close =>手动关闭

    ## 黑马头条PC-发布文章-封面图片选择组件封装及使用

    **`思路-步骤`**

    - 点击图片 =>弹层 =>放置一个组件 => 组件 => tab页 => 素材 /上传

    - 新建一个组件

    - ```html
      <template>
        <div class='cover-image'>
          <div @click="openDialog(index)" v-for="(item,index) in list" :key="index" class='cover-image-item'>
            <img :src="item ? item : defaultImg" alt="">
          </div>
          <!-- 放置一个对话框 -->
          <el-dialog :visible="dialogVisible" @close="closeDialog" >
                <!-- 放置另外一个组件 素材库组件 和上传组件 -->
                <!-- 监听谁的事件就在谁的标签上写监听 -->
                 <select-image @selectOneImg="receiveImg"></select-image>
          </el-dialog>
        </div>
      </template>
      
      <script>
      export default {
        props: ['list'],
        data () {
          return {
            defaultImg: require('../../assets/img/pic_bg.png'),
            dialogVisible: false, // 用来控制弹层的开关
            selectIndex: -1 // 用来存储点击的哪个图片的下标
          }
        },
        methods: {
          // 接收方法
          receiveImg (url) {
            // props  只能读取 不能修改
            this.$emit('selectTwoImg', url, this.selectIndex) // 再次传递
            this.closeDialog() // 关闭弹层
          },
          openDialog (index) {
            this.dialogVisible = true // 打开弹层
            this.selectIndex = index // 记录当前点击的是哪个图片
          },
          closeDialog () {
            this.dialogVisible = false // 关闭弹层
          }
        }
      }
      </script>
      
      <style lang='less' scoped>
         .cover-image {
           margin: 20px 100px;
           display: flex;
           .cover-image-item {
             border: 1px solid #ccc;
             width: 250px;
             height: 250px;
             padding: 20px;
             img {
               width: 100%;
               height: 100%;
             }
           }
         }
      </style>
      
      ```

    - ```html
      <template>
        <el-tabs v-model="activeName">
          <el-tab-pane label="素材库" name="material">
            <!-- 外层容器 -->
            <div class="select-image-list">
              <!-- 循环生成多个el-card -->
              <el-card v-for="item in list" :key="item.id" class="img-card">
                  <!-- 给图片注册点击事件 -->
                <img @click="clickImg(item.url)" :src="item.url" alt />
              </el-card>
            </div>
            <!-- 放置一个分页组件 -->
            <el-row type="flex" justify="center">
              <el-pagination background layout="prev, pager, next"
               :total="page.total"
               :current-page="page.currentPage"
               :page-size="page.pageSize"
               @current-change="changePage"
               ></el-pagination>
            </el-row>
          </el-tab-pane>
          <el-tab-pane label="上传图片" name="upload">上传图片</el-tab-pane>
        </el-tabs>
      </template>
      
      <script>
      export default {
        data () {
          return {
            activeName: 'material', // 默认选中是素材库
            list: [], // 接收素材管理的数据
            page: {
              currentPage: 1, // 默认请求页码
              pageSize: 8,
              total: 0 // 总页码
            }
          }
        },
        methods: {
          //   点击图片时触发
          clickImg (url) {
            //  点击图片时  => 要把图片传给显示的封面 自定义事件
            this.$emit('selectOneImg', url) // 自定义事件名 可以不用全小写了
          },
          //   改变页码事件
          changePage (newPage) {
            this.page.currentPage = newPage
            this.getAllImg()
          },
          //   获取所有素材
          getAllImg () {
            this.$axios({
              url: '/user/images',
              params: { collect: false, page: this.page.currentPage, per_page: this.page.pageSize }
            }).then(result => {
              this.list = result.data.results
              this.page.total = result.data.total_count // 获取总数
            })
          }
        },
        created () {
          this.getAllImg()
        }
      }
      </script>
      
      <style lang='less' scoped>
      .select-image-list {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        .img-card {
          width: 150px;
          height: 150px;
          margin: 20px 0;
          img {
            width: 100%;
            height: 100%;
          }
        }
      }
      </style>
      
      ```

    - ```js
      receiveImg (url, index) {
           // 现在拿到的url地址 还要拿到下标
           // 但是要改的是数组
           // this.formData.cover.images[index] = url //  这种写法 错误!!!!! 不能保证每次都成功
           // 响应式数据 => 数据变化 => 视图变化
           // 数据变化 =>vuejs => 检测到了数据变化 =>vuejs 对于数组的检测变化 不能通过索引来处理
           // Vuejs会检测到 新数组 替换原数组 => 进行响应式更新
           // this.formData.cover.images = this.formData.cover.images.map(function (item, i) {
           //   if (index === i) {
           //     // 说明找到了要替换的地址
           //     return url
           //   }
           //   // 如果没找到 要直接返回原来的数据
           //   return item
           // })
           this.formData.cover.images = this.formData.cover.images.map((item, i) => i === index ? url : item)
         },
      ```

      ![image-20191227155207656](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1227/%E7%AC%94%E8%AE%B0/assets/image-20191227155207656.png)

    ## 黑马头条PC-发布文章-封面图片选择组件上传

    **`思路-步骤`** 

    - 上传组件 => el-upload

    - ```js
      uploadImg (params) {
          let data = new FormData()
          data.append('image', params.file) // 加入参数
          this.$axios({
            url: '/user/images',
            method: 'post',
            data
          }).then(result => {
            // result.data.url
            this.$emit('selectOneImg', result.data.url) // 自定义事件名 可以不用全小写了
          })
        },
      ```

    - ```html
      <el-upload action="" :http-request="uploadImg" class='upload-img' :show-file-list="false">
              <i class='el-icon-plus'></i>
            </el-upload>
      ```

    - ```css
      .upload-img {
        display: flex;
        justify-content: center;
        i {
          font-size:50px;
          padding: 50px;
          border:1px dashed #ccc;
          border-radius: 4px;
        }
      }
      ```

    ## 黑马头条PC-账户信息-新增页面-挂载路由

    **`思路-步骤`**

    ## 黑马头条PC-账户信息-页面结构

    **`思路-步骤`**

    - 表单 => el-form=> el-form-item

    - ```css
      .head-upload {
         position: absolute;
         right: 300px;
         top:200px;
          img {
             width: 200px;
             height: 200px;
              border-radius: 50%;
          }
      }
      ```

    - ```html
      <el-card>
            <bread-crumb slot="header">
              <template slot='title'>账户信息</template>
            </bread-crumb>
            <!-- 表单 => 表单容器 -->
            <el-form style="margin-left:100px" label-width="100px">
                <el-form-item label="用户名">
                    <el-input style="width:40%"></el-input>
                </el-form-item>
                 <el-form-item label="简介">
                     <el-input style="width:40%"></el-input>
                 </el-form-item>
                 <el-form-item label="邮箱">
                     <el-input style="width:40%"></el-input>
                 </el-form-item>
                 <el-form-item label="手机号">
                     <el-input disabled style="width:40%"></el-input>
                 </el-form-item>
                 <el-form-item>
                     <el-button type="primary">保存信息</el-button>
                 </el-form-item>
            </el-form>
            <!-- 上传组件 -->
            <el-upload class='head-upload' action="" :show-file-list="false">
                <img src="../../assets/img/cat.jpg" alt="">
            </el-upload>
        </el-card>
      ```

    - 

    ## 黑马头条PC-账户信息-数据加载给表单

    **`思路-步骤`**

    ```js
    export default {
      data () {
        return {
          formData: {
            name: '', // 用户名
            intro: '', // 简介
            photo: '', // 头像
            email: '', // 邮箱
            mobile: ''
          },
          defaultImg: require('../../assets/img/cat.jpg')
        }
      },
      methods: {
        //   获取用户个人信息
        getUserInfo () {
          this.$axios({
            url: '/user/profile'
          }).then(result => {
            this.formData = result.data
          })
        }
      },
      created () {
        this.getUserInfo()
      }
    
    }
    ```

    

    ## 黑马头条PC-账户信息-用户数据保存

    **`思路-步骤`**

    - 保存之前  => 校验

    - el-form =>  model =>rules

    - el-form-item => prop

    - el-input  => v-model

    - 表单校验方法 validate  => 支持回调用法 ,也支持promise用法 => 校验成功会进入到then ,否则进入到catch

    - ```js
      // suncaiGuanli  => 千万杜绝
        // baocunyonghuxinxi
        // 保存用户信息
        saveUserInfo () {
          this.$refs.myForm.validate().then(result => {
            //  调用保存接口
            this.$axios({
              url: '/user/profile',
              method: 'patch',
              data: this.formData
            }).then(result => {
              this.$message({
                type: 'success',
                message: '保存用户信息成功'
              })
            })
          })
        }
      ```

    - 

    ## 黑马头条PC-账户信息-头像上传更新

    **`思路-步骤`**

    ```js
      uploadImg (params) {
          this.loading = true // 打开弹层
          let data = new FormData()
          data.append('photo', params.file)
          this.$axios({
            url: '/user/photo',
            method: 'patch',
            data
          }).then(result => {
            this.loading = false // 关闭弹层
            this.formData.photo = result.data.photo // 给当前的头像赋值
          })
        }
    ```

    ## 黑马头条PC-账户信息更新-同步到头部页面之eventBus

    **`思路-步骤`**

    - eventBus => event事件 Bus =>公共领域  => 公共事件池 

    - this.$emit => this => 当前实例 => 当前实例触发的事件,只能在当前实例监听

    - 通信 => 连接线 => 一个实例 =>A 组件 如果在它自己的实例中触发一个事件  => B组件肯定监听不到!!!!

    - A组件 在一个**`公共的实例`**上去触发一个事件,B组件去这个**`公共的实例`**上监听

    - 公共的实例  =>eventBus => 做一个公共的实例

    - ```js
      // 公共实例
      import Vue from 'vue'
      export default new Vue() // 公共实例 => 实例化了一个Vue
      
      ```

    - 任何组件间的传值  => eventBus => 父 => 子  子 => 父  兄弟传值  非关系组件

    - this.$emit => eventBus.**`$emit`**(自定义事件,若干参数)

    - eventBus.**`$on`**(事件名, function(若干参数){})

    - ```js
          // 认为保存成功 => 通知header组件 更新信息
          eventBus.$emit('updateUserInfo')
      ```

    - ```js
          eventBus.$on('updateUserInfo', () => {
            // 认为别人更新了数据 自己也应该更新
            this.getUserInfo()
          })
      ```

      

    ## 黑马头条PC-扩展-在素材管理中添加轮播图

    **`思路-步骤`**

    ```js
    openEnd () {
          // 此时已经可以获取走马灯实例了 ref
          this.$refs.myCarosel.setActiveItem(this.clickIndex)
        },
        // 打开弹层
        openDialog (index) {
          this.dialogVisible = true // dialog是懒加载 => 第一次没有弹出之前 是没有组件元素的
          // 没有办法在弹层中立刻做设置索引
          this.clickIndex = index // 存储一下 点击索引
        }
    ```

    ```html
     <el-dialog @opened="openEnd" :visible="dialogVisible" @close="dialogVisible = false">
           <el-carousel ref="myCarosel" indicator-position="outside" height="500px">
             <el-carousel-item v-for="(item,index) in list" :key="index">
               <img style="width:100%;height:100%" :src="item.url" alt="">
           </el-carousel-item>
          </el-carousel>
        </el-dialog>
    ```

    

## 黑马头条PC-左侧导航栏的折叠展开

**`思路-步骤`**

- 由头部组件触发 

- ```js
  // 折叠或者 展开
     collapseOrOpen () {
       this.collapse = !this.collapse // 不是展开就是折叠
       eventBus.$emit('changeCollapse') // 触发一个事件
     },
  ```

- 在home组件中监听

- ```js
  import eventBus from '../../utils/eventBus'
  export default {
    data () {
      return {
        collapse: false // 默认是展开
      }
    },
    created () {
      // 开启监听
      eventBus.$on('changeCollapse', () => {
        // 头部组件告诉折叠相关的所有组件 要改变了
        this.collapse = !this.collapse
      })
    }
  }
  ```

- ```html
  <el-aside :style="{width: collapse ? '60px' : '230px'}" style="transition: all 0.5s;  min-height:100vh;background-color:#353b4e;">
      <layout-aside :collapse="collapse"></layout-aside>
    </el-aside>
  ```

- ```html
  <div class='layout-aside'>
        <div class='title'>
            <img :src="collapse ? smallImg : bigImg" alt="">
        </div>
        <!-- 左侧导航组件  开启路由 :router="true" 或者 router-->
        <el-menu :collapse="collapse" router background-color="#353b4e" text-color="#adafb5" active-text-color="#ffd04b">
            <!-- 没有折叠选项 -->
            <el-menu-item index="/home">
            <i class='el-icon-s-home'></i>
            <span>首页</span></el-menu-item>
            <!-- 二级折叠菜单 -->
            <el-submenu index="1">
                <!-- 具名插槽 -->
                <template  slot='title'>
                      <i   class='el-icon-document-copy'></i>
                   <span>内容管理</span>
                </template>
                <!-- 匿名插槽 -->
               <el-menu-item index="/home/publish">发布文章</el-menu-item>
               <el-menu-item index="/home/articles">文章列表</el-menu-item>
               <el-menu-item index="/home/comment">评论管理</el-menu-item>
               <el-menu-item index="/home/material">素材管理</el-menu-item>
  
            </el-submenu>
            <el-submenu index="2">
                <!-- 具名插槽 -->
                <template slot='title'>
                  <i class='el-icon-female'></i>
                   <span >粉丝管理</span>
                </template>
                <!-- 匿名插槽 -->
               <el-menu-item index="/home/picture">图文数据</el-menu-item>
               <el-menu-item index="/home/fansinfo">粉丝概况</el-menu-item>
               <el-menu-item index="/home/fanspicture">粉丝画像</el-menu-item>
               <el-menu-item index="/home/fanslist">粉丝列表</el-menu-item>
            </el-submenu>
            <el-menu-item index="/home/account">
            <i class='el-icon-s-custom'></i>
            <span>账户信息</span>
            </el-menu-item>
  
        </el-menu>
    </div>
  ```

- 

## 黑马头条PC-echarts在项目中的应用

**`思路-步骤`**

[**5 分钟上手 ECharts**]([https://www.echartsjs.com/zh/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts](https://www.echartsjs.com/zh/tutorial.html#5 分钟上手 ECharts)

图表 =》echarts => 百度

Vue中使用echarts =》 和Vue没关系 =》 可以在Vue中使用

1. 下载安装echarts

   ```bash
   $ npm i echarts -S
   ```

2. 需要引入echarts => 偏大 =》只在某个页面引入 =》 按需加载 =》 只会讲echarts打包到某个模块

   ```bash
   $ import echarts from 'echarts'
   ```

3. echarts 使用 需要dom元素，需要给echarts一个盒子，一般给一个div,注意！！！**`div必须有高度和宽度`**

```xml
 <div class='echarts'></div>
 .echarts {
     width:600px;
     height: 400px;
 }
```

4. 需要获取之前准备好的dom元素，对图表进行初始化，并且得到一个图表的实例对象

​    beforeCreate created beforeMount =》 里面获取不到dom元素 =》 因为页面还没渲染

mounted => 可以获取到dom元素 => **`init`**

```js 
echarts.init(dom对象)  => 得到图表的实例 => init 方法是图表的方法
```

5. 用得到的图表实例来进行图表的渲染，调用一个图表的方法 ***`setOption`*** =》 设置图表的数据、样式、配置

option => 教程实例中的数据 或者查阅API所得 =》 一般情况下 直接看教程实例即可

![1569464889349](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1228/%E7%AC%94%E8%AE%B0/assets/1569464889349.png)

一旦数据发生变化，需要重新的**`setOption`**

## 黑马头条PC-页面进度条引入应用

**`思路-步骤`**

[nprogress](https://www.npmjs.com/package/nprogress)

- 安装进度条插件

  ```bash
  $ npm install --save nprogress
  ```

- 进度条 从哪里写 =》 导航守卫 =》路由发生变化时触发

- beforeEach => 开启进度条   start

- afterEach  => 关闭进度条   done

## 黑马头条PC-404页面应用

**`思路-步骤`**

- 404 找不到页面

- 当路由匹配不到组件时=》可以配置一个全局的404页面 =》配置方式

- 一级路由上 新建一个路由 path: *,compoent

- ```js
      {
        path: '*', // 匹配任何地址 但是如果其他的可以匹配 优先匹配其他 否则匹配该组件
        component: () => import('./views/404')
      },
  ```

## 黑马头条PC-async和await新异步方案应用/

- H5 /安卓/IOS/小程序 / 微信.支付/百度.抖音.头条.钉钉/qq.
- 微信开发原生小程序 => 扩展框架
- H5 /uni-app/MpVue/Diamon(滴滴)/Weex/Flutter/Taro/ReactNative/Expo
- React =>
- Vue =>
- 稳定 !!! 
- 生态 =>

**`思路-步骤`**

- ajax回调函数 =》 回调嵌套

- promise => 回调嵌套 =》 链式调用

- async/await 异步方案的终极解决方案

  ```js
  // 回调形式调用
  $.ajax({
      url,
      data,
      success:function(result){
          $.ajax({
              data:result,
              success: function(result1){
                  $.ajax({
                      url,
                      data: result1
                })
              }
          })
      }
  })
  ```

  ```js
  // 链式调用 没有嵌套
  axios({ url, data}).then(result => {
      return  axios({
           data:result
       })
  }).then(result1 => {
       return  axios({
           data:result1
     })
  }).then(result2 => {
     return axios({ data: result2 })
  }).then(result3 => {
      return axios({ data: result3 })
  })
  ```

  ```js
  // async/await 同步形式去写代码
  axios({}).then(result=>{
    var a=1
  })
  var b=1 // 一定先执行b=1
  await // 强制等待 
  ```

  **`await`** 后面要跟一个**`promise`**的方法，只有**`promise`**方法**`reslove`**之后，await下面的代码才会执行

  ```js
  await axios({}).then(result=>{
      var a=1
  })
  var b=1 // 一定先执行a=1
  ```

  await会造成代码的阻塞，也就是代码死了，只有reslove之后，后面的代码才能活，有办法解决这个问题，

  就是给await所在的function 标明一个 **`async`**的标记,async 的意思是该函数是异步函数

  ```js
  methods: {
    async  getArticles(){
     let result = await axios()  // 强制等待axios执行完毕 reslove => then /reject => catch 
        var b=1
    }，
      test () {
        this.getArticles() => 异步函数 =》 不用强制等待它里面的await执行完
          var a=1   // 先执行a=1 再执行b=1
      }
  }
  ```

  await 相当于将后面的**`异步函数`**强制性的变成 **`同步函数`**，后面promise的结果可以直接在前面接收

```js
        let result = await this.updateAxios() // 造成强制等待  同步写法
      this.count = result
        // 异步写法
      this.updateAxios().then(result => {
          this.count = result
          this.$message()
        })  
```

  **`await/async`** => 带来的改变就是 编程从异步变成同步了

  **`await不能滥用`** =》 await造成当前代码强制等待 如果 await下面的代码 和await执行的结果没关系，那么请不要放在await下面，可以单独拎出来形成一个方法 或者放在await上面

```js
  getChannels() // 获取频道
  await getArticles() // 获取文章
  this.$message()
  
  // await下面的逻辑 一定是等待着 await结果
```

  **`await必须和async配套使用`** => 用了await,你的父级函数必须是async函数

  await 后面的promise只有resolve了才会执行 下 面的逻辑

  如果想要捕获reject => 要在await函数外面包一层 try/catch

## 黑马头条PC-请求模块单独优化方案

**`思路-步骤`**

- 所有的请求都在组件中

- 所有的请求都抽提出去 形成一个单独的模块，组件只是调用

- 应该 组件中没有axios这类东西 

- export default / export 

- 第一种：

- ```js
  export function getArticles (params) {
    return axios({
      url: API.API_ARTICLES,
      params
    })
  }
  第二种
  ```

- ```js
  import { getArticles } from '../../api/articles'
  
  ```

  ```js
  export  default  obj
  ```

```js
import obj  from '路径'
```

组件和请求就完全分离了

组件只管数据展示和操作 

请求只处理请求

## 黑马头条PC-项目打包介绍

**`思路-步骤`**

- 中间过程代码 =》 html/js/css

- .vue/less=> html/js/css

- ```bash
  $ npm run build
  ```

- .vue =>{{}}/v-if/v-for/v-bind  =>  html/js/css

- ![1569486196199](D:/01%E5%89%8D%E7%AB%AF/%E5%B0%B1%E4%B8%9A%E7%8F%AD/vue/1228/%E7%AC%94%E8%AE%B0/assets/1569486196199.png)

这就是最终形态的代码 =》 上线=》 发布的就是这个 =》 webpack => 网络打包 =》 将web项目中的内容进行打包生成浏览器可识别的内容

## 黑马头条PC-打包在nodejs中运行

**`思路-步骤`**

- 阿里云服务器=》linux => ngix服务器=》nodejs服务器

通过nodejs的方式，创建http服务，以便运行打包好的项目

步骤：

1. 在桌面创建prorun目录

2. 把dist打包文件复制给prorun目录

3. 给prorun目录执行 npm init  生成 package.json文件

4. 给prorun目录执行  npm i express  安装需要的依赖包

5. 给prorun目录 创建  app.js文件 ，内容如下：

   ```js
   // 通过express创建一个http服务
   // 引入express
   var express = require('express')
   
   // 创建express实例化对象
   var app = express()
   
   // 设置dist目录被托管(运行内部的文件)
   app.use(express.static('./dist'))
   
   // 创建http服务
   app.listen(16677,function(){
     console.log('项目已经运行，具体在\n\nhttp://127.0.0.1:16677')
   })
   
   ```

   

6. 执行命令  node  app.js  运行项目

现在项目就可以执行了

