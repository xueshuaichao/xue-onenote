Global对象的encodeURL()和encodeURLComponent()方法可以对URL进行编码。有效的URL中不能包含某些字符串，例如空格。他们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器理解。

encodeURL()主要用于整个URL，而encodeURLComponent()主要用于对URL中的某一段。它们的区别在于，encodeURL()不会对本身属性url的特殊字符进行编码，例如“冒号、正斜杠、问号、井号”；而encodeURLComponent()则会对它发现的任何非标准字符进行编码。

```javascript
  let url = 'https://www.baidu.com/123456789/story'
  let encode = encodeURI(url) 
  let encodeComponent = encodeURIComponent(url)
  console.log(encode) // https://www.baidu.com/123456789/story
  console.log(encodeComponent) // https%3A%2F%2Fwww.baidu.com%2123456789%2Fstory
 let decode = decodeURI(encode) // encode 对应上面的代码
 let decodeComponent = decodeURIComponent(encodeComponent)
 console.log(decode) // https://www.baidu.com/123456789/story
 console.log(decodeComponent) // https://www.baidu.com/123456789/story
```
