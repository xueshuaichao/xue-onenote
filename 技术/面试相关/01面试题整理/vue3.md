​
>引用：

收藏文献：
Vue3 Hook详解：提升组件逻辑复用和可维护性的利器
https://juejin.cn/post/7326268975733145610
vue3封装Hooks实现更好的逻辑复用_vue3 封装table hooks-CSDN博客
https://blog.csdn.net/qq_62401119/article/details/137500862

### 1. Vue 3相比Vue 2有哪些主要改进？有哪些新增特性

 - api层面Vue3新特性主要包括:
 1. Composition API、Teleport传送门、Fragments 片段、Suspense、Emits选项、自定义渲染器、SFC CSS变量、SFC Composition API语法糖、
  ```
    1.使用了Composition API，提高了代码逻辑的可复用性。面对vue2的局限性，可以将相同的代码组织在一起，而不会散落在各个角落
    2.Teleport组件允许将子组件渲染到DOM中的任何位置。
    3.引入了Fragment，允许组件有多个根节点。
    4.提供了Suspense组件，用于处理异步组件的加载状态。
  ```

- 更快
  1. 虚拟DOM重写
  2. 编译器优化:静态提升
  3. vdom 的对比算法更新，新增静态标记（patchflag ），只更新 vdom 的绑定了动态数据的部分
  4. Vue3使用了Proxy代理对象，可以更快地跟踪数据变化，从而提高渲染速度。
- 更小:更好的tree-shaking优化
  
- 更容易维护:采用了TS来编写



### 1. Vue3 Composition API是什么？它的作用是什么？
Composition API 是一组基于函数的 API，它允许你以可复用的方式组织组件逻辑。它主要包括 ref、reactive、computed、watch、setup 等函数和钩子。

### 2. setup()函数在Vue 3中起什么作用？
setup() 是 Vue 3 组件选项 API 中的一个新选项。它是 Composition API 的入口点，在组件被创建之前执行，用于初始化状态、计算属性和方法，并返回在模板中使用的响应式引用。

### setup配置
Vue 3中的 setup 函数接收两个参数，分别是 props 和 context。
1. props：值为对象，包含: 组件外部传递过来。切组件内部声明接收了的属性。需要注意的是，Vue3中的 props 是只读的，即在setup 函数中不能修改 props 的值。如果需要修改传递过来的数据，可以使用响应式对象或ref。
2. context：上下文对象。
attrs:值为对象，包含组件外部传递过来，但没有在props配置中声明的属性。相当于this.$attrs
slots:收到的插槽内容，相当于this.$slots
emit:分发自定义事件的函数，相当于this.$emit

————————————————

注意：
1、这个钩子会在created之前执行
2、内部不存在this
3、如果返回值是一个对象，那么这个对象中的键值对会被合并到created钩子的this中，而在视图上也能访问相应的数据值

### 4. 请解释ref和reactive的区别？
- ref 用于创建简单的响应式引用，通常用于基本数据类型。
- reactive 用于创建响应式对象，通常用于复杂数据类型如数组和对象。
  
——————————————————————

reactive:

1. 它的响应式是更加‘深层次’的，底层本质是将传入的数据包装成一个Proxy。
2. 参数必须是对象或者数组，如果要让对象的某个元素实现响应式时比较麻烦。需要使用toRefs
ref:
1. 函数参数可以是基本数据类型，也可以接受对象类型
2. 如果参数是对象类型时，其实底层的本质还是reactive,系统会自动根据我们给ref传入的值转换成：reactive
3. 在template中访问，系统会自动添加.value;在js中需要手动.value
4. ref响应式原理是依赖于Object.defineProperty()的get()和set()的。

### 1. Vue 3中的watch和watchEffect有何不同？
watch 允许你监听特定的响应式引用或计算属性，并在它们改变时执行回调函数。
watchEffect 会立即执行一个函数，并自动追踪其依赖的响应式引用，当依赖改变时重新执行。



### 6. Vue 3中的Suspense组件是如何工作的？
Suspense 组件允许你指定一个加载中的状态（fallback）和一个加载失败的状态（fallback slot），用于处理异步组件的加载状态。当异步组件加载时，会先显示加载中的状态；加载完成后，会显示异步组件；如果加载失败，会显示加载失败的状态。

### 3. Vue3中的Teleport是什么？它的作用是什么？
Teleport 组件允许你将子组件渲染到DOM树中的任何位置，而不仅仅是其父组件的模板内。这在处理模态框、下拉菜单等需要渲染到特定位置的组件时非常有用。

### 5. Vue3中的Fragment是什么？它的作用是什么？
Fragment 允许组件有多个根节点，Fragment 在渲染时会被视为一个虚拟节点，并不会实际创建额外的 DOM 元素。可以解决在Vue2中，v-for迭代元素时需要添加一个包装元素的问题。

### 8. Vue 3如何优化性能？
- 使用v-show代替v-if来频繁切换元素，因为v-show只是切换元素的CSS属性。
- 使用key来优化列表渲染的性能。
- 使用computed和watch来减少不必要的计算和渲染。
- 使用v-memo来缓存组件的渲染结果。

### 6. 什么是响应式系统？ Vue3中的响应式系统有哪些更新？
答：响应式系统是Vue中的核心概念之一，它允许在状态发生变化时更新视图。Vue3中的响应式系统更新包括Proxy、Reflect和WeakMap等。

### 11. Vue 3中的响应式系统是如何工作的？
Vue 3的响应式系统通过ES6的Proxy对象来实现。当使用reactive或ref函数时，Vue会创建一个Proxy对象来包裹原始数据。这个Proxy对象会拦截对原始数据的访问和修改，从而可以追踪到数据的变化。当数据发生变化时，Vue会触发相应的依赖更新，重新渲染视图。

