<template>
  <productsList v-bind:products="products"></productsList>
</template>

<script>
import productsList from './products-list.vue';

export default {
  name: 'main',
  components: {
    productsList
  },
  data () {
    return {
      // 商品リスト
      products: [
        {
          id: '01',
          name: 'Michael<br>スマホケース',
          price: 1580,
          image: require("../assets/logo.png"),
          delv: 0,
          isSale: true
        },
        {
          id: '02',
          name: 'Raphael<br>スマホケース',
          price: 2480,
          image: require("../assets/logo.png"),
          delv: 0,
          isSale: false
        },
        {
          id: '03',
          name: 'Gabriel<br>スマホケース',
          price: 1680,
          image: require("../assets/logo.png"),
          delv: 0,
          isSale: true
        },
        {
          id: '04',
          name: 'Uriel<br>スマホケース',
          price: 980,
          image: require("../assets/logo.png"),
          delv: 240,
          isSale: false
        },
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
