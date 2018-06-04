<template>
    <div class="order">
        <div class="address">
        <p class="address_none" @click="editAddress"><img src="~@/assets/icon/position.png"><span>新建收货地址以确保商品顺利送达</span></p>
            <!-- 
            <img src="~@/assets/icon/position.png">
            <span>
                <b class="name">王先生&emsp;15201915217</b>
                <b>上海市 上海市 徐汇区 番禺路1199弄</b>
            </span> -->
            <img class="line" src="~@/assets/icon/line@2x.png">
        </div>
        <div class="middle">
            <ul class="list">
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <div class="left">
                        <p class="top">
                            <span class="fl">亚菲儿女士香水经典限量版本 量版本</span>
                            <span class="fr">¥90.00</span>
                        </p>
                        <p class="bottom">
                            <span class="fl">规格: 50ml</span><span class="fr">&Chi;1</span>
                        </p>
                    </div>
                </li>
                <li>
                    <img src="~@/assets/img/newgoods.png">
                    <div class="left">
                        <p class="top">
                            <span class="fl">亚菲儿女士香水经典限量版本 量版本</span>
                            <span class="fr">¥90.00</span>
                        </p>
                        <p class="bottom">
                            <span class="fl">规格: 50ml</span><span class="fr">&Chi;1</span>
                        </p>
                    </div>
                </li>
            </ul>
        </div>
        <p class="charge">
            <span>优惠券</span>
            <span class="right">2张可用 <img src="~@/assets/icon/goods-left.png"></span>
        </p>
        <p class="notes">
            <span>备注</span>
            <span class="right">给商家留言(50字以内)</span>
        </p>
        <p class="store">
            <span><img src="~@/assets/icon/store.png" />&ensp;会员卡省钱</span>
            <span class="right">-￥45.00</span>
        </p>
        <ul class="goods_list">
            <li>商品总价<span>￥760</span></li>
            <li>税费<span>0.00</span></li>
            <li>运费<span>包邮</span></li>
            <li>总优惠<span>-￥45</span></li>
            <li><span>订单金额<b>￥760</b></span></li>
        </ul>
        <p class="button">
            <span>订单金额:<b>￥715</b></span>
            <span class="right">确认付款</span>
        </p>
    </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'
import Vue from 'vue'
import $ from 'jquery'
import axios from 'axios'
import * as myPub from '@/assets/js/public.js'
import * as openId from '@/assets/js/opid_public.js'
export default {
    name: 'order',
    data() {
        return {
            account: null
        }
    },
    computed: {
        ...mapGetters(['selectedArr', 'userInfo']),
        totalDetail() {
            return this.userInfo.addressInfo.cityVal + ' ' + this.userInfo.addressInfo.detail
        }
    },
    created() {
        this.account = this.$route.query.account
    },
    methods: {
        ...mapMutations(['PLACE_ORDER']),
        pay() {
            if (!this.userInfo.addressInfo) {
                this.$vux.alert.show({
                    title: '下单提示',
                    content: `请填写您的收货地址`
                })
                return
            }
            const orderItem = {
                productItem: this.selectedArr,
                account: this.account
            }
            /* 下单和付款 */
            this.PLACE_ORDER(orderItem)
            this.$router.push({ path: '/page/user' })
        },
        editAddress() {
            this.$router.push({ path: '/page/address' })
        }
    },
    filters: {
        formatMoney(value) {
            return '￥' + value
        }
    },
}
</script>

