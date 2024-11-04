​
### 1.CSS实现垂直水平居中
 1. flex布局
```css
#dv1{
  width: 500px;
  height: 500px;
  border: 1px solid red;
  /*是在父元素上添加这些属性，而不是子元素*/
  display: flex;
  justify-content: center;
  align-items: center;
}
```

1. 通过transform移动
```css
#dv1 {
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%; -50%);
/* margin-top:-100px ; 
margin-left: -100px; */
}
```

2.使用Grid(网格)布局
```css
display:grid;
place-items:center;
```

### 10.如何实现多栏布局(左右固定宽度，中间自适应)
1. calc计算属性
2. flex布局
```css
flex: 1;
```
3. grid网格布局

```css
display: grid;
grid-template-columns: 1fr 200px 1fr;
```
1. CSS浮动
第一个float:left，第二个float:right，第三个设置margin-left和margin-right
直接这么设置就行，不需要什么特殊的操作
```css
#dv1 {
border: 1px solid red;
margin-left: 100px;
margin-right: 100px;
height: 100px;
}

<div id="dv1">
</div>
```
 

### 2、px和em和rem的区别
- px的值是固定的，指定是多少就是多少。
- em是一种相对长度单位，它基于父元素的字体大小而定，em的值表示当前元素的字体大小的倍数。
- rem是相对于根节点的字体大小而定

### 3、什么是CSS Hack?
一般来说是针对不同的浏览器写不同的CSS,就是 CSS Hack。
IE浏览器Hack一般又分为三种，条件Hack、属性级Hack、选择符Hack
```css
// 1、条件Hack
<!--[if IE]>
  <style>
                .test{color:red;}
  </style>
<![endif]-->

// 2、属性Hack
.test{
color:#090\9; /* For IE8+ */
*color:#f00;  /* For IE7 and earlier */
_color:#ff0;  /* For IE6 and earlier */
}

// 3、选择符Hack
* html .test{color:#090;}       /* For IE6 and earlier */
* + html .test{color:#ff0;}     /* For IE7 */
```



### 4、绝对定位和相对定位的区别
- 绝对定位:是相对于元素最近的已定位的祖先元素(包括绝对定位，相对定位)，如果没有，那么它的位置则是相对于body
- 相对定位:相对于元素在文档中的初始位置

### 5、重绘和重排(回流)的区别
重绘不一定重排，重排必定导致重绘
- 重绘：指一个元素外观被改变会导致绘制，比如改变元素的背景色、文字颜色，字体大小
- 重排 ：当渲染树的部分节点更新，浏览器会重新构造渲染树引发重排：
- 1、页面渲染初始化
- 2、添加、删除可见的dom
- 优化
1. 将多次改变样式属性的操作合并成一次操作，减少DOM访问。
2. 为动画效果的元素设置绝对定位，修改样式就不会进行重绘。
3. 对隐藏的元素操作不会引发其他元素的重排。如果要对一个元素进行复杂的操作时，可以先隐藏它，操作完成后再显示。这样只在隐藏和显示时触发两次重排。


### 6、移动端怎么做适配的
- 使用viewport，随着屏幕宽度变化，页面也会跟着变化
```html
<meta name="viewport" content="width=device-width; initial-scale=1; maximum-scale=1; minimum-scale=1; user-scalable=no;">
```

width设置成了设备的宽度，initial-scale控制了页面加载时候的缩放等级，maximum-scale为用户最大缩放值，user-scalabel是否允许用户进行缩放

viewport有视窗、视区等含义，是专门为手机移动设备设计的，当在手机移动设备打开网页时，就会检测网页meta标签是否设置了viewport，如果设置了，就会按照设置viewport的要求在手机移动设备中显示网页。

### 7、CSS可继承的属性
- 字体系列属性，例如字体粗细，风格，大小，行高，文本颜色

- 无继承的属性：display，背景属性，盒子模型的属性，定位属性

### 8、简述一下 Sass 和 Less以及两者区别
      首先，less和sass都可以视为一种基于CSS之上的高级语言，他们引入了变量、Mixin、函数等特性，加快了css的开发效率。  
      二者的区别：
  1. 实现方式不同。less是基于JavaScript运行,所以less是在客户端处理。而sass的安装需要Ruby，是在服务端处理的。
  2. 变量。less是以@开头定义的变量，如：@mainColor:#339;    而sass是以$开头定义的变量，如：$mainColor:#339;
  3. 条件语句。less不支持条件语句，而sass可以使用if{}else{}，for{}循环等等。

### 9、JS动画和CSS3动画差异性
- js功能涵盖面比css3广
- css3比js更易实现
- css3存在兼容问题 js不存在兼容问题




### 11、flex布局的一些常用属性
flex-direction：决定主轴的方向。
flex-wrap：如果一条轴线排不下，如何换行。

justify-content：定义项目在主轴上的对齐方式。
align-items：定义项目在交叉轴上如何对齐。

flex-grow：定义项目的放大比例，默认为 0，即如果存在剩余空间，也不放大。
flex-shrink：定义了项目的缩小比例，默认为 1，即如果空间不足，该项目将缩小。

> flex:1 是三个属性的简写，完整写法应该是： flex: 1 1 0%;
第一个参数表示: flex-grow 定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
第二个参数表示: flex-shrink 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
第三个参数表示: flex-basis相当于width，给上面两个属性分配多余空间之前, 计算项目是否有多余空间, 默认值为 auto, 即项目本身的大小





### 12. px转为rem
1. 通过postcss-pxtorem插件，将像素单元转为rem单位。
2. 在main.js中引入rem.js，根据屏幕宽度动态改变html font-size的值
​

