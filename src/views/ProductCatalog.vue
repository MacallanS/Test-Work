<template>
  <div class="product-catalog">
    <div class="product-catalog__wrapper">
      <aside class="product-catalog__sidebar">
        <FilterSidebar :filters="filters" @filter="applyFilter" />
      </aside>
      <main class="product-catalog__content">
        <ProductList :products="filteredProducts" />
      </main>
    </div>
    <div class="product-catalog__mobil-wrapper">
      <h1 class="product-catalog__mobil-heading">Название категории</h1>
      <main class="product-catalog__mobil-content">
        <ProductList :products="filteredProducts" />
      </main>
    </div>
  </div>
</template>


<script>
import FilterSidebar from '../components/FilterSidebar.vue';
import ProductList from '../components/ProductList.vue';
import productsData from '../assets/products.json'; 

export default {
  name: 'ProductCatalog',
  components: {
    FilterSidebar,
    ProductList
  },
  data() {
    return {
      filters: {
        priceRange: [0, 10000]
      },
      products: [],
      filteredProducts: []
    };
  },
  methods: {
    applyFilter(filter) {
      this.filters = filter;
      this.filterProducts();
    },
    filterProducts() {
      this.filteredProducts = this.products.filter(product => {
        return (
          product.price >= this.filters.priceRange[0] &&
          product.price <= this.filters.priceRange[1]
        );
      });
    }
  },
  created() {
    this.products = productsData.map(product => ({
      ...product,
      price: product.isAvailable ? (product.price * (1 - 0.25)) : null 
    }));
    this.filterProducts();
  }
};
</script>

<style lang="scss">
.product-catalog {
  display: flex;
  justify-content: center;

  &__mobil-wrapper {
    display: none;
  }

  &__wrapper {
    display: flex;
    width: 1720px; 
    @media (max-width: 1920px) {
      width: calc(100% - 240px); 
    }
  }

  &__sidebar {
    width: 20%;
  }

  &__content {
    width: 70%;
    margin: 0px 30px;
  }
}

@media (max-width: 1300px) {
  .product-catalog {
    &__mobil-wrapper {
      display: block;
      width: 80vw;
      margin: 0 auto;
      padding: 10px;
    }

    &__wrapper {
      display: none;
    }

    &__mobil-content {
      display: flex;
      width: 100%;
      flex-direction: column;
    }

    &__mobil-heading {
      font-size: 20px;
    }
  }
}
</style>

