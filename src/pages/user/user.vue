<template>
    <div class="user">
        
    </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
    name: 'user',
    data() {
        return {}
    },
    computed: {
        ...mapGetters(['userInfo']),
        totalDetail() {
            return this.userInfo.addressInfo.cityVal + ' ' + this.userInfo.addressInfo.detail
        }
    },
    mounted() {},
    methods: {
        editAddress() {
            this.$router.push({ path: '/page/address' })
        }
    },
    filters: {
        formatMoney(value) {
            return '￥' + value
        }
    }
}
</script>

<style scoped lang="less">
.user {
}
</style>
