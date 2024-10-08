### cssText 本质是什么？
cssText 的本质就是设置 HTML 元素的 style 属性值。
document.getElementById("d1").style.cssText = "color:red; font-size:13px;";
但在ie中兼容性不好，这里暂不讨论

### cssText的使用优势
一般情况下我们用js设置元素对象的样式会使用这样的形式：
var element= document.getElementById(“id”);
element.style.width=”20px”;
element.style.height=”20px”;
element.style.border=”solid 1px red”;
样式一多，代码就很多；而且通过JS来覆写对象的样式是比较典型的一种销毁原样式并重建的过程，这种销毁和重建，都会增加浏览器的开销。

element.style.cssText=”width:20px;height:20px;border:solid 1px red;”;
这样就可以尽量避免页面reflow，提高页面性能。

但是，这样会有一个问题，会把原有的cssText清掉，比如原来的style中有’display:none;’，那么执行完上面的JS后，display就被删掉了。
为了解决这个问题，可以采用cssText累加的方法：
Element.style.cssText += ‘width:100px;height:100px;top:100px;left:100px;’
因此，上面cssText累加的方法在IE中是无效的。
最后，可以在前面添加一个分号来解决这个问题：
Element.style.cssText += ‘;width:100px;height:100px;top:100px;left:100px;’

















