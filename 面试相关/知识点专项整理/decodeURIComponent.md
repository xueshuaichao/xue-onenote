在url跳转的时候，传参可能会有一些中文，因此就涉及到对url进行编码，接受放进行解码。
使用方式：
encodeURI(url) - 编码
decodeURI(url) - 解码
encodeURIComponent(url) - 编码
decodeURIComponent(url) - 解码
二者区别：
二者都对一些特殊字符不进行编码，encodeURI不编码的字符有82个，而encodeURIComponent不编码的字符有71个。
也就是说encodeURL不会处理#、;、/、?、:、@、&、=、+、$、,这些字符。