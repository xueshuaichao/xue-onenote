- 需要理解接口（Interfaces）、泛型（Generics）、类（Classes）、枚举类型（Enums）

1. 解释TypeScript中联合类型的概念并提供示例。‌
联合类型允许一个变量有多种类型。‌它通过使用|来表示类型之间的符号。‌这允许变量存储任何指定类型的值。‌例如：‌
```javascript
function printId(id: number | string): void {
  console.log(`ID:${id}`);
}
printId(123); // Output: "ID: 123"
printId('abc'); // Output: "ID: abc"
```

2.TypeScript中的类型断言是什么？‌举个例子。‌
类型断言允许您显式告诉编译器变量的类型，‌当无法自动推断类型时使用。‌这可以通过<type>或as type语法实现。‌例如：‌
```javascript
let length: any = '5';
let numberLength: number = <number>length; // Using <type> syntax
let stringLength: number = length as number; // Using "as type" syntax
```

3. 描述TypeScript的类型推断机制如何工作。‌

TypeScript的类型推断是指编译器在没有显式类型注释的情况下自动推断和分配类型的能力。‌虽然鼓励显式类型，‌但编译器会尽可能使用上下文（‌如变量初始化、‌返回语句等）‌来推断类型。‌

4.什么是类型防护，‌如何创建自定义类型防护？‌

类型保护是执行运行时检查并缩小条件块内类型范围的表达式。‌常见的类型保护包括typeof和instanceof。‌自定义类型保护是一个函数，‌其返回类型是使用is关键字缩小类型的类型谓词，‌例如function isFish(pet: Fish | Bird): pet is Fish。‌

5.讨论TypeScript中声明合并的工作原理。‌

声明合并是指编译器将多个同名的声明合并到一个定义中。‌此功能对于接口非常强大：‌如果多次定义一个接口，‌TypeScript会将其视为具有组合成员的单个接口。‌这在扩展现有类型或使用模块化代码时非常有用。‌

6.解释在高级类型场景中如何以及为何使用
keyof和typeof运算符。‌
keyof运算符生成给定类型的已知公共属性名称的并集，‌这对于限制可能的字符串值或创建映射类型很有用。‌而typeof运算符用于获取变量的类型信息，‌这在某些类型操作中可能很有用12。‌


2、TypeScript 中的原始类型有哪些 ？






3、这是数组使用的两种方式？
```javascript
// 还可以使用以下简写语法创建数组
let values: number[]=[15,20,25,30];
// Typescript 提供了另一种语法来指定 Array 类型
let values: Array<number>=[15，20，25,30];
```



5、什么是void，什么时候使用void类型 ？

void 表示变量没有类型，它充当与任何相反的类型，它在不返回值的函数中特别有用
如果变量是 void 类型，则只能将 null 或 undefined 值分配给该变量。
```javascript
function notify(): void {
  alert("Hello world !");
}
```

10、说说枚举在 TypeScript 中是如何工作的 ？
枚举允许我们创建命名常量，这是一种为数字常量值赋予更友好名称的简单方法
枚举由关键字 enum 定义，后跟其名称和成员。

13、TypeScript 中控制成员可见性有几种方法 ？
TypeScript 提供了三个关键字来控制类成员的可见性
- public：您可以在 class 外的任何地方访问公共成员。默认情况下，所有类成员都是公共的。
- protected：受保护的成员仅对包含该成员的类的子类可见。不扩展容器类的外部代码无法访问受保护的成员。
- private：私有成员仅在类内部可见，没有外部代码可以访问类的私有成员。

14、TypeScript 支持静态类吗 ？为什么 ？

TypeScript 不支持静态类，这与流行的 C# 和 Java 等面向对象的编程语言不同。  
这些语言需要静态类，因为所有代码，即数据和函数，都需要在一个类中并且不能独立存在。静态类提供了一种方法来允许这些功能，而无需将它们与任何对象相关联。在 TypeScript 中，您`可以将任何数据和函数创建为简单对象`，而`无需创建包含类`。因此 `TypeScript 不需要静态类`，单例类只是 TypeScript 中的一个简单对象。




