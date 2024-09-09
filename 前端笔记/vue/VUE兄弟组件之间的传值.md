 ## 兄弟组件之间的传值
兄弟组件之间的传值和父子组件之间的传值非常相似，都是通过$emit;

 ### 原理是：vue一个新的实例，类似于一个站，连接着两个组件，也就是一个中央事件总线；
下面是一个bus实例：

eventBus.js
```javascript
import Vue from 'Vue
export default new Vue;
```

1、创建一个firstChild组件，引入bus,接着一个按绑定数据传输事件：
firstChild.js
```javascript
<script>
import bus from'../assets/eventBus';
export default{
  methods:{
    sendMsg:function(){
      bus.$emit("userDefinedEvent","thismessage is fromfirstchild");
    }
  }
}

</script>
```
我们通过一个$emit自定义一个事件，并传递数据；
$emit实例方法触发当前实例(这里的当前实例就是bus)上的事件,附加参数都会传给监听器回调。
下面是另一个组件，引入bus实例，通过一个p标签接收数据：
```javascript
<script>
import bus from'../assets/eventBus';
export default{
  data(){
    return {
      msg:"默认值"
    }
  },
  mounted(){
    var self=this;
    bus.$on("userDefinedEvent",function(msg){
      self.msg=msg;
    });
  }
}
</script>
```

这个组件的mounted里，我们监听了userDefinedEvent事件，并把传递过来的事件通过$on监听回调函数；

on:监听当前实例上的自定义事件(此处当前实例为bus)。事件可以由on:监听当前实例上的自定义事件(此处当前实例为bus)。事件可以由on:监听当前实例上的自定义事件(此处当前实例为bus)。事件可以由emit触发，回调函数会接收所有传入事件触发函数($emit)的额外参数。

 ### 总结:
1，首先创建一个事件总线，例如bus，作为一个通讯的桥梁；
2，在需要传值的组件中，通过emit触发一个自定义事件，并传递参数；
3，在接收数据的组件中，通过emit触发一个自定义事件，并传递参数；
3，在接收数据的组件中，通过emit触发一个自定义事件，并传递参数；
3，在接收数据的组件中，通过on监听自定义事件，并处理传递过来的参数；
另外：
1、兄弟组件之间与父子组件之间的数据交互，两者相比较，兄弟组件之间的通信其实和子组件向父组件传值有些类似，其实他们的通信原理都是相同的，例如子向父传值也是emit和emit和emit和on的形式，只是没有eventBus，但若我们仔细想想，此时父组件其实就充当了bus这个事件总线的角色。
2、这种用一个Vue实例来作为中央事件总线来管理组件通信的方法只适用于通信需求简单一点的项目，对于更复杂的情况，Vue也有提供更复杂的状态管理模式Vuex来进行处理。
在项目中，可以简化
```javascript
Vue.prototype.$eventBus=newVue();
this.$eventBus.$on('on-play',(id)=>{this.currentResourceId=id;})
```
