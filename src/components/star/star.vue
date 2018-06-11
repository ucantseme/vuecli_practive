<template>
    <div class="star">
        <span v-for="star in stars" :class="star" class="star-item"></span>
    </div>
</template>
<script>
    const Length = 5
    const star_on = 'on'
    const star_half = 'half'
    const star_off = 'off'

    export default{
        props: {
            score: {
                type: Number,
            }
        },
        computed: {
            stars () {
                let result = []
                // 向下取0.5倍數
                let score = Math.floor(this.score*2) / 2
                // 小數, 半星
                let decimal = score % 1 !== 0
                // 整數, 全星
                let integer = Math.floor(score)

                for(let i=0;i<integer;i++){
                    result.push(star_on)
                }

                if(decimal){
                    result.push(star_half)
                }
                while (result.length < Length) {
                    result.push(star_off)
                }
                return result
            }
        }
    }
</script>
<style lang="scss" scoped>
.star-item{
    display: inline-block;
    width: 10px;
    height: 10px;
    margin-right: 3px;
    background-size: 10px 10px;
    background-repeat: no-repeat;
    &.on{
        background-image: url('star24_on@2x.png');
    }
    &.half{
        background-image: url('star24_half@2x.png');
    }
    &.off{
        background-image: url('star24_off@2x.png');
    }
}

</style>
