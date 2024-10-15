​

>(回答问题记住wwh原则，是什么，为什么以及怎么用，一次回答全，不要让面试官一个个问)

### 虚拟dom解决了哪些问题，存在什么问题
1. 解决了数据驱动视图可能会导致很多无效的更新，因此虚拟dom就诞生了，先通过diff算法看哪些部分更新了，从而做到最小变动
2. 存在的问题就是消耗了性能。



### 什么是虚拟dom 
虚拟dom是表示真实dom的js对象，虚拟dom通过diff算法找出变化部分，从而实现最小更新


### 什么是diff算法
- diff算法是找出新旧两个虚拟dom对象的差异，最小更新视图，
- 具体流程
1. 数据改变后，会触发双向绑定的setter更新，通知所有的订阅者，生成新旧两个dom树，diff算法是同级比较，
2. 从根节点开始比较，先看标签是否相同，如果不同，直接替换，如果相同，这是会有几种情况，
3. 如果都有文本节点，用新文本替换旧文本，
4. 如果旧虚拟dom中没有子节点，新dom中有，则增加新的子节点，如果旧的有，新的没有则删除子节点，
5. 如果新旧都有子节点，则执行updatechildren方法
vue2.0通过双端交叉指针法，新老vdom各有两个指针，通过头头，尾尾，头尾，尾头 4次比较，如果寻找到元素的key相同就会复用
，如果这4种情况都没有匹配，就会从vdom的队头开始再去寻找，看老的vdom里边有没有对应的元素，进行相应的移动，删除和创建


```
但双端diff算法的缺陷在于他去找这个节点，如果可以复用，那么就会产生移动，它没有去关注哪些节点不用去移动，这样就会产生额外的移动操作。
vue3中就采用了最长递增子序列的思想，尽可能少移动节点，减少无意义的移动
具体操作：创建一个新节点在旧节点中的位置的映射表，根据这个映射表计算出最长递增子序列，这个序列中的结点代表可以原地复用。之后移动剩下的新结点到正确的位置即递增序列的间隙中。

vue3.0叫做双端快速diff，实际上他也有两个指针，新老vdom各有两个，只对比两种情况，队头和队头，队尾和队尾，如果能够匹配上，和vue2.0是完全一致的，
一旦没有匹配上，会触发对新的vdom去进行最长递增子序列的计算，生成列表，对不在这个列表中的元素进行新增删除和创建





而且vue2diff算法采用的是递归比对（浪费性能），vue3在模板编译的时候会标记，哪些是动态节点，只比较动态节点！
```

React DOM diff 和 Vue DOM diff 的区别
React 是从左向右遍历对比，Vue 是双端交叉对比。






### 2. vue中的data为什么是函数形式
因为一个组件可能被多个地方引用，这就要求data数据都是相互隔离的，这就要求data不是一个单纯对象，而是一个函数返回值，每个组件实例可以维护一份被返回对象的独立拷贝



### 3. vue2和vue3中的 v-if和v-for优先级问题
- vue2中，v-for的优先级高于v-if
- vue3中，v-if的优先级是高于v-for

> ***永远不要把 v-if 和 v-for 同时用在同一个元素上***
如何避免出现这种情况，在外层进行 v-if 判断，在内部进行 v-for 循环
```javascript
<template v-if="isShow">
  <p v-for="item in items">
</template>
```

如果条件出现在循环内部，可通过计算属性computed提前过滤掉那些不需要显示的项
```javascript
computed: {
    items: function() {
      return this.list.filter(function (item) {
        return item.isShow
      })
    }
}
```


### 4、vue双向绑定的实现原理
首先回答，是基于数据劫持和发布订阅者模式实现的
通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发给订阅者，触发相应的监听回调，

具体步骤：
  -  第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化。
  - 第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图。
  - 第三步：watcher订阅者是Observe和compile之间通信的桥梁，主要做的事情是：
    1. 在自身实例化时往属性订阅器（dep）里面添加自己
    2. 自身必须有一个update方法
    3. 待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调函数。
  - 第四步：MVVM作为数据绑定的入口，整合Observe和Compile和Watcher三者，通过Observe来监听自身的model数据变化，通过Compile来解析模板指令，最终利用Watcher搭起两者之间通信的桥梁，达到数据变化->视图更新；视图交互变化（input）->数据model变更的双向绑定效果。
  ```javascript
  //在console.log(book.name)同时,直接给书加一个书号
  var Book = {};
  var name = '';
  Object.defineProperty(Book,'name',{
      set:function(value) {
          name = value;
          console.log('你取了一个书名叫:'+value);
      },
      get:function() {
          console.log('get方法被监听到');
          return '<'+name+'>';
      }
  });
  Book.name = '人性的弱点';  //你取了一个书名叫:人性的弱点
  console.log(Book.name);　//<人性的弱点>
  ```



### 5、vue的生命周期
  ```
  Vue2--------------vue3
  beforeCreate  -> setup()
  created       -> setup()
  beforeMount   -> onBeforeMount
  mounted       -> onMounted
  beforeUpdate  -> onBeforeUpdate
  updated       -> onUpdated
  beforeDestroy -> onBeforeUnmount
  destroyed     -> onUnmounted
  activated     -> onActivated
  deactivated   -> onDeactivated

  beforeCreate函数：组件被创建了，但是vue对象的属性还没有绑定，如data属性
  Created：vue对象的属性有值了，但是DOM还没有生成，
  beforeMount函数：此时 this.$el有值，但是数据还没有挂载到页面上。
  Monuted函数：模板编译完成，数据挂载完毕,一般来说，我们在此处发送异步请求
  beforeUpdate函数：组件更新之前执行
  updated函数：组件更新完成之后执行
  beforeDestroy：组件卸载之前执行
  destroyed：组件卸载完成后执行
  ```

