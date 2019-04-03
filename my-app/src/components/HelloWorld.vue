<template>
  <div>
    <header>
      <div class="result">
        検索結果：<span class="count">{{count}}件</span>
      </div>
      <div class="condition">
        <div class="target">
          <label><input type="checkbox" v-model="showSaleItem">セール対象 <code>{{showSaleItem}}</code></label>
          <label><input type="checkbox" v-model="showDelvFree">送料無料 <code>{{showDelvFree}}</code></label>
        </div>
        <div class="sort">
          <label for="sort">並び替え <code>{{sortOrder}}</code></label>
          <select id="sort" v-model.number="sortOrder">
            <option value="1">標準</option>
            <option value="2">価格が安い順</option>
          </select>
        </div>
      </div>
    </header>
    <div class="list">
      <div class="item" v-for="product in filteredList" v-bind:key="product.id">
        <figure>
          <img v-bind:src="product.image">
          <figcaption v-html="product.name"></figcaption>
        </figure>
        <p>{{product.price | number_format}}円</p>
        <template v-if="product.isSale">
          <p>SALE</p>
        </template>
        <template v-if="product.delv == 0">
          <p>送料無料</p>
        </template>
        <template v-else>
          <p>+送料 {{product.delv | number_format}}円</p>
        </template>
      </div>
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
      // count: 0,
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
  },
  computed: {
    // 絞り込み後の商品リストを返す算出プロパティ
    filteredList: function () {
      // 絞り込み後の商品リストを格納する新しい配列
      var newList = [];
      for (var i=0; i<this.products.length; i++) {
        // 表示対象かどうかを判定するフラグ
        var isShow = true;
        // i番目の商品が表示対象かどうかを判定する
        if (this.showSaleItem && !this.products[i].isSale) {
          // 「セール対象」チェックありで、セール対象商品ではない場合
          isShow = false; // この商品は表示しない
        }
        if (this.showDelvFree && this.products[i].delv > 0) {
          //「送料無料」チェック有りで、送料有りの商品の場合
          isShow = false; // この商品は表示しない
        }
        if (isShow) {
          newList.push(this.products[i]);
        }
      }
      // 新しい配列を並び替える
      if (this.sortOrder == 1) {
        // 元の順番にpushしているので並び替え済み
      } else if (this.sortOrder == 2) {
        // 価格が安い順に並び替える
        newList.sort(function (a,b) {
          return a.price - b.price;
        });
      }
      // 絞り込み後の商品リストを返す
      return newList;
    },
    count: function () {
      return this.filteredList.length;
    }
  },
  watch: {
    //「セール対象」チェックボックスの状態を監視するウォッチャ
    showSaleItem: function (newVal, oldVal) {
      // ここで products の配列を書き換える
      console.log('showSaleItem ウォッチャが呼び出されました。');
    },
    //「送料無料」チェックボックスの状態を監視するウォッチャ
    showDelvFree: function (newVal, oldVal) {
      // ここで products の配列を書き換える
      console.log('showDelvFree ウォッチャが呼び出されました。');
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
header {
  display: flex;
}
.condition {
  display: flex;
}
code {
  background: #ccc;
}
.list {
  display: flex;
  text-align: center;
  list-style: none;
}
.item {
  width: 25%;
  padding: 20px;
  border: #000 1px solid;
  font-size: 14px;
  line-height: 1.2;
}
.item p {
  margin-bottom: 10px;
}
.item p:last-child {
  margin-bottom: 0;
}
img {
  max-width: 60px;
  height: auto;
}
</style>
