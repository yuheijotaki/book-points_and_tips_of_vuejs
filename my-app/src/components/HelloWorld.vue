<template>
  <div class="list">
    <div class="item" v-for="product in products" v-bind:key="product.id">
      <figure>
        <template v-if="product.isSale">
          <p>SALE</p>
        </template>
        <img v-bind:src="product.image">
        <figcaption>{{product.name}}</figcaption>
      </figure>
      <p>{{product.price | number_format}}円</p>
      <template v-if="product.delv == 0">
        <p>送料無料</p>
      </template>
      <template v-else>
        <p>+送料 {{product.delv | number_format}}円</p>
      </template>
    </div>
  </div>
</template>

<script>
// 商品一覧コンポーネント
export default {
  name: 'HelloWorld',
  data () {
    return {
      // 表示中の商品数
      count: 0,
      // 「セール対象」のチェック状態（true:チェックあり、false:チェックなし）
      showSaleItem: false,
      // 「送料無料」のチェック状態（true:チェックあり、false:チェックなし）
      showDelvFree: false,
      // 「並び替え」の選択値（1:標準、2:価格が安い順）
      sortOrder: 1,
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
          price: 1480,
          image: require("../assets/logo.png"),
          delv: 0,
          isSale: true
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
  },
  filters: {
    // 数値を通貨書式「#,###,###」に変換するフィルター
    number_format: function (val) {
      return val.toLocaleString();
    }
  }
}
</script>

<style scoped>
*,html {
  margin: 0;
  padding: 0;
}
body {
  margin: 0;
  padding: 0;
}
.list {
  display: flex;
  text-align: center;
}
.item {
  max-width: 200px;
  border: #000 1px solid;
}
img {
  max-width: 100px;
  height: auto;
}
</style>