### 1、vue2和vue3响应式原理
Vue2通过Object.defineProperty对data中的属性进行劫持，当属性值发生变化时，会触发对应的更新函数，从而更新视图。
Vue2通过Watcher来实现数据与视图的双向绑定，当数据发生变化时，Watcher会通知对应的视图进行更新。
存在问题
1.速度慢，深度递归遍历待处理的对象才能对它进行完全拦截
2.无法监听对象或数组新增、删除，需要针对常用数组原型方法push、pop、shift、unshift、splice、sort、reverse进行了hack处理；提供Vue.set监听对象/数组新增属性。


Vue3的响应式原理：
Vue3使用Proxy可以监听到对象的所有属性，包括新增和删除操作。
Proxy 是 ES6 新特性，通过第2个参数 handler 拦截目标对象的行为。相较于 Object.defineProperty 提供语言全范围的响应能力，消除了局限性。
Vue3使用了WeakMap来存储依赖关系，避免了Vue2中Watcher的内存泄漏问题。


Proxy代理
对数组进行拦截，还能对Map，Set实现拦截
proxy是懒处理行为，没有嵌套对象时，不会实施拦截，也使之初始化速度和内存得到改善
proxy存在兼容性问题，IE不支持。




### 1. Vue3中的事件修饰符有哪些？
Vue3中的事件修饰符与Vue2基本相同，包括stop、prevent、capture和self等。

### 1. Vue3中的指令有哪些？

Vue3中的指令包括v-if、v-for、v-bind、v-on、v-html、v-model、v-show、v-slot、v-text等。
1. Vue3中如何实现动态组件？
答：Vue3中使用 <component> 元素和 v-bind:is 属性来实现动态组件。例如， 
```javascript
<component v-bind:is="currentComponent"></component> 
```


### 1.  Vue3如何实现插槽？
 ```javascript
// 父组件
<template v-slot:slot-name></template>

// 子组件
<slot name="slot-name"></slot>
 ```
举例：
 ```javascript
 // 父组件
<FancyButton>
  Click me! <!-- 插槽内容 -->
</FancyButton>

// 子组件
<button class="fancy-btn">
  <slot></slot> <!-- 插槽出口 -->
</button>
```

### 12. Vue3如何实现自定义指令？
Vue3使用 app.directive() 方法来全局注册自定义指令。
自定义指令的定义包括一个名字、一个或多个钩子函数（如 bind、inserted、update、componentUpdated 和 unbind）。
```javascript
// 在mounted时触发自定义指令
app.directive('focus', {mounted(el) {el.focus()}}) 

// 用法
<div v-focus>This div will have a red background.</div>
```

### 13. Vue3如何实现混入？
Vue3使用 app.mixin() 方法来注册混入，例如 
```javascript
app.mixin({created() {console.log('mixin created')}}) 
```

14. Vue3如何实现自定义渲染函数？

Vue3使用 h() 函数来创建虚拟节点，例如 
```javascript
h('div', {class: 'container'}, 'Hello, world') 
```
### 1. Vue3中的响应式系统如何处理循环引用问题？
Vue3中使用WeakMap来处理循环引用问题。

### 1. Vue 3的provide和inject是如何工作的？
provide 和 inject 允许你在祖先组件和后代组件之间传递数据，而不需要通过props和events进行逐层传递。provide 在祖先组件中定义要传递的数据，inject 在后代组件中接收数据。通过 provide 和 inject 传递的数据是响应式的
```javascript
// 父组件
<script setup>
    import {ref, provide} from 'vue';
     let modalType = ref('confirm');
    provide('modalType', modalType);
</script>

// 子组件
<script setup>
    import { inject } from 'vue';
    // 获取弹框类型
    const type = inject('modalType', 'default'); 
    //default：设置默认值，可以不写，是可选参数。
</script>

//需要注意的是，provide和inject只能在setup函数中使用，而且provide提供的数据只能在其子组件中使用。如果要在兄弟组件中共享数据，可以使用一个共享的对象或者使用Vuex等状态管理库。
```

### 10. Vue 3如何处理组件的异步加载？

Vue 3 使用 defineAsyncComponent 函数来定义异步组件。异步组件允许你延迟加载组件，直到需要时才加载，从而优化性能。

### 17. Vue3中的ref指令有哪些用途？
答：Vue3中的ref指令可以用来在组件内部获取子组件的实例，也可以用来获取DOM元素或其他组件的实例。


### 20. Vue3如何实现异步验证表单输入？
答：使用 watch() 函数，监听表单输入的变化，并使用异步函数处理验证逻辑。

### 21. Vue3中如何使用路由？
答：Vue3中使用Vue Router来实现路由。首先需要安装Vue Router，然后使用 createRouter() 函数创建路由对象，然后在根Vue实例中使用 app.use() 方法注册Vue Router。

### 20. Vue 3的生命周期钩子有哪些变化？
Vue 3对生命周期钩子进行了一些调整和优化。
首先，Vue 3将beforeDestroy和destroyed钩子重命名为beforeUnmount和unmounted，以更好地反映组件的卸载过程。
其次，Vue 3新增了setup钩子函数，用于在组件创建之前执行初始化逻辑。
此外，Vue 3还提供了onBeforeMount、onMounted、onBeforeUpdate、onUpdated、onBeforeUnmount和onUnmounted等生命周期钩子函数，用于在组件的不同生命周期阶段执行自定义逻辑。

​