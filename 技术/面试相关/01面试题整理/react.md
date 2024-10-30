​
### 1. react的生命周期：
```
componentWillMount
componentDidMount
componentWillReceiveProps
shouldComponentUpdate
componentWillupdate
componentDidupdate
componentWillUnmount
```

### react hooks 与class组件的区别在于什么，Hooks有什么优势，解决了什么问题
1.hooks不用将所有逻辑放到一个生命周期内，避免代码臃肿，可读性更高。
2.可以方便从组件中抽离状态逻辑，单独封装。


### 常用的hooks
>自变量
```
useState：更新状态，usestate 的返回值为状态数据和修改状态的方法；是异步的，也可以是同步的

useContext：用于在函数组件中使用 Context，可以很方便地获取到全局共享的数据；

useReducer：类似于 Redux 的 reducer，可以用于管理复杂的状态逻辑，可以传入初始状态和一个 reducer 函数，返回当前状态和 dispatch 方法；
```

> 因变量  
```
useEffect：模拟一些生命周期，处理一些状态的副作用，请求接口；

useMemo：返回一个缓存值，当依赖项没有发生变化时，可以避免重复计算；

useCallback：缓存一个函数，避免在每次渲染时创建新的回调函数，从而提升性能；
```
```
useRef：用于在函数组件中获取对 DOM 元素或组件实例的引用，也可以用来存储任意可变值。

useLayoutEffect 比 useEffect 的时机更提前一些

useImperativeHandle：一般会和 forwardRef,
```

### useLayoutEffect和useEffect的区别
执行时机：useEffect在所有DOM变更完成后执行，通常在浏览器的绘制过程中；而useLayoutEffect在DOM变更之前执行，这意味着它在浏览器绘制之前同步运行。
性能：由于useLayoutEffect在绘制前执行，因此它可能会导致重排和重绘，影响性能。如果你的副作用不依赖于布局信息，通常建议使用useEffect。

何时使用useLayoutEffect？
  useLayoutEffect适用于需要直接读取DOM布局或同步修改DOM布局的场景。例如，当你需要基于容器的大小来计算样式或进行布局调整时，useLayoutEffect是合适的选择。
```js
function ResizeObserver() {
  const ref = React.useRef(null);

  useLayoutEffect(() => {
    if (ref.current) {
      const observer = new ResizeObserver(entries => {
        console.log('Container size:', entries[0].contentRect);
      });

      observer.observe(ref.current);
      return () => observer.disconnect();
    }
  }, []);

  return <div ref={ref}>Resize me!</div>;
}

```


### purecomponent
PureComponent其实就是一个继承自Component的子类，会自动加载shouldComponentUpdate函数。当组件需要更新的时候，shouldComponentUpdate会对组件的props和state进行一次浅比较。如果props和state都没有发生变化，则不会更新


### react 组件间的通信
1. 父子组件：props + 回调函数，也可通过ref方式获取
2. 爷孙组件：两层父子通信或者使用 Context.Provider和 Context.Consumer
3. 任意组件通信：通过消息订阅-发布的一些库(pubSub)、也可通过集中式管理(Redux、Mobx)
mobx比redux简洁很多，没那么重
```javascript
// PubSub
import PubSub from ‘pubsub-js’ //引入
PubSub.publish(‘delete’, data) //发布消息
PubSub.subscribe(‘delete’, function(data){ }); //订阅
```


### 5、key使用index会有什么问题
key是这条数据唯一的标识，用来追踪列表中哪条元素进行变动了。如果key用index，如果数组某项数据删除，以前的数据和重新渲染后的数据没法建立关联关系. 这就失去了 key 值存在的意义，可能就会导致数据错乱。一般都会使用每条数据的id，因为id是唯一的



### 15、了解redux吗？
redux是公共管理状态的，主要有三个核心方法，action,reducer,store，工作流程就是view调用dispatch触发action，action可以写异步操作，然后分发dispatch，reducer会根据action分发的dispatch中的type和state来更新状态。当我们在组件中使用则需要使用connect将组件与store连接起来。

