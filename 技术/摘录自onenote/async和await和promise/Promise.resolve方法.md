Promise.resolve方法有下面三种形式：
Promise.resolve(value); 
Promise.resolve(promise); 
Promise.resolve(thenable); 
Promise.resolve可以把，普通值，一个promise，一个thenable类型的对象都包裹成一个新的Promise。
提供了创建一个Promise的副本的能力，是将一个类似Promise的对象转换成一个真正的Promise对象。它的一个重要作用是将一个其他实现的Promise对象封装成一个当前实现的Promise对象。

var promise1 = Promise.resolve(123);
promise1.then(function (value) {
  console.log(value); // 123
});
Promise.resolve的执行顺序

setTimeout(function () {
  console.log(3);
}, 0);
Promise.resolve().then(function () {
  console.log(2);
});
console.log(1);

Promise.resolve方法允许调用时不带参数，直接返回一个resolved状态的 Promise 对象。
所以，如果希望得到一个 Promise 对象，比较方便的方法就是直接调用Promise.resolve方法。
需要注意的是，立即resolve的 Promise 对象，是在本轮“事件循环”（event loop）的结束时，而不是在下一轮“事件循环”的开始时。
上面代码中，setTimeout(fn, 0)在下一轮“事件循环”开始时执行，Promise.resolve()在本轮“事件循环”结束时执行，console.log(1)则是立即执行，因此最先输出。
