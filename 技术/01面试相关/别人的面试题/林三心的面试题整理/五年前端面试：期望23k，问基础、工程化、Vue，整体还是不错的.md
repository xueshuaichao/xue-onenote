  1. 技术选型的考虑
  -考虑跨平台
  -人气如何
  -生态
  -扩展性
  -维护活跃度
  
2.前优化做过哪些
  -lodash -> lodash-es
  -移动模块预加载
  -组件库

3.Vite 和 Webapck
相对来说，vite开发环境会相对快一点
- 为什么快?
vite是es module，webpack是全量的打包，所以会快一点

4.Template、JsX、Render?区别
我感觉jsx更具体一点，render有很多看不懂的地方
render函数更快一点，因为jsx也会去编译

5.你知道vue3里边 template和jsx哪个性能更好

6.vue3有哪些优化点，
响应式的优化proxy
diff算法的更新
静态提升

7.二次封装 localStorage 考虑哪些问题?

8.判断对象有环引用?
深度遍历，放到一个数组里边，如果数组中有这个对象了，就是环引用

9.nexttick？
nexttick是怎么获取到最新dom的？
是等updated之后执行

是微任务还是宏任务？
是微任务
10.Promise为什么支持链式调用
因为每次返回时会判断返回值是不是promise，如果不是，他会包装一层
promise去返回，所以支持链式调用

11.webpack5的treeshaking不需要配置，默认打开

12.你配置过cdn吗

13.项目题：有一个老项目，有很多计算表达式，之前没有精度丢失，切到新项目
现在有精度丢失了，里边有很多个，怎样统一处理
答：从webpack编译的抽象语法树，用babel工具通过标识符去判断，只要能找到表达式
通过一个方法就能修改
考察点：ast抽象语法树

14.虚拟列表的缺点
1.需要频繁的计算dom
2.因为频繁的计算导致有短暂的白屏现象，用预加载，先加载下边的20条

15.git rebase 和 git merge 的区别