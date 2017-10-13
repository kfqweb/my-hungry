<template>
    <div id="app">
        <div id="example">
            <my-header :seller="seller"></my-header>
        </div>
        <div>
            <div class="tab">
                <div class='tab-item'>
                    <router-link to="/comm">商品</router-link>
                </div>
                <div class='tab-item'>
                    <router-link to="/eval">评价</router-link>
                </div>
                <div class='tab-item'>
                    <router-link to="/busi">商家</router-link>
                </div>


            </div>
            <!-- 路由出口 -->
            <!-- 路由匹配到的组件将渲染在这里 -->
            <router-view></router-view>
        </div>
    </div>
</template>

<script>
    //    import {urlParse} from 'common/js/util';

    import myHeader from './components/header/myHeader.vue'

    export default {
        name: 'app',
        data () {
            return {
                seller: {}
            };
        },
        created() {
            this.$http.get('data.json', {})
                .then(function (response) {
                    if (response) {
                        this.seller = response.body.seller;
                        /*console.log(this.seller);
                        console.log(
                            (Object.values(response.body.seller.avatar)).join('')
                        )*/
                    }
                }, function (response) {
                    alert(response.status)
                })
        },
        components: {
            'my-header': myHeader
        }
    }

</script>

<style lang="less" rel="stylesheet/less">
    .router-link-active {
        color: #f60;
    }

    .tab {
        width: 100%;
        display: flex;
        height: 40px;
        line-height: 40px;
        border-bottom: 1px solid rgba(1, 17, 27, 0.1);

        .tab-item {
            flex: 1;
            text-align: center;
            font-size: 16px;
            height:40px;
            line-height: 40px;
        }

    }
</style>
