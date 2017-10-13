<template id="myHeader">
    <div class="header">
        <div class="content-wrapper">
            <!-- 商家图片 -->
            <div class="avatar">
                <img width="64" height="64" :src="seller.avatar">
            </div>
            <!-- 内容 -->
            <div class="content">
                <!-- 标题 -->
                <div class="tatle">
                    <!-- 品牌 -->
                    <span class="brand"></span>
                    <!-- 名称 -->
                    <span class="name">{{ seller.name }}</span>
                </div>
                <!-- 描述 、配送时间 -->
                <div class="description">
                    {{ seller.description }}/{{ seller.deliveryTime }}分钟送达

                </div>
                <!-- 优惠 -->
                <div v-if="seller.supports"
                     class="supports" @click="showData">
                    <span class="icon" :class="classMap[seller.supports[0].type]"></span>
                    <span class="text">
                        {{ seller.supports[0].description }}
                    </span>
                </div>
                <!-- 右侧的个数 -->
                <div v-if="seller.supports" class="supports-count"
                     @click="showData">
                    <span class="count">{{ seller.supports.length }} 个 </span>
                    <i class="icon-keyboard_arrow_right"></i>
                </div>
            </div>
        </div>
        <!-- 公告区域 -->
        <div class="bulletin-wrapper">
            <span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>
        <!-- 大背景 -->
        <div class="background">
            <img :src="seller.avatar"
                 width='100%' height="100%">
        </div>
        <!-- 折扣详细 -->
        <transition name="slide-fade">
            <div v-show="detailShow" class="detail">
                <div class="detail-wrapper clearfix">
                    <div class="detail-main">
                        <h1 class="detail-tile">{{ seller.name }}</h1>
                    </div>
                    <div class="stars-wrapper">
                        <stars :size="48" :score="seller.score"></stars>
                    </div>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">优惠信息</div>
                        <div class="line"></div>
                    </div>
                    <!-- 优惠展示 -->
                    <div class="detail-youhui">
                        <!-- 优惠 -->
                        <ul v-for="(supports,index) in seller.supports" class="supports">
                            <li v-if="seller.supports">
                                <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                                <span class="text">{{ seller.supports[index].description }}</span>
                            </li>
                        </ul>
                    </div>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">商家信息</div>
                        <div class="line"></div>
                    </div>
                    <!-- 商家公告文字 -->
                    <div class="detail-text">
                        {{ seller.bulletin }}

                    </div>
                </div>
                <div class="detail-close" @click="down">
                    <i class="icon-close"></i>
                </div>
            </div>
        </transition>
    </div>
</template>
<script>

    import stars from '../star/stars.vue'

    export default {
        props: {
            seller: {
                type: Object
            }
        },
        data() {
            return {
                detailShow: false,
            }
        },
        methods: {
            showData() {
                this.detailShow = true
            },
            down() {
                this.detailShow = false
            }
        },
        created() {
            this.classMap = ["decrase", "discount", "guarantee", "invoice", "special"];
        },
        components: {
            stars
        }
    }
