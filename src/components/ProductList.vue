<template>
  <div class="product-list">
    <ProductItem 
      v-for="product in products" 
      :key="product.id" 
      :product="product" 
    />
  </div>
</template>

<script>
import ProductItem from './ProductItem.vue';

export default {
  name: 'ProductList',
  components: {
    ProductItem
  },
  props: {
    products: Array
  }
};
</script>

<style>
.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); 
  gap: 15px; 
}
</style>
