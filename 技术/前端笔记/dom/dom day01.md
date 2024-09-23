offset系列的几个属性   
以后不要去刻意追求offsetLeft有没有脱标，没有特殊说明，都可以认为是距离浏览器左边框的距离
1 offsetWidth和offsetHeight可以获取元素的宽和高,没有px，但是不能设置，只读的。
 2 可以从style标签和html标签中的style属性中都可以获取
       
下面的代码可以直接从style标签中获取元素的宽和高
console.log(my$("dv").offsetWidth);
console.log(my$("dv").offsetHeight);
console.log(my$("dv").offsetLeft);
console.log(my$("dv").offsetTop);
        
以下代码时无效的
my$("dv").offsetWidth="500px";
        
以后想要获取元素的宽,高,left,top，通过offset系列来获取(此时这句话是对的,过两天就有瑕疵了)
offsetLeft是相对父级元素的左边框的距离

分为三种情况
第一种：子元素脱标，父元素随便
此时offsetLeft值就是子元素的left值
第二种：子元素未脱标，父元素未脱标
offsetLeft:父级元素的margin+父级元素的padding+父级元素的边框+子级元素的margin
第三者：子元素未脱标，父元素脱标
offsetLeft：得到的是子元素的margin值

记得之前学过层级，如果脱标后就不在同一层级了，所以offsetLeft 只是这一层级相对其边界的距离。

简单的点击按钮移动动画的封装
 function animate(element,target) {
        clearInterval(element.setId);
        element.setId=setInterval(function () {
            //获取元素的当前的位置
            var current=element.offsetLeft;//数字类型的
            //每次移动的步数
            var step=10;
            step=current<target?step:-step;
            //设置当前位置的值
            current+=step;
            if(Math.abs(current-target)>Math.abs(step)){
                element.style.left=current+"px";
            }else{
                element.style.left=target+"px";
                //到达目标,清理计时器
                clearInterval(element.setId);
            }
        },20);
    }