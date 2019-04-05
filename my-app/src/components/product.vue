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

<style lang="scss" scoped>
.item {
  width: 25%;
  padding: 50px 10px 20px;
  border: #ddd 1px solid;
  border-right: 0;
  box-sizing: border-box;
  position: relative;
  &:last-child,
  &:nth-child(4n) {
    border-right: #ddd 1px solid;
  }
  &:nth-child(n+5) {
    border-top: 0;
  }
  figure {
    text-align: center;
    img {
      max-width: 120px;
      height: auto;
      border-radius: 4px;
    }
  }
  .icon {
    position: absolute;
    top: 4px;
    left: 4px;
    display: flex;
    list-style: none;
    li {
      color: #fff;
      font-size: 11px;
      line-height: 1;
      font-weight: bold;
      border-radius: 2px;
      margin-right: 4px;
      &:last-child {
        margin-right: 0;
      }
      span {
        display: inline-block;
        padding: 5px 7px;
      }
      &.sale {
        background: rgb(240, 53, 53);
      }
      &.delv {
        background: #999;
      }
    }
  }
  .meta {
    margin-top: 4px;
    text-align: center;
    h2 {
      color: #666;
      font-size: 12px;
    }
    h3 {
      font-size: 16px;
    }
  }
}
</style>
