
## path.join和path.resolve的区别

resolve和join都用来进行路径片段的连接，但是区别有两点：
  1. resolve会生成绝对路径，而join只是返回当前连接的路径。
  2. resolve会以最后出现的 ‘/’为起点，作为根路径，忽略前面的片段，而join不会。
举例如下：
  1. resolve
console.log(path.resolve())      // returns /workspace/demo
console.log(path.resolve(''))     // returns /workspace/demo
console.log(path.resolve(__dirname)) // returns /workspace/demo
console.log(path.resolve('/img/books', '/net'))  // returns '/net'
console.log(path.resolve('img/books', '/net'))  // returns '/net'
console.log(path.resolve('img/books', './net'))  // returns '/workspace/demo/img/books/net'
console.log(path.resolve('/img/books', './net'))  // returns '/img/books/net'
console.log(path.resolve('/img/books', 'net'))   // returns '/img/books/net'
console.log(path.resolve('/img/books', '../net'))     // returns '/img/net'
console.log(path.resolve('src','/img/books', '../net'))  // returns '/img/net'
console.log(path.resolve('src','./img/books', '../net'))  // returns '/workspace/demo/src/img/net'
console.log(path.resolve('src','img/books', '../net'))   // returns '/workspace/demo/src/img/net'


  2. join
path.join('/img', 'book', 'net/abc', 'inter', '..'); // returns /img/book/net/abc
console.log(path.join('/img/books', '../net'))  // returns /img/net
console.log(path.join('img/books', '../net'))   // returns img/net
console.log(path.join('/img/books', './net'))   // returns /img/books/net
console.log(path.join('img/books', './net'))   // returns img/books/net
console.log(path.join('/img/books', 'net'))    // returns /img/books/net
console.log(path.join('img/books', 'net'))    // returns /img/books/net
console.log(path.join('/img/books', '/net'))   // returns /img/books/net
console.log(path.join('img/books', '/net'))    // returns img/books/net



1. 对于以/开始的路径片段，path.join只是简单的将该路径片段进行拼接，而path.resolve将以/开始的路径片段作为根目录，在此之前的路径将会被丢弃，就像是在terminal中使用cd命令一样。
path.join('/a', '/b') // 'a/b'
path.resolve('/a', '/b') // '/b'
 
2. path.resolve总是返回一个以相对于当前的工作目录（working directory）的绝对路径。
path.join('./a', './b') // 'a/b'
path.resolve('./a', './b') // '/Users/username/Projects/webpack-demo/a/b'



