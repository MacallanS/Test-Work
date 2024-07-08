<template>
  <div class="product-item">
    <div class="product-item__image-container">
      <p class="product-item__discount-text">
        Хит продаж
        <img
          :src="fireIcon"
          alt="Fire Icon"
          class="product-item__discount-icon"
        />
      </p>
      <img
        :src="require('@/assets/box.svg')"
        alt="Product Image"
        class="product-item__image"
      />
      <p class="product-item__discount-info">{{ product.discount }}%</p>
    </div>
    <div class="product-item__details">
      <p class="product-item__info">Бренд</p>
      <p class="product-item__name">{{ truncatedName }}</p>
      <div v-if="product.isAvailable" class="product-item__price-info">
        <p class="product-item__discounted-price">
          {{ formattedDiscountedPrice }}
        </p>
        <p v-if="product.discount > 0" class="product-item__original-price">
          {{ formattedOriginalPrice }}
        </p>
      </div>
      <div v-else class="product-item__notify">
        <p>Сообщить о поступлении</p>
      </div>
      <button
        class="product-item__buy-button"
        v-if="product.isAvailable && product.price !== null"
      >
        Купить
      </button>
    </div>
  </div>
</template>

<script>
import fireIcon from "@/assets/fire.svg";

export default {
  name: "ProductItem",
  props: {
    product: Object,
  },
  computed: {
    truncatedName() {
      const maxLength = 30;
      if (this.product.name.length > maxLength) {
        return this.product.name.slice(0, maxLength) + "...";
      }
      return this.product.name;
    },
    formattedOriginalPrice() {
      if (
        this.product.price === null ||
        this.product.discount === null ||
        this.product.discount === 0
      ) {
        return null;
      }
      const originalPrice = (
        this.product.price /
        (1 - this.product.discount / 100)
      ).toFixed(2);
      return `${originalPrice} ₽`;
    },
    formattedDiscountedPrice() {
      if (this.product.price === null) {
        return null;
      }
      return `${this.product.price.toFixed(2)} ₽`;
    },
  },
  data() {
    return {
      fireIcon,
    };
  },
};
</script>

<style lang="scss">
.product-item {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 10px;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  min-height: 370px;

  &:hover {
    transform: scale(1.02);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  &__info {
    color: #aaaaaa;
    font-size: 14px;
    margin-bottom: 10px;
  }

  &__image-container {
    position: relative;
    width: 100%;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #f8f8fa;
  }

  &__discount-text {
    display: flex;
    align-items: center;
    gap: 5px;
    position: absolute;
    top: 10px;
    left: 10px;
    background-color: white;
    padding: 5px;
    border-radius: 4px;
    font-size: 14px;
    z-index: 1;

    &-icon {
      margin-left: 5px;
      vertical-align: middle;
    }
  }

  &__image {
    width: 60px;
    height: 60px;
    object-fit: cover;
  }

  &__discount-info {
    position: absolute;
    bottom: 10px;
    left: 10px;
    background-color: #7397f5;
    padding: 7px;
    border-radius: 4px;
    font-size: 14px;
    z-index: 1;
  }

  &__details {
    padding: 10px;
  }

  &__name {
    font-size: 14px;
    overflow: hidden;
    text-overflow: ellipsis;
    margin-bottom: 16px;
  }

  &__price-info {
    display: flex;
    gap: 10px;
    margin-bottom: 16px;
  }

  &__original-price {
    text-decoration: line-through;
    color: #999;
  }

  &__discounted-price {
    font-size: 18px;
    color: #e74c3c;
  }

  &__notify {
    margin: 10px 0;
    font-size: 14px;
    color: #3498db;
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    padding: 10px;
    border-radius: 4px;
    text-align: center;
    position: absolute;
    bottom: 10px;
    left: 0;
    right: 0;
    z-index: 1;
    margin: 0 10px;
  }

  &__buy-button {
    padding: 10px 20px;
    background-color: white;
    color: #7397f5;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
    border: 1px solid #7397f5;

    &:hover {
      background-color: #7397f5;
      color: white;
    }
  }
}
</style>
