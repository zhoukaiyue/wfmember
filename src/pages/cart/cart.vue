<template>
  <div class="cart">
  <!-- 顶部数据 -->
    <div>
        <ul  class="middle">
            <li>
                <div class="goods">
                    <h5>
                        <input class="cirucle" />&ensp;来自<span>西北店</span>的营销商品 <span class="right">优惠券&ensp;<img src="~@/assets/icon/left.png"></span>
                    </h5>
                    <table>
                        <tr>
                            <td class="img">
                                <!-- <input type="checkbox" :value="item.id" v-model="checked" @click="currClick(item,$index)" :id='item.id'>
                                <label :for="item.id" class="cb-label"></label> -->
                                <input class="cirucle" />
                                <img src="~@/assets/img/category-goods.png">
                            </td>
                            <td class="sm_goods">
                                <h5>mac/魅可子弹头口红经典限量唇</h5>
                                <p>已选择：限量版、砖红色</p>
                                <p class="num">￥128.00 <span class="price">券后价</span><span class="reduce" @click="reduce">-</span><input placeholder="0" value="0" /><span class="add" @click="add">+</span><span class="right"><img src="~@/assets/icon/goodsdown.png"></span></p>
                            </td>
                        </tr>
                        <tr>
                            <td class="img">
                                <!-- <input type="checkbox" :value="item.id" v-model="checked" @click="currClick(item,$index)" :id='item.id'>
                                <label :for="item.id" class="cb-label"></label> -->
                                <input class="cirucle" />
                                <img src="~@/assets/img/category-goods.png">
                            </td>
                            <td class="sm_goods">
                                <h5>mac/魅可子弹头口红经典限量唇</h5>
                                <p>已选择：限量版、砖红色</p>
                                <p class="num">￥128.00 <span class="price">券后价</span><span class="reduce" @click="reduce">-</span><input placeholder="0" value="0" /><span class="add" @click="add">+</span><span class="right"><img src="~@/assets/icon/goodsdown.png"></span></p>
                            </td>
                        </tr>
                    </table>
                </div>
            </li>
            <li>
                <div class="goods">
                    <h5>
                        <input class="cirucle" />&ensp;来自<span>西北店</span>的营销商品 <span class="right">优惠券&ensp;<img src="~@/assets/icon/left.png"></span>
                    </h5>
                    <table>
                        <tr>
                            <td class="img">
                                <input class="cirucle" />
                                <img src="~@/assets/img/category-goods.png">
                            </td>
                            <td class="sm_goods">
                                <h5>mac/魅可子弹头口红经典限量唇</h5>
                                <p>已选择：限量版、砖红色</p>
                                <p class="num">￥128.00 <span class="price">券后价</span><span class="reduce" @click="reduce">-</span><input placeholder="0" value="0" /><span class="add" @click="add">+</span><span class="right"><img src="~@/assets/icon/goodsdown.png"></span></p>
                            </td>
                        </tr>
                        <tr>
                            <td class="img">
                                <input class="cirucle" />
                                <img src="~@/assets/img/category-goods.png">
                            </td>
                            <td class="sm_goods">
                                <h5>mac/魅可子弹头口红经典限量唇</h5>
                                <p>已选择：限量版、砖红色</p>
                                <p class="num">￥128.00 <span class="price">券后价</span><span class="reduce" @click="reduce">-</span><input placeholder="0" value="0" /><span class="add" @click="add">+</span><span class="right"><img src="~@/assets/icon/goodsdown.png"></span></p>
                            </td>
                        </tr>
                    </table>
                </div>
            </li>
        </ul>
    </div>
    <div class="bottom">
        <p><img src="~@/assets/icon/store.png">&ensp;成为 <b>店加圈会员</b> 本单可省<span>45.00元</span> <span class="right"> 立即省钱&ensp;<img src="~@/assets/icon/goods-left.png"></span></p>
        <span class="cirucle"></span>
        <div>
            <span class="select"><input class="cirucle" />&ensp;全选</span>
            <p class="right">
                <span>
                    总计：￥998.00
                    <b>免邮</b>
                </span>
                <span @click="toorder" class="button">去结算(3)</span>
            </p>
        </div>
    </div>
  </div>
</template>

