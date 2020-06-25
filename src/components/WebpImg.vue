<template>
    <img :src="imgFinalSrc" @error="loadOriginPic()" alt />
</template>

<script>
/**
 * 图片优化的点:
 * 1.根据业务场景不同选择对应的JPG,PNG,GIF等格式
 * 2.设计给到图片后首先自己用 TinyPNG4MAC 进行压缩
 * 3.小 icon 使用 iconfont
 * 4.小图使用 base64 打进 html 文档中,webpack 模式的阈值是 5kb
 * 5.懒加载
 * 6.动静分离，从主域名上进行剥离
 * 7.使用 webp
 * 
 * STEP
 * 1.首先判断浏览器是否支持 webp
 * 2.支持则加载 webp 图片，不支持则加载原格式的图片，例:jpg/jpeg/png
 * 3.如果 webp 图片加载失败则触发 @error 方法加载原格式图片兜底
 * 
 * 后续：
 * 1.服务器支持自动转化 webp
 * 2.服务器通过请求头 Accept: image/webp,image/apng,image/*,* 去判断客户端是否支持 webp 按需返回格式
 * 
 * 适合场景：
 * 1.安卓原生APP瘦身,iOS 不支持
 * 2.小程序瘦身，待调研。可以确定的是iOS是肯定不支持的
 * 3.移动端渲染速度优化
 * 4.节省CDN支出
 */
export default {
    props: ['path'],
    data() {
        return {
            isSupportWebp: false
        }
    },
    created() {
        this.checkSupportWebpStatus();
    },
    computed: {
        imgFinalSrc() {
            return this.isSupportWebp && process.env.NODE_ENV == 'production' ? this.path + '.webp' : this.path;
        }
    },
    methods: {
        checkSupportWebpStatus() {
            this.isSupportWebp = !![].map && document.createElement('canvas').toDataURL('image/webp').indexOf('data:image/webp') == 0;
        },
        loadOriginPic() {
            let img = event.srcElement;
            img.src = this.path;
            img.onerror = null;
        }
    }
}
</script>