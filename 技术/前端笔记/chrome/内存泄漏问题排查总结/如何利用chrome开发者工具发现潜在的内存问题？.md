
### 发现脱离文档的节点
![alt text](assets/image-25.png)
今天给大家分享下，js内存分析中一个很重要的概念叫做 detached dom node
为什么说重要，因为日常遇到的很多关于内存泄漏的问题都是他造成的

比如上边的实例，一直往window的nodes对象中push节点，没有释放

参见别的文档：经典：JavaScript内存泄漏（二）.md







































