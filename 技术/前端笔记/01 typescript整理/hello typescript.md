
TypeScript 只会进行静态检查，如果发现有错误，编译的时候就会报错。

TypeScript 是 JavaScript 的一个超集，主要提供了类型系统和对 ES6 的支持，它由 Microsoft 开发

TypeScript 是 JavaScript 的类型的超集，它可以编译成纯 JavaScript。编译出来的 JavaScript 可以运行在任何浏览器上。TypeScript 编译工具可以运行在任何服务器和任何系统上。

 ## 为什么选择 TypeScript
1. TypeScript 增加了代码的可读性和可维护性
2. 可以在编译阶段就发现大部分错误，这总比在运行时候出错好

 ## TypeScript 的缺点
1. 有一定的学习成本，需要理解接口（Interfaces）、泛型（Generics）、类（Classes）、枚举类型（Enums）等
2. 短期可能会增加一些开发成本，毕竟要多写一些类型的定义，不过对于一个需要长期维护的项目，TypeScript 能够减少其维护成本


 ## 安装typescript
TypeScript 的命令行工具安装方法如下：
```javascript
npm install -g typescript
```

以上命令会在全局环境下安装 tsc 命令，安装完成之后，我们就可以在任何地方执行 tsc 命令了。
```javascript
tsc hello.ts
```







