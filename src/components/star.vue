<template>
    <div class="star-con">
        <ul class="star-list">
            <li
                v-for="item in 5"
                :key="item"
                @click="changeRate(item,$event)"
                ref="star"
                :class="{'active': star !== null && item <= star}"
            >
                <svg
                    width="34px"
                    height="32px"
                    viewBox="0 0 34 32"
                    class="base-star"
                >
                    <g
                        stroke="none"
                        stroke-width="1"
                        fill="none"
                        fill-rule="evenodd"
                    >
                        <g fill="#E7ECF7">
                            <path
                                d="M16.2687063,27.3515731 L7.51484209,31.8929407 C7.05394275,32.132048 6.48387966,31.9571871 6.24157054,31.5023779 C6.14508178,31.3212705 6.1117859,31.1138264 6.1468375,30.9121603 L7.8186768,21.2933895 C7.90610571,20.7903755 7.73710508,20.2771179 7.36675029,19.9208814 L0.284725354,13.1088301 C-0.0881500424,12.750169 -0.0957797447,12.1611357 0.267683936,11.7931874 C0.412417081,11.6466684 0.602061001,11.5513168 0.807256611,11.5218941 L10.5943744,10.1185344 C11.1061921,10.0451456 11.5486415,9.72793493 11.7775333,9.27027766 L16.1544654,0.518830913 C16.3849151,0.0580588599 16.9502628,-0.131122837 17.4172048,0.0962817656 C17.6031436,0.186835471 17.7536459,0.335349065 17.8454121,0.518830913 L22.2223442,9.27027766 C22.4512361,9.72793493 22.8936855,10.0451456 23.4055032,10.1185344 L33.192621,11.5218941 C33.7079221,11.5957823 34.0649559,12.0678949 33.9900782,12.5763871 C33.9602616,12.7788713 33.8636332,12.9660094 33.7151522,13.1088301 L26.6331273,19.9208814 C26.2627725,20.2771179 26.0937719,20.7903755 26.1812008,21.2933895 L27.8530401,30.9121603 C27.941064,31.4185978 27.5963753,31.8995611 27.0831564,31.986422 C26.8787899,32.0210104 26.668568,31.9881545 26.4850355,31.8929407 L17.7311712,27.3515731 C17.2733875,27.1140821 16.72649,27.1140821 16.2687063,27.3515731 Z"
                                id="星形"
                            ></path>
                        </g>
                    </g>
                    <svg
                        width="17"
                        height="32"
                        class="half-star"
                        v-if="half && Math.ceil(star) === item"
                    >
                        <g
                            fill-rule="evenodd"
                            fill="none"
                        >
                            <g fill="#E7ECF7">
                                <path
                                    fill="#ffbc37"
                                    id="星形"
                                    d="m16.26871,27.35157l-8.75387,4.54137c-0.4609,0.23911 -1.03096,0.06425 -1.27327,-0.39056c-0.09649,-0.18111 -0.12978,-0.38855 -0.09473,-0.59022l1.67184,-9.61877c0.08743,-0.50301 -0.08157,-1.01627 -0.45193,-1.37251l-7.08202,-6.81205c-0.37288,-0.35866 -0.38051,-0.94769 -0.01705,-1.31564c0.14474,-0.14652 0.33438,-0.24187 0.53958,-0.2713l9.78711,-1.40336c0.51182,-0.07338 0.95427,-0.3906 1.18316,-0.84825l4.37694,-8.75145c0.23045,-0.46077 0.79579,-0.64995 1.26273,-0.42255c0.18594,0.09056 0.33645,0.23907 0.42821,0.42255l4.37693,8.75145c0.2289,0.45765 0.67135,0.77487 1.18316,0.84825l9.78712,1.40336c0.5153,0.07389 0.87234,0.546 0.79746,1.0545c-0.02982,0.20248 -0.12645,0.38962 -0.27493,0.53244l-7.08202,6.81205c-0.37036,0.35624 -0.53936,0.8695 -0.45193,1.37251l1.67184,9.61877c0.08802,0.50644 -0.25666,0.9874 -0.76988,1.07426c-0.20437,0.03459 -0.41459,0.00173 -0.59812,-0.09348l-8.75387,-4.54137c-0.45778,-0.23749 -1.00468,-0.23749 -1.46246,0z"
                                />
                            </g>
                        </g>
                    </svg>
                </svg>
                <i class="icon-star base-star">
                    <i
                        class="icon-star half-star"
                        v-if="half && Math.ceil(star) === item"
                    ></i>
                </i>
            </li>
        </ul>
        <div :class="{'has-rate': star, 'rate-text': true}">{{star ? rateTexts[Math.ceil(star)-1] : info}}</div>
    </div>
</template>

<script>
    export default {
        name: 'star-rate',
        props: {
            // 星星当前实际值
            rate: {
                default: null
            },
            // 初始默认信息
            info: {
                type: String,
                default: '请您对我的服务做出评价'
            },
            // 是否允许半星
            half: {
                type: Boolean,
                default: false
            },
            // 星级对应文本值
            texts: {
                type: Array,
                default: () => [
                    '非常不满意，体验很差',
                    '不满意，体验不佳',
                    '一般，还需改善',
                    '满意',
                    '非常满意，无可挑剔'
                ]
            },
            // 评星数值的数组，数组数值必须排序，从小到大
            stars: {
                type: Array,
                default: [1, 2, 3, 4, 5]
            }
        },
        data() {
            return {
                // 评星
                starArr: [],
                // 评价的星数
                star: null,
                // 星级评价
                rateTexts: []
            };
        },
        methods: {
            /**
             * @description: 点击评星，可评半星
             * @param {number} value   评星分数
             * @param {event} e   事件对象
             * @return: nowstar   拼星的实际值   star第几课星星
             */
            changeRate(value, e) {
                if (this.half) {
                    let width = this.$refs.star[0].offsetWidth;
                    if (e.offsetX <= width / 2) {
                        this.star = parseInt(value) - 0.5;
                    } else {
                        this.star = value;
                    }
                } else {
                    this.star = value;
                }
                // 获取星星对应的星值
                let nowStar = this.starArr[this.star - 1];
                this.$emit('change', nowStar, this.star);
            }
        },
        watch: {
            /**
             * @description: 监听星级对应文本内容
             * @param {array} val   文本数组
             * @return:
             */
            texts(val) {
                this.rateTexts = val;
            }
        },
        mounted() {
            var _this = this;
            this.$nextTick(() => {
                // 评星对应的数值的数组进行从小到大的排序
                _this.starArr = _this.stars.sort(function(a, b) {
                    return a - b;
                });
                // 获取当前星值是第几颗星
                _this.star = _this.starArr.indexOf(this.rate) + 1;
                _this.rateTexts = _this.texts;
            });
        }
    };
</script>

<style scoped lang="less">
.star-con {
    text-align: center;
}
.rate-text {
    font-size: 12px;
    color: #00c0eb;
    text-align: center;
    padding-top: 12px;
    line-height: 17px;
    font-size: 12px;
}
.rate-text.has-rate {
    font-size: 14px;
    line-height: 20px;
}
.star-list {
    text-align: center;
    height: 34px;
    margin: 0;
    padding: 0;
    li {
        display: inline-block;
        color: #e7ecf7;
        margin: 0 10px;
        line-height: 1;
        height: 100%;
    }
    li.active {
        svg path {
            fill: #ffbc37;
        }
    }
    .base-star {
        position: relative;
        .half-star {
            position: absolute;
            top: 0;
            left: 0;
        }
    }
}
</style>