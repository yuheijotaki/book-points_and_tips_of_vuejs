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

<style lang="scss" scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  line-height: 1;
  code {
    background: #eee;
    color: #333;
    font-family: monospace;
    font-size: 12px;
    line-height: 1;
    padding: 3px 5px 2px;
    display: inline-block;
  }
}
.condition {
  display: flex;
  align-items: center;
}
.result {
  span {
    font-weight: bold;
  }
}
.target {
  margin-right: 20px;
  label {
    margin-right: 10px;
    &:last-child {
      margin-right: 0;
    }
  }
}
.sort {
  select {
    vertical-align: -1px;
  }
}
</style>
