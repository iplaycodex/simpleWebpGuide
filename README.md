## 1.日常针对图片资源做的一些优化
 - 图片优化的点:
 - 1.根据业务场景不同选择对应的JPG,PNG,GIF等格式
 - 2.设计给到图片后首先自己用 TinyPNG4MAC 进行压缩
 - 3.小 icon 使用 iconfont
 - 4.小图使用 base64 打进 html 文档中,webpack 模式的阈值是 5kb
 - 5.懒加载
 - 6.动静分离，从主域名上进行剥离
 - 7.使用 webp
 - ...

## 2.使用 weibp 图片的一个流程
- 1.判断浏览器是否支持 webp 格式
- 2.支持则去加载 webp 的图片
- 3.服务器上有 webp 格式的图片则load之，渲染之
- 4.服务器上没有触发 `@error` 方法，加载 originPic
- 5.渲染常规格式的图片

## 3.运行本项目

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

## 4.没有做的一些优化点
- 1.获取浏览器支持应该只获取一次，然后将状态值存到 store 或 cookie 中，共享之
- 2.服务器通过请求头 Accept: image/webp,image/apng,image/*,* 去判断客户端是否支持 webp 按需返回格式
- 3.大规模使用需要服务器端进行支持，本项目仅作为一个尝鲜的demo示例