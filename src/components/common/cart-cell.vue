<template>
    <div class="cartCell">
        <div class="cell" v-for="(product, index) in products" :key="index">

            <div class="icon left" @click="delProduct(product)">
                <img src="../../assets/icons/good-sel.png" alt="">
            </div>
            <div class="content left">
                <img v-bind:src="product.product.image" alt="">
                <p class="title">{{product.product.name}}</p>
                <p class="price red">￥{{product.product.price}}</p>
            </div>
            <div class="num left">
                <ul>
                    <li @click="reduce(product)">-</li>
                    <li class="priceNum">{{product.quantity}}</li>
                    <li @click="add(product)">+</li>
                </ul>
            </div>

        </div>

        <div v-if="exist" class="CartCount">
            <div class="icon">
                <span class="right red">￥{{total}}</span>
            </div>
            <div class="content lh44"></div>
            <div class="num">
                <mt-button type="primary">结算</mt-button>
            </div>
        </div>

        <div v-if="!exist" class="empty">
            <img src="../../assets/icons/shopping-sel.png" alt="">
            <p>购物车空空如也，赶紧逛逛吧</p>
        </div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {
    computed: {
        ...mapGetters({
            products: 'cartProducts',
            total: 'cartTotalPrice' 
        }),
        exist: function() {
            return this.products.length > 0
        }
    },
    methods: {
        ...mapActions([
            'add', 'reduce', 'delProduct'
        ])
    }
}

</script>

<style scoped>
.cartCell {
    width: 100%;
    height: 100%;
    padding: 2%;
}
.cell {
    width: 100%;
    height: 80px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-basis: auto;
    margin-top: 10px;
}
ul {
    margin: 0;
    padding: 0;
    list-style: none;
    position: absolute;
    bottom: 0;
}
li {
    float: left;
    outline: 1px solid #888;
    padding: 6px;
    -webkit-tap-highlight-color: rgba(0,0,0,0);  
    -webkit-tap-highlight-color: transparent; 
    max-width: 21px;
    overflow: hidden;
}
.priceNum {
    width: 21px;
}
.icon {
    width: 8%;
}
img {
    width: 100%;
    height: 100%;
}
.content {
    width: 65%;
    height: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
.content > p {
    font-size: 14px;
    text-align: left;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
.content > img {
    width: 38%;
    height: 100%;
    float: left;
}
.num {
    width: 27%;
    height: 100%;
    position: relative;
}
.left {
    float: left;
}
.title {
    
}
.CartCount {
    position: fixed;
    margin-left: -15px;
    bottom: 52px;
    width: 100%;
    height: 44px;
    border-top: 1px solid #999;
    display: flex;
    padding-left: 20px;
    flex-direction: row;
    align-items: center;
}
.lh44 {
    line-height: 44px;
    padding: 10px;
}
.red {
    color: #fe4544;
    font-size: 22px;
}
.empty img {
    width: 20%;
    margin-top: 100px;
    filter: grayscale(100%);
    filter: gray;
}
.empty p {
    color: #888888;
}
</style>