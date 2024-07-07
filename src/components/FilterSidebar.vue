<template>
  <div class="filter-sidebar">
    <div class="filter-sidebar__categories">
      <p class="filter-sidebar__category-title">
        Все категории
        <span class="filter-sidebar__category-count">3</span>
      </p>
      <ul class="filter-sidebar__category-list">
        <li v-for="category in categories" :key="category.name" class="filter-sidebar__category-item">
          <p class="filter-sidebar__category-title">
            {{ category.name }}
            <span class="filter-sidebar__category-count">{{ category.count }}</span>
          </p>
        </li>
      </ul>
    </div>

    <div class="filter-sidebar__price">
      <p class="filter-sidebar__price-title">Цена</p>
      <div class="filter-sidebar__price-filters">
        <label for="minPrice" class="filter-sidebar__price-label">
          от
          <input
            id="minPrice"
            v-model.number="priceRange[0]"
            @input="updateFilter"
            placeholder="0"
            class="filter-sidebar__price-input"
          />
        </label>
        <span class="filter-sidebar__price-separator"></span>
        <label for="maxPrice" class="filter-sidebar__price-label">
          до
          <input
            id="maxPrice"
            v-model.number="priceRange[1]"
            @input="updateFilter"
            placeholder="10000"
            class="filter-sidebar__price-input"
          />
        </label>
      </div>
    </div>

    <div class="filter-sidebar__brand">
      <p class="filter-sidebar__brand-title">
        Бренд
        <span class="filter-sidebar__brand-clear" @click="clearBrands">Очистить</span>
      </p>
      <label for="brandSearch" class="filter-sidebar__brand-search">
        <img src="../assets/search-filter.svg" alt="Поиск" class="filter-sidebar__brand-search-icon">
        <input
          type="text"
          id="brandSearch"
          placeholder="Поиск по 100 000 товаров"
          class="filter-sidebar__brand-search-input"
        />
      </label>
      <ul class="filter-sidebar__brand-list">
        <li v-for="brand in brands" :key="brand.id" class="filter-sidebar__brand-item">
          <label class="filter-sidebar__brand-label">
            <input type="checkbox" class="filter-sidebar__brand-checkbox" :value="brand.id" v-model="selectedBrands">
            <p class="filter-sidebar__brand-name">
              {{ brand.name }}
              <span class="filter-sidebar__brand-count">{{ brand.count }}</span>
            </p>
          </label>
        </li>
      </ul>
    </div>

    <div class="filter-sidebar__size">
      <p class="filter-sidebar__size-title">Размер</p>
      <ul class="filter-sidebar__size-list">
        <li v-for="size in sizes" :key="size.id" class="filter-sidebar__size-item">
          <label class="filter-sidebar__size-label">
            <input type="checkbox" class="filter-sidebar__size-checkbox" :value="size.id" v-model="selectedSizes">
            <p class="filter-sidebar__size-name">
              {{ size.name }}
              <span class="filter-sidebar__size-count">{{ size.count }}</span>
            </p>
          </label>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "FilterSidebar",
  props: {
    filters: {
      type: Object,
      default: () => ({ priceRange: [0, 10000] })
    },
  },
  data() {
    return {
      categories: [
        { name: 'Категории', count: 1 },
        { name: 'Категории', count: 2 },
        { name: 'Категории', count: 3 }
      ],
      brands: [
        { id: 1, name: 'Бренд', count: 1 },
        { id: 2, name: 'Бренд', count: 2 },
        { id: 3, name: 'Бренд', count: 3 }
      ],
      sizes: [
        { id: 1, name: 'Размер S', count: 1 },
        { id: 2, name: 'Размер M', count: 2 },
        { id: 3, name: 'Размер L', count: 3 }
      ],
      selectedBrands: [],
      selectedSizes: []
    };
  },
  computed: {
    priceRange: {
      get() {
        return this.filters.priceRange || [0, 10000];
      },
      set(newRange) {
        this.$emit("filter", { priceRange: newRange });
      }
    }
  },
  methods: {
    updateFilter() {
      this.$emit("filter", { priceRange: this.priceRange });
    },
    clearBrands() {
      this.selectedBrands = [];
    }
  }
};
</script>

