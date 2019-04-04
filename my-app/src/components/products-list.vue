<template>
  <div>
    <product-header></product-header>
    <div class="list">
      <product></product>
    </div>
  </div>
</template>

<script>
import productsHeader from './products-header.vue';
import products from './products.vue';

export default {
  name: 'productsList',
  components: {
    'product-header': productsHeader,
    'product': products
  }
}
</script>

<style lang="scss" scoped>
</style>
