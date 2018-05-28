<template>
    <div class="home">
        <div class="banner">
            <swiper :aspect-ratio="400/750"
                loop
                auto
                dots-position="center"
                :duration="800">
                <swiper-item class="swiper-item"
                    v-for="(item, index) in imgList"
                    :key="index"
                    @click.native="linkToDetail(item.key_word)">
                    <img :src="item.img.url"
                        alt="image">
                </swiper-item>
            </swiper>
            <div class="bottom">
                <h5 class="title">
                    <img src="~@/assets/img/logo-icon.png">
                    <span>国际大牌大优惠&emsp;品牌尖货</span>
                </h5>
                <h5><span class="circular"></span>免税区直邮发货&emsp;<span class="circular"></span>30天无忧退货&emsp;<span class="circular"></span>48小时快速退款</h5>
            </div>
        </div>
        <!-- 今日新品 -->
        <div class="newgoods">
            <div class="top">
                <h5 class="title">今日新品</h5>
                <div class="left">
                    <b>每日焕新 天天大不同</b>
                    <img src="~@/assets/img/goods.png">
                </div>
                <div class="right"><img src="~@/assets/img/newgoods.png"></div>
            </div>
            <div class="bottom">
                <div class="left">
                    <h5>热卖推荐</h5>
                    <span><b>热卖大牌折扣</b><img src="~@/assets/img/ximian.png"></span>
                </div>
                <div class="right">
                    <h5>会员福利</h5>
                    <span><b>开卡送好礼</b><img src="~@/assets/img/category-goods.png"></span>
                </div>
            </div>
        </div>
        <!-- 活动专场 -->
        <div class="product">
            <div class="title">
                <h5><span class="square"></span>&emsp;活动专场&emsp;<span class="square"></span></h5>
                <p>大牌活动精选，超低折扣</p>
            </div>
            <ul class="list">
                <li>
                    <p>
                        <img src="~@/assets/icon/watch.png" />&ensp;结束时间：<span>2018/06/22 10:00:00</span>
                        <span class="right">剩余 <b>12</b> 天</span>
                    </p>
                </li>
                <li>
                    <p>
                        <img src="~@/assets/icon/watch.png" />&ensp;结束时间：<span>2018/06/22 10:00:00</span>
                        <span class="right">剩余 <b>12</b> 天</span>
                    </p>
                </li>
            </ul>
        </div>
        <!-- 好物推荐 -->
        <div class="Goodthing">
            <div class="title">
                <h5><span class="square"></span>&emsp;好物推荐&emsp;<span class="square"></span></h5>
                <p>你喜欢的都在这里，好物尽选</p>
            </div>
            <ul class="list">
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
                <li>
                    <img src="~@/assets/img/category-goods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
            </ul>
        </div>
        <!-- 热门购买 -->
        <div class="Goodthing">
            <div class="title">
                <h5><span class="square"></span>&emsp;热门购买&emsp;<span class="square"></span></h5>
                <p>身边的小伙伴，大家都在买</p>
            </div>
            <ul class="list">
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
                <li>
                    <img src="~@/assets/img/category-goods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <p>精美礼盒亚菲儿女士香士香</p>
                    <p class="c-f54321">￥385.00</p>
                </li>
            </ul>
        </div>
        <div class="selected-themes">
            <div class="title">
                <h5>精选主题</h5>
            </div>
            <div class="selectd-box">
                <div class="selectd-item big"
                    v-if="index===2"
                    v-for="(item,index) in themeList"
                    :key="index"
                    @click="linkToTheme(item.id)"
                    :data-name="item.name">
                    <img :src="item.topic_img.url"
                        alt="">
                </div>
                <div class="selectd-item"
                    :data-id="item.id"
                    :data-name="item.name"
                    @click="linkToTheme(item.id)"
                    v-else>
                    <img :src="item.topic_img.url"
                        alt="">
                </div>
            </div>
        </div>
        <div class="recent-products">
            <div class="title">
                <h5>最近新品</h5>
            </div>
            <products :products="recentList"></products>
        </div>
    </div>
</template>

