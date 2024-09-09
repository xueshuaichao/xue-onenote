 ## TS中declare的简单使用方法

> declare 关键字用来告诉编译器,某个类型是存在的,可以在当前文件中使用,本文给大家介绍TS中declare的简单使用方法,感兴趣的朋友一起看看吧

 ### .d.ts的顶级声明必须以declare开头
> 以declare声明的变量和模块后，其他地方不需要引入，就可以直接使用了
 注意我们需要在配置文件下，引入声明文件
```javascript
{
    "compilerOptions": {
        "include": ["src/**/*.ts"，"src/**/*.d.ts"，"src/**/*.tsx"，"src/**/*.vue"]
    }
}

```

 ### 声明一个类型
```javascript
declare type Asd {
    name: string;
}
```
在include包含的文件范围内可以直接使用Asd这个type

 ### declare声明一个模块
```javascript
declare module '*.css';
declare module '*.less';
declare module '*.png';
```
这样，我们可以在ts中引入相关的文件而不报错了

 ### declare声明一个变量
```javascript
declare var jQuery:(selector:string) => any;// 声明变量直接使用
jQuery("#box")
```

对于引入第三方的库特别有效


 ### 声明一个作用域
```javascript
 declare namespace API{
    interface ResponseObj {

    }
}
```
>注意
- declare 与export 不要同级使用，不然的话，声明文件就需要导入了
- 在声明文件中 type 与 interface 也可以不用加declare ，效果相同
```javascript
type myType = string | number;
// 两者效果相同
declare type myType = string | number;
```