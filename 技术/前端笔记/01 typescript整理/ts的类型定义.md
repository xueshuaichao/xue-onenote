
TS中常用的基本类型可以细分为两类：1. js已有类型，2.ts新增类型。
JS 已有类型（原始类型）：
布尔值、数值、字符串、null、undefined、Symbol
JS 已有类型（对象类型）：
object、array、function


TS 新增类型：
字面量	限制变量的值就是该字面量的值
any	任意类型
unknown	类型安全的any
void	没有值
never	不能是任何值
tuple	元组，固定长度数组
enum	枚举
type	类型别名
interface 接口

2.1、联合类型（|）
由两个或多个其他类型组成的类型，表示可以是这些类型中的然后一种。
```javascript
// 可以使用 | 来连接多个类型（联合类型）
let b: "male" | "female";
b = "male";
b = "female";

let c: boolean | string;
c = true;
c = "hello";
```

2.2、交叉类型（&）
类似于接口继承（extends），用于组合多个类型为应该类型（常用于对象类型）
```javascript
interface Person {name: string};
interface Contact {phone: string};
type PersonDetail = Person & Contact
let obj: PersonDetail = {
	name: 'jack',
	phone: '15698324'
}
// 使用交叉类型后，新的类型PersonDetail就同时具备了Person和Contact的所有属性类型。
// 相当于：
type PersonDetail = {name: string; phone: string;}

```
2.3、索引签名类型（[key: type]: type）
使得对象中可以出现任意多个属性
```javascript
// [propName: string]: any 表示任意类型的属性
let h: {name: string, [propName: string]: any};
h  = {name: "张三", age: 13, gender: "男"};


/*
	1.  使用[key: string]来约束该接口中允许出现的属性名称。
	2. 表示只要是string类型的属性名称，都可以出现在对象中。
	3. 这样，对象 obj 中就可以出现任意多个属性
	4. key 只是一个占位符，可以换成任意合法的变量名称。
	5. 须知：js中对象的键是 string 类型的。
*/
interface AnyObject {
	[key: string]: number;
}
let obj: AnyObject = {
	a: 1,
	b: 2,
}
```
2.4、任意类型（any）
any 表示任意类型，一个变量设置类型为 any 后相当于对该变量关闭了TS的类型检查（使用TS时，不建议使用 any 类型）
声明变量如果不指定类型，则TS解析器会自动判断变量的类型为 any
```javascript
let d;			// 隐式的any
let d: any;		// 显式的any
d = 10;
d = "hello";
d = true;
let dd: string;
dd = d; // d的类型是any，它可以赋值给任意变量，并改变dd的类型
```

2.5、未知的值（unknown）
unknown 表示未知的值， 实际上就是一个类型安全的any
```javascript
// unknown 类型的变量，不能直接赋值给其他变量
let e: unknown;
e = 10;
e = "hello";
e = true;
let ee: string;
ee = e; // d的类型是unknown，赋值给ee会报错
// 如果需要赋值并不报错，可以先进行类型判断
if(typeof ee === "string"){
	ee = e; // 不会报错
}

```

2.6、空值（void）
void 表示没有任何类型
当一个函数返回空值时，它的返回值为 void 类型。
```javascript
// 以函数为例，就表示没有返回值的函数
function fn(): void{
	console.log('仅打印');
}
```

2.7、无值（never）
never 表示永远不存在的值的类型
但是，当一个函数永不返回时（或者总是抛出错误），它的返回值为 never 类型。
```javascript
function fun(): never{}

let foo: never = 123; // Error: number 类型不能赋值给 never 类型

// ok, 作为函数返回类型的 never
let bar: never = (() => {
  throw new Error('Throw my hands in the air like I just dont care');
})();
```

2.8、元组（tuple）
元组：固定长度的数组
```javascript
// 语法：[类型，类型，类型]
let l: [string, number];
l = ["hello", 123]

```

2.9、类型别名（type）
```javascript
// 类型的别名
type myType = 1 | 2 | 3;
let o1: myType;
let o2: myType;
let o3: myType;
```

2.10、枚举（enum）
```javascript
// enum 枚举
enum Gender{
	Male = 0,
	Female = 1
}
let m: {name: string, gender: Gender};
m = {
	name: "王五",
	gender: Gender.Male	// 0
}
console.log(m.gender === Gender.Male);

```

2.11、接口（interface ）
```javascript
// 接口: 主要为了实现对象的复用。
// {} 用来指定对象中可以包含哪些属性
// 语法：{属性名：属性值，属性名：属性值}
// 在属性名后面加上？，表示属性是可选的
interface  PeosonType = {name: string, age?: number}
let g: PeosonType;
g = {name: "张三", age: 13};
g = {name: "张三"};		// 没有？号就会报错
```

2.12、泛型

2.13、字面量类型
你可以使用一个字符串字面量作为一个类型：
```javascript
let foo: 'Hello';
foo = 'Bar'; // Error: 'bar' 不能赋值给类型 'Hello'

// 通常在联合类型中使用
type CardinalDirection = 'North' | 'East' | 'South' | 'West';

function move(distance: number, direction: CardinalDirection) {
  // ...
}

move(1, 'North'); // ok
move(1, 'Nurth'); // Error

```
其他字面量类型：
```javascript
type OneToFive = 1 | 2 | 3 | 4 | 5;
type Bools = true | false;

```





