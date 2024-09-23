
 ## 1.reduce语法说明

reduce() 方法对数组中的每个元素执行一次提供的回调函数，且该函数为升序执行，并将其结果汇总为单个返回值。

 ## 1.2 参数说明
```javascript
let value = arr.reduce(function(accumulator, currentValue, currentIndex, array) {
  // ...
}, [initial]);

```
 第一个参数：callback函数。该函数会遍历并应用于所有数组元素，并将其结果带到到下一个调用。此回调函数包含四个参数：

- accumulator：累计器（必需）。是上一个函数调用的结果，第一次等于 initial（如果提供了 initial 的话）
- currentValue：当前元素（必需）。数组中正在处理的元素。
- currentIndex：当前处理元素的索引（可选）。`如果提供了initialValue，则起始索引号为0，否则从索引1起始。`
- array：原始数组（可选）。

第二个参数：initialValue初始值（可选）

 ### 注意

- 如果没有提供initialValue：accumulator取数组中的第一个值，currentValue取数组中的第二个值。reduce 会从索引1的地方开始执行 callback 方法，跳过第一个索引。

- 如果提供了initialValue：accumulator取值为initialValue，currentValue取数组中的第一个值。reduce 会从从索引0开始执行 callback 方法。

 # 简单示例：

1. 累加
```javascript
let arr = [1, 2, 3, 4, 5];
let result = arr.reduce((sum, current) => sum + current, 0);
console.log(result); // 15
```

2. 找最大值
```javascript
const result = [1, 2, 3, 2, 1].reduce((pre, cur) => Math.max(pre, cur));
console.log(result);
```

3. //数组去重
```javascript
const resultList = [1, 2, 3, 2, 1].reduce((preList, cur) => {
if (preList.indexOf(cur) === -1) {
  preList.push(cur);
}
return preList;
}, []);
console.log(resultList);
```

4. // 归类
```javascript
const dataList = [
  { name: "aa", country: "china" },
  {
    name: "bb",
    country: "china",
  },
  {
    name: "cc",
    country: "USA",
  },
  {
    name: "dd",
    country: "EN",
  },
];
const resultobj = dataList.reduce((preobj, cur) => {
  const { country } = cur;
  if (!preobj[country]) {
    preobj[country] = [];
  }
  preobj[country].push(cur);
  return preobj;
}, {});
console.log(resultobj);

//结果为
{
  "china":[{"name":"aa","country":"china"},{"name":"bb","country":"china"}],
  "USA":[{"name":"cc","country":"USA"}],
  "EN":[{"name":"dd","country":"EN"}]
}
```

 5. // 字符串反转
```javascript
const str = "hello world";
const resultStr = Array.from(str).reduce((pre, cur) => {
  return `${cur}${pre}`;
}, "");
console.log(resultStr);
```

6. 数组扁平
```javascript
const flatArr = (arr) => {
  return arr.reduce(
    (acc, cur) => acc.concat(Array.isArray(cur) ? flatArr(cur) : cur),
    []
  );
};
```   

      
7. 数字千分化
```javascript
function ThousandNum(num = 0) {
    const str = (+num).toString().split(".");
    const int = nums => nums.split("").reverse().reduceRight((t, v, i) => t + (i % 3 ? v : `${v},`), "").replace(/^,|,$/g, "");
    const dec = nums => nums.split("").reduce((t, v, i) => t + ((i + 1) % 3 ? v : `${v},`), "").replace(/^,|,$/g, "");
    return str.length > 1 ? `${int(str[0])}.${dec(str[1])}` : int(str[0]);
}

ThousandNum(1234); // "1,234"
ThousandNum(1234.00); // "1,234"
ThousandNum(0.1234); // "0.123,4"
ThousandNum(1234.5678); // "1,234.567,8"
``` 

      
















