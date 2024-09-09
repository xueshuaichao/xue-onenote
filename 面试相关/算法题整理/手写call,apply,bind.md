
要做到能手写其中一个代码，比如手写call

## 手写call
```javascript
Function.prototype._call = function(ctx, ...args) {
  // 此时this就是method方法
  ctx.key = this 
  // 这里为什么要赋值一下，因为method内部this要指向ctx，如果不这么写，会指向window
  // 此时args是数组，记住如果传参时分散传入，用...args接收时，args就是数组
  const result = ctx.key(...args) 
  // 此时这里用...args是分散传入的
  delete ctx.key;
  return result // 如果返回结果，还需要将结果返回
}
```
>到这里只能给50分，如果传入的obj是null呢，如果obj里边已经有fn这个属性了呢，这不是覆盖了吗

```javascript
Function.prototype._call = function(ctx, ...args) {
  ctx = (ctx === null || ctx === undefined) ? globalThis : Object(ctx) 
  // 这里之所以用globalThis 不用window，是因为window只代表浏览器环境，但有可能是node环境，所以用globalThis表示全局对象

  var key = Symbol('temp');
  // 此时this就是method方法
  ctx.key = this // 这里为什么要赋值一下，因为method内部this要指向ctx，如果不这么写，会指向window
  // 此时args是数组，记住如果传参时分散传入，用...args接收时，args就是数组
  const result = ctx.key(...args) // 此时这里用...args是分散传入的
  delete ctx.key;
  return result // 如果返回结果，还需要将结果返回
}
```


## 手写apply
```javascript
Function.prototype.myApply = function (context) {
  var context = context || window;

  context.fn = this;
  var result;
  // apply是用数组包裹传参
  result = context.fn(...arguments[1]);
  
  delete context.fn;
  return result;
};
```


## 手写bind
```javascript
Function.prototype.myBind = function (context) {
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  var _this = this;
  var args = [...arguments].slice(1);
  // 返回一个函数
  return function F() {
    // 因为返回了一个函数，我们可以 new F()，所以需要判断
    if (this instanceof F) {
      return new _this(...args, ...arguments);
    }
    return _this.apply(context, args.concat(...arguments));
  };
};
```

