
jquery 中的样式操作
.addClass()
.removeClass()
.hasClass()
.toggleClass()  实现样式的切换

toggleClass 的意思是如果有这个类名，就去掉，如果没有就加上，少了hasClass判断的过程。不要以为这句话显而易见，但让我知道了toggleClass运作的原理。
 $(document.body).toggleClass('cls')    不需要用 .cls

经过我的亲身验证，发现jquery中的.find() 和 .children()效果是一样的。唯一的区别是
find括号中不能为空，他们都可以找到特定的标签。

修复断链的方法
//断链: 修复断链,只需要找到断链的位置,加入一个方法,就可以修复断链:.end()
//         $(this).prevAll().css("backgroundColor","yellow").end().nextAll().css("backgroundColor","blue");

jquery有隐式迭代功能，并且可以通过index()直接获取当前索引
 $(function(){
        $('.tab li').mouseover(function(){
            $(this).addClass('active').siblings('li').removeClass('active');
            $('.products div:eq('+$(this).index()+')').addClass('selected').siblings().removeClass('selected');
        })
       })


  var allLength = $("#j_tb :checkbox").length;
$(input[type='button']).click()
jquery中的选择器可以是标签，也可以是某个特性 ：checkbox

console.log($(document).scrollLeft());
 console.log($(document).scrollTop());
和offset().left    offset().top不一样

jquery中的 事件绑定
$("#dv").on("click","p",function () {
          alert("中午吃啥捏.吃个鸭梨");
  });
on是可以绑定事件的

冒泡事件
 $('#dv3').click(function(){
               console.log($(this).attr("id"));
                return false;
     })
return false只有在jquery元素中才能阻止冒泡
如果是dom元素，必须要用e.cancelBubble=true;
再次实验，证明这句话是正确的。return  false，虽然可以阻止函数的执行，但并不能阻止不冒泡。
document.getElementById('two').onclick=function(e){
    console.log('two')
    // e.cancelBubble=true;
    return false;
    console.log('hello')   //如果有return false，改句不执行
}


animate 小动画


 $('#im').animate({ width: '500px', height: '500px', opacity: '0.5' }, 1000, () => {
     $('#im').animate({ width: '50px', height: '50px' })
 })
现在看来，animate方法，和 .css 方法还是挺像的。直接在里边写样式就行了，只不过有时间，有回掉。



创建元素的两种方式
//第一种方式
    $('#dv').append($('<a href="www.baidu.com">百度</a>'))

//第二种方式
    $('<a href="www.baidu.com">百度</a>').appendTo('#dv');




$('<p>'+item+'</p>')   在这里就是一个jquery元素。


剪切
  $('#se2').append($('#se1 option:selected'))
如果append的不是标签，而是页面中已经存在的元素，那么就是剪切。

移除元素
remove这种方法，移除比较彻底。
  $(()=>{
            $('#btn').click(()=>{
                $('#dv').remove()
            })
        })

克隆
$('#dv2').append($('#dv1 p').clone(true));
如果只是append($(‘#dv1 p’)) 就是剪切了，幸亏后边加了 clone
<!-- vertical,horizontal,inline -->
<!-- :wrapper-col="wrapperCol" -->
<!-- :label-col="labelCol" :wrapper-col="wrapperCol" -->