<script>
import { Swiper, SwiperItem, ButtonTab, ButtonTabItem, Divider,Toast} from 'vux'
import products from '@/components/Products'
const bannerId = 1
const themeIds = '1,2,3'
export default {
    name: 'Home',
    data() {
        return {
            imgList: [],
            themeList: [],
            recentList: []
        }
    },
    created() {
        this.getBanner()
        this.getTheme()
        this.getRecent()
    },
    methods: {
        linkToDetail(id) {
            this.$router.push({ path: '/page/detail', query: { id: id } })
        },
        linkToTheme(id) {
            this.$router.push({
                path: '/page/theme',
                query: { id: id }
            })
        },
        getBanner() {
            this.$http
                .get(
                    `https://www.easy-mock.com/mock/5a4896ba62de717d44f2406e/api/v1/banner/${bannerId}`
                )
                .then(res => {
                    this.imgList = res.data.data.items
                })
        },
        getTheme() {
            this.$http
                .get(
                    `https://www.easy-mock.com/mock/5a4896ba62de717d44f2406e/api/v1/theme?ids=${themeIds}`
                )
                .then(res => {
                    this.themeList = res.data.data
                })
        },
        getRecent() {
            this.$http
                .get(
                    'https://www.easy-mock.com/mock/5a4896ba62de717d44f2406e/api/v1/product/recent'
                )
                .then(res => {
                    this.recentList = res.data.data
                })
        }
    },

    components: {
        Swiper,
        SwiperItem,
        products
    }
}
</script>

