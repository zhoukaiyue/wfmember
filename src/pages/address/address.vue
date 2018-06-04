<template>
    <div class="address">
    <h5>地址信息</h5>
        <group>
            <x-input title="联系人"
                     placeholder="收货人姓名"
                     v-model="form.name"></x-input>
            <x-input title="手机号码"
                     placeholder="请输入联系电话"
                     v-model="form.mobile"></x-input>
            <x-address title="所在地区"
                       class="border"
                       v-model="form.cityArr"
                       :list="addressData"
                       placeholder="请选择地取"></x-address>
            <x-input title="详细地址"
                        :max="20"
                        name="detail"
                        v-model="form.detail"></x-input>
        </group>
        <div class="card">
            身份证信息（加密保存）
            <p>跨境保税商品必须提供收货人身份证信息用以办理相关手续。</p>
        </div>
        <group>
            <x-input title="身份证号"
                 placeholder="请填写收件人身份证信息"
                 v-model="form.card"></x-input>
             </group>
        <div style="margin-top: 30px;padding: 0 15px">
            <x-button @click.native="submitAddress">保存</x-button>
        </div>
        <div style="margin-top: 20px;padding: 0 15px;" class="del">
            <x-button>删除</x-button>
        </div>
    </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'
import {
    XTextarea,
    Group,
    XInput,
    XAddress,
    ChinaAddressV4Data,
    XButton,
    Value2nameFilter as value2name,
    Cell
} from 'vux'
export default {
    name: 'address',
    data() {
        return {
            form: {
                name: '',
                mobile: '',
                card:'',
                cityArr: [],
                detail: ''
            },
            addressData: ChinaAddressV4Data
        }
    },
    created() {
        if (this.userInfo.addressInfo) {
            this.form = {
                name: this.userInfo.addressInfo.name,
                mobile: this.userInfo.addressInfo.mobile,
                cityArr: this.userInfo.addressInfo.cityArr,
                detail: this.userInfo.addressInfo.detail
            }
        }
    },
    computed: {
        ...mapGetters(['userInfo'])
    },
    methods: {
        ...mapMutations(['UPDATE_ADDRESS']),
        submitAddress() {
            const { name, mobile, cityArr, detail } = this.form
            if (!name) {
                this.$vux.toast.text('请输入名字~', 'middle')
                return
            }
            if (!mobile) {
                this.$vux.toast.text('请输入手机号~', 'middle')
                return
            }
            if (!cityArr) {
                this.$vux.toast.text('请选择地区~', 'middle')
                return
            }
            if (!detail) {
                this.$vux.toast.text('请输入详情地址~', 'middle')
                return
            }
            let cityVal = value2name(cityArr, ChinaAddressV4Data)
            this.UPDATE_ADDRESS({
                name: name,
                mobile: mobile,
                cityArr: cityArr,
                cityVal: cityVal,
                detail: detail
            })
            this.$router.go(-1)
        }
    },
    components: {
        XTextarea,
        Group,
        XInput,
        XAddress,
        XButton,
        Cell
    }
}
</script>
<style type="text/css">
    .weui-cells{margin-top: 0!important;color: #333333;font-size: 0.9rem!important;line-height: 30px!important;}
    .weui-cells:after{display: none!important;}
    ::-webkit-input-placeholder{color: #999999;font-size: 0.8rem;line-height: 50px;text-align: right;}
    .vux-cell-placeholder{font-size: 0.8rem;}
    .weui-btn_default{background: #F54321!important;color: #ffffff!important;font-size: 0.9rem;}
    .del .weui-btn_default{background: #cccccc!important;}
</style>
<style scoped lang="less">
.address{
    background: #f7f7f7;
    h5{font-weight: normal;font-size: 0.9rem;line-height: 40px;padding: 0 15px;background: #f7f7f7;}
    .card{
        background: #f7f7f7;color: #777777;padding: 20px 15px;font-size: 0.8rem;line-height: 25px;
        p{color: #F54321;font-size: 0.75rem;}
    }
}
.border {
    position: relative;
    &::before {
        content: ' ';
        position: absolute;
        left: 0;
        top: 0;
        right: 0;
        height: 1px;
        border-top: 1px solid #d9d9d9;
        color: #d9d9d9;
        -webkit-transform-origin: 0 0;
        transform-origin: 0 0;
        -webkit-transform: scaleY(0.5);
        transform: scaleY(0.5);
        left: 15px;
    }
}
</style>
