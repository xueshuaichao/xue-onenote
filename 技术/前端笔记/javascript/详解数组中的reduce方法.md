reduce的原理
将这个方法定义为数组的归并方法，这个方法和迭代方法（map,forEach,filter...）一样，都会对数组进行遍历，reduce与他们不同的是函数的第一个参数得到的是迭代计算后的效果

语法
 这个方法接收两个参数：
要执行的函数，要执行的函数中也可传入参数，分别为
prev：上次调用函数的返回值
cur：当前元素
index：当前元素索引
arr：被遍历的数组
函数迭代的初始值
举例
1.没有设置函数的初始迭代值
```javascript
let arr = [1, 2, 3, 4];
let sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
})
console.log(arr, sum);
```
运行结果：

分析：
 我们可以看到，在这里reduce的作用就是对这个数组进行求和，迭代了3次，函数迭代的初始值是1，也就是默认值（数组的第一项），prev的值是每次计算后的值，现在理解了吧！

设置初始迭代值
```javascript
let arr = [1, 2, 3, 4];
let sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
},5)
console.log(arr, sum);
```
运行结果：

分析：
 这里我们添加了一个初始的迭代值，也就是让prev从5开始计算，可以看到，这里迭代了4次，结果也加上了初始值。

reduce的应用
初级应用
 最常见的应用一般就是求和以及求乘积了，比如说下面的例子：
```javascript
let arr = [1,2,3,4,5]
console.log(arr.reduce((a,b) => a + b))//15
console.log(arr.reduce((a,b) => a * b))//120
```

高级应用
计算数组中每个元素出现的次数
```javascript
let arr = ['name','age','long','short','long','name','name'] 

let arrResult = arr.reduce((pre,cur) =>{
    console.log(pre,cur)
    if(cur in pre){
        pre[cur]++
    }else{
        pre[cur] = 1
    }
    return pre
},{})

console.log(arrResult)//结果：{name: 3, age: 1, long: 2, short: 1}
```
运行结果：（第一个console.log）

去除数组中重复的元素
```javascript
let arrResult = arr.reduce((pre,cur) =>{
    if(!pre.includes(cur)){
        pre.push(cur)
    }
    return pre;
},[])

console.log(arrResult)//结果：["name", "age", "long", "short"]
```
对对象的属性求和

```javascript
let person = [
    {
        name: 'xiaoming',
        age: 18
    },{
        name: 'xiaohong',
        age: 17
    },{
        name: 'xiaogang',
        age: 19
    }
]

let result = person.reduce((a,b) =>{
    a = a + b.age;
    return a;
},0)

console.log(result)//结果：54
```

总结
 使用reduce操作数组时，最重要的就是理解第一个参数是怎么迭代的，可以好好利用初始化这个参数的数据类型来减少很多不必要的代码。上面举的三个高级应用的例子都是利用了这个优点，当然，reduce还有更多的应用，后面碰到还会进行补充的。
