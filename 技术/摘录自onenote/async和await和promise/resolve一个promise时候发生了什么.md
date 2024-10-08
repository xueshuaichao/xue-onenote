这次单讲resolve(promise)这种情况。有些地方说"resolve(promise)返回了一个promise的副本"。这句话应该怎么理解呢？我们来看一个小例子： 
```js
var p1 = new Promise(function (resolve, reject) {
  console.log("这是p1");
  setTimeout(function () {
    resolve("ok");
  }, 2000);
});
var p2 = new Promise(function (resolve, reject) {
  resolve(p1); //resolve了一个promise
});
p2.then(function (res) {
  console.log(p1); //Promise {<resolved>: "ok"}
  console.log(res); //“ok"
});
console.log(p1); //Promise { <pending> }
console.log(p2); //Promise { <pending> }
```
   resolve（value），当value等于普通值，res就等于这个值， 而value如果等于p1，程序就会等待p1变成resolved后再往下执行。所以resolve(p1)等待p1的状态改变（resolved或者rejected)再执行p2.then里的回调。注意，这里说”等待“，而不是”去执行“，因为p1是在定义时候自执行的,而不是resolve(p1)驱动的。这段代码执行顺序如下：
         1. new Promise同时就执行了resolve("ok")，这是个异步操作，程序继续往下执行；（这个确实是，经过实验，会立即打印"这是p1",而不是等有then时再执行。）
         2. new Promise 得到p2, 执行到resolve(p1)，异步操作，而且p1还是pending状态（2000ms没有到)，不能resolve p2，继续执行
         3. 到了console.log(p1),这时候p1还是pending，输出 Promise(<pending>)
         4. p2的状态取决于p1，则输出Promise(<pending>)
         5. 2000ms时间到,p1变成resolved,紧接着p2变成resolved,
         6. 执行p2.then回调函数，输出"ok"
         就上面这个简单的例子来说，它也可以这样写：
var p2 = Promise.resolve(p1) 
 从这个表达式可以一目了然，p2就是p1的一个副本，因为p2的状态(pending,resolved,rejected)取决于p1
