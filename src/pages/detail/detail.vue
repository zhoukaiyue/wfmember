<template>
    <div class="detail">
        <div class="detail-main"
             v-if="product">
            <div class="detail-img">
                <swiper :list="demo01_list" v-model="demo02_index" @on-index-change="demo01_onIndexChange"></swiper>
            </div>
            <div class="product-info-box">
                <div class="price">
                    <span class="coupon_price">券后价</span>￥599 <s>￥600</s>
                    <span class="order_information order_information_s">包税</span><span class="order_information">包邮</span>
                </div>
                <div class="sold_information">
                    <div class="sold"><span>已售1</span>件</div>
                    <div class="preview">已有<span>15</span>人预览</div>
                </div>
                <div class="Member">
                    <span class="specail"><img src="~@/assets/icon/store.png"> 会员价 ¥81.00</span><span>加入会员，一年至少可省4500元 <img src="~@/assets/icon/goods-left.png"></span>
                </div>
                <div class="name_box">
                    <div class="name_tbor"></div>
                    <p class="name">汽车</p>
                </div>
                <div class="country">
                    <div class="country_span">来自中国
                        <img src="~@/assets/icon/Bitmap@2x.png" alt="">
                    </div>
                    <div class="country_label">本商品售价已含税，无需额外支付税费</div>
                </div>
            </div>
        </div>
        <!-- 领取优惠券 -->
        <div class="charge">
            <p>领券<span class="charge_detail">满135-50 <img src="~@/assets/icon/goods-left.png" @click="charge"></span></p>
            <div v-if="is_show1" class="charge_list" >
                <p>领取优惠券<span class="charge_detail"><img src="~@/assets/icon/close.png" @click="hide"></span></p>
                <ul>
                    <li>
                        <div>
                            <p class="title">￥50&emsp;<span>满135元使用</span></p>
                            <p>仅限亚菲儿女士香水商品使用</p>
                            <p class="Notes">领取后3天内使用</p>
                        </div>
                        <span class="button">立即领取</span>
                    </li>
                </ul>
                <p></p>
            </div>
        </div>
        <!-- 商品规格 -->
        <div class="goods">
            <p>商品规格<span class="charge_detail">已选：100&Chi;1<img src="~@/assets/icon/goods-left.png" @click="charge"></span></p>
        </div>
        <p class="middle">继续拖动，查看图文详情</p>
        <div class="detail-bottom">
            <tab :line-width=2
                 active-color='#AB956D'
                 v-model="index">
                <tab-item class="vux-center"
                          :selected="selectd === item"
                          v-for="(item, index) in list"
                          @click="selectd = item"
                          :key="index">{{item}}</tab-item>
            </tab>
            <swiper v-model="index"
                    height="auto"
                    :show-dots="false">
                <swiper-item v-for="(item, index) in list"
                             :key="index">
                    <div class="tab-swiper vux-center">{{item}}</div>
                </swiper-item>
            </swiper>
        </div>
        <div class="bottom">
            <label>
                <img src="~@/assets/icon/index.png">
                <span>首页</span>
            </label>
            <label>
                <img src="~@/assets/icon/shop.png">
                <span>客服</span>
            </label>
            <label>
                <img src="~@/assets/icon/Combined Shape@2x.png">
                <span>购物车</span>
                <span class="cirule">6</span>
            </label>
            <span class="curt" @click="addCart">加入购物车</span>
            <span class="buy">立即购买</span>
        </div>
        <div class="joinCart" v-if="is_show3">
            <div class="top">
                <img class="goodsimg" src="~@/assets/img/newgoods.png">
                <p>
                    <span><b>￥90.00</b><b class="specail"><img src="~@/assets/icon/store.png"> 会员价 ¥81.00<img @click="hidecart" class="img" src="~@/assets/icon/close.png"></b></span>
                    <span class="Specifications">已选择：淡香型、50ml</span>
                </p>
            </div>
            <div class="middle">
                <p>颜色</p>
                <p>
                    <span class="none">浓香</span><span>男士</span><span>淡香</span><span>任意发货</span>
                </p>
            </div>
            <div class="middle">
                <p>尺寸</p>
                <p>
                    <span class="none">10ML</span><span>30ML</span><span>50ML</span>
                </p>
            </div>
            <div class="middle">
                <p class="num">数量 <span class="reduce" @click="reduce">-</span><input placeholder="0" value="0" /><span class="add" @click="add">+</span></p>
            </div>
            <div class="bottom">确认加入</div>
        </div>
         <div class="bg" v-if="is_show2"></div>
    </div> 
