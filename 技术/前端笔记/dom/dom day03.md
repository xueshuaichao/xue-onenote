事件参数对象以及图片随着鼠标移动的完整版封装

    IE8中,没有事件参数对象,   用的是window.event;
    谷歌和火狐有事件参数对象
    document.onmousemove = function (evt) {
        var event = window.event ? window.event : evt;//更严谨
       my$("im").style.left=evt.clientX+"px";//谷歌和火狐的写法
      my$("im").style.left=window.event.clientX+"px";//IE8的写法
 
        //下面的代码如果页面中有滚动条位置就不一样,鸟飞了
       my$("im").style.left=event.clientX+"px";
        my$("im").style.top=event.clientY+"px";

        因为有卷曲出去的距离,所以,导致坐标出问题了

        //pageX和pageY感觉很好,但是,IE8不支持
        my$("im").style.left = event.pageX + "px";
        my$("im").style.top = event.pageY + "px";

        if(event.pageX){
            my$("im").style.left = event.pageX + "px";
        }else{
            my$("im").style.left = event.clientX+getScroll().left+"px";
        }
        if(event.pageY){
            my$("im").style.top = event.pageY + "px";
        }else{
            my$("im").style.top=event.clientY+getScroll().top+"px";
        }
    };

图片跟着鼠标飞工具函数的封装
 document.onmousemove=function (e) {
        my$("im").style.left=eventTools.getPageX(e)+"px";
        my$("im").style.top=eventTools.getPageY(e)+"px";
    };
    var eventTools={
        getEvt:function (e) {//返回事件参数对象
            return window.event?window.event:e;
        },
        getClientX:function (e) {//返回的是可视区域的横坐标
            return this.getEvt(e).clientX;
        },
        getClientY:function (e) {//返回的是可视区域的纵坐标
            return this.getEvt(e).clientY;
        },
        getScrollLeft:function () {//卷曲出去的横坐标
            return window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft||0;
        },
        getScrollTop:function () {//卷曲出去的纵坐标
            return window.pageYOffset||document.documentElement.scrollTop||document.body.scrollTop||0;
        },
        getPageX:function (e) {//文档的横坐标:可视区域的横坐标+卷曲出去的横坐标
            return this.getEvt(e).pageX?this.getEvt(e).pageX:this.getClientX(e)+this.getScrollLeft();
        },
        getPageY:function (e) {//文档的纵坐标:可视区域的纵坐标+卷曲出去的纵坐标
            return this.getEvt(e).pageY?this.getEvt(e).pageY:this.getClientY(e)+this.getScrollTop();
        }
    };

client兼容代码的封装
 function getClient() {
        return{
            width:window.innerWidth||document.documentElement.clientWidth||document.body.clientWidth||0,
            height:window.innerHeight||document.documentElement.clientHeight||document.body.clientHeight||0
        }
    }

三大系列的总结

offset系列:
offsetLeft:元素距离左边的像素(父级元素的margin+父级元素的padding+父级元素的border+自身的margin)
offsetTop:元素距离上面的像素(父级元素的margin+父级元素的padding+父级元素的border+自身的margin)
offsetWidth:元素自身的宽度(有边框的宽度)
offsetHeight:元素自身的高度(有边框的宽度)

scroll系列:
scrollLeft:滚出去的左边距离
scrollTop:滚出去的上面的距离
scrollWidth:内容的宽度(没有内容,元素自身的宽度,没有边框)
scrollHeight:内容的高度(没有内容,元素自身的高度,没有边框)

client系列:
clientX:可视区域的横坐标
clientY:可视区域的纵坐标
clientWidth:可视区域的宽度
clientHeight:可视区域的高度
