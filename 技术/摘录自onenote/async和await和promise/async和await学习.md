简单理解：
async是 让方法变成异步；
await是等待异步方法执行完成。
因为await访问 本身会造成程序停止阻塞，所以await必须在异步方法中使用。
一个一般的函数
```js
function fn() {
  return "123";
}
console.log(fn()); // 123
```
async可以把函数变为异步
```js
async function fn() {
  return "123";
}
console.log(fn());
```
结果是一个promise对象
1. Promise {<resolved>: "1234"}
1. __proto__: Promise
2. [[PromiseStatus]]: "resolved"
3. [[PromiseValue]]: "1234"
这时候有两种方法可以得到返回的数据
方法一：
```js
var p = fn();
p.then((data) => {
  console.log(data);
});
```
方法二：
await 是等待异步方法执行完成，可以获取异步方法里边的数据，但必须得用在异步方法里边
注意此处的做法是在fn外边再套一层f1的异步方法。
```js
async function f1() {
  var d = await fn();
  console.log(d); //123
}
f1();
```
这个案例多好，await就不是用来return的，而是直接console的。这个和上边的then有相同效果，如果return，又变成了promise。
await阻塞的功能，把异步变为同步
```js
async function fn() {
  console.log(2);
  return "123";
}
async function f1() {
  console.log(1);
  var d = await fn();
  console.log(3);
}
f1(); // 打印顺序 1，2，3 ，此处，await将异步变为同步。
```
经典写法：
```js
async function getData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      var username = "张三";
      resolve(username);
    }, 1000);
  });
}
async function test() {
  var data = await getData();
  //就是在一个异步函数中去获取上一个异步函数获取的数据。
  console.log(data);
}
test();
```
如果将上边的resolve(username);改为 reject(username);会报错：

所以应该写如下：
```js
async function getData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      var username = "张三";
      reject(username);
    }, 1000);
  });
}
async function test() {
  try {
    var data = await getData();
    //就是在一个异步函数中去获取上一个异步函数获取的数据。
    console.log(data);
  } catch (e) {
    console.log(e); //张三
  }
}
test();
```
