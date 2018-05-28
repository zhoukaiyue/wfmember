<template>
    <div class="goodlist">
        <ul class="nav">
            <li v-bind:class="{ select: is_show1}" @click="salesVolume1()">综合</li>
            <li v-bind:class="{ select: is_show2}" @click="salesVolume2()">销量</li>
            <li v-bind:class="{ select: is_show3}" @click="salesVolume3()">价格</li>
            <li v-bind:class="{ select: is_show4}" @click="salesVolume4()" class="last">筛选</li>
        </ul>
        <ul class="goods">
            <li>
                <img src="~@/assets/img/newgoods.png">
                <p>精美礼盒亚菲儿女士香水女士持久淡香清新50ml香水</p>
                <p><span>￥358.00</span><img src="~@/assets/icon/cartselect.png"></p>
            </li>
            <li>
                <img src="~@/assets/img/category-goods.png">
                <p>精美礼盒亚菲儿女士香水女士持久淡香清新50ml香水</p>
                <p><span>￥358.00</span><img src="~@/assets/icon/cartselect.png"></p>
            </li>
            <li>
                <img src="~@/assets/img/newgoods.png">
                <p>精美礼盒亚菲儿女士香水女士持久淡香清新50ml香水</p>
                <p><span>￥358.00</span><img src="~@/assets/icon/cartselect.png"></p>
            </li>
            <li>
                <img src="~@/assets/img/category-goods.png">
                <p>精美礼盒亚菲儿女士香水女士持久淡香清新50ml香水</p>
                <p><span>￥358.00</span><img src="~@/assets/icon/cartselect.png"></p>
            </li>
        </ul>
    </div>
</template>
<script>
import Vue from 'vue'
import axios from 'axios'
import $ from 'jquery'
import { XInput, Group, XButton, Cell, Toast, base64 } from 'vux'
export default {
    name: 'category',
    data() {
        return {
            is_show1:true,
            is_show2:false,
            is_show3:false,
            is_show4:false
        }
    },
    created() {
    },
    computed: {
        menuBanner() {
            return this.menu[this.currentIndex].img.url
        },
        categoryTitle() {
            return this.menu[this.currentIndex].name
        }
    },
    methods: {
        switchCategory(index, id) {
            this.currentIndex = index
            this.getProduct(id)
        },
        linktoDetail(id) {
            this.$router.push({ path: '/page/detail', query: { id: id } })
        },
        // 综合
        salesVolume1:function(){
            const _this = this;
            this.is_show1=true
            this.is_show2=false
            this.is_show3=false
            this.is_show4=false
            _this.$loading.show();//显示
            setTimeout(() => {
                _this.$loading.hide();//隐藏
            }, 2000)
        },
        // 销量
        salesVolume2:function(){
            const _this = this;
            this.is_show1=false
            this.is_show2=true
            this.is_show3=false
            this.is_show4=false
            _this.$loading.show();//显示
            setTimeout(() => {
                _this.$loading.hide();//隐藏
            }, 2000)
        },
        // 价格
        salesVolume3:function(){
            const _this = this;
            this.is_show1=false
            this.is_show2=false
            this.is_show3=true
            this.is_show4=false
           _this.$loading.show();//显示
            setTimeout(() => {
                _this.$loading.hide();//隐藏
            }, 2000)
            const flag=this.is_flag
            if(flag){
                
                //请求销量高
                console.log('请求销量高')
                this.is_flag=!this.is_flag
            }else{
                _this.$loading.show();//显示
                setTimeout(() => {
                    _this.$loading.hide();//隐藏
                }, 2000)
                //请求销量低
                console.log('请求销量低')
                this.is_flag=!this.is_flag
            }
        },
        // 筛选
        salesVolume4:function(){
            const _this = this;
            this.is_show1=false
            this.is_show2=false
            this.is_show3=false
            this.is_show4=true
           _this.$loading.show();//显示
            setTimeout(() => {
                _this.$loading.hide();//隐藏
            }, 2000)
        }
    },
    components: {
        XInput, 
        Group, 
        XButton, 
        Cell, 
        Toast, 
        base64
    }
}
</script>

<style scoped lang="less">
.goodlist{
    color: #333333;
    .nav{
        margin: 0 auto;padding: 0;width: 100%;border-bottom: 1px solid #eeeeee;
        li{display: inline-block;width: 23%;line-height: 2.5rem;text-align: center;font-size: 0.8rem;color: #999999}
        .select{color: #F54321;font-weight: 600;}
        .last{position: relative;}
        .last:after{position: absolute;content: '';display: inline-block;width: 1px;height: 40%;top: 0.8rem;left: 0;background: #eeeeee;}
    }
    .goods{
        margin: 0;padding: 0 1%;
        li{width: 47%;border-bottom: 1px solid #eeeeee;display: inline-block;padding: 1.5rem 0.2rem 1rem 0.2rem;text-align: center;
            img{width: 60%;}
            p{font-size: 0.8rem;text-align:left;margin-top:0.5rem;img{float: right;width: 1rem;}span{color: #F54321}}
        }
        li:nth-child(2n){border-left: 1px solid #eeeeee;}
    }
}
</style>
