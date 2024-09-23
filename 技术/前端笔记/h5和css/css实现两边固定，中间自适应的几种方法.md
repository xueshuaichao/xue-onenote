### 1. flex布局 
父盒子设置成display：flex，两边固定宽度，中间flex:1,
### 2.利用浮动（float）
   让左右元素浮动，缺点是中间元素必须置于二者之后，不然right元素会进入下一行

  <style type="text/css">
    .left,.right{
      width:200px;
      height:200px;
      background-color:#999;
    }
    .left{
      float:left;
    }
    .right{
      float:right;
    }
    .center{
      margin:0 200px;
      height:300px;
      background-color:#f00;
    }
  </style>  
</head>  
<body>  
  <!--该布局法的好处是受外界影响小，但是不足是 三个元素的顺序，center一定要放在最后，这是             
和绝对定位不一样的地方，center占据文档流位置，所以一定要放在最后，左右两个元素位置没有关系。
当浏览器窗口很小的时候，右边元素会被击倒下一行。-->
  <div class="left">left</div>
  <div class="right">right</div>
  <div class="center">center</div>
  
</body>


### 3.利用绝对定位（position）
center居中并利用margin为左右两边留出位置，左右绝对定位

  <style type="text/css">   
    /*左右固定，中间自适应  利用绝对定位*/
    .container{
        width: 100%;
        height: 100%;
        position: relative;
    }
    .left{
        position: absolute;
        left: 0;
        top: 0;
        width: 400px;
        height: 200px;
        background-color: black;
        color:#fff;
    }
    .center{
        /*width: auto;*/   /*如果没有这一句，那么，center这个div的文字就不会自动换行*/
        margin: 0 400px;
        height: 400px;
        background-color: yellow;
    }
    .right{
        position: absolute;
        top: 0;
        right: 0;
        width: 400px;
        height: 300px;
        background-color: red;
    }
  </style>
</head>
<body>
  <div class="container">
      <div class="left">left</div>
      <div class="center">center</div>
      <div class="right">right</div>
  </div>
</body>



### 5.双飞翼布局（重点来了）
 目的：为了优先显示中间主要部分，浏览器渲染引擎在构建和渲染渲染树是异步的（谁先构建好谁先显示），故在编写时，先构建中间main部分，但由于布局原因，将left置于center左边，故而出现了双飞翼布局。

<style type="text/css">
  body {
    min-width: 550px;
  }
  .col {
    float: left;
  }
  #main {
    width: 100%;
    height: 200px;
    background-color: #ccc;
  }
  #main-wrap {
    margin: 0 190px;
    /*这是圣杯和双飞翼最明显的区别，在main内部使用的是margin，而圣杯是直接在container部分使用padding*/
  }
  #left,
  #right {
    width: 190px;
    height: 200px;
    background-color: #0000FF;
  }
  #left {
    margin-left: -100%;
  }
  #right {
    margin-left: -190px;
    background-color: #FF0000;
  }
</style>
</head>
<body>
  <div id="container">
    <div id="main" class="col">
      <div id="main-wrap"> #main </div>
    </div>
    <div id="left" class="col">#left</div>
    <div id="right" class="col">#right</div>
  </div>
</body>
这种布局的好处是：两边（left和right）不会盖住中间(center)部分，left和right盖住的是wrap元素的两边，即main-wrap的margin部分。


### 6.圣杯布局（也是重点）

<style type="text/css">
  .wrapper {
    padding: 0 100px;
    overflow: hidden;
  }
  .col {
    position: relative;
    float: left;
  }
  .main {
    width: 100%;
    height: 200px;
    background: yellow;
  }
  .left,
  .right {
    width: 100px;
    height: 200px;
    background: red;
  }
  .left {
    margin-left: -100%;
    left: -100px;
  }
  .right {
    margin-left: -100px;
    right: -100px;
  }
</style>
</head>
<body>
  <section class="wrapper">
    <section class="col main">main</section>
    <aside class="col left">left</aside>
    <aside class="col right">right</aside>
  </section>
</body>





