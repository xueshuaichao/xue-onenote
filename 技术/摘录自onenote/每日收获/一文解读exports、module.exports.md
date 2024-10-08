
## 一文解读exports、module.exports

第一部分：exports 和 module.exports
为了让Node.js的文件可以相互调用，Node.js提供了一个简单的模块系统。模块是Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个 Node.js 文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。
1. exports
1.1 导出模块
exports 对象是由模块系统创建的。在我们自己写模块的时候，需要在模块最后写好模块接口，声明这个模块对外暴露什么内容，exports 提供了暴露接口的方法。如下代码示例：
```javascript
//hello.js
var sayHello = function () {
    console.log('hello')
}
var sos = 110;
var app = {
    name: 'testApp',
    version: '1.0.0',
    help: function () {
        console.log('what can i do for you?')
    }
}
//导出一个方法
exports.sayHello = sayHello;
//导出一个变量
exports.sos = sos;
//导出一个JSON对象
exports.app = app;

//导出一个方法
module.exports.sayHello = sayHello;
//导出一个变量
module.exports.sos = sos;
//导出一个JSON对象
module.exports.app = app;
```
或者写成下面的形式：
```javascript
//hello.js
exports.sayHello = function () {
    console.log('hello')
}
exports.sos = 110;
exports.app = {
    name: 'testApp',
    version: '1.0.0',
    help: function () {
        console.log('what can i do for you?')
    }
}
```

1.2 引入模块
```javascript
//main.js
var hello = require('./hello');
//调用模块hello中的方法
hello.sayHello();
//调用模块hello中的变量
console.log(hello.sos)
console.log(hello.app.version)
//调用模块hello中的JSON对象属性
hello.app.help()
```
Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。
将上边的exports换成module.exports，得到一样结果，所以这么来看，两者是一样的





2. module.exports
2.1 导出模块
有时候我们希望把一个对象封装到模块中，格式如下：
```javascript
//hello.js 
function Hello() {
    var name;
    var sos = '110';
    this.setName = function (thyName) {
        name = thyName;
    };
    this.sayHello = function () {
        console.log('Hello ' + name);
    };
    this.app = {
        name: 'testApp',
        version: '1.0.0',
        help: function () {
            console.log('what can i do for you?')
        }
    };
};
// 把变量、方法、JSON对象等封装在一起，一并导出
module.exports = Hello;
```
2.2 引入模块
```javascript
//main.js
var Hello = require('./hello')
//通过new关键字，实例化一个hello模块的对象，通过这个对象才能调用hello模块相关的方法。
hello = new Hello();

hello.setName("zhangSan")
hello.sayHello()

console.log(hello.app.version)
hello.app.help()

如果将上述 module.exports = Hello; 改为 exports = Hello则报错
```
说说他们之间的区别
• exports只能使用语法来向外暴露内部变量：如http://exports.xxx = xxx;
• module.exports既可以通过语法，也可以直接赋值一个对象。

我们要明白一点，exports和module.exports其实是一个东西
console.log(module.exports===exports);
//输出结果为：true
因为他们是引用类型的一个变量名，所以当exports再指向一个引用类型的时候，那么他们就不再全等。
exports=[0,1];
console.log(exports===module.exports);
//输出结果为：false

当然，如果直接通过http://exports.xxx的形式赋值，那么他们依然会指向同一个地址：
exports.array=[0,1];
console.log(exports===module.exports);
//输出结果为：true

那么我们再来说为什么module.exports可以赋值一个对象，而exports却不可以。要明白这点，就要从nodejs的模块化说起，当nodejs执行模块中的代码时，它会将模块中的代码，用一个函数进行包裹：
function(exports,require,module,__filename,__dirname){}

这里面的其他参数就在这篇文章中不仔细讲解了，不过可以发现，里面有个熟悉的参数module。这里就要说到exports的本质了，正如上面所说exports = module.exports，也就是说他们指向了堆空间的同一个东西，如果对exports进行赋值，那么exports的指向就不一样了，在另外的文件里面就无法再找到通过exports这个变量传递的东西，而module.exports是在执行模块代码中就将module传入到了函数中，所以即使module.exports的值改变也能够在其他文件中进行调用。

再写到这里的时候我产生了一个疑问，如果将module.exports的指向改变，那么通过http://exports.xxx传递的值在其他文件中还能进行调用嘛，于是我尝试了下面的代码：
//test.js
exports.add=100;
module.exports=1;
//test1.js文件
let test=require("./test");
let p=test.add;
let b=test;
console.log("p的值是："+p);
console.log("b的值是："+b);
/*
输出结果是：
p的值是：undefined
b的值是：1
*/
可以看出，改变了module.exports的指向后，http://exports.xxx的值在其他文件中也无法调用。

再试
//test.js
exports=100;
//test1.js文件
let test=require("./test");
console.log（test);
/*
输出结果是：
{}
*/

为了避免歧义，一般都用module.exports