1.我们先写一个createAction的函数
```javascript
export function setAnalysisParams(params) {
  return {
    type: SET_ANALYSIS_PARAMS,
    result: params
  }
}


2.在reducer里面：
export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    case SET_ANALYSIS_PARAMS:
      return {
        ...state,
        params: action.result
      };
    default:
      return state;
  }
```
当action触发reducer时，会把action的result传给reducer的params。写好这里，我们就可以在组件中传给adction params了。


3.先把actionCreator拿出来。
在组件的某个需要的地方，可以直接向它传我们要放进redux里的数据：
```javascript
this.props.setAnalysisParams({
  someModels
});

@connect(
  () => ({
  }),
  {
    setAnalysisParams
  })
```

这时，我们就可以在另外一个组件中取到刚刚放进去的数据。
另外一个组件：
```javascript
@connect(
  state => ({
    example: state.clinic.params
  }),
  {}
)
```

把redux中的params数据映射到example上。
下面，就可以用了：
```javascript
const {someNames, ...} = this.props.example; //取出数据名
```



# 27、react框架的优点
1、react速度快，因为含有虚拟dom
2、组件化，便于维护
3、单向数据流，便于阅读代码
4、纯粹的javaScript语法，没有任何专有的react语法





### 28、vue框架和react框架的区别
- 相同点：
1.都是数据驱动视图
2.都用了虚拟dom和diff算法
3.都提倡组件化

- 不同点：
1.react的数据流向比较清晰
react主张函数式编程，单向数据流，数据流向比较清晰，当然需要双向的地方也可以手动实现，比如借助 onChange 和 setState 来实现一个双向的数据流。
vue是双向数据绑定，通过v-model实现数据和视图的同步更新，就可能比较乱，比如在pinia中，可以直接通过赋值修改pinia中的值。这就不太好


2.性能优化
vue中的每个组件内部自动实现了,不需要手动优化
vue会跟踪每一个组件的依赖关系(比如静态标记)，更快地计算出Virtual DOM的差异，不需要重新渲染整个组件树。
而对于React而言,每当应用的状态被改变时,全部组件都会重新渲染,所以react需要shouldComponentUpdate手动去优化其性能。

但是当数据特别多的时候vue中的watcher也会特别多，从而造成页面卡顿，所以一般数据比较多的大型项目会倾向于使用react。在react官网中，官方也建议我们使用React来构建快速响应的大型 Web 应用程序。

3.方便性
但现在vue升级到3后，增加了很多小东西，比如状态的赋值要不要加value就很繁琐。不够优雅。比如现在我想看数据的变化必须要写个watcher。

4、模板渲染方式的不同
react使用jsx语法，把html和css全都写进js中，vue使用html模板，就是在html中写css和js，最后再用webpack和vue-loader进行打包，这种编码方式对于初学者而言是很舒服的



### 29 什么是高阶组件，以及举例说一个你封装过的高阶组件   简称(HOC)
- 高阶组件就是一个函数，接受一个组件作为参数返回一个新的组件
const EnhancedComponent = higherOrderComponent(MyComponent);
higherOrderComponent就是我们的高阶组件，在其中可以加入各种逻辑来增强我们的 MyComponent

- 高阶组件的应用场景
```javascript
权限控制: 利用高阶组件的 条件渲染 特性可以对页面进行权限控制

// HOC.js    
function withAdminAuth(WrappedComponent) {    
    return class extends React.Component {    
        state = {    
            isAdmin: false,    
        }    
        async componentWillMount() {    
            const currentRole = await getCurrentUserRole();    
            this.setState({    
                isAdmin: currentRole === 'Admin',    
            });    
        }    
        render() {    
            if (this.state.isAdmin) {    
                return &lt;WrappedComponent {...this.props} /&gt;;    
            } else {    
                return (&lt;div&gt;您没有权限查看该页面，请联系管理员！&lt;/div&gt;);    
            }    
        }    
    };    
}

// 使用
// pages/page-a.js    
class PageA extends React.Component {    
    constructor(props) {    
        super(props);    
        // something here...    
    }    
    componentWillMount() {    
        // fetching data    
    }    
    render() {    
        // render page with data    
    }    
}    
export default withAdminAuth(PageA);
```


