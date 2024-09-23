reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
reduce() 可以作为一个高阶函数，用于函数的 compose。

```javascript
var numbers = [65, 44, 12, 4];
function getSum(total, num) {
  return total + num;
}
function myFunction(item) {
  document.getElementById("demo").innerHTML = numbers.reduce(getSum);
}
```
reduce()方法接收一个函数作为累加器，reduce为数组中的每一个元素依次执行回调函数，接收四个参数：初始值（上一次回调返回的值），当前元素，当前索引，原数组。
语法：reduce（callback， [initialValue]
callbck包含四个参数：
• previousvalue：上一次回调函数的返回值，或者提供的初始值（initialValue）
• currentValue: 数组中当前被处理的元素
• index： 当前索引
• array： 原数组

需要注意的是：当提供了初始值initialValue，则第一次执行回调函数时previousvalue就是initialValue，则currentValue是数组第一项，如果没有提供初始值，则previousvalue是数组第一项，currentValue是数组第二项。
使用reduce方法可以完成多维度的数据叠加
利用reduce来计算一个字符串中每个字母出现次数：
```javascript
const str = "jshdjsihh";
const obj = str.split("").reduce((pre, item) => {
  pre[item] ? pre[item]++ : (pre[item] = 1);
  return pre;
}, {});
console.log(obj); // {j: 2, s: 2, h: 3, d: 1, i: 1}
```