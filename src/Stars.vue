<template>
    <div class="stars">
        <div v-for="(item, index) in starsCount" :key="index" class="star" ref="star">

        </div>
    </div>
</template>

<script>
export default {
    name: "stars",
    data() {
        return {
            starsCount: 800,  //星星数量
            distance: 800,     //星星间距
        }
    },

    mounted(){
        // 原生js
        let _starList = document.getElementsByClassName("star")
        let starArr = Array.prototype.slice.call(_starList)
        // vue
        let starList = this.$refs.star
        // 遍历添加样式
        starArr.forEach(item => {
            let s = 0.2 + (Math.random() * 1);
            let thisDistance = this.distance + (Math.random() * 300);
            item.style.transformOrigin = `0 0 ${thisDistance}px`
            item.style.transform = `translate3d(0,0,-${thisDistance}px) rotateY(${(Math.random() * 360)}deg) rotateX(${(Math.random() * -50)}deg) scale(${s},${s})`
        })
    }
}
</script>

<style lang="less" scoped>

    //动画
    @keyframes rotate {
        0% {
            transform: perspective(400px) rotateZ(20deg) rotateX(-40deg) rotateY(0);
        }
        100% {
            transform: perspective(400px) rotateZ(20deg) rotateX(-40deg) rotateY(-360deg);
        }
    }

    .stars{
        transform: perspective(500px);
        transform-style: preserve-3d;
        position: absolute;
        perspective-origin: 50% 100%;
        left: 50%;
        animation: rotate 90s infinite linear;
        bottom: 0;
    }

    .star{
        width: 2px;
        height: 2px;
        background: #f7f7b8;
        position: absolute;
        top: 0;
        left: 0;
        backface-visibility: hidden;
    }

</style>