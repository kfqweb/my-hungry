<template>
    <div class="star" :class="starType">
        <span v-for="itemClass in itemClasses" :class="itemClass" class="star-item"></span>
    </div>
</template>

<script>
    const LENGTH = 5;
    const CLS_ON = "on";
    const CLS_HALF = "half";
    const CLS_OFF = "off";
    export default{
        // 引入两个参数
        props: {
            size: {
                type: Number
            },
            score: {
                type: Number
            }
        },
        computed: {
            starType() {
                return 'star-' + this.size;
            },
            itemClasses() {
                // 定义一个空的数组，存放获取到的类名
                let result = [];
                // 计算评价的得分
                let scor = Math.floor(this.score * 2) / 2;
                let hasDecimal = scor % 1 !== 0;
                //console.log(scor);
                // 获取评分的整数部分
                let integer = Math.floor(scor);
                // 添加对应的完整的星星数
                for (let i = 0; i < integer; i++) {
                    result.push(CLS_ON);
                }
                // 如果 出现小数 代表出现 半颗星
                if (hasDecimal) {
                    result.push(CLS_HALF)
                }
                while (result.length < LENGTH) {
                    result.push(CLS_OFF)
                }
                return result;
            }
        }
    }
</script>

<style lang="less" rel="stylesheet/less">

    .star {
        font-size: 0;
        text-align: center;
        .star-item {
            display: inline-block;
            background-repeat: no-repeat;
        }
    }

    /* 48大小的星星 */
    .star-48 {
        .star-item {
            width: 20px;
            height: 20px;
            margin-right: 22px;
            -webkit-background-size: 20px 20px;
            background-size: 20px 20px;
        }
        .on {
            background-image: url('./star48_on@2x.png');
        }
        .half {
            background-image: url('./star48_half@2x.png');
        }
        .off {
            background-image: url('./star48_off@2x.png');
        }
        .star-item:last-child {
            margin-right: 0;
        }

    }

    /* 36大小的星星 */
    .star-36 {
        .star-item {
            width: 15px;
            height: 15px;
            margin-right: 6px;
            -webkit-background-size: 15px 15px;
            background-size: 15px 15px;
        }
        .on {
            background-image: url('./star36_on@2x.png');
        }
        .half {
            background-image: url('./star36_half@2x.png');
        }
        .off {
            background-image: url('./star36_off@2x.png');
        }
    }

    /* 24大小的星星 */
    .star-24 {
        .star-item {
            width: 10px;
            height: 10px;
            margin-right: 3px;
            -webkit-background-size: 10px 10px;
            background-size: 10px 10px;
        }
        .on {
            background-image: url('./star24_on@2x.png');
        }
        .half {
            background-image: url('./star24_half@2x.png');
        }
        .off {
            background-image: url('./star24_off@2x.png');
        }
    }
</style>