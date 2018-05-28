<template>
    <div class="category">
        <ul class="category-menu vux-1px-r">
            <li v-for="(item,index) in menu"
                :key="index"
                class="menu-item"
                :class="[currentIndex === index?'active':'']"
                @click="switchCategory(index,item.id)">
                <span>
                    {{item.name}}
                </span>
            </li>
        </ul>
        <div class="category-main">
            <div class="category-detail-box">
                <div class="category-list">
                    <div class="category-goods-items"
                         v-for="(item,index) in list"
                         @click="linktoDetail(item.id)"
                         :key="index">
                        <img :src="item.main_img_url"
                             alt=""
                             class="goods-image">
                        <div class="goods-name">{{item.name}}</div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'category',
    data() {
        return {
            menu: [],
            list: [],
            currentIndex: 0
        }
    },
    created() {
        this.getCategory()
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
        getCategory() {
            this.$http
                .get(
                    'https://www.easy-mock.com/mock/5a4896ba62de717d44f2406e/api/v1/category/all'
                )
                .then(res => {
                    this.menu = res.data.data.category
                    this.getProduct(this.menu[0].id)
                })
        },
        getProduct(id) {
            this.$http
                .get(
                    'https://www.easy-mock.com/mock/5a4896ba62de717d44f2406e/api/v1/product/by_category',
                {
                    params: {
                        id: id
                    }
                }
                )
                .then(res => {
                    this.list = res.data.data.list
                })
        }
    }
}
</script>

<style scoped lang="less">
.category {
    height: 100%;
    display: flex;
    overflow: hidden;
    .category-menu {
        width: 100px;
        flex: 0 0 100px;
        height: 100%;
        background: #f4f4f4;
        .menu-item {
            height: 25px;
            padding: 10px 0;
            font-size: 0.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            &.active {
                span{
                    color: #ffffff;
                    background: #F54321;
                    border-radius: 50px;
                    padding: 0.1rem 1rem;
                }
            }
        }
    }
    .category-main {
        flex: 1;
        height: 100%;
        transition: all 500ms ease-in-out;
        .category-detail-box {
            overflow-y: auto;
            padding: 20px;
            height: 100%;
            box-sizing: border-box;
            -webkit-overflow-scrolling: touch; 
            .category-top {
                .category-header {
                    img {
                        width: 100%;
                        vertical-align: top;
                        border-radius: 2px;
                    }
                }
                .category-title {
                    margin: 15px;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    .text {
                        font-size: 12px;
                        color: #ab956d;
                        font-weight: normal;
                        &::before,
                        &::after {
                            content: '';
                            display: inline-block;
                            position: relative;
                            top: -3px;
                            width: 35px;
                            height: 1px;
                            margin: 0 10px;
                            background-color: #979797;
                            transform: scaleY(0.5);
                        }
                    }
                }
            }
            .category-list {
                display: flex;
                flex-wrap: wrap;
                .category-goods-items {
                    width: 30%;
                    margin-right: 5%;
                    margin-bottom: 10px;
                    text-align: center;
                    &:nth-child(3n) {
                        margin-right: 0;
                    }
                    .goods-image {
                        width: 80%;
                        border-radius: 50%;
                    }
                    .goods-name {
                        color: #444452;
                        font-size: 12px;
                    }
                }
            }
        }
    }
}
</style>