### 10、BFC是什么 （bfc的全称是Block Format Content，直译为块级格式化上下文）？
- 概念
它是一个独立的渲染区域，也就是说，触发bfc的元素会形成一个独立的渲染区域，这个区域里面的元素不会影响外部元素的渲染，  

- 触发BFC的条件  
1. 设置了float属性且值不为none
2. position的值为absolute或者fixed
3. 设置overflow并且值是除visible以外的值（比如说hidden）

- BFC能解决哪些问题  
1. 解决外边距塌陷问题  
当有两个div并且上边的div设置了margin-bottom:100px属性，下边的div设置了margin-top:100px;
我们会发现两个盒子上下距离不是200px而是100px，  
而解决这种情况的方式就是在其中一个盒子外部套一个具有bfc属性的父盒子
```css
.container {
    /* 添加bfc的触发条件，让其形成bfc区域 */
    overflow: hidden;
}
.div1,
.div2 {
    width: 200px;
    height: 200px;
    background-color: aqua;
    margin: 100px;
}
```
```html
<body>
  <div class="div1"></div>
  <div class="container">
    <div class="div2"></div>
  </div>
</body>
```



2、包含塌陷
当内部盒子设置margin-top属性时，父盒子会跟随内部盒子一起移动

解决办法：将子元素添加overflow:hidden可解决

​2、解决浮动元素造成的父元素高度塌陷问题
解决办法：给子元素加个父盒子并设置overflow:hidden

3、解决浮动元素给后面的元素带来的影响
本来三个盒子是上中下排列，给上边两个元素加浮动后，float:left，上面的两个设置了浮动的盒子将第三个盒子给盖起来了，也就是说浮动会影响后面元素的布局

解决办法：给浮动元素添加一个父元素并设置overflow:hidden;属性

### 如何画一条 0.5px 的边框，如何解决1像素的问题
0.5px的问题是各浏览器设备的像素比不同，导致的1px失真

发现目前的实现方案都离不开以下三种

1、使用伪元素 + CSS3``缩放的方式
2、使用 动态 viewport + rem 布局 的方式（即 Flexible 实现方案）
3、新方案：使用 vw 单位适配方案（将来推荐的一种方案，但目前项目中没有实际应用，故本文不做讨论）

1. 使用伪元素 + CSS3缩放的方式
```css
// 通过伪元素实现 0.5px border
.border::after {
    content: "";
    box-sizing: border-box; // 为了与原元素等大
    position: absolute;
    left: 0;
    top: 0;
    width: 200%; 
    height: 200%; 
    border: 1px solid gray;
    transform: scale(0.5); 
    transform-origin: 0 0;
}

// dpr适配可以这样写
@media (-webkit-min-device-pixel-ratio: 2)  {
    .line::after {
    	...
     	height: 1px;
      transform: scale(0.5);
      transform-origin: 0 0;
    }
}

@media (-webkit-min-device-pixel-ratio: 3)  {
    .line::after {
        ...
     	height: 1px;
      transform: scale(0.333);
      transform-origin: 0 0;
    }
}
```
> 为什么要先放大 200% 再缩小 0.5？
如果直接 scale(0.5) 的话 border 整体大小也会变成二分之一，所以先放大 200%（放大的时候 border 的粗细是不会被放大的）再缩放，就能保持原大小不变了。

为什么采用缩放的方式，就可以解决手机对小数点处理的兼容性问题？

此处我是这样理解的。首先代码中处理的是 1px ，避免了直接操作小数像素的问题；当 dpr=2 时，换算成物理像素为 2px，此时去缩放 scale(0.5)、当 dpr=3 时，换算成物理像素为 3px，此时缩放 scale(0.3) 后，手机均会默认使用最小物理像素 1px 来渲染。按照 CSS3 transform 的 scale 定义，边框可以任意细，理论上可以实现任意细的缩放效果。




1. 使用 动态 viewport + rem 布局 的方式（即 Flexible 实现方案）
initial-scale 设置为0.5

1. 新方案：使用 vw 单位适配方案（将来推荐的一种方案，但目前项目中没有实际应用，故本文不做讨论）

### 移动端是用什么单位写的，他是怎么转成rem的。
我们一般用px来写，一般给的是375px的设计稿，通过postcss-pxtorem，将px转为rem，再在跟组件写入方法，动态监听当前屏幕的宽度，
改变根节点font-size的大小。

postcss-pxtorem是PostCSS的插件，用于将像素单元生成rem单位。

1.安装依赖
npm install postcss-pxtorem -D
2.设置规则（更改postcss.config.js,该文件为使用vue-cli3自动创建的文件）
```javascript
module.exports = {
  plugins: {
    'autoprefixer': {
      browsers: ['Android >= 4.0', 'iOS >= 7']
    },
    'postcss-pxtorem': {
      rootValue: 15,//结果为：设计稿元素尺寸/15，比如元素宽375px,最终页面会换算成 25rem，基准值是随便设置的，一般设置为100
      propList: ['*']
    }
  }
}
```
> 基准值可以随便设置吗？是的
上边的意思是：将页面分成25，每份为15，当实际页面宽度为750时，每份变成(750/25 = 30)，30*25份=750

在main.js中引入rem.js
import './libs/rem.js'; 
```javascript
// 设置 rem 函数
function setRem () {
  // 375 默认大小15px; 375px = 25rem ;每个元素px基础上/15
  let htmlWidth = document.documentElement.clientWidth || document.body.clientWidth;
  //得到html的Dom元素
  let htmlDom = document.getElementsByTagName('html')[0];
  //设置根元素字体大小
  htmlDom.style.fontSize= htmlWidth/25 + 'px';
}
// 初始化
setRem();
// 改变窗口大小时重新设置 rem
window.onresize = function () {
  setRem()
}
```


### 移动端界面布局适配方案

 