</script>
<style lang="less" rel="stylesheet/less">

    //@import "../../common/style/mixin.less";

    .header {
        position: relative;
        color: #fff;
        background-color: rgba(7, 17, 27, 0.5);
        overflow: hidden;
        /* */
        .content-wrapper {
            position: relative;
            padding: 24px 12px 18px 24px;
            font-size: 0;
            .avatar {
                font-size: 14px;
                display: inline-block;
                margin-bottom: 8px;
                vertical-align: top;
                img {
                    border-radius: 2px;
                }
            }
            .content {
                font-size: 14px;
                display: inline-block;
                margin-left: 16px;
                .tatle {
                    margin: 2px 0 8px 0;
                    .brand {
                        display: inline-block;
                        width: 30px;
                        height: 18px;
                        background: url('./brand@2x.png');
                        -webkit-background-size: 30px 18px;
                        background-size: 30px 18px;
                        background-repeat: no-repeat;
                        vertical-align: middle;
                    }
                    .name {
                        margin-left: 6px;
                        font-size: 16px;
                        color: rgb(255, 255, 255);
                        font-weight: bold;
                        line-height: 16px;
                    }
                }
                .description {
                    margin-bottom: 10px;
                    font-size: 12px;
                    color: rgb(255, 255, 255);
                    font-weight: 100;
                    line-height: 12px;
                }
                .supports {
                    line-height: 12px;
                    font-size: 10px;
                    color: rgb(255, 255, 255);
                    font-weight: 100;
                    .icon {
                        display: inline-block;
                        width: 12px;
                        height: 12px;
                        margin-right: 4px;
                        -webkit-background-size: 12px 12px;
                        background-size: 12px 12px;
                        background-repeat: no-repeat;
                        vertical-align: top;
                    }
                    .decrase {
                        background-image: url('decrease_1@2x.png');
                    }
                    .discount {
                        background-image: url('discount_1@2x.png');
                    }
                    .guarantee {
                        background-image: url('guarantee_1@2x.png');
                    }
                    .invoice {
                        background-image: url('invoice_1@2x.png');
                    }
                    .special {
                        background-image: url('special_1@2x.png');
                    }
                }
                .text {
                    line-height: 12px;
                    font-size: 10px;
                }
                .supports-count {
                    position: absolute;
                    right: 12px;
                    bottom: 20px;
                    padding: 7px 8px;
                    height: 24px;
                    line-height: 24px;
                    border-radius: 14px;
                    background-color: rgba(0, 0, 0, 0.2);
                    text-align: center;
                    .count {
                        font-size: 10px;
                    }
                    .icon-keyboard_arrow_right {
                        font-size: 10px;
                        margin-left: 2px;
                        vertical-align: middle;
                        line-height: 24px;
                    }
                }
            }
        }
        /* */
        .bulletin-wrapper {
            /* 会影响省略号*/
            /*font-size: 0;*/
            height: 28px;
            line-height: 28px;
            padding: 0 22px 0 12px;
            white-space: nowrap;
            overflow: hidden;
            background-color: rgba(7, 17, 27, 0.2);
            text-overflow: ellipsis;
            position: relative;
            .bulletin-title {
                display: inline-block;
                width: 22px;
                height: 12px;
                line-height: 12px;
                margin-right: 4px;
                background: url('./bulletin@2x.png');
                -webkit-background-size: 22px 12px;
                background-size: 22px 12px;
                background-repeat: no-repeat;
                vertical-align: middle;
            }
            .bulletin-text {
                font-size: 10px;
                margin: 0 4px;
            }
            .icon-keyboard_arrow_right {
                position: absolute;
                font-size: 10px;
                right: 12px;
                top: 10px;
            }
        }
        /* */
        .background {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            filter: blur(10px);
        }
        .detail {
            position: fixed;
            top: 0;
            left: 0;
            z-index: 100;
            width: 100%;
            height: 100%;
            overflow: auto;
            padding: 0 36px;;
            box-sizing: border-box;
            background-color: rgba(7, 17, 27, 0.8);
            /*transition: all 0.5s;*/
            backdrop-filter: blur(10px);
            .detail-wrapper {
                width: 100%;
                min-height: 99%;
                .detail-main {
                    margin-top: 16px;
                    padding-bottom: 16px;
                    .detail-tile {
                        text-align: center;
                        font-size: 12px;
                        font-weight: 700;
                        line-height: 32px;
                        margin-top: 32px;
                        margin-bottom: 16px;
                    }
                }
                .detail-zhanwei {
                    width: 100%;
                    height: 188px;
                    background-color: pink;
                }
                .title {
                    display: flex;
                    width: 80%;
                    margin: 28px auto 24px auto;
                    .line {
                        flex: 1;
                        position: relative;
                        top: -6px;
                        border-bottom: 1px solid rgba(255, 255, 255, .2);
                    }
                    .text {
                        flex: 1;
                        text-align: center;
                        padding: 0 12px;
                        font-size: 14px;
                        font-weight: 700;
                    }
                }
                /* 优惠的展示 */
                .detail-youhui {
                    font-size: 12px;
                    line-height: 12px;
                    .supports {
                        margin-bottom: 12px;
                        .icon {
                            display: inline-block;
                            width: 12px;
                            height: 12px;
                            margin-right: 4px;
                            -webkit-background-size: 12px 12px;
                            background-size: 12px 12px;
                            background-repeat: no-repeat;
                            vertical-align: top;
                            margin-left: 12px;
                        }
                        .decrase {
                            background-image: url('decrease_1@2x.png');
                        }
                        .discount {
                            background-image: url('discount_1@2x.png');
                        }
                        .guarantee {
                            background-image: url('guarantee_1@2x.png');
                        }
                        .invoice {
                            background-image: url('invoice_1@2x.png');
                        }
                        .special {
                            background-image: url('special_1@2x.png');
                        }
                    }
                }
                /* 占位置，明天写 */
                .detail-zhanwei2 {
                    width: 100%;
                    height: 128px;
                    background-color: pink;
                }
                .detail-text {
                    padding: 0 12px;
                    font-size: 12px;
                    line-height: 24px;
                }
            }
            .detail-close {
                position: relative;
                width: 32px;
                height: 32px;
                margin: -64px auto;
                clear: both;
                font-size: 32px;
            }
        }
        /*.fade-transition {
             opacity: 1;
             background-color: rgba(7, 17, 27, 0.8);
         }
        .fade-enter, .fade-leave {
            opacity: 0;
            background-color: rgba(7, 17, 27, 0);
        }*/
        .slide-fade-enter-active {
            transition: all .8s ease;
        }
        .slide-fade-leave-active {
            transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
        }
        .slide-fade-enter, .slide-fade-leave-to
            /* .slide-fade-leave-active for below version 2.1.8 */ {
            transform: translateX(10px);
            opacity: 0;
        }
    }
</style>