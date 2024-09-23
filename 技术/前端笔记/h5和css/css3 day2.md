## 背景
### 背景尺寸
让背景图 完全显示在盒子里头
background-size: contain;
让背景图  完全铺满整个盒子
background-size: cover; 
    
### 背景原点
所谓的背景原点其实调整的是背景图片位置一个参照点
    
 以边框的外侧为参照(包括边框)
background-origin: border-box;

内边距的外侧为参照(默认)就是不包括边框。
background-origin: padding-box;

是以内容的外侧为参照
background-origin: content-box; 

### 背景裁切
边框外侧之外
background-clip: border-box;

padding之外的都裁掉（就是边框内侧之外）
    background-clip: padding-box;

content之外的都裁掉
background-clip: content-box;

多背景图片
 background: url(images/head.jpg) left top no-repeat,
    url(images/foot.jpg) left bottom no-repeat; 

线性渐变   
    1.渐变的方向 
 ( to top(0deg) right(90deg)  left  bottom )  角度 deg ( 0deg 从下到上  顺时针是正角度 )
    2.起始的颜色
    3.结束的颜色
background-image:linear-gradient(0deg,transparent,rgba(255,0,0,0.6));
background-image: linear-gradient(to left ,transparent,rgba(255,0,0,0.6)); 
    
渐变可以同一个颜色 并且可以利用百分设置渐变的区间 
  background-image: linear-gradient(
      45deg,
      yellow 0%,
      yellow 25%,
      blue 25%,
      blue 50%,
      yellow 50%,
      yellow 75%,
      blue 75%,
      blue 100%
  );
    
    background-size: 100px 100px;
    
### 径向渐变
     1.辐射半径
     2.中心点的位子
     3.起始颜色
     4.结束颜色           
    background-image: radial-gradient(150px at 80px 80px,#fff,#00f);
    
过度    
1. transition-property: all;   需要过渡的属性
2. transition-duration: 2s;    过渡的时间
3. transition-timing-function: linear; 过渡的时候的动画速度 linear 匀速
                                                                            ease 快慢  默认的
                                                                            ease-in
                                                                            ease-out
                                                                            ease-in-out
4. transition-delay: 2s;       过渡延时时间

 .transition {
    width: 200px;
    height: 200px;
    transition:all 2s linear 2s;
}
.transition:hover {
    width: 800px;
    height: 400px;
            left: 400px;
} 
    
    
## 2d转换 
rotate    translate   skew    scale
scale(缩放)
.scale {
  width: 200px;
  height: 200px;
  transition: all 1s;
}

.scale:hover{
    transform: scale(0.5,0.5);
}
第一个参数  x轴方向的缩放比例
第二个参数  y轴方向的缩放比例

移动(不用脱标也能移动)
 第一个参数  x轴方向的移动距离
第二个参数  y轴方向的移动距离

    .translate {
  width: 200px;
  height: 600px;
  transition: all 1s;
    }
  
  .translate:hover{
    transform: translate(-100px,20px);
  }

box-shadow
    第一个参数：x轴移动的距离
    第二个参数：y轴移动的距离
    第三个参数：延伸的长度
    第四个参数：颜色
box-shadow:0 1px 4px rgba(0,0,0,0.3),  0 0 40px rgba(0,0,0,0.1) inset;

## 旋转
    第一个参数  单位是deg   当是顺时针旋转的时候  值的正的   反之负的
    .rotate{
    width: 200px;
    height: 200px;
    transition:all 2s;
  }
  div:hover{
    transform:rotate(350deg);
  } 
    
倾斜 skew

    .skew:hover{

  第一个参数  x轴方向的变形
  第二个参数  y轴方向的变形

  x
  变形的时候是逆时针  角度是正的
  变形的时候是顺时针  角度是负的

  y
  变形的时候是顺时针  角度是正的
  变形的时候是逆时针  角度是负的

  一般只会设置一个参数
  
  transform: skew(45deg,0deg);
  transform: skew(0deg,45deg);
}
    
转换原点 transform-origin  (最好加在非hover标签中)
 设置转换原点的属性 ( 默认的是中心)
transform-origin: left top;
使用px 做定位原点
transform-origin: -40px 0;		
    
结合使用
.box:hover {
  transform: rotate(360deg) translate(100px, 100px) scale(0.2);
}  
    
让任意元素水平居中
    .dv{
        width: 200px;
        height: 200px;
        position:absolute;
        top:50%;
        left:50%;
        background-color: #f00;
        transform: translate(-50%,-50%);

    }
    
## 3d转换 
 rotateX    
如果是负的 就是顺时针   正的是逆时针

    .rotateX {
        perspective: 100px;   			
  }

  .rotateX img {
    transition: all 5s;
  }

  .rotateX:hover img {
     transform: rotateX(-180deg);
  }
  
    <div class="rotateX">
        <img src="./images/x.jpg" alt="">
    </div>    
    
rotateY

    .rotateY {
    perspective: 100px;
  }

  .rotateY img {
    transition: all 5s;
  }

  .rotateY:hover img {
    transform: perspective(100px) rotateY(180deg);
  }
    
perspective有两种写法
a) 作为一个属性，设置给父元素，作用于所有3D转换的子元素
b) 作为transform属性的一个值，做用于元素自身
      

rotateZ
如果是负的 就是顺时针   正的是逆时针
transform: perspective(100px) rotateZ(-180deg); 
    
移动 transformX
    .translateX:hover {
    transform:translateX(300px);
  }
    
3d 移动 transformY
    .translateY:hover {
    transform: translateY(400px);
  }
 
3d 移动 transformZ
    .translateZ:hover {
    transform:  translateZ(400px);
  }
    
3D呈现（transform-style）
设置内嵌的元素在 3D 空间如何呈现，里面的子元素必须为变形元素。
transform-style: preserve-3d;
flat：所有子元素在 2D 平面呈现
    
backface-visibility
    设置元素背面是否可见
    
立方体案例

     .box {
    width: 100px;
    height: 100px;
    text-align: center;
    line-height: 100px;
    font-size: 24px;
    margin: 100px auto;
    position: relative;
    transform: rotateY(30deg) rotateX(-30deg);
        transform-style: preserve-3d;
        prespective:1000px;
  }
    
    .box div{
        width: 200px;
        height: 200px;
        position: absolute;
        left: 0;
        top: 0;
        opacity: 0.6;
    }
    
    .front{
        background: yellow;
        transform: translateZ(100px);
    }
    
    .back{
        background: yellowgreen;
        transform: translateZ(-100px);
    }
    
    .left{
        background: blue;
        transform:translateX(-100px) rotateY(-90deg);
    }
    
    .right{
        background: purple;
        transform:translateX(100px) rotateY(-90deg);
    }
    
    
    .top{
        background: pink;
        transform:translateY(-100px) rotateX(-90deg);
    }
    
    .bottom{
        background: green;
        transform:translateY(100px) rotateX(-90deg);

    }