### 6、ajax请求放在哪个生命周期中？
在mounted中，此时DOM已经渲染出来，可以直接操作DOM节点。
一般情况下都放到mounted中

### 7、v-if 和 v-show 区别
v-if按照条件是否渲染，v-show是display的block或none；

### 8、$route和$router的区别
  - this.$route是当前激活的路由对象，通过他可以拿到当前路由的一些信息，比如path，query，meta等属性，
  - this.$router是vueRouter的一个实例，是全局路由对象，this.$router.push可实现路由跳转

### 9、vue几种常用的指令
v-for 、 v-if 、v-bind、v-on、v-show、v-else

### 10、vue常用的修饰符？
 ```
  .prevent: 提交事件不再重载页面；
  .stop: 阻止单击事件冒泡；
  .self: 当事件发生在该元素本身而不是子元素的时候会触发；
  .capture: 事件侦听，事件发生的时候会调用
  ```


### 11、vue中 key 值的作用？
1. key的作用主要是为了更高效的更新虚拟DOM。
2. 在patch过程中，会执行updateChildren方法，通过key可以判断是不是同一个节点，如果没有加key会认为是相同的节点，哪怕它们实际上不是，会增加不必要而更新，如果加上key后，如果key相等，只需要移动就行。同样道理，key也不能用数组索引

3. vue中在使用相同标签元素过渡切换时，也会使用key属性，其目的也是为了让vue可以区分它们，否则vue只会替换其内部属性而不会触发过渡效果。



### 13、vue等单页面应用及其优缺点
  - 优点：通过尽可能简单的 API 实现响应的数据驱动视图。比较轻量高效

 - 缺点：
不利于SEO的优化（如果要支持SEO，建议通过服务端来进行渲染组件）；
第一次加载首页耗时相对长一些；
不可以使用浏览器的导航按钮需要自行实现前进、后退。

### 14、父子组件的加载顺序：
  ```
  1、父子组件的加载顺序为
  父beforeCreated ->父created ->父beforeMounted ->子beforeCreated ->子created ->子beforeMounted ->子mounted -> 父mounted
  3、子组件更新顺序为
  父beforeUpdate->子beforeUpdate->子updated->父updated
  4、父子组件销毁顺序为
  父beforeDestroy->子beforeDestroy->子destroyed->父destroyed
  ```


### 15、{{}},v-text,v-html表达式是怎么用的，有什么区别，
 - v-html:在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 XSS 攻击。只在可信内容上使用 v-html，永不用在用户提交的内容上。
 - v-text: 
 ```
<p v-text= "username"></p>
v-text 指令会覆盖元素内默认的值。
 ```
 
 - {{ }}: 插值表达式, 前后可以添加其他的内容,专门用来解决v-text会覆盖默认文本内容的问题


### 16、组件间的通信
 - 父子组件：props和$emits用于父子组件间传参
 - 兄弟组件：通过vuex或pinia状态管理，或者vue2中的event-bus
 - 深层组件：provide和inject用于深层次组件传参很方便

```
// 祖先组件app.vue
export default {
    name: 'app',
    provide() {
        return {
            someval:'来自app.vue'
        }
    }
}
// 子组件
export default {
    name: 'app',
    inject: ['someval']
}
```


> provide 和 inject 主要为高阶插件/组件库提供用例。并不推荐直接用于应用程序代码中。


### 17、介绍Vuex
vuex能对vue项目进行状态管理，主要一般通过state，mutations，action这三个模块构造，一般在页面中通过mapState来读取数据，通过mapActions来操作action。面对复杂的应用我们还需要创建modules，将vuex的store对象拆分成模块来写。
1. state是保存所有数据，
2. mutations用来保存所有方法，用来改变state的数据，
3. action一般暴露给用户使用，可执行异步操作，用来触发mutations的方法，用来改变数据。
一般在页面中通过mapState来读取数据，通过mapActions来操作action。面对复杂的应用我们还需要创建modules，将vuex的store对象拆分成模块来写。


### 19、vue-router原理
前端路由主要有两种模式，hash模式和history模式，
- hash模式
```
hash会在域名后面加一个#号，hash虽然会出现在url中，但不会包括在http请求中
通过监听hashChange事件来知道路由发生变化，从而进一步去更新我们的页面
hash模式会创建hashHistory对象,hashHistory对象有两个方法，push() 和 replace()
```

- history模式
```
而history没有#号，这种模式需要服务端支持。服务端接收到请求后，都指向同一个html文件。
通过监听 popstate事件来监听路由改变，从而更新页面
通过history.pushState()或者history.replaceState() 改变地址，但不会向服务器去发送请求
需要和服务器配合使用，否则容易出现页面404的情况
```


### 21、MVVM是什么？
MVVM即Model-View-ViewModel的简写。Model指的是后端传递的数据。View指视图。视图模型(ViewModel)是mvvm模式的核心，它是连接view和model的桥梁。

### 22、vue-router 有哪几种导航钩子?
1. 全局导航钩子：router.beforeEach(to,from,next)作用：跳转前进行判断拦截
2. 路由独享钩子可以在路由配置上直接定义 beforeEnter
3. 组件内的导航钩子有三种：
```
beforeRouteEnter 在进入当前组件对应的路由前调用
beforeRouteUpdate 在当前路由改变，但是该组件被复用时调用
beforeRouteLeave 在离开当前组件对应的路由前调用=
```


### 23、vue中什么是递归组件？举个例子说明下？
当前注册一个vue组件定义 name 为 ‘node-tree’ ，在组件 template 内部调用 实现递归。
组件自己调用自己，场景有用于生成树形结构菜单​