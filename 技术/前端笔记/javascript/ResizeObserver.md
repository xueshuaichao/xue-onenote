
ResizeObserver 是浏览器提供的一个现代 API，用于监听 DOM 元素尺寸的变化（如宽度、高度变化）。相比传统的 resize 事件（仅适用于 window 对象），ResizeObserver 可以更高效、精准地监听任意元素的尺寸变化。


### 为什么需要 ResizeObserver？
1.传统方式的局限性
过去监听元素尺寸变化需依赖 window.resize 事件或手动轮询（如 setInterval 检查元素尺寸），但这些方法性能开销大且不够精准。

2.响应式设计需求
现代前端需要动态响应元素尺寸变化（如布局调整、图表重绘、自适应组件），ResizeObserver 为此提供了标准化解决方案。

### 基本用法
```js
// 1. 创建 ResizeObserver 实例
const observer = new ResizeObserver((entries) => {
  for (const entry of entries) {
    // entry 包含目标元素尺寸变化的详细信息
    console.log('元素尺寸变化:', entry.target, entry.contentRect);
  }
});

// 2. 监听目标元素
const targetElement = document.querySelector('.box');
observer.observe(targetElement); // 开始监听

// 3. 停止监听
observer.unobserve(targetElement); // 停止监听单个元素
observer.disconnect(); // 停止所有监听并释放资源
```

### ResizeObserverEntry 对象
回调函数的参数 entries 是一个 ResizeObserverEntry 数组，每个对象包含以下关键属性：
- target：被监听的 DOM 元素。
- contentRect：返回元素的尺寸和位置信息（如 width, height, top, left 等）。
- borderBoxSize / contentBoxSize：返回更详细的尺寸信息（具体取决于浏览器支持）。

### 实际应用场景
1. 响应式布局
动态调整布局或样式，例如容器查询（Container Queries）的替代方案。
```js
new ResizeObserver((entries) => {
  const entry = entries[0];
  if (entry.contentRect.width < 600) {
    entry.target.classList.add('mobile-mode');
  } else {
    entry.target.classList.remove('mobile-mode');
  }
}).observe(container);
```

注意：
ResizeObserver 并非 ECMAScript（ES）标准的一部分，而是由浏览器实现的 Web API，属于现代浏览器提供的原生功能。它首次在浏览器中被广泛支持的时间可以追溯到 2020 年 7 月