### 使用React Hooks实现自定义Hooks
要使用React Hooks来实现自定义Hooks，首先需要创建一个函数，该函数的名称通常以"use"开头，例如"useCustomHook"。在函数中，可以使用React提供的Hooks（例如useState、useEffect等）来管理状态和副作用。

以下是一个简单的示例，演示了如何创建一个自定义Hooks来管理计数器的状态：
```js
import React, { useState } from 'react';

const useCounter = (initialCount) => {
  const [count, setCount] = useState(initialCount);

  const increment = () => {
    setCount(count + 1);
  };

  const decrement = () => {
    setCount(count - 1);
  };

  return [count, increment, decrement];
};

export default useCounter;
```

```js
const Counter = () => {
  const [count, increment, decrement] = useCounter(0);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
};

export default Counter;
```


### React父级获取子级的数据的方式
 1. 使用ref属性获取子组件实例，然后直接访问其状态或方法。
```javascript
this.child.current.getData()
```

 1. useImperativeHandle
```javascript
// 父组件
ChildRef.current.func();

// 子组件
useImperativeHandle(props.onRef，()=>{
  // 需要将暴露的接口返回出去
  return {
    func:func
  }
})
```




### react如何减少组件重渲染
1. 使用 useCallback 和 useMemo 钩子（仅适用于函数组件）: 这些钩子可以帮助你记住回调函数或经常使用的值，以避免它们在每次渲染时都被创建。
2. 使用 useRef 钩子来存储可变状态。
3. React.PureComponent 或 React.memo（推荐使用函数组件的memo方式）: 这些组件自动实现浅比较，避免不必要的重渲染。
4. 给列表增加key值
5. 将频繁触发的状态抽离出来，单独封装，比如音量变化组件

以下是使用 React.memo 的例子：

### react fiber架构
在老的版本里，react的挂在和更新是利用深度优先遍历，一直执行到底，如果你的组件特别复杂，这个过程js耗时比较长，在极端情况下会花费几秒的时间，用户页面会卡顿，体验差
 从16.8版本开始，引入fiber概念，中文翻译为细小，纤维，简单讲，fiber将之前的组件更新从一个大的任务拆分为很多细小的task，所有组件的更新任务从一个task变为多个task。
 这些任务可以打断，回滚。那task的拆分带来哪些变化？这里涉及到大名鼎鼎的requestIdlecallback。这个是浏览器新的api，可以获取浏览器的空闲时间，之前说过浏览器的主线程
 主要分为js和渲染，其他的暂时忽略。主线程每过16.6ms会把渲染任务拉过来执行一下，也就变成了页面中的每秒60帧，16.6ms里又包含了js的执行，之前说过时间循环虽然是个永不停歇的循环，但永不停歇的循环并不占用cpu资源，除非你的js在执行任务，在这16.6ms里减去渲染和js执行花费的时间，那就是空闲时间。接下来再看fiber为什么可以解决更新非常复杂时的卡顿问题，举个例子，用户在input输入一段内容，task本身有优先级定义，用户的输入是最高优先级，会优先执行这个task，这是第一点。第二点，因为我们用浏览器的空闲时间去
 执行task，意味着不管我的更新任务多么庞大，每16.6ms浏览器都会得到一个喘息的机会，都会把执行权交给主线程。所以页面才可以得到渲染。 不过在最新的18版本的react中，并没有使用requestIdlecallback，而是用messagechannel，做了一个模拟，间隔时间大概是5ms左右，因为兼容性问题，

 vue3.0为什么只抄了hooks，没有抄fiber
 因为vue本身就是响应式精准更新，哪里变了改哪里，跟react底层原理不一样，react是自顶向下更新，所以vue不需要