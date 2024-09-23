经典的网页布局
```html
<body>  
<header>
  <nav class="nav"></nav>
</header>
<section class="main">
  <article></article>
  <aside></aside>
</section>
<footer></footer>
</body>
```

### 兼容低版本浏览器

[if lte IE 8]
      <script src="js/html5shiv.min.js"></script>
[endif]

条件注释：该文件是让h5在低版本浏览器中兼容    当浏览器版本小于等于ie8时使用

### h5中的常用后缀   
email:
<input type="email" name="qq" required autocomplete  autofocus placeholder pattern="1\d{10}">

当验证未通过时触发
input.oninvalid=function(){
  this.setCustomValidity('该项必填')
}

### audio(音频) 控件
  1.controls 显示控制栏
  2.autoplay 自动播放
<audio autoplay controls>
    <source src="See%20You%20Again.mp3"/>
    <source src="See%20You%20Again.wav"/>
    <source src="See%20You%20Again.ogg"/>
</audio>

### video（视频） 控件
<video preload='auto'  controls autoplay width="600" height="400">
            <source src="fun.mp4"/>
            <source src="fun.ogv"/>
            <source src="fun.webm"/>
</video>

### 伪类选择器
li:nth-child(3) a{
  color: pink;
}
document.querySelector('li:nth-child(3) > a');
var a01 = document.querySelector('li:nth-child(3)'); 获取第三个li标签
var a02 =document.querySelector('li');      获取的是第一个li标签

只能获取一个dom元素  如果有多个则获取第一个
document.querySelector('li').style.color = 'red';

querySelectorAll  获取多个元素
var lis = document.querySelectorAll('.outer li > ul > li a');

### classList 为元素添加属性
nav.onclick = function(e){  
var a = e.target;       因为nav是导航条，所有e.target表示选择的那一个
if(a.classList.contains('active')){ 
  return false;
}
document.querySelector('nav > a.active').classList.remove('active');
a.classList.add('active');
e.target.classList.toggle('active');

增：a.classList.add('active')      
删：a.classList.remove('active')   
改：a.classList.toggle('active')    
查：a.classList.contains('active')  

### jquery 中data的使用
data()在jquery 当中是用来存储数据用的，不会有任何表现
设置：
$('li').data('color','red');
获取：
console.log($('li').data('color'));

### h5中自定义属性dataset的操作

设置自定义属性
dom.dataset.cont='global'; 
dom.dataset.userName='itcast'; 
<a href="javascript:;" data-cont="global">国际新闻</a>
<a id="news" href="javascript:;" data-user-name="itcast" data-age="10">国内新闻</a>

获取自定义属性
console.log(dom.dataset.name);
console.log(dom.dataset.userName); 
