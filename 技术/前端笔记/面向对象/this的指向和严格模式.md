### 求一下例子中this的指代
```js
var obj = {
    say: function() {
      console.log(this);
    }
};
```
1. 这种情况下，小括号无效，相当于没有小括号的情况
(obj.say)(); // 相当于 obj.say();  this指向obj

2. 赋值表达式，赋值表达式的值由等号右边的值来决定，等号右边的值就是：函数
```js
// 此时，就是以函数模式调用的
(obj.say = obj.say)(); // window
```

3. 当前逻辑或表达式的值 是等号右边的值，也是一个函数，所以，也是以函数模式
```js
// 调用的，this === window
(false || obj.say)(); // window*/
```

### 辨别一下三种方式的异同
1
```js
setTimeout(function() {
  console.log(this); // window
}, 1000);
```

2  最终这个函数还是由浏览器来调用的，所以，内部的this还是指向 window
setTimeout(obj.say, 1000); // this 指向window;

3 
```js
setTimeout(function () {
  console.log(this === window);
  // 方法调用模式，所以，方法内部的this指向了当前对象
  obj.say();
}, 1000);
```

EC5内容补充

严格模式
开启严格模式：
1 开启严格模式必须要写在程序的第一行, 才会生效
2 一般情况下只会在某个函数内部开启严格模式，因为严格模式与作用域关联，只对函数内部的作用域起作用！
'use strict';
使用严格模式的好处：
1 有利于开发人员向新的语言规范过度
2 提高了代码运行的效率（严格模式中执行效率高）
```js
(function () {
  // 只在沙箱内部开启严格模式
  "use strict";

  // 1 使用未声明的变量，会报错
  num = 123;

  // 2 使用 with 语句，作用：会改变当前js执行的上下文
  // 因此，这个语句会造成性能问题，所以，也不推荐使用！

  var obj = {
    name: 'xiaoming',
    age: 19
  };

  // console.log( obj.name )
  // console.log( obj.age )
  with( obj ) {
    // 告诉 js引擎，将当前执行上下文切换为 obj
    // 因此，接下来访问 name 属性，就相当与访问 obj.name
    // console.log( obj.name );
    console.log( name );
    console.log( age );
  }

  console.log( obj.name );*/

  // 3 严格模式中不能删除声明的变量
  // var obj = {};
  // delete obj;
  // console.log( obj )

  // 4 不能在 语句块 中使用函数声明，否则会报错

  if (true) {
    function fn() {} //不可行
    var fn = function () {
      //可行
      console.log(1123);
    };
  }
  fn();
})();
```
 		
    		
