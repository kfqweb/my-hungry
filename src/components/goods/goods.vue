<template>
    <div class="goods">
        <!-- 左侧 -->
        <div class="menu-wrapper" ref="menuWrapper">
            <ul>
                <li v-for="(item,index) in goods" class="menu-item"
                    :class="{'current':currentIndex===index}">
                    <span class="text">
                        <span v-show="item.type>0" class="icon"
                              :class="classMap[item.type]">
                        </span>
                        {{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="foods-wrapper" ref="foodsWrapper">
            <ul>
                <li v-for="item in goods" class="food-list food-list-hook">
                    <h1 class="title">{{item.name}}</h1>
                    <ul>
                        <li v-for="food in item.foods" class="food-item">
                            <div class="icon">
                                <img width="57" height="57" :src="food.icon"></img>
                            </div>
                            <div class="content">
                                <h2 class="name">{{food.name}}</h2>
                                <p class="desc">{{food.description}}</p>
                                <div class="extra">
                                    <span class="count">月售{{food.sellCount}}份</span><span>好评率{{food.sellCount}}%</span>
                                </div>
                                <div class="price">
                                    <span class="now">¥{{food.price}}</span><span class="old"
                                                                                  v-show="food.oldPrice">¥{{food.oldPrice}}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import BScroll from 'better-scroll';

    export default {
        prop: {
            seller: {
                type: Object
            }
        },
        data() {
            return {
                goods: [],
                listHeight: [],
                scrollY: 0
            };
        },
        computed: {
            currentIndex() {
                for (var i = 0; i < this.listHeight.length; i++) {
                    var height = this.listHeight[i];
                    var height1 = this.listHeight[i + 1];
                    alert()
                    if (!height1 || this.scrollY > height && this.scrollY < height1) {
                        return i;
                    }else {
                        return 0;
                    }
                }
            }
        },
        created() {
            this.classMap = ["decrase", "discount", "guarantee", "invoice", "special"];
            this.$http.get('data.json', {})
                .then(function (response) {
                    if (response) {
                        this.goods = response.body.goods;
                        this.$nextTick(() => {
                            this._initScroll();
                            this._obtainHeight();
                        });
                        //console.log(this.goods);
                        /*console.log(
                            (Object.values(response.body.goods.avatar)).join('')
                        )*/
                    }
                }, function (response) {
                    alert(response.status)
                })
        },
        methods: {
            _initScroll() {
                this.meunScroll = new BScroll(this.$refs.menuWrapper, {});
                this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {
                    probeType: 3
                });
                this.foodsScroll.on('scroll', function (pos) {
                    this.scrollY = Math.abs(Math.round(pos.y));
                    console.log(this.scrollY);
                })
            },
            _obtainHeight() {
                var foodList = this.$refs.foodsWrapper.getElementsByClassName("food-list-hook");
                var height = 0;
                this.listHeight.push(height);
                for (var i = 0; i < foodList.length; i++) {
                    var item = foodList[i];
                    height += item.clientHeight;
                    this.listHeight.push(height);
                    console.log(this.listHeight);
                }

            }
        }
    }
</script>


<style lang="less" rel="stylesheet/less">
    //@import "../../common/style/mixin.less";
    .goods {
        display: flex;
        position: absolute;
        top: 185px;
        bottom: 46px;
        width: 100%;
        overflow: hidden;
        .menu-wrapper {
            flex: 0 0 80px;
            width: 80px;
            background: #f3f5f7;
            .menu-item {
                display: table;
                height: 54px;
                width: 56px;
                line-height: 14px;
                padding: 0 10px;
                .icon {
                    display: inline-block;
                    width: 12px;
                    height: 12px;
                    margin-right: 2px;
                    -webkit-background-size: 12px 12px;
                    background-size: 12px 12px;
                    background-repeat: no-repeat;
                    vertical-align: top;
                }
                .decrase {
                    background-image: url('decrease_3@2x.png');
                }
                .discount {
                    background-image: url('discount_3@2x.png');
                }
                .guarantee {
                    background-image: url('guarantee_3@2x.png');
                }
                .invoice {
                    background-image: url('invoice_3@2x.png');
                }
                .special {
                    background-image: url('special_3@2x.png');
                }
                .text {
                    display: table-cell;
                    width: 56px;
                    vertical-align: middle;
                    font-size: 12px;
                    border-bottom: 1px solid rgba(7, 17, 27, 0.1);
                    text-align: center;
                }

            }
            .current{
                position: relative;
                margin-top:-1px;
                z-index: 10;
                background: #fff;
                font-weight: 700;
                .text{
                    border:none;
                }
            }
        }
        .foods-wrapper {
            flex: 1;
            .title {
                padding-left: 14px;
                height: 26px;
                line-height: 26px;
                border-left: 2px solid #d9dde1;
                font-size: 12px;
                color: rgb(147, 153, 159);
                background-color: #f3f5f7;
            }
            .food-item {
                display: flex;
                margin: 10px;
                padding-bottom: 18px;
                border-bottom: 1px solid rgba(7, 17, 27, 0.1);
                .food-item:last-child {
                    border-bottom: 0;
                    padding-bottom: 0px;
                }
                .icon {
                    flex: 0 0 57px;
                    margin-right: 10px;
                }
                .content {
                    flex: 1;
                    .name {
                        font-size: 14px;
                        margin: 2px 0 8px 0;
                        height: 14px;
                        line-height: 14px;
                        color: rgb(7, 17, 27);
                    }
                    .desc, .extra {
                        line-height: 10px;
                        font-size: 10px;
                        color: rgb(147, 153, 159);
                    }
                    .desc {
                        margin-bottom: 8px;
                        line-height: 13px;
                    }
                    .extra {
                        .count {
                            margin-right: 12px;
                        }
                    }
                    .price {
                        font-weight: 700;
                        line-height: 24px;
                        .now {
                            margin-right: 8px;
                            font-size: 14px;
                            color: rgb(240, 20, 20);
                        }
                        .old {
                            text-decoration: line-through;
                            font-size: 10px;
                            color: rgb(147, 153, 159);
                        }
                    }
                }
            }
        }
    }


</style>