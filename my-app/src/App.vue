<template>
  <div id="app">
    <product-list v-bind:products="products"></product-list>
  </div>
</template>

<script>
import "normalize.css";
import productList from './components/product-list.vue';

export default {
  name: 'App',
  components: {
    'product-list': productList
  },
  data: function () {
    return {
      // 商品リスト
      products: [
        {
          id: '01',
          name: '紫いものビスケット',
          price: 1580,
          image: require("./assets/product/01.jpg"),
          delv: 0,
          isSale: true
        },
        {
          id: '02',
          name: '豆乳のビスケット',
          price: 2480,
          image: require("./assets/product/02.jpg"),
          delv: 0,
          isSale: false
        },
        {
          id: '03',
          name: 'かぼちゃのビスケット',
          price: 480,
          image: require("./assets/product/03.jpg"),
          delv: 200,
          isSale: false
        },
        {
          id: '04',
          name: 'カップケーキ',
          price: 1280,
          image: require("./assets/product/04.jpg"),
          delv: 0,
          isSale: true
        },
        {
          id: '05',
          name: 'トマトのカップケーキ',
          price: 2880,
          image: require("./assets/product/05.jpg"),
          delv: 0,
          isSale: false
        },
        {
          id: '06',
          name: 'プルーンのカップケーキ',
          price: 2280,
          image: require("./assets/product/06.jpg"),
          delv: 0,
          isSale: false
        },
        {
          id: '07',
          name: 'ミルクのビスケット',
          price: 2380,
          image: require("./assets/product/07.jpg"),
          delv: 0,
          isSale: false
        },
        {
          id: '08',
          name: '黒糖のビスケット',
          price: 1680,
          image: require("./assets/product/08.jpg"),
          delv: 0,
          isSale: true
        },
        {
          id: '09',
          name: 'コーンのラスク',
          price: 1480,
          image: require("./assets/product/09.jpg"),
          delv: 0,
          isSale: false
        },
        {
          id: '10',
          name: '黒糖のラスク',
          price: 1480,
          image: require("./assets/product/10.jpg"),
          delv: 0,
          isSale: false
        },
        {
          id: '11',
          name: 'みどりのラスク',
          price: 980,
          image: require("./assets/product/11.jpg"),
          delv: 200,
          isSale: true
        },
        {
          id: '12',
          name: 'きいろのラスク',
          price: 280,
          image: require("./assets/product/12.jpg"),
          delv: 200,
          isSale: false
        }
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
  color: #444;
  font-size: 12px;
  letter-spacing: .01em;
  line-height: 1.4;
}
</style>