</template>

<script>
import { PopupPicker, Tabbar, TabbarItem,ViewBox,Actionsheet, Tab, TabItem, Swiper, SwiperItem,Qrcode, GroupTitle,  Divider,XDialog, Popup, Group, Cell, XButton, XSwitch, Toast, XAddress, ChinaAddressData,TransferDomDirective as TransferDom } from 'vux'
import { mapState, mapMutations, mapGetters } from 'vuex'
import axios from 'axios'
import $ from 'jquery'
const tabList = () => ['图文详情']
const baseList = [{
  img: 'https://ww1.sinaimg.cn/large/663d3650gy1fq66vvsr72j20p00gogo2.jpg',
}, {
  img: 'https://ww1.sinaimg.cn/large/663d3650gy1fq66vw1k2wj20p00goq7n.jpg',
}, {
  img: 'https://static.vux.li/demo/5.jpg', // 404
  fallbackImg: 'https://ww1.sinaimg.cn/large/663d3650gy1fq66vw50iwj20ff0aaaci.jpg'
}]
export default {
    name: 'detail',
    data() {
        return {
            product: null,
            countsArray: [[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]],
            count: ['1'],
            list: tabList(),
            selectd: '商品详情',
            index: 0,
            isFly: false,
            isShake: false,
            demo01_list: baseList,
            demo02_index: 1,
            is_show1:false,
            is_show2:false,
            is_show3:false,
        }
    },
    computed: {
        ...mapState(['userInfo']),
        ...mapGetters(['totalCount']),
        isDisabled() {
            return this.product.stock > 0
        }
    },
    created() {},
    activated() {
        this.getALLProducts()
    },
    methods: {
        ...mapMutations(['ADD_TO_CART']),
        linkToCart() {
            this.$router.push({ path: '/page/cart' })
        },
        demo01_onIndexChange (index) {
          this.demo01_index = index
        },
        getALLProducts() {
            this.$http
                .get(
                    'https://www.easy-mock.com/mock/5a4896ba62de717d44f2406e/api/v1/product/all'
                )
                .then(res => {
                    let detailData = res.data.data.filter(item => {
                        return item.id === +this.$route.query.id
                    })
                    this.product = detailData[0]
                })
        },
        onAddToCart() {
            // 如果没登录，先去登录
            if (!this.userInfo) {
                this.$router.push({ path: '/login' })
            }
            // 缺货时禁止点击
            if (!this.isDisabled) {
                this.$vux.toast.text('暂时缺货哦~', 'middle')
                return
            }
            // 防止过快点击
            if (this.isFly) return
            // 移动距离
            let rect1 = this.$refs.smallTopImg.getBoundingClientRect()
            let rect2 = this.$refs.topCart.getBoundingClientRect()
            let x = rect1.right - rect2.right + (40 - 16)
            let y = rect2.top - rect1.top - 20
            this.isFly = true
            this.$nextTick(() => {
                this.$refs.smallTopImg.style.transform = `translate(${x}px,${y}px) rotate(350deg) scale(0)`
            })
            setTimeout(() => {
                // 飞入购物车动画恢复到最初状态
                this.isFly = false
                this.$refs.smallTopImg.style.transform = 'none'
                // 右侧购物车图标放大
                this.isShake = true
                setTimeout(() => {
                    let count = +this.count // 字符串类型数字转为数字
                    if (this.product.isChecked === undefined) {
                        this.$set(this.product, 'isChecked', true)
                    }
                    this.ADD_TO_CART(
                        Object.assign({}, this.product, { count: count })
                    )
                    this.isShake = false
                }, 200)
            }, 1000)
        },
        charge(){
            const _this = this
            _this.is_show1 = true
            _this.is_show2 = true
        },
        hide(){
            const _this = this
            _this.is_show1 = false
            _this.is_show2 = false
        },
        add(){
            const _this = this
            const value =$('.num input').val()
            console.log(value)
            if (value >= '0') {
                // parseInt(.num input.val()) + 1
                $('.num input').val(parseInt($('.num input').val()) + 1)
            }
        },
        reduce(){
            const _this = this
            const value =$('.num input').val()
            console.log(value)
            if (value > '0') {
                // parseInt(.num input.val()) + 1
                $('.num input').val(parseInt($('.num input').val()) - 1)
            }
        },
        addCart(){
            const _this = this
            _this.is_show2 = true
            _this.is_show3 = true
        },
        hidecart(){
            const _this = this
            _this.is_show2 = false
            _this.is_show3 = false
        }
    },
    components: {
        PopupPicker,
        Tab,
        TabItem,
        Swiper,
        SwiperItem,
        Qrcode,
        Divider,
        XDialog,
        Popup,
        Group,
        XSwitch,
        Popup,
        Group,
        Cell,
        XSwitch,
        Toast,
        XAddress,
        XButton,
        GroupTitle,
        Tabbar,
        TabbarItem,
        ViewBox,
        Actionsheet,
        TransferDom
    }
}
</script>