<style lang="scss">
.filter-sidebar {
  &__category {
    margin-bottom: 20px;
    margin: 10px;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);

    &-title {
      margin: 10px 10px 10px 5px;
      color: #333;
      display: flex;
      justify-content: space-between;
      font-size: 14px;
      font-weight: 115%;
    }

    &-list {
      padding: 0;
      margin: 0;
      display: flex;
      flex-direction: column;
    }

    &-item {
      padding-left: 24px;
      &:hover {
        background-color: #E2EFFF;
        border-radius: 5px;
      }
    }
    &-count {
      opacity: 0.5;
    }
  }

  &__price {
    padding: 15px;
    text-align: center;

    &-title {
      font-size: 16px;
      font-weight: bold;
      margin-bottom: 15px;
      color: #333;
      line-height: 125%;
    }

    &-filters {
      display: flex;
      position: relative;
      justify-content: space-between;
    }

    &-label {
      width: 45%;
      position: relative;
      display: flex;
      align-items: center;
      font-size: 12px;
      color: #555;
      border: 1px solid #ddd;
      border-radius: 4px;
      padding: 10px;
      color: #aaa;

      & > span {
        margin-right: 5px;
        width: 40px;
      }
    }

    &-input {
      border: none;
      font-size: 14px;
      margin-left: 5px;
      outline: none;
      background-color: transparent;
      max-width: 60px;

      &::placeholder {
        color: #aaa;
      }
      
      @media (max-width: 1920px) {
        max-width: 40px; 
      }
    }

    &-separator {
      width: 10px;
      background-color: #d5d5d5;
      height: 1px;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }

  &__brand {
    &-title {
      margin: 10px 10px 10px 5px;
      color: #333;
      display: flex;
      justify-content: space-between;
      font-size: 14px;
      font-weight: bold;
    }

    &-clear {
      color: #AAAAAA;
      font-size: 14px;
      text-decoration: underline;

      &:hover {
        cursor: pointer;
      }
    }

    &-search {
      display: flex;
      align-items: center;
      padding: 10px;
      margin-right: 20px;
      border: 1px solid #D5D5D5;
      border-radius: 10px; 
      background-color: #fff;
      width: 100%;
      margin-top: 20px;
  
      &-icon {
        margin-right: 8px; 
      }
  
      &-input {
        border: none; 
        outline: none; 
        padding: 5px;
        width: 100%; 
      }
    }

    &-list {
      padding: 0;
      margin: 0;
      display: flex;
      flex-direction: column;
    }

    &-item {
      margin-top: 10px;
      width: 100%;
    }

    &-label {
      display: flex;
      min-width: 100%;
    }

    &-name {
      display: flex;
      width: 100%;
      justify-content: space-between;
    }
    
    &-checkbox {
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      display: inline-block;
      width: 20px;
      height: 20px;
      margin-right: 10px;
      border-radius: 6px; 
      border: 2px solid #ddd; 
      background-color: #fff; 
      cursor: pointer;
      transition: border-color 0.3s, background-color 0.3s, box-shadow 0.3s;
    
      &:hover {
        border-color: #3785BC;
      }
    
      &:checked {
        background-color: #3785BC; 
        border-color: #3785BC; 
        background-image: url("../assets/active.svg");
        background-repeat: no-repeat;
        background-position: center;
      }
    
      &:focus {
        outline: none;
        box-shadow: 0 0 0 2px rgba(#3785BC, 0.25); 
      }
    
      &:disabled {
        background-color: #e9ecef; 
        border-color: #e9ecef; 
        cursor: not-allowed; 
      }
    }
  }

  &__size {
    margin-top: 25px;
    &-title {
      margin: 10px 10px 10px 5px;
      color: #333;
      display: flex;
      justify-content: space-between;
      font-size: 14px;
      font-weight: bold;
    }

    &-list {
      padding: 0;
      margin: 0;
      display: flex;
      flex-direction: column;
    }

    &-item {
      width: 100%;
      margin-top: 10px;
    }

    &-label {
      display: flex;
      min-width: 100%;
    }

    &-name {
      display: flex;
      width: 100%;
      justify-content: space-between;
    }

    &-checkbox {
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      display: inline-block;
      width: 20px;
      height: 20px;
      margin-right: 10px;
      border-radius: 6px;
      border: 2px solid #ddd; 
      background-color: #fff; 
      cursor: pointer;
      transition: border-color 0.3s, background-color 0.3s, box-shadow 0.3s;
    
      &:hover {
        border-color: #3785BC;
      }
    
      &:checked {
        background-color: #3785BC;
        border-color: #3785BC;
        background-image: url("../assets/active.svg");
        background-repeat: no-repeat;
        background-position: center;
      }
    
      &:focus {
        outline: none;
        box-shadow: 0 0 0 2px rgba(#3785BC, 0.25); 
      }
    
      &:disabled {
        background-color: #e9ecef; 
        border-color: #e9ecef; 
        cursor: not-allowed;
      }
    }
  }
}
</style>
