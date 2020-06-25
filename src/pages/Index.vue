<template>
    <div class="hello">
        <h4>custom img component support webp type</h4>
        <webp-img :path="img" />
        <webp-img :path="require('../assets/pic2.jpg')" />
    </div>
</template>

<script>
import WebpImg from '../components/WebpImg';
export default {
    data() {
        return {
            img: require('../assets/pic1.jpg')
        }
    },
    components: {
        WebpImg
    }
}
</script>

<style scoped>
.hello {
    width: 100%;
}
.hello img {
    width: 100%;
}
</style>