<style scoped lang="less">
.home {
    color: #333333;
    background: #f7f7f7;
    .banner{
        position: relative;
        padding-bottom: 2.5rem;
        .swiper-item img {
            width: 100%;
        }
        .bottom{width: 90%;margin-left: 5%;background: #ffffff;border-radius: 5px;padding: 0.5rem 0;position: absolute;bottom: 0rem;z-index: 1;
            .title{
                line-height: 3rem;padding: 0 1rem;
                img{width:5rem;position: relative;top: 0.5rem;padding-right: 1.3rem;border-right: 0.1rem solid #FF8134}
                span{padding: 0 1rem;font-size: 0.9rem;}
            }
            h5{padding:0rem 1rem;font-size: 0.7rem;font-weight: normal;
            .circular{display: inline-block;width: 0.1rem;height: 0.1rem;border-radius: 50%;border: 1px solid #FF8134;padding: 0;position: relative;bottom: 0.1rem;margin-right: 0.3rem;}
            }
        }
    }
    /*新品*/
    .newgoods{
        background: #ffffff;margin-top: 15px;padding:0 5%;
        .top{
            position: relative;
            top: 0.5rem;
            border-bottom: 1px solid #eeeeee;
            .title{font-weight: 600;font-size: 0.9rem;}
            .left{display: inline-block;width: 45%;text-align: right;
                b{font-weight: normal;color: #999999;font-size: 0.7rem;text-align: left;display: inline-block;width: 100%;}
                img{width: 5rem;}
            }
            .right{display: inline-block;width: 45%;text-align:center;margin-left:5%;img{width:7rem;}}
        }
        .bottom{
            min-height: 120px;
            margin-top: 0.9rem;
            vertical-align: top;
            h5{font-size: 1rem;}
            .left{width: 48%;display: inline-block;height: 100%;
                span{
                    display: inline-block;width: 100%;
                    b{color: #999999;font-size: 0.7rem;vertical-align: top;font-weight: normal;display: inline-block;}
                    img{width: 3.5rem;margin-left: 1rem;}
                }
            }
            .right{display: inline-block;width: 48%;margin-left: 2%;height: 100%;
                b{color: #ffffff;font-weight: normal;font-size: 0.6rem;text-align: center;line-height: 1rem;background: #DCC6A5;padding: 0.1rem 0.5rem;border-radius: 50px;vertical-align: top;}
                img{width: 6rem;}
            }
        }
    }
    /*活动*/
    .product{
        background: #ffffff;margin-top: 15px;padding: 1rem 3%;
        .title{
            h5{text-align: center;line-height: 2rem;position: relative;
            .square{display:inline-block;width: 4px;height: 4px;background: #333333;transform: rotate(40deg);position: relative;top: -0.2rem;}
            }
            h5:after{content: '';display: inline-block;width: 20%;height: 1px;background: #333333;position: absolute;left: 16%;top: 50%;}
            h5:before{content: '';display: inline-block;width: 20%;height: 1px;background: #333333;position: absolute;right: 16%;top: 50%;}
            p{text-align: center;color: #999999;font-size: 0.8rem;}
        }
        .list{margin: 0;padding: 0;
            li{min-height: 175px;list-style: none;border-radius: 5px;border: 1px solid #eeeeee;position: relative;margin-top: 10px;
                p{position: absolute;bottom: 0;border-bottom-right-radius: 5px;border-bottom-left-radius: 5px;background: rgba(0,0,0,.5);height:30px;line-height: 30px;color: #ffffff;width: 98%;font-size: 0.8rem;padding-left:0.5rem;left: 0; 
                    img{width: 1rem;position: relative;top: 0.2rem;}
                    .right{float: right;margin-right: 0.5rem;
                        b{font-weight: normal;width: 1.2rem;height: 1.2rem;background: #F54321;color: #ffffff;text-align: center;line-height: 1.2rem;border-radius: 5px;display: inline-block;}
                    }
                }
            }
        }
    }
    /*好物*/
    .Goodthing{
        background: #ffffff;margin-top: 15px;padding: 1rem 3%;
        .title{
            h5{text-align: center;line-height: 2rem;position: relative;
            .square{display:inline-block;width: 4px;height: 4px;background: #333333;transform: rotate(40deg);position: relative;top: -0.2rem;}
            }
            h5:after{content: '';display: inline-block;width: 20%;height: 1px;background: #333333;position: absolute;left: 16%;top: 50%;}
            h5:before{content: '';display: inline-block;width: 20%;height: 1px;background: #333333;position: absolute;right: 16%;top: 50%;}
            p{text-align: center;color: #999999;font-size: 0.8rem;}
        }
        .list{
            display:flex;
            overflow-x: auto;
            overflow-y: hidden;
            padding-bottom: 10px;
            white-space: nowrap;
        }
        .list::-webkit-scrollbar {
            display: none;
        }
        .list{
            margin-top: 10px;
            li{display: inline-block;width: 33%;padding-right: 1rem;
                img{width: 100%;}
                p{width: 100%;overflow: hidden;height: 1.2rem;font-size: 0.8rem;}
                .c-f54321{color: #F54321}
            }
        }
    }
    .selected-themes {
        overflow: hidden;
        .title {
            padding: 10px 0;
            font-size: 18px;
            color: #ab956d;
            text-align: center;
            h5 {
                font-weight: normal;
            }
        }
        .selectd-box {
            font-size: 0;
            overflow: hidden;
            .selectd-item {
                display: inline-block;
                width: 50%;
                border-bottom: 2px solid #fff;
                box-sizing: border-box;
                img {
                    width: 100%;
                }
                &:nth-child(1){
                    border-right:1px solid #fff;
                }
                &:nth-child(2) {
                    border-left:1px solid #fff;
                }
                &.big {
                    width: 100%;
                }
            }
        }
    }
    .recent-products {
        .title {
            padding: 10px 0;
            font-size: 18px;
            color: #ab956d;
            text-align: center;
            h5 {
                font-weight: normal;
            }
        }
    }
    /*设置5/se样式*/
    @media screen and (max-width: 320px) {
        .banner{
            .bottom{
                .title{
                    img{width:4rem;position: relative;top: 0.5rem;padding-right: 1rem;border-right: 0.1rem solid #FF8134}
                    span{padding: 0 0.8rem;font-size: 0.8rem;}
                }
                h5{padding:0rem 1rem;font-size: 0.6rem;font-weight: normal;}
            }
        }
        .newgoods{
            .bottom{
                h5{font-size: 0.8rem;}
                .left{width: 48%;display: inline-block;height: 100%;
                    span{
                        img{width: 2.5rem;margin-left: 1rem;}
                    }
                }
                .right{display: inline-block;width: 48%;margin-left: 2%;height: 100%;
                    img{width: 4rem;}
                }
            }
        }
        .product{
            .title{
                h5:after{left: 12%;}
                h5:before{right: 12%;}
            }
        }
        .Goodthing{
            .title{
                h5:after{left: 12%;}
                h5:before{right: 12%;}
            }
        }
        .product{
            .title{
                h5:after{left: 12%;}
                h5:before{right: 12%;}
            }
        }
    }
}
</style>
