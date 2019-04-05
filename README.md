# 【学習メモ】Vue.js のツボとコツがゼッタイにわかる本 その3

Vue.js のツボとコツがゼッタイにわかる本 の学習メモ続きです。

第3章全体で作成した商品一覧、6-2. でコンポーネント化をして、6-5. で単一ファイルコンポーネント（SFC）での構築説明があったので、それに倣ってデータの中身を変えて作ってみました。

GitHub Pages：https://yuheijotaki.github.io/book-points_and_tips_of_vuejs/  
リポジトリ：https://github.com/yuheijotaki/book-points_and_tips_of_vuejs/



## 第6章 Vue.js のコンポーネントをモジュール化してみよう！

### 6-5 商品一覧を単一ファイルコンポーネントで再構築する

**ファイル構成**

```
/src/
└ App.vue
└ main.js
└ /components/
  └ product-list.vue
  └ product-header.vue
  └ product.vue
  └ filter.js
└ /assets/
  └ /product/
    └ 01.jpg
    └ ...
```

**各機能**

| コンポーネント                   | データ     | 定義場所           | 備考                                               |
| -------------------------------- | ---------- | ------------------ | -------------------------------------------------- |
| ルート（`App.vue`）              | 商品データ | `data` オプション  | 実際のアプリケーションでは外部から受け取る         |
| 商品一覧（`products-list.vue`）  | 商品データ | `props` オプション | 親コンポーネント（`App.vue`）から受け取る          |
| 商品一覧（`products-list.vue`）  | 検索条件   | `data` オプション  | 子コンポーネント（`product.header.vue`）に渡す     |
| ヘッダー（`product-header.vue`） | 検索条件   | `props` オプション | 親コンポーネント（`product-list.vue`）から受け取る |
| ヘッダー（`product-header.vue`） | 表示件数   | `props` オプション | 親コンポーネント（`product-list.vue`）から受け取る |
| 商品（`products.vue`）           | 商品データ | `props` オプション | 親コンポーネント（`product-list.vue`）から受け取る |

#### `App.vue`

ルートのファイルにあたる。このファイルに商品のデータをもたす。（本運用の場合はJSON取得）

```html
<template>
  <div id="app">
    <product-list v-bind:products="products"></product-list>
  </div>
</template>

<script>
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
	       	...
```

#### `product-list.vue`

ヘッダーと商品リストを含めたラッパー的なコンポーネント。絞り込み後の商品リストを表示する算出プロパティなどを置く。

```html
<template>
  <div class="wrapper">
    <product-header
      v-bind:count="filteredList.length"
      v-bind:showSaleItem="showSaleItem"
      v-bind:showDelvFree="showDelvFree"
      v-bind:sortOrder="sortOrder"
      v-on:showSaleItemChanged="showSaleItem=!showSaleItem"
      v-on:showDelvFreeChanged="showDelvFree=!showDelvFree"
      v-on:sortOrderChanged="sortOrderChanged">
    </product-header>
    <div class="list">
      <product
        v-for="product in filteredList"
        v-bind:product="product"
        v-bind:key="product.id">
      </product>
    </div>
  </div>
</template>

<script>
  ...
```

#### `product-header.vue`

ヘッダーのコンポーネント。  
`['count','showSaleItem','showDelvFree','sortOrder']` の各データは `props` で `product-list.vue` へ受け渡す。

```html
<template>
  <header>
    <div class="result">
      検索結果：<span class="count">{{count}}</span> 件
    </div>
    <div class="condition">
      <div class="target">
        <label>
          <input type="checkbox"
            v-bind:checked="showSaleItem"
            v-on:change="$emit('showSaleItemChanged')"
          > セール対象 <code>{{showSaleItem}}</code></label>
        <label>
          <input type="checkbox"
            v-bind:checked="showDelvFree"
            v-on:change="$emit('showDelvFreeChanged')"
          > 送料無料 <code>{{showDelvFree}}</code></label>
      </div>
      <div class="sort">
        <label for="sort">並び替え <code>{{sortOrder}}</code></label>
        <select id="sort"
          v-bind:value="sortOrder"
          v-on:change="$emit('sortOrderChanged',parseInt($event.target.value))"
        >
          <option value="1">標準</option>
          <option value="2">価格が安い順</option>
        </select>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'productHeader',
  props: ['count','showSaleItem','showDelvFree','sortOrder']
}
</script>

...
```

#### `product.vue`

商品一覧の各アイテムひとつひとつのコンポーネント。`product-list.vue` から受け取った `product` を使って商品情報を描画する。

```html
<template>
  <div class="item">
    <ul class="icon">
      <template v-if="product.isSale">
        <li class="sale"><span>SALE</span></li>
      </template>
      <template v-if="product.delv == 0">
        <li class="delv"><span>送料無料</span></li>
      </template>
      <template v-else>
        <li class="delv"><span>送料 ¥{{product.delv | number_format}}</span></li>
      </template>
    </ul>
    <figure>
      <img v-bind:src="product.image">
    </figure>
    <div class="meta">
      <h2 v-html="product.name"></h2>
      <h3>¥{{product.price | number_format}}</h3>
    </div>
  </div>
</template>

<script>
import './filter.js';

export default {
  name: 'product',
  props: ['product']
}
</script>

...
```



## まとめ

本のはじめから Vue CLI を使って組んでいましたが、コンポーネントに分けずに1ファイルでしてしまったので、実際に分けている説明みるとなるほどなぁと思いました。  
さっぱりに近かったコンポーネント間の受け渡しについても少し分かったので、これを応用すれば、前回のポートフォリオのもコンポーネントに分けてできるような気がします。

Vue.js に関しては本の内容の難易度が簡単になっていってしまっていますが、また体系的にやれたのでもう一度自分で作ってみるモチベーションが湧いた（少し）ので、その点が良かったかなと思います。