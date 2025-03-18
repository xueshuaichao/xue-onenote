
在前端优化中，避免阻塞渲染的脚本是提升首屏加载速度的关键策略之一。通过合理使用 `<script> `标签的 async 和 defer 属性，可以显著减少 JavaScript 对页面渲染的阻塞。以下是详细解析：

一、默认的脚本加载行为
默认情况下，浏览器解析 HTML 时遇到 <script> 标签会立即停止解析（即 阻塞 DOM 构建），并执行以下操作：
1.下载脚本：从服务器获取脚本文件。
2.执行脚本：立即执行下载的脚本。
3.恢复解析：脚本执行完成后，继续解析后续 HTML。

这种行为会导致：
1.页面渲染延迟：用户需要等待脚本下载和执行完成后才能看到内容。
2.首屏时间（FCP/LCP）变长：尤其当脚本体积大或网络较慢时，影响更明显。


二、async 与 defer 的作用
通过 async 和 defer 属性，可以改变脚本的加载和执行行为，从而减少阻塞：

1.async（异步脚本）
- 行为：
  - 异步下载脚本，不阻塞 HTML 解析。
  - 脚本下载完成后立即执行（可能在 HTML 解析完成前或完成后）。
  - 多个 async 脚本的执行顺序不确定（先下载完的先执行）。

- 适用场景：
  - 独立脚本，不依赖其他脚本或 DOM。
  - 如：统计代码（Analytics）、广告脚本等。

- 示例：
```html
<script async src="analytics.js"></script>
```

2.defer（延迟脚本）
- 行为：
  - 异步下载脚本，不阻塞 HTML 解析。
  - 脚本下载完成后等待 HTML 解析完成，再按顺序执行。
  - 多个 defer 脚本按文档顺序执行。

- 适用场景：
  - 依赖 DOM 或其他脚本的代码。
  - 如：初始化页面逻辑的脚本、第三方库（需保证执行顺序）。

- 示例：
```html
<script defer src="vendor.js"></script>
<script defer src="app.js"></script>  <!-- 确保 vendor.js 先执行 -->
```

三、对比与执行时机
属性	  下载行为	        执行时机	                执行顺序	          是否阻塞渲染
无属性	立即下载并阻塞解析	下载完成后立即执行	        文档顺序	是
async	 异步下载，不阻塞解析	下载完成后立即执行	        不确定（谁先下载完谁先执行）	可能阻塞（若执行时间长）
defer	 异步下载，不阻塞解析	HTML 解析完成后，按文档顺序执行	文档顺序	            否

- 关键时间点示意图
HTML 解析开始
│
├── 遇到普通 <script>       → 阻塞解析，下载并执行 → 恢复解析
│
├── 遇到 <script async>     → 异步下载，下载完成后立即执行（可能中断解析）
│
├── 遇到 <script defer>     → 异步下载，延迟到 HTML 解析完成后执行
│
└── HTML 解析完成 → 触发 DOMContentLoaded 事件 → 执行所有 defer 脚本 → 触发 load 事件

四、最佳实践与注意事项
1.优先使用 defer：
  - 适用于大多数需要操作 DOM 或有依赖关系的脚本，确保执行顺序且不阻塞渲染。
2.谨慎使用 async：
  - 仅用于完全独立且无需等待 DOM 或其他脚本的代码（如监控脚本）。
3.内联脚本的优化：
  - 内联脚本（无 src 的 <script>）无法使用 async/defer，建议将其移至页面底部或异步加载。
4.动态脚本加载：
  - 通过 JavaScript 动态创建 <script> 标签并插入 DOM，默认行为类似 async，可手动设置为 defer：

```js
const script = document.createElement('script');
script.src = 'app.js';
script.defer = true; // 设置为 defer 行为
document.head.appendChild(script);
```

5.模块化脚本（ES6 Modules）：
  - 使用 type="module" 的脚本默认具有 defer 行为，但可通过 async 覆盖：
```html
<script type="module" src="app.js"></script>        <!-- 等效于 defer -->
<script type="module" async src="analytics.js"></script> <!-- 等效于 async -->
```

五、实际优化案例
假设页面有以下脚本：
```html
<script src="heavy-library.js"></script> <!-- 大型库，阻塞渲染 -->
<script src="main.js"></script>          <!-- 依赖 heavy-library.js -->
```

- 优化步骤：

1.添加 defer 到所有脚本，确保按顺序执行且不阻塞：
```html
<script defer src="heavy-library.js"></script>
<script defer src="main.js"></script>
```

2.若 heavy-library.js 无需立即执行，可进一步使用 async（需确保无依赖）：

```html
<script async src="heavy-library.js"></script>
<script defer src="main.js"></script> <!-- 需确保 heavy-library.js 已加载 -->
```

六、验证与监控
使用工具验证优化效果：
- Lighthouse：检查“减少阻塞渲染的资源”建议。
- Chrome DevTools → Network 面板：观察脚本加载时序。
- Performance 面板：分析主线程是否被脚本执行阻塞。




































