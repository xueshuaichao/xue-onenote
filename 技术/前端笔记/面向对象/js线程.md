

### setTimeout和setInterval中的执行队列问题
可以把 setTimeout/setInterval 中的代码看作是异步执行的代码，
这里面的回调函数总是被延后执行的！！！

 * JavaScript 是一门单线程的编程语言
   
JS 会优先执行除了 setTimeout/setInterval/ajax 等回调函数中的代码
等到这些代码执行完毕了以后，在来执行 这些回调函数中的代码！！！

 * JS 中的事件循环
JS 是一门事件驱动型语言，在js中是通过 回调函数 实现的事件驱动机制


与 JS 相关的 三个常驻 线程：
 
1 主线程
作用：执行js代码

2 事件循环线程
作用：将事件队列中的回调函数取出来，然后交给 主线程，最终回调函数的代码还是由 主线程 来执行的

3 UI渲染线程  并不是style样式中的css代码，而是js中控制dom的代码。
作用：渲染页面  

其中，JS主线程 和 UI渲染线程 是互斥的，也就是同时只能有一个线程在执行！

为什么不能将 js 放到head中引入？？

因为js代码执行的时候，渲染页面就停止了，用户先看到一个白屏的效果，这样
用户体验不好！

 * 一个案例
```js
for (var i = 0; i < 10; i++) {
  setTimeout(function () {
    console.log(i);
  }, 0);
}
执行结果为10个10；
```
    
执行过程：
1 执行for循环
2 每一次执行的时候，都会调用 setTimeout 函数
3 将 setTimeout 执行的回调函数放到 事件队列 中
4 for 循环执行完毕以后，放到事件队列中的回调函数才会被依次执行
5 因为 for 循环执行完毕，所以，i的为：10，并且 i 是一个全局变量


有回调函数的队列执行问题
 // 如果我们能够将每一次循环 i 的值保存起来，然后，最终打印
 // 每一次保存的 i 的值，这样就能打印出 0-9 了
```js
var i;
for (i = 0; i < 10; i++) {
  var fn = function () {
    var num = i;
    // console.log('for循环执行时候 num 的值为:'+ num );
    return function () {
      console.log("setTimeout中打印的结果:" + num);
    };
  };
  // 函数fn被调用了10次，每一次调用i的值都是不同的，
  // 因为 num 的值是由 i 的来决定的，所以，每一次 num 的值也就不同了!
  var f = fn();
  setTimeout(f, 0);
  // 直接打印i的值就是:0-9
  // console.log(i );
}
```
for循环创建了10个fn，每一次调用fn产生的闭包中 num 的值都不同，
所以，这个 num 的值，就在内存中得到了维持，没有被释放掉














