通过document直接获取的元素
 1. var txt=document.title;//获取的并不是title标签对象,而是标签中的内容
   document.title="修改吧";
   
 2.  console.log(document.body);//获取的是body对象
    
 3. console.log(document.documentElement);//获取的是html标签对象

scroll系列
scrollWidth:元素中内容的实际的宽度(如果没有内容是元素的宽度,没有边框)
scrollHeight:元素中内容的实际的高度(如果没有内容是元素的高度,没有边框)
scrollLeft:元素中内容向左滚出去(卷曲出去)的宽度
scrollTop:元素中内容向上滚出去(卷曲出去)的高度

页面卷曲事件的封装
function getScroll() {
   return {
            top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0,
            left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft || 0
        };
    }

减速移动动画函数的封装
    function animate(element,target) {
        clearInterval(element.setId);
        element.setId=setInterval(function () {
            //当前位置
            var current=element.offsetLeft;
            //每次移动的步数
            var step=(target-current)/10;
            //判断
            step=step>0?Math.ceil(step):Math.floor(step);
            current+=step;
            element.style.left=current+"px";
            if(current==target){
                clearInterval(element.setId);
            }
            console.log("target:"+target+",current:"+current+",step:"+step);
        },20);
    }

获取元素计算后的样式属性的封装
console.log(my$("dv").offsetLeft);   获取元素样式属性计算后的值,是字符串类型，而且如果元素脱标，样式表现不出来，属性的值拿不到，(但我觉得下边的没啥用，因为我要的就是表现出来的值，没有表现的我也不要，)
但下边的不一样，都能拿到。但又兼容问题。所以需要封装
        
     获取的元素的宽度(真实的,没有边框)
        console.log(window.getComputedStyle(my$("dv"),null).width);
        console.log(window.getComputedStyle(my$("dv"),null)["width"]);
        //获取的元素的高度(真实的,没有边框)
        console.log(window.getComputedStyle(my$("dv"),null).height);
        console.log(window.getComputedStyle(my$("dv"),null)["height"]);
        //获取的元素的left值(真实的,没有边框)
        console.log(window.getComputedStyle(my$("dv"),null).left);
        console.log(window.getComputedStyle(my$("dv"),null)["left"]);
        //获取的元素的top值(真实的,没有边框)
        console.log(window.getComputedStyle(my$("dv"),null).top);
        console.log(window.getComputedStyle(my$("dv"),null)["top"]);

代码的封装    
 谷歌支持getComputedStyle IE8支持currentStyle 
function getStyle(element,attr) {
        return window.getComputedStyle?window.getComputedStyle(element,null)[attr]:element.currentStyle[attr]||0;
    }
console.log(getStyle(my$("dv"),"left"));

增加任意属性动画函数的封装
  function getStyle(element,attr) {
        return window.getComputedStyle?window.getComputedStyle(element,null)[attr]:element.currentStyle[attr]||0;
    }

    my$("btn").onclick=function () {
        var obj={"left":200,"top":400,"width":400,"height":500};
        animate(my$("dv"),obj,function () {
            animate(my$("dv"),{"left":30,"top":30,"width":30,"height":30},function () {
                animate(my$("dv"),{"left":50,"top":50,"width":100,"height":100},function(){
                     alert("结束了");
                });
            });
        });
    };

图片跟着鼠标飞案例
    document.onmousemove=function (event) {
          var evt=window.event||event;//兼容代码
//        my$("im").style.left=evt.clientX+"px";
//        my$("im").style.top=evt.clientY+"px";
 //pageX和pageY是获取鼠标在页面中的横纵坐标(包括可视区域的横坐标+向左卷曲出去的距离,包括可视区域的纵坐标+向上卷曲出去的距离)
        //IE8不支持
        my$("im").style.left=evt.pageX+"px";
        my$("im").style.top=evt.pageY+"px";
    };