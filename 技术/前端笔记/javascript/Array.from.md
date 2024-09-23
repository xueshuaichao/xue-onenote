
 # JS学习之Array.from() 五个超好用的用途

  ## 概念
Array.from用于将两类对象转为真正的数组：类似数组的对象和可遍历对象（数组、类数组对象、字符串、map 、set 等可迭代对象）。

1. 

```javascript
// 从字符串创建数组
Array.from('Hey'); // => ['H', 'e', 'y']
// 从 Set 创建数组
Array.from(new Set(['one', 'two'])); // => ['one', 'two']

const map = new Map();
map.set('one', 1)
map.set('two', 2);
Array.from(map); // => [['one', 1], ['two', 2]]
```

```javascript
// 从类数组对象创建数组
let arrayLike = {0: 'a', 1: 'b', 2: 'c', length: 3};
let arr = Array.from(arrayLike);
console.log(arr); // 输出: ['a', 'b', 'c']
```