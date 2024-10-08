aspect ratio翻译为中文就是宽高比（也称：纵横比）即x:y。
为什么会有这个属性呢？
因为，一般情况下只有某些替换的元素具有长宽比，尤其是图像。对于它们，如果仅指定宽度和高度之一，则可以使用固有长宽比从中计算出另一个。然而对于大多数元素是不具有此性质的，此属性允许为任何其他元素显式指定长宽比，以获得相似的行为。

2、之前的解决方案：Padding-Top Hack

3、使用aspect-ratio
```css
.preferably-square {
  width: 300px;
  aspect-ratio: 2 / 1;
}
表示该元素的高为150px


.preferably-square {
  width: 300px;
  aspect-ratio: auto 2 / 1;
}
```
如果可替换元素和非可替换元素同时使用该样式，
则可替换元素执行auto样式，即维持其自身固有的宽高比
非可替换元素执行则执行 2/1的宽高比

```css
.preferably-square {
  width: 300px;
  aspect-ratio: 2 / 1;
}
```
如果可替换元素和非可替换元素同时使用该样式，则都执行2/1的宽高比








