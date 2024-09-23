1 Object.keys()
var obj = { foo: "bar", baz: 42 };Object.keys(obj)// ["foo", "baz"]

2 Object.values()
var obj = { foo: "bar", baz: 42 };Object.values(obj)// ["bar", 42]

3 Object.entries
var obj = { foo: 'bar', baz: 42 };Object.entries(obj)// [ ["foo", "bar"], ["baz", 42] ]

Object.entries的基本用途是遍历对象的属性。
```javascript
for (let [k, v] of Object.entries(obj)) {
    console.log(`${JSON.stringify(k)}: ${JSON.stringify(v)}`);
}// "one": 1// "two": 2
```