<style scoped lang="less">
.detail {
    position: relative;
    background-color: #f8f8f8;
    .bg{position: absolute;width: 100%;height: 100%;background: rgba(0,0,0, .3);top: 0;left:0; }
    .detail-main {
        background: #fff;
        .fixed-cart-box {
            position: fixed;
            z-index: 10;
            top: 71px;
            right: 12px;
            width: 40px;
            height: 32px;
            img {
                width: 32px;
                height: 32px;
            }
            .total-count {
                font-size: 12px;
                background-color: #ab956d;
                color: #fff;
                position: absolute;
                right: 32px;
                top: 0;
                height: 18px;
                width: 18px;
                line-height: 18px;
                border-radius: 18px;
                text-align: center;
            }
            &.animate {
                animation: animateCartScale 200ms
                    cubic-bezier(0.17, 0.67, 0.83, 0.67);
                animation-fill-mode: backwards;
            }
        }
        .detail-img {
            position: relative;
            height: 0;
            padding-top: 180px;
            .vux-slider{top: -180px;}
        }
        .product-info-box {
            border-top:1px solid #eeeeee;
            border-bottom:1px solid #eeeeee;
            padding:8px 0;
            color:#454552;
            /*text-align:center;
            */
           .price {
                font-size:1.3rem;
                color:#f54321;
                .coupon_price {
                    margin-left:17px;
                    margin-top:6.5px;
                    float:left;
                    border:1px solid #f54321;
                    border-radius:4px;
                    width:40px;
                    height:17px;
                    line-height:17px;
                    font-family:PingFangSC-Semibold;
                    font-size:0.6rem;
                    color:#f54321;
                    letter-spacing:0;
                    text-align:center;
                }
                s{
                    font-family:PingFangSC-Regular;
                    font-size:14px;
                    color:#999999;
                    letter-spacing:0;
                    text-align:left;
                }
                .order_information {
                    display:inline-block;
                    background:#ff5f41;
                    border-radius:4px;
                    width:33px;
                    height:23px;
                    margin-left:10px;
                    font-family:PingFangSC-Regular;
                    font-size:0.6rem;
                    color:#ffffff;
                    letter-spacing:0;
                    text-align:center;
                    line-height:23px;
                    vertical-align:text-bottom;
                }
                .order_information_s {
                    background:#56c66a;
                }
            }
            .country {
                width:100%;
                padding:0px 17px;
                font-size:0.8rem;
                color:#999999;
                letter-spacing:0;
                text-align:left;
                display:flex;
                height:2rem;
                line-height:2rem;
                /*border:1px solid red;*/
                box-sizing:border-box;
                flex-wrap:nowrap;
                justify-content:space-between;
                .country_span {
                    font-size: 0.9rem;
                     img {
                            display:inline-block;
                            width:1.5rem;
                            height:1rem;
                            /*background:red;*/
                            vertical-align: middle;
                        }
                    }
                    .country_span,.country_label {
                        margin:0;
                    }
                }
                .Member{
                    background: #F5F7F9;
                    margin-left: 17px;
                    margin-right: 17px;
                    padding: 5px 17px;
                    height: 30px;
                    span{
                        color: #777777;
                        font-size: 0.7rem;
                        float: right;
                        line-height: 30px;
                        img{width: 0.6rem;position: relative;top: 0.3rem;}
                    }
                    .specail{
                        color: #F98800;
                        font-size: 0.9rem;
                        float: left;
                        line-height: 30px;
                        img{width: 1rem;position: relative;top: 0.1rem;}
                    }
                }
                .name_box {
                    box-sizing:border-box;
                    width:100%;
                    font-size:20px;
                    padding:0px 17px;
                    .name_tbor {
                        background:#eeeeee;
                        width:100%;
                        height:1px;
                    }
                .name {
                    font-family:PingFangSC-Semibold;
                    font-size:1rem;
                    color:#333333;
                    letter-spacing:0;
                    text-align:left;
                    font-weight:700;
                }
            }
            .name_box {
                    box-sizing:border-box;
                    width:100%;
                    font-size:20px;
                    padding:0px 17px;
                    .name_tbor {
                        background:#eeeeee;
                        width:100%;
                        height:1px;
                    }
                .name {
                    font-family:PingFangSC-Semibold;
                    font-size:1rem;
                    color:#333333;
                    letter-spacing:0;
                    text-align:left;
                    font-weight:700;
                }
            }
            .sold_information {
                width:100%;
                height:17px;
                display:flex;
                box-sizing:border-box;
                flex-wrap:nowrap;
                justify-content:space-between;
                padding:0px 17px;
                font-family:PingFangSC-Regular;
                font-size:13px;
                color:#999999;
                letter-spacing:0;
                text-align:left;
                .sold {
                    height:100%;
                    margin:0px!important;
                }
                .preview {
                    height:100%;
                    margin:0px!important;
                }
            }
            div {
                margin:10px auto;
                .stock {
                    font-size:0.6rem;
                .no {
                    color:#b42f2d;
                }
            }
                
            }
        }
    }
    .charge{
        width: 100%;height: 50px;line-height: 50px;margin-top: 10px;background: #ffffff;position: relative;
        p{
            font-size: 1rem;font-weight: 600;padding: 0 17px;
            span{
                float: right;color: #F54321;font-weight: normal;margin-right: 0.2rem;
                img{width: 0.6rem;position: relative;top: 0.1rem;}
            }
        }
        .charge_list{
            width: 100%;
            position: fixed;
            background: #ffffff;
            bottom: 0;
            z-index: 1111;
            padding-bottom: 2.5rem;
            p{
                 span{
                    float: right;color: #F54321;font-weight: normal;
                    img{width: 1rem;border: 1px solid #eeeeee;}
                }
            }
            ul{
                margin: 0;padding: 0;
                li{
                    background: url(~@/assets/icon/Rectangle 8@2x.png);
                    background-size: 100%;
                    height:6.7rem;
                    div{
                        float: left;width: 70%;
                        p{font-size: 0.9rem;color: #333333;font-weight: normal;line-height: 35px;}
                        .title{
                            font-size: 1.5rem;color: #FF8134;
                            span{font-size: 0.8rem;margin-right:3rem;}
                        }
                        .Notes{font-size: 0.8rem;color: #999999}
                    }
                    .button{display: inline-block;width: 30%;height: 30px;background: #FF8134;border-radius: 50px;color: #ffffff;text-align: center;line-height: 30px;position: relative;right:8%;top: 20%;}
                }
            }
        }
    }
    .goods{
        width: 100%;height: 50px;line-height: 50px;margin-top: 10px;background: #ffffff;position: relative;
        p{
            font-size: 1rem;font-weight: 600;padding: 0 17px;
            span{
                float: right;color: #999999;font-weight: normal;margin-right: 0.2rem;
                img{width: 0.6rem;position: relative;top: 0.1rem;}
            }
        }
    }
    .middle{height: 40px;width: 100%;font-size: 0.8rem;text-align: center;color: #999999;line-height: 40px;}
    .detail-bottom{
        margin-top: 10px;
    }
    .bottom{
        width: 100%;
        background: #ffffff;
        height: 60px;
        line-height: 60px;
        position: fixed;
        bottom: 0;
        border-top: 1px solid #eeeeee;
        label{
            display: inline-block;
            width: 12%;
            height: 100%;
            text-align: center;
            color: #777777;
            position: relative;
            float: left;
            img{width: 1.2rem;}
            span{font-size: 0.7rem;width: 100%;line-height: 20px;display: inline-block;position: relative;bottom: 40px}
            .cirule{display:inline-block;width: 0.8rem;height: 0.8rem;background: #F54321;color: #ffffff;right: 0.4rem;top:0.9rem;border-radius: 50%;position: absolute;text-align: center;line-height: 0.8rem;font-size: 0.2rem;}
        }
        .curt{width: 32%;display: inline-block;background: #F87B63;color: #ffffff;text-align: center;line-height: 60px;height: 60px;position: relative;float: left;}
        .buy{width: 32%;display: inline-block;background: #F54321;color: #ffffff;text-align: center;line-height: 60px;height: 60px;position: relative;float: left;}
    }
    .joinCart{
        width: 100%;
        background: #ffffff;
        position: fixed;
        bottom: 0;
        z-index: 11111;
        height: 325px;
        .top{
            vertical-align: top;
            padding: 10px;
            position: relative;
            border-bottom: 1px solid #eeeeee;
            min-height: 55px;
            .goodsimg{width:25%;position: absolute;top:-30px;border:1px solid #eeeeee;}
            p{
                vertical-align: top;
                display: inline-block;
                width:70%;
                float: right;
                b{color:#F54321;font-weight: normal;}
                .img{width: 0.8rem;float: right;margin-top:5px;margin-right: 5px;}
                .specail{
                    color: #F98800;font-size: 0.8rem;margin-left: 1rem;
                    img{width: 0.8rem;}
                }
                .Specifications{color: #999999;display: block;font-size: 0.7rem;margin-top: 0.2rem;}
            }
        }
        .middle{
            text-align: left;
            padding: 0 17px;
            color: #999999;
            font-size: 0.8rem;
            height: auto;
            margin-bottom: 15px;
            p{
                line-height: 30px;
                span{padding: 3px 5px;border:1px solid #dddddd;color: #999999;margin-right: 5px;}
                .none{background: #f7f7f7;color: #dddddd}
                .select{color: #F54321;border:1px solid #F54321;}
            }
            .num{
                margin-top: 10px;
                input{width: 50px;border: 1px solid #eeeeee;height: 26px;position: relative;top:-1px;text-align: center;line-height: 26px;}
                .reduce{width: 30px;padding: 0;display: inline-block;height: 25px;text-align: center;line-height: 25px;margin-right: 0;margin-left: 10px;}
                .add{width: 30px;padding: 0;display: inline-block;height: 25px;text-align: center;line-height: 25px;}
            }          
        }
        .bottom{
            height: 40px;line-height: 40px;width: 100%;text-align: center;color: #ffffff;background: #F54321
        }
    }
}

@keyframes animateCartScale {
    0% {
        -webkit-transform: scale(1.2);
    }
    100% {
        -webkit-transform: scale(1);
    }
}
</style>
