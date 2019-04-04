<template>
  <header>
    <div class="result">
      検索結果：<span class="count">{{count}}件</span>
    </div>
    <div class="condition">
      <div class="target">
        <label>
          <input type="checkbox"
            v-bind:checked="showSaleItem"
            v-on:change="$emit('showSaleItemChanged')"
          >セール対象 <code>{{showSaleItem}}</code></label>
        <label>
          <input type="checkbox"
            v-bind:checked="showDelvFree"
            v-on:change="$emit('showDelvFreeChanged')"
          >送料無料 <code>{{showDelvFree}}</code></label>
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
  name: 'productsHeader',
  props: ['count','showSaleItem','showDelvFree','sortOrder']
}
</script>

<style lang="scss" scoped>
</style>
