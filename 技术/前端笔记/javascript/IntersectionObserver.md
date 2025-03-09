
IntersectionObserver 是 JavaScript 中用于异步监测目标元素与祖先元素或视口（viewport）交叉状态的 API。它常用于实现懒加载、无限滚动、曝光统计等功能，相比传统的 scroll 事件监听更高效。

### 基础用法
1. 创建观察器
```js
const observer = new IntersectionObserver((entries, observer) => {
  // entries: 被观察的元素数组
  // observer: 观察器实例
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // 元素进入视口时触发
      console.log("元素可见！", entry.target);
    } else {
      // 元素离开视口时触发
      console.log("元素隐藏！", entry.target);
    }
  });
}, {
  // 可选配置选项
  root: null,       // 默认视口，也可指定父元素
  rootMargin: '0px',// 提前/延迟触发的边距（如 '100px' 或 '0px 0px -20% 0px'）
  threshold: 0.5    // 触发回调的交叉比例（0-1，或数组 [0, 0.25, 0.5, 1]）
});
```

2. 观察目标元素
```js
const targetElement = document.querySelector('#myElement');
observer.observe(targetElement); // 开始观察
```
3. 停止观察
```js
observer.unobserve(targetElement); // 停止观察单个元素
observer.disconnect(); // 停止所有观察
```

### 关键参数解释
1.root: 观察的根元素，默认是视口（null），也可以是某个父元素。
2.rootMargin: 类似 CSS 的 margin，用于扩展或缩小交叉区域。例如 '100px 0px' 表示在视口顶部和底部外扩 100px 的范围内触发，左右不扩展。
3.threshold:
- 单个数值（如 0.1）：当交叉比例达到 10% 时触发。
- 数组（如 [0, 0.25, 0.5, 1]）：在多个比例点触发回调。


### 实际案例
1. 图片懒加载
```js
<img data-src="real-image.jpg" class="lazy-load" />

<script>
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src; // 替换为真实图片地址
      observer.unobserve(img); // 加载后停止观察
    }
  });
}, { rootMargin: '200px 0px' }); // 顶部和底部提前 200px 加载，左右不扩展

document.querySelectorAll('.lazy-load').forEach(img => observer.observe(img));
</script>
```

2. 无限滚动加载
```js
const sentinel = document.querySelector('#load-more-trigger');
const observer = new IntersectionObserver((entries) => {
  if (entries[0].isIntersecting) {
    loadMoreContent(); // 加载更多内容的函数
  }
});

observer.observe(sentinel); // 观察底部触发元素
```

3. 广告曝光统计
```js
const ad = document.querySelector('#ad');
const observer = new IntersectionObserver((entries) => {
  if (entries[0].isIntersecting) {
    sendImpressionLog(); // 发送曝光日志
    observer.unobserve(ad); // 仅统计一次
  }
}, { threshold: 0.5 }); // 至少 50% 可见时触发

observer.observe(ad);
```
































