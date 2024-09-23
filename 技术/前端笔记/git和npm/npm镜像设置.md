
 ## npm 设置淘宝镜像


 ### npm设置淘宝镜像
```javascript
npm config set registry https://registry.npmmirror.com
// 查看源
npm config get registry
// 切回官方镜像
npm config set registry https://registry.npmjs.org
// 查看npm设置
npm config list
```

 ### yarn设置淘宝镜像
```javascript
yarn config set registry https://registry.npmmirror.com
// 查看源
yarn config get registry
// 切回官方镜像
yarn config set registry https://registry.yarnpkg.com

```

 ### pnpm设置淘宝镜像
```javascript
pnpm config set registry https://registry.npmmirror.com
// 查看源
pnpm config get registry
// 切回官方镜像
pnpm config set registry https://registry.npmjs.org


```

四、常见问题
npm修改了下载源，仍然是之前的下载源。或者下载失败、下载到某处停止不动。可以进行如下操作。
（1）清除缓存
（2）将对应项目中的node_modules文件夹以及package-lock.json文件删除。
（3）执行安装 + 需要的下载源。
```javascript
npm cache clean -f
```



 ### 指定npm镜像
```javascript 
npm 官方原始镜像网址是：https://registry.npmjs.org/
淘宝 NPM 镜像：http://registry.npmmirror.com
阿里云 NPM 镜像：https://npm.aliyun.com
腾讯云 NPM 镜像：https://mirrors.cloud.tencent.com/npm/
华为云 NPM 镜像：https://mirrors.huaweicloud.com/repository/npm/
网易 NPM 镜像：https://mirrors.163.com/npm/
中国科学技术大学开源镜像站：http://mirrors.ustc.edu.cn/
清华大学开源镜像站：https://mirrors.tuna.tsinghua.edu.cn/
腾讯，华为，阿里的镜像站基本上比较全
```