<script>
import { XInput, Group, XButton, Cell, Toast, base64 } from 'vux'
import Vue from 'vue'
import $ from 'jquery'
import axios from 'axios'
import * as myPub from '@/assets/js/public.js'
import * as openId from '@/assets/js/opid_public.js'
export default {
    name: 'category',
    data(){
    　　　　return {
        show:true,
            checked:[],
            totalPrice:[],
            lists :[],
            shop:''
    　　　　　}
    　　　},
    computed: {
      totalMoney:function(item,index){
              let sum = 0;
              for(let i=0;i<this.totalPrice.length;i++){
                  sum += this.totalPrice[i];
              };
              return sum;
          },
          checkAll: {
              get: function() {
                  return this.checkedCount == this.lists.length;
              },
              set: function(value){
                  var _this = this;
                  if (value) {
                      this.totalPrice = [];
                      this.checked = this.lists.map(function(item) {
                          item.checked = true;
                          let total = item.id;
                          _this.totalPrice.push(total);
                          return item.id
                      })
                  }else{
                      this.checked = [];
                      this.totalPrice=[];
                      this.lists.forEach(function(item,index){
                          item.checked = false;
                      });
                  }
              }
          },
          checkedCount: {
              get: function() {
                  console.log(this.totalPrice)
                  return this.checked.length;
              }
          }
        },
        mounted() {
        },
        deactivated () {
            this.$destroy()
        },
        methods: {
            toorder(){
                this.$router.push({ path: '/page/order'})
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
            // 多选框判断
            currClick:function(item,index){
                var _this = this;
                if(typeof item.checked == 'undefined'){
                    this.$set(item,'checked',true);
                        let total = item.id;
                        this.totalPrice.push(total);
                        console.log(this.totalPrice);
                }else{
                    item.checked = !item.checked;
                    if(item.checked){
                        this.totalPrice = [];
                        this.lists.forEach(function(item,index){
                            if(item.checked){
                                let total = item.id;
                                _this.totalPrice.push(total);
                            }
                        });
                    }else{
                        this.totalPrice = [];
                        this.lists.forEach(function(item,index){
                            if(item.checked){
                                let total = item.id;
                                v.push(total);
                            }
                        });
                    }
                }
            }
        }
    }
</script>

<style scoped lang="less">
/*顶部背景 样式*/
.cart{
    background: #f7f7f7;
    .middle{
        margin: 0 auto;
        padding: 0;
        li{
            background: #ffffff;
            margin-top: 15px;
            color: #333333;
            list-style: none;
            .goods{
                h5{
                    padding:0.3rem 5px;
                    line-height: 40px;font-weight: normal;font-size: 0.9rem;
                    .cirucle{width: 1.1rem;height:1.1rem;border-radius: 50%;background: #ffffff;border: 1px solid #dddddd;margin-left: 5px;}
                    span{color: #F54321}
                    .right{
                        float: right;
                        margin-right: 5px;
                        img{width: 0.6rem;position: relative;top: 0.2rem;}
                    }
                }
                table{
                    width: 100%;
                    td{border-top: 1px solid #eeeeee;padding: 0.5rem 0;}
                    .img{
                        width: 35%;
                        .cirucle{width:1.1rem;height:1.1rem;border-radius: 50%;background: #ffffff;border: 1px solid #dddddd;position: relative;top: -2rem;margin-left: 5px;}
                        img{width: 60%;border: 1px solid #eeeeee;margin-left: 0.5rem;}
                    }
                    .sm_goods{
                        h5{width: 90%;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;padding: 0;line-height: 30px;border: 0;}
                        p{color: #999999;font-size: 0.7rem;}
                        .num{
                            color: #F54321;
                            font-size: 0.9rem;
                            margin-top:5px;
                            span{display: inline-block;width: 1rem;height: 30px;line-height: 30px;text-align: center;border: 1px solid #eeeeee;color: #999999;}
                            .price{width: 2.5rem;height: 1rem;line-height: 1rem;border: 1px solid #F54321;color: #F54321;font-size: 0.7rem;}
                            input{width: 2rem;border: 1px solid #eeeeee;height: 25px;position: relative;text-align: center;line-height: 26px;position: relative;top: -1px;}
                            .reduce{width: 1rem;padding: 0;display: inline-block;height: 25px;text-align: center;line-height: 25px;margin-right: 0;margin-left: 10px;}
                            .add{width:1rem;padding: 0;display: inline-block;height: 25px;text-align: center;line-height: 25px;}
                            .right{position: relative;right: 5px;float: right;border:0;img{width: 1rem;}}
                        }
                    }
                }
            }
        }
    }
    .bottom{
        width: 100%;
        position: fixed;bottom: 0;
        p{
            line-height: 30px;background: #FFF2DD;font-size: 0.8rem;color: #333333;padding: 0.3rem 0.5rem;
            img{width: 1rem;position: relative;top: 0.2rem;}
            span{color: #F54321}
            .right{float: right;color: #4E4E55;img{width: 0.6rem;position: relative;top: 0.2rem;}}
        }
        div{
            height: 50px;
            line-height: 50px;
            .select{
                width: 20%;
                .cirucle{width: 1.1rem;height:1.1rem;border-radius: 50%;background: #ffffff;border: 1px solid #dddddd;margin-left: 5px;position: relative;top: -1px;}
            }
            .right{
                float: right;
                display: inline-block;
                background: #ffffff;
                padding: 0;
                width: 70%;
                text-align: right;
                line-height: 50px;
                span{
                    width:40%;display: inline-block;line-height: 17px;font-size: 0.8rem;
                    b{font-weight: normal;display: inline-block;position: relative;top: 5px;color: #999999;}
                }
                .button{display: inline-block;width:40%;height: 50px;background: #F54321;color: #ffffff;line-height: 50px;text-align: center;}
            }
        }
    }
}
/*兼容iphone5*/
@media screen and (max-width: 320px) {
   .cart{
    background: #f7f7f7;
    .middle{
        margin: 0 auto;
        padding: 0;
        background: #ffffff;
        li{
            color: #333333;
            list-style: none;
            .goods{
                table{
                    .img{
                        width: 48%;
                        img{width:60%;border: 1px solid #eeeeee;margin-left:0.1rem;}
                    }
                    .sm_goods{
                        .num{
                            color: #F54321;
                            font-size: 0.9rem;
                            margin-top:5px;
                            .price{width: 2.5rem;height: 1rem;line-height: 1rem;border: 1px solid #F54321;color: #F54321;font-size: 0.7rem;}
                            .right{position: relative;float: right;border:0;img{width: 0.8rem;}}
                        }
                    }
                }
            }
        }
    }
  }
}
/*多选框样式*/
input[type="checkbox"]{
  display:none;
}

.cb-label{
  position: relative;
  bottom: 0.1rem;
  height: 20px;
  width: 20px;
  border:0.2px ;
  border-radius: 50%;
  position: relative;
  display: inline-block;
  box-sizing: border-box;
  transition: border-color ease .4s/2;
  -moz-transition: border-color ease .4s/2;
  -o-transition: border-color ease .4s/2;
  -webkit-transition: border-color ease .4s/2;
    vertical-align: middle;
  cursor: pointer;
  margin-right:5px;
  border:1px solid #dddddd;
  background: #ffffff;
}
input[type=checkbox]:checked + .cb-label,
.cb-label.checked{

  background: rgb(101,141,181)g;
  border-color:rgb(101,141,181)g;
  &::after{
    content: "";
   display: inline-block;
   width: 19px;
   height: 19px;
    background: url(~@/assets/icon/circle@selected.png);
   top: -1px;
   left: 0;
   border-radius: 50%;
   background-size: 100%;
   position: absolute;
}


}
@-moz-keyframes dothabottomcheck{
  0% { height: 0; }
  100% { height: 20px *0.35; }
}

@-webkit-keyframes dothabottomcheck{
  0% { height: 0; }
  100% { height: 20px *0.35; }
}

@keyframes dothabottomcheck{
  0% { height: 0; }
  100% { height: 20px *0.35;  }
}

@keyframes dothatopcheck{
  0% { height: 0; }
  50% { height: 0; }
  100% { height: 20px * 0.7; }
}
@-webkit-keyframes dothatopcheck{
  0% { height: 0; }
  50% { height: 0; }
  100% { height: 20px * 0.7; }
}
@-moz-keyframes dothatopcheck{
  0% { height: 0; }
  50% { height: 0; }
  100% { height: 20px * 0.7; }
}
</style>
