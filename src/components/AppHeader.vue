<template>
  <header class="header">
    <div class="header__wrapper">
      <img src="../assets/logo.png" class="header__logo-img" alt="Логотип" />
      <p class="header__logo-text">Логотип</p>
      <button class="header__catalog-btn">Каталог</button>
      <nav class="header__nav">
        <label for="search" class="header__search">
          <img
            src="../assets/search.svg"
            alt="Поиск"
            class="header__search-icon"
          />
          <input
            type="text"
            id="search"
            placeholder="Поиск по 100 000 товаров"
            class="header__search-input"
          />
        </label>
        <a href="#" class="header__nav-link">Информация о компании</a>
        <a href="#" class="header__nav-link">Контакты</a>
        <a href="#" class="header__nav-link">Полезные ссылки</a>
      </nav>
    </div>
    <div class="header__mobile-wrapper">
      <div class="header__mobile-info">
        <p class="header__mobile-time">9:41</p>
        <img
          src="../assets/phone-2.svg"
          class="header__mobile-icon"
          alt="Телефон"
        />
      </div>
      <div class="header__mobile-search">
        <img
          src="../assets/arrow.svg"
          alt="стрелочка назад"
          class="header__mobile-search-arrow"
        />
        <div class="header__mobile-search-stripe">
          <label for="mobile-search-input" class="header__mobile-search-label">
            <input
              type="text"
              id="mobile-search-input"
              class="header__mobile-search-input"
              ref="mobileSearchInput"
              placeholder="Запрос"
            />
            <button class="header__mobile-search-clear-btn" @click="clearMobileSearch">
              <img
                src="../assets/clear.svg"
                alt="Очистить поиск"
                class="header__mobile-search-clear-icon"
              />
            </button>
          </label>
          <button class="header__mobile-search-submit-btn">Найти</button>
        </div>
      </div>
    </div>
  </header>
</template>


<script>
export default {
  name: "AppHeader",
  methods: {
    clearMobileSearch() {
      const input = this.$refs.mobileSearchInput;
      if (input) {
        input.value = "";
      }
    },
  },
};
</script>


<style lang="scss">
.header {
  display: flex;
  justify-content: center;
  margin-bottom: 12px;

  &__wrapper {
    width: 1720px;
    display: flex;
    align-items: center;
    margin: 12px 0;

    @media (max-width: 1920px) {
      width: calc(100% - 240px);
    }
  }

  &__logo-img {
    margin-left: 24px;
    margin-right: 5px;
  }

  &__logo-text {
    font-size: 16px;
    font-weight: bold;
    margin-right: 20px;
    line-height: 120%;
  }

  &__catalog-btn {
    margin-right: 20px;
    padding: 15.5px 25px;
    background-color: transparent;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    border: 1px solid #73aff4;
  }

  &__nav {
    display: flex;
    align-items: center;
    width: 100%;
  }

  &__search {
    display: flex;
    align-items: center;
    padding: 10px;
    margin-right: 20px;
    border: 1px solid #73aff4;
    border-radius: 10px;
    background-color: #fff;
    width: 60%;
    min-width: 225px;

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

  &__nav-link {
    margin-left: 20px;
    white-space: nowrap;

    &:hover {
      text-decoration: underline;
      color: #007bff;
    }
  }

  &__mobile-wrapper {
    display: none;
    width: 70vw;
    margin: 0 auto;
    padding: 10px;
  }

  &__mobile-info {
    display: flex;
    justify-content: space-between;
  }

  &__mobile-time {
    margin-right: 10px;
  }

  &__mobile-search {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 20px;
  }

  &__mobile-search-label {
    display: flex;
    align-items: center;
    margin-right: 10px;
    width: 80%;
  }

  &__mobile-search-input {
    border: none;
    padding: 5px;
    border-radius: 4px;
    width: 150px;
    width: 95%;
  }

  &__mobile-search-stripe {
    display: flex;
    border-bottom: 1px solid grey;
    width: 80%;
    justify-content: space-between;
    padding: 10px 0;
  }

  &__mobile-search-arrow {
    margin-right: 15px;
  }

  &__mobile-search-clear-btn {
    background: none;
    border: none;
    cursor: pointer;
    margin-left: 5px;
  }

  &__mobile-search-clear-icon {
    width: 20px;
    height: 20px;
  }

  &__mobile-search-submit-btn {
    padding: 5px 10px;
    background-color: #7397F5;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;

    &:hover {
      background-color: #4467bf;
    }
  }
}
@media (max-width: 1300px) {
  .header {
    &__mobile-wrapper {
      display: block;
    }

    &__wrapper {
      display: none;
    }
  }
}
</style>
