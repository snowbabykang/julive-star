<template>
    <div id="app">
        <star-rate
            @change="change"
            :rate="rate"
            :half="true"
            :stars="[0,1,3,4,5]"
            info="请给我五星评价呀!"
            :texts="[
                    '非常不满意，体验很差!',
                    '不满意，体验不佳!',
                    '一般，还需改善!',
                    '满意!!!',
                    '非常满意，无可挑剔!!!'
                ]"
        ></star-rate>
    </div>
</template>

<script>
    import starRate from '../src/components/star';
    export default {
        data() {
            return {
                // 评价的星数 1-5
                rate: null,
                // 评价的星星实际值
                rateValue: null
            };
        },
        components: {
            starRate
        },
        methods: {
            /**
             * @description: 评星组件返回的评星等级
             * @param {string} val 评星实际值0，1，3，4，5
             * @param {string} star 评星等级 1-5
             * @return:
             */
            change(val, star) {
                this.rateValue = val;
                this.rate = star;
            }
        },
        mounted() {
            console.log(starRate);
        }
    };
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
