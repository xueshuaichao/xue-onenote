
## 是时候用 rel=“preload“ 来加速你的网站了
相关链接：https://blog.csdn.net/liangshanbo1215/article/details/142257503
### 什么是rel="preload"？
rel=“preload”属性允许您告诉浏览器在页面呈现期间需要某些资源之前开始下载它们。通过这样做，您可以确保更快地获取字体、样式表或脚本等关键资源，从而减少页面完全呈现所需的时间。

简单地说，你给浏览器一个提示，说明哪些文件对流畅的体验很重要。

### 为什么要使用Preload？
大多数Web性能优化都专注于减少加载资源所需的时间。当有关键资源（如字体、CSS或JavaScript文件）直接影响页面显示和功能的速度时，预加载特别有用。

以下是 preload 如何提供帮助：

1.减少渲染阻塞：通过预加载关键的CSS或字体，您可以避免渲染阻塞问题，即页面在显示内容之前等待加载这些资源。
2.改进首次内容绘制（FCP）：预加载可确保更快地下载重要资源，从而提高首次视觉内容显示给用户的速度。
3.更好的用户体验：更快的加载页面感觉更灵敏，并增强了整体用户体验，特别是对于资源密集型资源，如字体或英雄图像。

### 什么类型的内容可以被预加载？
可以预加载多种类型的内容。as 属性可能的值包括：

audio：音频文件，通常在 <audio> 中使用。
document：用于嵌入在 <frame> 或 <iframe> 中的 HTML 文档。
font：字体文件。
image：图像文件。
script：JavaScript 文件。
style：CSS 样式表。
worker：JavaScript web worker 或 shared worker。
video：视频文件，通常在 <video> 中使用。

> 备注：预加载 font 和 fetch 资源需要设置 crossorigin 属性；

### 语法和用法 
让我们从一个如何使用rel=“preload”的基本示例开始。下面是一个简单的HTML代码片段，演示了如何预加载自定义字体：
```html
<link rel="preload" href="/fonts/MyFont.woff2" as="font" type="font/woff2" crossorigin="anonymous">
```
在本例中：

href 指定资源的URL。

as 指示资源的类型（例如，字体、图像、脚本）。

type 帮助浏览器理解文件的确切格式（对于字体很有用）。

crossorigin 从不同域加载资源时需要跨域。浏览器看到这个标签，知道要尽早下载字体，即使使用该字体的CSS尚未应用。

### 使用rel=“preload”的最佳实践

虽然preload是一个强大的工具，但您应该仔细使用它。以下是一些最佳实践：

1.仅预加载关键资源：预加载所有内容实际上会降低网站的速度。坚持使用初始页面呈现所必需的资源。
2.对外部资源使用crossorigin：从不同的域预加载资源时，请确保包含crossorigin属性。这可以确保您的资源可以正确获取，而不会出现CORS问题。
3.确保正确的缓存处理：预加载的资源应该是可缓存的，以防止冗余的网络请求。这将减少服务器和用户浏览器的负载。
4.不要预加载所有内容：过度预加载会对浏览器造成不必要的压力，导致性能下降。仅预加载关键渲染路径所必需的资源。

在您的网站上使用rel=“preload”的示例
这里有一个完整的例子，说明如何在一个典型的网页中集成rel=“preload”：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Preload Example</title>
 
    <!-- Preload important resources -->
    <link rel="preload" href="/fonts/OpenSans.woff2" as="font" type="font/woff2" crossorigin="anonymous">
    <link rel="preload" href="/css/main.css" as="style">
    <link rel="preload" href="/scripts/main.js" as="script">
    <link rel="preload" href="/images/hero.jpg" as="image">
 
    <!-- Link stylesheet -->
    <link rel="stylesheet" href="/css/main.css">
</head>
<body>
    <header>
        <h1>Preload Example</h1>
        <img src="/images/hero.jpg" alt="Hero Image">
    </header>
 
    <script src="/scripts/main.js"></script>
</body>
</html>
```

### 什么时候不使用rel=“preload”
虽然preload功能强大，但它并不是所有资源的神奇解决方案。以下是您可能希望避免使用它的几种情况：
1.非关键资源：不要预加载对页面的初始呈现不重要的资源。
2.不可预测的资源：如果某些资源是有条件的或取决于用户交互（例如折叠下方图像或延迟的JavaScript），最好让浏览器在需要时获取它们。

### 结论
使用rel=“preload”是一种简单而有效的方法，可以通过告诉浏览器尽快获取关键资源来加速您的网站。通过专注于预加载基本资源，如字体、样式表和图像，您可以减少加载时间并增强用户体验。













































