 # Typescript

###  interface和type的区别

- 都能描述对象，但 type 还能描述其他任意类型，例如 string、number 等基本类型、联合或交叉等类型。


```javascript
// 都能描述对象
interface IPerson {
  name: string
  age: number
}
type TPerson ={
  name: string
  age: number
}
const person: IPerson = {
  name:'i47',
  age: 18
}
```
联合类型
```javascript
// 期望描述一个性别，可能是数字或字符串
type 字符串或数字 = string | number
const sex:字符串或数字 = 0
```

- 都能进行类型拓展，interface 通过 extends 来实现，type 通过 & 交叉运算符号形成交叉类型。

interface
```javascript
interface I2d {
  x: number
  y: number
}

interface I3d extends I2d {
  z: number
}

const the3: I3d ={
  x:4,
  y:7,
  z:5
}
```

type
```javascript
type T2d={
  x: number
  y: number
}
type T3d = T2d & {
  z: number
}
const the3: T3d ={
  X:4,
  y:7,
  z:5
}
```

1. 名字相同时的表现，相同的 interface 会合并，相同的 type 会报错。

```javascript
interface IPerson {
  name: string
  age: number
}
interface IPerson {
  money: number
}
const person: IPerson ={
  name: 'elser',
  age: 18,
  money: 888
}
```

总结： 一般应该怎样去用  
个人一般使用 interface 来描述对象结构，用 type 来描述类型之间的关系
```javascript
interface IPerson {
  name: string
  age: number
}
type TTemp ='男' |'女'|0|1
```


### ts相关面试题
- Typescript相较于JavaScript有什么优势和劣势？

- const func = (a, b) => a + b; 要求编写Typescript，要求a，b参数类型一致，都为number或者都为string

- 实现ReturnType

- 实现DeepReadOnly

 ### 基于已有类型生成新类型：剔除类型中的width属性
```javascript
interface A {
  content: string;
  width: number;
  height: number;
}
```

方法一：通过在子接口中声明一个同名属性来覆盖父接口中的属性。
```javascript
interface ParentInterface {  
  requiredProperty: string;  
  optionalProperty: any; // 可以是任意类型  
}  
  
interface ChildInterface extends ParentInterface {  
  requiredProperty: string;  
  optionalProperty?: any; // 重写 optionalProperty 属性  
}  
```

通过Omit 踢出一个元素
```js
interface Test {
    a: string;
    b: number;
    c: boolean;
}

// Omit a single property:
type OmitA = Omit<Test, "a">; // Equivalent to: {b: number, c: boolean}

// Or, to omit multiple properties:
type OmitAB = Omit<Test, "a"|"b">; // Equivalent to: {c: boolean}
```