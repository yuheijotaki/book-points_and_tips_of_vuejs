<template>
  <div id="app">
    <router-view/>
    <productsList v-bind:products="products"></productsList>
  </div>
</template>

<script>
import "normalize.css";
import productsList from './components/products-list.vue';

export default {
  name: 'App',
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
          image: require("./assets/logo.png"),
          delv: 0,
          isSale: true
        },
        {
          id: '02',
          name: 'Raphael<br>スマホケース',
          price: 2480,
          image: require("./assets/logo.png"),
          delv: 0,
          isSale: false
        },
        {
          id: '03',
          name: 'Gabriel<br>スマホケース',
          price: 1680,
          image: require("./assets/logo.png"),
          delv: 0,
          isSale: true
        },
        {
          id: '04',
          name: 'Uriel<br>スマホケース',
          price: 980,
          image: require("./assets/logo.png"),
          delv: 240,
          isSale: false
        },
      ]
    }
  }

}
</script>

<style lang="scss">
html,* {
  margin: 0;
  padding: 0;
}
h1,h2,h3,h4,h5,h6 {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Helvetica Neue, Helvetica, Arial, 'Hiragino Kaku Gothic ProN', Meiryo, sans-serif;
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
  font-feature-settings : "palt";
  max-width: 800px;
  margin: 40px auto;
  padding: 0 20px;
  letter-spacing: .01em;
}
</style>
