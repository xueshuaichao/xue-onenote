

 ## 手写filter
 简单写法
  ```javascript
// 精髓是让每一项执行filter函数，并返回数组
Array.prototype._filter = function (callback) {
  const newArr = [];
  this.forEach((item) => {
    if (callback(item)) {
      newArr.push(item);
    }
  });
  return newArr;
};
```

```javascript
Array.prototype._filter = function (callback, thisArg) {
  if (typeof callback !== "function") {
    throw Error("参数必须是一个函数");
  }
  console.log(thisArg);
  //定义一个返回结果的数组
  const filteredArray = [];
  const thisContext = thisArg || globalThis;
  //遍历数组的每一个元素
  for (let i = 0; i < this.length; i++) {
    //使用call方法将this绑定到thisContext上，并传入当前元素和索引
    if (callback.call(thisContext, this[i], i, this)) {
      //如果回调函数返回true，将当前元素添加到结果数组中
      filteredArray.push(this[i]);
    }
  }
  return filteredArray;
};
const nums = [1, 2, 3, 4, 5, 6, 7, 8];
const filterNum = nums._filter((num) => num > 5);
console.log(filterNum);
```