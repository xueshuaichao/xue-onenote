今天用到了具体promise的用法，了解一下。
 // 手动上传图片
```js
handleBeforeUpload(data) {
  // 检查图片尺寸是否合格，合格就执行上传操作
  this.checkFile(data).then(()=>{
      this.uploadImage(data);
  })
 
  return false;
}
```
```js
checkFile(data) {
  return new Promise((resolve, reject) => {
      if (data.size > this.maxSize) {
          this.$Message.error('请上传合适大小的图片');
          reject();
      } else{
          var filePic = data;
          var reader = new FileReader();
          reader.onload =  (e) =>{
              var data = e.target.result;
              //加载图片获取图片真实宽度和高度
              var image = new Image();
          
              image.onload=()=>{
                  var width = image.width;
                  var height = image.height;
                  if(width===924 && height===376){
                      resolve();
                  }else{
                      this.$Message.error('图片尺寸不正确');
                      reject();
                  }
              };
              image.src= data;
          };
          reader.readAsDataURL(filePic);
      }
      
  });
},
```              
这是一个图片上传的方法。我完全可以在this.checkFile中放一个callback，无论成功还是失败调用回调函数，另一种方法如下所示，用promise用法。
两种用法对比：
promise用法：
1. 调用checkFile要加.then 用来处理resolve操作。
2. checkFile中要写成new Promise 用法，再写上触发resolve和reject的情况。
回调函数用法：
1. 调用checkFile时传入回调函数。
2. checkFile中正常写逻辑，然后调用成功回调和失败回调。
推荐使用promise用法，因为是趋势。具体到什么时候用呢？凡是用到回调函数的地方都可以用promise。
