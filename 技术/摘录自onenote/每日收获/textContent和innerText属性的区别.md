```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
            <title>
            </title>
        </meta>
    </head>
    <body>
        <div class="test" id="test">
            test
            <div style="display:none">
                <span>
                    test
                </span>
            </div>
            <style>
                hi
            </style>
        </div>
        <script type="text/javascript">
            var testDiv = document.getElementById('test');
        console.log("我是textContent输出的"+testDiv.textContent);
        console.log("我是innerText输出的"+testDiv.innerText);
        </script>
    </body>
</html>
```

输出的结果：
我是textContent输出的testtesthi
我是innerText输出的test

1.主要差异
- textContent 会获取style= “display:none” 中的文本，而innerText不会
- textContent 会获取style标签里面的文本，而innerText

实例2：
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
            <title>
            </title>
        </meta>
    </head>
    <body>
        <div class="test" id="test">
            test
            <div style="display:none">
                <span>
                    test
                </span>
            </div>
            <p>
                hi
            </p>
        </div>
        <script type="text/javascript">
        var testDiv = document.getElementById('test');
        console.log("我是textContent输出的"+testDiv.textContent);
        console.log("我是innerText输出的"+testDiv.innerText);
        </script>
    </body>
</html>
```
输出结果：
```
我是textContent输出的
            test


                    test



                hi

我是innerText输出的test
hi
```

差异：
1. textContent不会理会html格式，直接输出不换行的文本
2. innerText会根据标签里面的元素独立一行

3.兼容性：
innerText 对IE的兼容性较好
textContent虽然作为标准方法但是只支持IE8+以上的浏览器
最新的浏览器，两个都可以使用















