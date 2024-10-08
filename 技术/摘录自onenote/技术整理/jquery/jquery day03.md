自定义属性
aObj.attr("id","ak");
aObj.attr("href","http://www.baidu.com");
console.log($("#ak").attr("href"));
jquery对象添加自定义属性的方法，和setAttribute 差不多，但明显比原生的要好用。


var flag=$("#ck3").prop("checked");
if(flag){
    $("#ck3").prop("checked",false);
}else{
    $("#ck3").prop("checked",true);
}

jquery 的内置方法
var width=$("#dv").width();
.width()方法 如果括号中写了值,不需要加px,是设置
获取宽还可以用
$('#dv').css('width')


var left=$("#dv").offset().left;
var top= $("#dv").offset().top;
$("#dv").offset({"left":left*2,"top":top*2});

补充内容:
如果元素脱离了文档流,那么只是设置了left和top值
如果元素没有脱离文档流,那么设置offset()的值的时候,会自动设置为relative,
$("#dv").offset({"left":100,"top":200});


$(function () {
    $(window).scroll(function () {
  //console.log(window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft);
        console.log($(document).scrollLeft());
        console.log($(document).scrollTop());
    });
});

绑定事件的两种方式

1. 
$("#btn).click(function(){});
这种比较常用

on 绑定事件
$('#btn').on('click',()=>{})   这种和上边的一样。
$('#btn').on('click','p',()=>{})  这种是绑定子元素，注意必须是子元素。



   $("#btn").click(function () {
        $("#txt").focus();
        $("#txt").trigger("focus");
        $("#txt").triggerHandler("focus");
        第一种和第二种可以触发浏览器的默认的事件
        第三种不会触发
    });


keydown事件
   $(document).on("keydown",function (e) {
            console.log(e.keyCode);
        });



事件冒泡
jquery 中用return false
dom    中用e.cancelBubble=true;

each方法的应用  
这种方法伪数组和数组都能用，因为jquery内部已经做好了兼容。
    $("ul>li").each(function (index,ele) {
        $(ele).css("opacity",(index+1)/10);
    });

上下两个的区别。
var left=$("#dv").css("left");
var top=$("#dv").css("top");

同样能得到left，top值，
但是offset() 得到的是对象。
上边可以显示我设置在style中的值，但不一定是真实生效的值，比如我设置了 left top 但没有设置
position:absolute 此时该属性是不生效的。但上边显示我设置的值，下边显示0

//.offset()方法返回的是对象,对象中两个属性:left和top
console.log($("#dv").offset().left);
console.log($("#dv").offset().top);

获得页面卷曲的高度和宽度

$(document).scrollLeft()
$(document).scrollTop()

为什么document不用双引号，因为document本身就是dom元素。所以不用。
如果用原生的方法是  document.documentElement.scrollTop  没有括号，所以jquery是将所有的东西都内置为方法。



解绑事件
$("#dv").on("click","input", function () {
      console.log("今天中午非常悲剧,我丢了每天都需要的东西");
});

$("#btn2").click(function () {
     $("#dv").off("click","input");
});


$("#dv").off("click","input");//解绑子元素的点击事件
$("#dv").off("click");//会把父元素和子元素的相同的点击事件全部解绑
$("#btn").off("事件名字 事件名字");
$("#dv").off("click","**");//把父级元素中所有的子级元素的点击事件全部解绑
$("#dv").off();//父元素和子元素的所有的事件全部解绑


触发事件
 $("#txt").focus(function () {
        $(this).next("span").text("触发了");
});
有三种触发该事件的方法。

$("#txt").focus();//调用
       
$("#txt").trigger("focus");
             
$("#txt").triggerHandler("focus");

         
//第一种和第二种可以触发浏览器的默认的事件
//第三种不会触发
默认事件比如说。输入框会变蓝。但第三个不会。

jquery中的each遍历
$("ul>li").each(function (index,ele) {
       $(ele).css("opacity",(index+1)/10);
});
each也是jquery的内置方法，要注意的是ele 是dom元素。
