私有前缀
兼容主流浏览器各个版本
    -webkit-border-radius: 50px;/*谷歌 苹果*/
    -moz-border-radius: 50px;/*火狐*/
    -ms-border-radius:50px;/*IE*/
    -o-border-radius:50px;/*欧鹏*/  
                           
选择器
CSS3新增了许多灵活查找元素的方法，极大的提高了查找元素的效率和精准度。CSS3选择器与jQuery中所提供的绝大部分选择器兼容。            
1 属性选择器
E[attr] 
E[attr=val] 
E[attr*=val] 属性值里包含val字符并且在“任意”位置；
E[attr^=val] 属性值里包含val字符并且在“开始”位置；
E[attr$=val] 属性值里包含val字符并且在“结束”位置；
                       
a[href]{         a和[href]直接不能有空格。
      color:red;
}
[class]{
     color:blue;
}
[class='abc']{
        color:yellow;
}
 [class !='abc']{     //非  不存在这种选择器
       color:green;
}
    
 [class ^='abc']{
         color:pink;
}
    
[href='a'][class='abc']{
        color:yellowgreen;
 }                          
                         
2.  结构性的伪类选择器
结构性伪类选择器的顺序选择器
li:first-child
先找到li的父元素,找到父元素当中的所有的子元素,找第一个子元素,匹配是不是li这个类型                          

  li:first-child{
    color: red;
  }   
  li:last-child{
      color: green;
    } 
    p:first-child::first-letter {
    li:nth-child(7n){} 
    li:nth-child(7n-1){}  
    li:nth-last-child(-n+3){};                  
                              
按照父元素来查找(必须要有空格)
1.选择第一个元素 
父元素下面的子元素当中的第一个 (必须要有空格),不管后边是什么标签，只查找第一个。
ul :first-child{
     color: red;
}

2. 选择第几个元素
 父元素下面的子元素当中的第几个(注意是序号)
    ul :nth-child(5){
    color: red;
  }                       
                          
3. 查找奇数 
ul :nth-child(odd){} 
ul :nth-child(even){}                                            
                         
伪类选择器，not
   排除某些元素
.test:not([name="special"]){
   background-color: red;
}                           
                         
伪元素选择器
li::before{/*必须有内容 默认认为是行内元素*/
  content: "A";
}
li:after{
  content: "B";
}                                                   

选中第一个字(如果是单词，选中第一个字母)
li::first-letter{
      color: red;
}                                                

p::first-line{  
         color:green;
  }                     
                           
选中的颜色为绿色，背景为红色。
p:first-child::selection{
      color: green;
      background: red;
}                                                  
设置首字下沉 

    p:first-child::first-letter {
    font-size: 40px;
    float: left;
  }                      
                         
颜色

opacity 
子元素或继承父元素的透明度                   
                              
transparent  
不可调节，始终完全透明                         
rgba 
没有继承性，不影响子元素的颜色
background: rgba(255,0,0,0.5);                          
                              
文本阴影  text-shadow
1. 参数1  x轴方向的偏移
2. 参数2  y轴方向的偏移
3. 参数3  阴影的模糊度   不可为负值
4. 参数4  阴影的颜色                             
可以设置多个阴影，以英文逗号分隔。 
li:last-child{
    text-shadow:  3px 3px 5px #000 , -3px -3px 5px red;
}                                            