<style scoped lang="less">
.order {
    background-color: #f7f7f7;
    font-size: 0.8rem;
    .address{
        height: 80px;
        position: relative;
        background: #ffffff;
        .line{position:absolute;top:80px;width: 100%;left: -12px;}
        img{width: 1.5rem;margin-left: 1rem;position: relative;top: 0rem;}
        span{
            color: #999999;font-size: 0.9rem;line-height: 80px;display: inline-block;margin-left: 0.5rem;width: 80%;line-height: 20px;
            b{font-weight: normal;}
            .name{color: #333333;font-size: 0.9rem;display: inline-block;width: 100%;margin-top: 1rem;}
        }
        .address_none{
            img{position: relative;top: 0.3rem}
            span{line-height: 80px;}
        }
    }
    .middle{
        margin-top: 15px;
        background: #ffffff;
        .list{
            li{
                padding:15px;
                border-bottom: 1px solid #eeeeee;
                img{width: 25%;border:1px solid #eeeeee;}
                .left{
                    width: 70%;float: right;
                    p{
                        width: 100%;
                        color: #333333;
                        font-size: 1rem;
                        .fl{width: 70%;display: inline-block;}
                        .fr{vertical-align: top;text-align: right;width:28%;display: inline-block;}
                    }
                    .bottom{color: #999999;font-size: 0.8rem;margin-top: 10px;}
                }
            }
            li:last-child{border-bottom: 0;}
        }
    }
    .charge{
        background: #ffffff;
        margin-top: 15px;
        padding: 15px;
        span{font-size: 1rem;color: #333333;}
        .right{
            float: right;color: #F54321;
            position: relative;
            top: -0.2rem;
            img{width: 0.8rem;position: relative;top: 0.3rem;}
        }
    }
    .notes{
        background: #ffffff;
        margin-top: 15px;
        padding: 15px;
        span{font-size: 1rem;color: #333333;}
        .right{
            float: right;color: #999999;
            font-size: 0.9rem;
        }
    }
    .store{
        background: #ffffff;
        margin-top: 15px;
        padding: 15px;
        span{font-size: 1rem;color: #333333;img{width: 1rem;position: relative;top: 0.1rem;}}
        .right{
            float: right;color: #F54321;
            font-size: 0.9rem;
        }
    }
    .goods_list{
        margin-top: 15px;
        background: #ffffff;
        padding: 15px;
        li{
            font-size: 0.9rem;color: #333333;list-style: none;line-height: 40px;height: 40px;
            span{float: right;b{font-weight: normal;color: #FF5639}}
        }
    }
    .button{
        background: #ffffff;position: fixed;bottom: 0;width: 100%;height: 50px;line-height: 50px;
        span{
            font-size: 0.9rem;
            margin-left: 15px;
            b{color: #FF5639;margin-left: 5px;}
        }
        .right{display: inline-block;float: right;width: 30%;color: #ffffff;background: #F54321;text-align: center;line-height: 50px;margin-left: 0;}
    }
   /* .order-address-info {
        padding: 10px 20px;
        margin-bottom: 10px;
        background: #fff;
        .address-box {
            display: flex;
            .contact-box {
                flex: 1;
                .contact {
                    display: flex;
                    justify-content: space-between;
                    margin-bottom: 12px;
                    div {
                        display: flex;
                        align-items: center;
                        &.mobile {
                            flex-basis: 100px;
                        }
                        img {
                            height: 16px;
                            width: 16px;
                            margin-right: 5px;
                        }
                        .text {
                            color: #333;
                        }
                    }
                }
                .detail {
                    color: #999999;
                }
            }
            .contact-icon {
                flex-basis: 55px;
                display: flex;
                align-items: center;
                justify-content: flex-end;
                img {
                    transform: rotate(270deg);
                    height: 24px;
                    width: 24px;
                }
            }
        }
        .add-address {
            width: 100%;
            color: #989898;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            .icon-add {
                font-style: normal;
                margin-right: 5px;
            }
        }
    }
    .order-main {
        background-color: #fff;
        padding-bottom: 46px;
        .product-item {
            display: flex;
            justify-content: space-around;
            height: 90px;
            color: #6d6d6d;
            border-bottom: 1px solid #e9e9e9;
            padding: 10px;
            .item-left {
                flex-basis: 90px;
                height: 100%;
                background-color: #f5f6f5;
                border-radius: 2px;
                img {
                    width: 100%;
                    height: 100%;
                }
            }
            .item-middle {
                flex: 1;
                margin-left: 10px;
            }
            .item-right {
                flex-basis: 45px;
                text-align: center;
            }
        }
    }
    .footer-account-box {
        position: fixed;
        z-index: 100;
        bottom: 0;
        height: 46px;
        width: 100%;
        background: #fff;
        display: flex;
        border-top: 1px solid #ccc;
        border-bottom: 1px solid #ccc;
        box-sizing: border-box;
        div {
            display: flex;
            align-items: center;
            &.total-account {
                flex: 1;
                color: #93312e;
                padding-left: 10px;
            }
            &.pay {
                flex-basis: 120px;
                background-color: #ab956d;
                color: #fff;
                justify-content: center;
                &.active {
                    background: #84704d;
                }
                &.disabled {
                    background: rgba(171, 149, 109, 0.6);
                    pointer-events: auto;
                }
            }
        }
    }*/
}
</style>
