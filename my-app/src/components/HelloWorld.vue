<template>
  <div>
    <table border="1">
      <tr>
        <th>商品コード</th>
        <th>商品名</th>
      </tr>
      <tr v-for="item in products" v-bind:key="item.code">
        <td>{{item.code}}</td>
        <td>{{item.name}}</td>
      </tr>
    </table>
    <p>ウィンドウの横幅：{{width}}</p>
    <p>ウィンドウの高さ：{{height}}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      products: [
        {
          code: 'A01',
          name: 'プロダクトA',
        },
        {
          code: 'B01',
          name: 'プロダクトB',
        },
        {
          code: 'C01',
          name: 'プロダクトC',
        }
      ],
      width: window.innerWidth,
      height: window.innerHeight
    }
  },
  created: function() {
    // イベントハンドラを登録
    addEventListener('resize', this.resizeHandler);
  },
  beforeDestroy: function() {
    // イベントハンドラを削除
    removeEventListener('resize', this.resizeHandler);
  },
  methods: {
    // イベントハンドラ
    resizeHandler: function($event) {
      // 現在のウィンドウサイズでプロパティを更新
      this.width = $event.target.innerWidth;
      this.height = $event.target.innerHeight;
    }
  },
}
</script>

<style scoped>
</style>
