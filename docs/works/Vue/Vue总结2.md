# **1.为何vue中采取异步渲染**

原因：Vue中视图不是实时更新的；

解决：**vue中的nextTick可以获取更新DOM后的操作

This.$nextTick()

# **2.nextTick实现原理  异步执行**

异步执行原理：

（1）所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。**（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。**
（4）主线程不断重复上面的第三步。

 

 

# **3.ajax请求放在哪个生命周期中**  

 created（最好）  mounted   created阶段就可以获取到data中的数据，

 

# **4.父子组件生命周期函数执行过程**

**加载渲染过程**

　　父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted

**子组件更新过程**

　　父beforeUpdate->子beforeUpdate->子updated->父updated

**父组件更新过程**

　　父beforeUpdate->父updated

**销毁过程**

　　父beforeDestroy->子beforeDestroy->子destroyed->父destroyed

# **5..vue中computed特点**

computed是属性调用，而methods是函数调用

computed带有缓存功能，而methods不是

# **6.watch中deep:true   深度监听**

需要监听未在data定义的对象的属性时。由于 Vue 会在初始化实例时对属性执行 getter/setter 转化过程，所以属性必须在 data 对象上存在才能让 Vue 转换它，这样才能让它是响应的。

deep的意思就是深入观察，监听器会一层层的往下遍历，给对象的所有属性都加上这个监听器。

# **7.Vue中v-html注意事项**

V-html更新的是元素的 innerHTML 。内容按普通 HTML 插入， 不会作为 Vue 模板进行编译 。

解决：使用组件来代替

# **8.v-if和v-show区别**

vue-show本质就是标签display设置为none，控制隐藏

vue-if是动态的向DOM树内添加或者删除DOM元素

# **9.v-for与v-if不能同时使用**

原因：v-for比v-if优先，如果每一次都需要遍历整个数组，将会影响速度，尤其是当之需要渲染很小一部分的时候。

# **10.**v-model实现原理

v-bind:绑定响应式数据

触发 input 事件 并传递数据 (核心和重点)

# **11.组件中data为什么是一个函数**

组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。而单纯的写成对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都会变的结果。

# **12.**具名插槽、作用域插槽

```js
具名插槽

​```// 子组件<template>

​```

​    <section>

​        <slot name="article-title">这里放标题</slot>

​        <slot>这里放作者</slot>

​        <slot name="article-content">这里放文章内容</slot>

</section>

</template>
// 父组件<template>

​    <section>

​        <slot-child>

​            <h1 slot="article-title">vue作用域插槽，你真的懂了吗？</h1>

            <p slot="article-content">好像有点懂了</p>

            <div>王五</div>

​        </slot-child>

​    </section></template>

**作用域插槽**

<slot :nickName="'Tusi'"></slot>

<template>

​    <section>

​        <slot-child>

​            <template slot-scope="scope">

                <div>{{scope.nickName}}</div>

​            </template>

​        </slot-child>

​    </section></template>
```



# **13.vnode（虚拟节点）**

渲染视图的过程是先创建vnode，然后在使用vnode去生成真实的DOM元素，最后插入到页面渲染视图。

VNode是一个类，可以生产不同类型的vnode实例，不同类型的实例表示不同类型的真实DOM。

# **14.diff算法**

Diff算法的作用是用来计算出 Virtual（虚拟） DOM 中被改变的部分，然后针对该部分进行原生DOM操作，而不用重新渲染整个页面。

# **15****.v-for为什么要加key属性**

vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以标识组件的唯一性，为了更好地区别各个组件 key的作用**主要是为了高效的更新虚拟DOM。**

# **16.v****ue组件渲染和更新**

\1. 把模板编译为render函数

\2. 实例进行挂载, 根据根节点render函数的调用，递归的生成虚拟dom

\3. 对比虚拟dom，渲染到真实dom

\4. 组件内部data发生变化，组件和子组件引用data作为props重新调用render函数，生成虚拟dom, 返回到步骤3

# **17.v****ue中性能优化**  

 **性能优化9法：**

1.函数形组件 <template function> 不做生命周期耗时处理，作为函数进行处理

2.子组件拆分 重处理不要写在本组件当中，写在子组件中

3.局部变量 例如：调用计算属性，在方法内定义一个常量，将计算属性赋值给常量，方法内使用时直接调用常量，提高效率。

4.活用v-show  减少v-if （v-show不操作DOM树）

5.使用keep-alive  组件缓存 

6.活用延迟装载（Defer） 安排顺序执行（按逻辑先后执行） 先装载和延迟装载提高用户观察页面效果，其实并未提高效率。

7.分批处理  提高画面渲染的性能

8.非响应式（非观察模式） 不需要vue检测数据变化时，object.defineProperty直接设置数据，不通过vue转化并检测

9.仅渲染可视化部分  用户看不到的数据慢慢渲染进来

**Vue 应用运行时性能优化措施：**

引入生产环境的 Vue 文件

使用单文件组件预编译模板

提取组件的 CSS 到单独到文件

利用Object.freeze()提升性能（不转化getter，setter ）

扁平化 Store 数据结构

合理使用持久化 Store 数据

组件懒加载

**Vue 应用加载性能优化措施：**

服务端渲染 / 预渲染

组件懒加载

# **18.keep-alive**

是Vue的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM。节省性能（组件切换过程中默认会被销毁）。

keep-alive包裹动态组件的时候，会缓存不活动的组件实例，而不是销毁他们；

主要依赖 beforeRouteLeave函数动态设置需要缓存的组件

生命周期：当引入keep-alive的时候，页面第一次进入，钩子的触发顺序created-> mounted-> activated，退出时触发deactivated。当再次进入（前进或者后退）时，只触发activated。

# **19.****hash路由与history路由**

**hash ——** 即地址栏 URL 中的 # 符号（此 hash 不是密码学里的散列运算）。比如这个 URL：http://www.abc.com/#/hello，hash 的值为 #/hello。**它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。**

**history ——** 利用了 HTML5 History Interface 中新增的 pushState() 和 replaceState() 方法，需要服务器配合才行。（需要特定浏览器支持）这两个方法应用于浏览器的历史记录栈，在当前已有的 back、forward、go 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。

# **20****.vue-router中导航守卫**

全局守卫，挂载在全局路由对象中

router.beforeEach((to, from, next) => {})

router.beforeResolve((to, from, next) => {})

router.afterEach((to, from) => {})

单个路由独享

beforeEnter((to, from, next) => {})

组件级别

beforeRouteLeave((to, from, next) => {})

beforeRouteEnter((to, from, next) => {})

beforeRouteUpdate((to, from, next) => {})

# **21.vuex原理（简述）**

① Vue Components 是我们的 vue 组件，组件会触发（dispatch）一些事件或动作，也就是图中的 Actions；

② 我们在组件中发出的动作，肯定是想获取或者改变数据的，但是在 vuex 中，数据是集中管理的，我们不能直接去更改数据，所以会把这个动作提交（Commit）到 Mutations 中；

③ 然后 Mutations 就去改变（Mutate）State 中的数据；

④ 当 State 中的数据被改变之后，就会重新渲染（Render）到 Vue Components 中去，组件展示更新后的数据，完成一个流程。

 