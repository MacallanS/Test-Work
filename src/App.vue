<template>
  <div id="app">
    <AppHeader />
    <ProductCatalog />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import ProductCatalog from './views/ProductCatalog.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    ProductCatalog
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: Arial;
  color: #333333;
  font-weight: 400;
  box-sizing: border-box;
}

ul {
  list-style: none;
}

a {
  text-decoration: none;
}
</style>
