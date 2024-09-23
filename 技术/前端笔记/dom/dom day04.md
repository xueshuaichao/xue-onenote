点击按钮调用另一个事件执行
my$("btn2").onclick=function () {
    //第一种写法
    my$("btn").onclick();
    //第二种写法
     my$("btn").click();
};

注册多个相同事件
第一种方式:
    * 参数1:事件的类型(事件的名字),没有on
    * 参数2:事件处理函数(匿名函数或者命名函数)
    * 参数3:false
    * addEventListener();谷歌支持,火狐支持,IE11支持,IE8不支持    （常用）
    *
    * 第二种方式:
    * 参数1:事件类型(事件的名字)有on
    * 参数2:事件处理函数(匿名函数或者命名函数)
    * attachEvent()谷歌不支持,IE8支持,火狐不支持,IE11不支持

* 实例 
```
   为按钮注册多个相同的点击事件
   my$("btn").addEventListener("click",function () {
       console.log("为何要吃饭");
   });
   my$("btn").addEventListener("click",function () {
       console.log("为何要喝水");
   });
   my$("btn").addEventListener("click",function () {
       console.log("为何要睡觉");
   });

移除事件的方式

    * 第一种注册事件方式:
     * obj.onclick=function(){}
     * 第一种移除事件的方式:
     * obj.onclick=null;
     *
     * 第二种注册事件方式:IE8中不支持
     * 对象.addEventListener(没有on的事件类型,事件处理函数,false);
     * 第二种移除事件方式:IE8中不支持
     * 对象.removeEventListener(没有on的事件类型,事件处理函数的名字,false);
     *
     * 第三种注册事件方式:
     * 对象.attachEvent("有on的事件类型",事件处理函数);
     * 第三种移除事件方式:
     * 对象.detachEvent("有on的事件类型",有名字的事件处理函数);


两种方法的区别

    * 注册事件的区别
    * 对象.addEventListener();      里面的this是触发这个事件的对象
    * 对象.attachEvent();           里面的this是浏览器的顶级对象window
    *  注册事件的区别:
    *  1.this是不同的对象
    *  2.方法名不同,参数个数不相同
    *  addEventListener方法三个参数
    *  attachEvent方法两个参数
    *  3.
    *  addEventListener方法事件类型没有on
    *  attachEvent方法事件类型有on
    *  4.
    *  addEventListener方法谷歌支持,火狐支持,IE11也支持,IE8不支持
    *  attachEvent方法谷歌不支持,火狐不支持,IE11不支持,IE8支持
    *
    *  相同点:都可以为元素添加多个相同的事件
    *  都是对象调用方法(元素.方法)

阻止事件冒泡的三种方式

 my$("dv3").onclick=function (e) {
        e.cancelBubble=true;
        //e.stopPropagation();//原本属于火狐的,但是现在谷歌和火狐都支持
    };
jquery支持return false，切记原生中不支持。

事件的阶段
<div id="dv1">
    <div id="dv2">
        <div id="dv3"></div>
    </div>
</div>

 var objs=[my$("dv3"),my$("dv2"),my$("dv1")];
    objs.forEach(function (element) {
        element.addEventListener("click",function (e) {
            //console.log(this.id+e);
            console.log(this.id+"===="+e.eventPhase);
        },true);   //默认为false 
        //当为true时，点击dv3  得到的结果为1，1，2  说明是从外向里执行，捕获
        //当为false时，点击dv3 得到的结果为2，3，3  说明是从里向外执行，冒泡
    });

    //捕获的阶段:  e.eventPhase ===1
    //目标的阶段:  e.eventPhase ===2
    //冒泡的阶段:  e.eventPhase ===3

iframe 标签
<iframe src="http://www.baidu.com" frameborder="0" width="80%" height="40%"></iframe>
