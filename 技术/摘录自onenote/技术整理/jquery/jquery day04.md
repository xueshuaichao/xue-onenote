多库共存
   var xy24kcs=$.noConflict(); 
   xy24kcs(function () {
       //为按钮注册点击事件
   xy24kcs("#btn").click(function () {
           console.log("今天天气格外好");
       });
   });

知识更新
$('#tab-main').children('div')  不包括a标签，可以放心使用。 

        <div class="products" id="tab-main">
          <div class="main selected">
            <a href="###"><img src="imgs/guojidapai.jpg" alt="" /></a>
          </div>
          
          <div class="main">
            <a href="###"><img src="imgs/nanshijingpin.jpg" alt="" /></a>
          </div>   
        </div>

attr和prop的区别
attr()方法可以设置或者获取标签自带属性和自定义属性的值
$("chekcbox").attr("checked"); undefined
prop()方法可以设置或者获取标签的属性值,而且可以获取复选框checked的true或者false值
