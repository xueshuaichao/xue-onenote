
内置的函数没有prototype属性，因为prototype是用来继承的，而内置函数不可能用来继承

### Object.prototype中成员的介绍
1. constructor属性，指向当前的构造函数
```js
console.log(Object.prototype.constructor==Object);
```
2. hasOwnProperty
判断属性是不是对象自身提供的，如果是就返回：true，
```js
var obj={age:19};
console.log( obj.hasOwnProperty('age') );   true
console.log( obj.hasOwnProperty('toString') );  false
```

   
3. isPrototypeof 

判断原型对象是不是实例对象的原型对象，如果是就返回true。
准确来说：只有前面对象在后面对象的原型链上，就为true。
```js
var Person = function() {
	this.name = '小明';
};
var p =new Person();

 console.log( Person.prototype.isPrototypeOf(p) );		// true
console.log( Object.prototype.isPrototypeOf(Person.prototype ) );  //true	
```



4. toLocalString 转换为本地内容
```js
toString 转化为字符串
var d=new Date();
console.log(d.toString());
console.log(d.toLocalString()); 
```
  

5. instanceof 运算符
语法： 实例对象 instanceof (构造函数)
用来检测构造函数prototype属性的值是否在被检测对象的原型链上 
规律：在创建对象后，没有修改prototype的值，结果就为：true,修改了就为false。
```js
var Person=function(){};
var p=new Person();
console.log(p instanceof Person); true;
如果 Person.prototype={};
console.log(p instanceof Person); false;

！！所以会有判断是不是数组的方式
console.log(arr instanceof Array) 但是这种方法不严谨

Object.prototype 在任何一个对象的原型链上，所以结果为：true
console.log(p instanceof Object);  true
console.log([] instanceof Object); true   
```

### 函数创建的三种方式

1.函数声明
function fn(){};

2. 函数表达式
var fn=function(){};

3. new Function();   一般不用这种方式
```js
  var foo=function(num1,num2){
console.log(num1+num2);
  }
  var fn=new Function('num1','num2','console.log(num1+num2)');
  fn(10,20);
```
   

### 代码块和对象字面量
花括号在js中有两种解析方式：
1 被解析为：代码块
2 被解析为：对象字面量
具体被解析为哪一种，是由js引擎 词法分析 的结果



### 函数的原型链

因为函数也是对象，说明函数也是 __proto__ 属性
 实际上，函数既有：prototype属性 也有 __proto__ 属性
```js
var fn=new Function();
console.log(Function.prototype); 函数对象
console.log(Function.__proto__.__proto__) Object;
```

### 以下全为false
```js
var arr=new Array();
var newArr=[];
console.log(arr==newArr);   //虽然arr也是数组，但因为不是同一个，所以为false
console.log([]===[]);   //和上边一样


var obj=new Object();
var newobj={};
console.log(obj===newobj);//和上边一样  
```

### eval 的用法
作用：就是将字符串解析成代码执行
```js
eval('var num=123')
console.log(num)   //123
```
