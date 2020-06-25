<template>
    <img :src="imgFinalSrc" @error="loadOriginPic()" alt />
</template>

<script>
/**
 * STEP
 * 1.首先判断浏览器是否支持 webp
 * 2.支持则加载 webp 图片，不支持则加载原格式的图片，例:jpg/jpeg/png
 * 3.如果 webp 图片加载失败则触发 @error 方法加载原格式图片兜底
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