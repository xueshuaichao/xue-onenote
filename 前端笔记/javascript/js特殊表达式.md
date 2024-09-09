
ECMAScript 2020（ES2020）标准引入了三个新的语法特性：?? 运算符、?. 运算符和 ?. 运算符，用于简化代码编和处理可能的空值情况。

 ### 空值处理的挑战
在编程中，经常会遇到处理可能为空的值的情况，例如在访问对象属性或调用函数时。在传统的JavaScript中，我们通常使用长短路运算符（如）或条件语句（如if-else）来处理空值情况。然而，这些方法在编写代码时会显得冗长，可读性较差，并且容易出错。为了解决这个问题，ES2020引入了新的语法特性。

 ### 解决方案1：?? 运算符
基本用法
?? 运算符（空值合并运算符）可以用来判断一个值是否为null或undefined，并提供一个默认值。
其语法为：value1 ?? value2，如果value1是null或undefined，则返回value2；否则返回value1的值。

下面是一个示例代码：
```javascript
const x = null;
const y = 10;
const result = x ?? y;

console.log(result); // 输出 10

```

 ### 与 || 运算符的区别
|| 运算符只能判断一个值是否为 “false”（例如：null、undefined、false、0、‘’），而 ?? 运算符能够精确地判断一个值是否为null或undefined。
```javascript
const x = 0;
const y = 10;
const result1 = x || y; // 使用 || 运算符
const result2 = x ?? y; // 使用 ?? 运算符

console.log(result1); // 输出 10
console.log(result2); // 输出 0

```

 ### 解决方案2：?. 运算符
?. 运算符（可选链运算符）可以简化对可能为null或undefined的值进行属性访问或方法调用的代码。其语法为：object?.property 或 object?.method()。

?运算符与.运算符类似，但它们之间有一些关键的区别。如果对象的某个属性或方法不存在，. 运算符会抛出一个TypeError，而?. 运算符会返回undefined，不会导致程序崩溃。
```javascript
const obj = {
  foo: null
};

const result1 = obj.foo.bar; // 使用 . 运算符
const result2 = obj?.foo?.bar; // 使用 ?. 运算符

console.log(result1); // TypeError: Cannot read property 'bar' of null
console.log(result2); // 输出 undefined

```










