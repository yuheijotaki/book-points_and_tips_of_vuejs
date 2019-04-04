<template>
  <div class="item">
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
</template>

<script>
export default {
  name: 'products',
  props: ['product']
}
</script>

<style lang="scss" scoped>
</style>
