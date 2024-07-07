<template>
  <header class="header">
    <div class="header__wrapper">
      <img src="../assets/logo.png" class="header__img-logo">
      <p class="header__logo">Логотип</p>
      <button class="header__catalog-btn">Каталог</button>
      <nav class="header__nav">
        <label for="search" class="header__search">
          <img src="../assets/search.svg" alt="Поиск" class="header__search-icon">
          <input type="text" id="search" placeholder="Поиск по 100 000 товаров" class="header__search-input">
        </label>

        <a href="#" class="header__link">Информация о компании</a>
        <a href="#" class="header__link">Контакты</a>
        <a href="#" class="header__link">Полезные ссылки</a>
      </nav>
    </div>
    <div class="header__mobil-wrapper">
      <p class="header__mobil-text">9:41</p>
      <img src="../assets/phone-2.svg" class="header__mobil-img">
    </div>
  </header>
</template>


<script>
export default {
  name: 'AppHeader'
};
</script>

<style lang="scss">
.header {
  display: flex;
  justify-content: center;
  margin-bottom: 12px;

  &__mobil-wrapper {
    display: none;
  }

  &__wrapper {
    width: 1720px;
    display: flex;
    align-items: center;
    margin: 12px 0px;
    @media (max-width: 1920px) {
      width: calc(100% - 240px); 
    }
  }

  &__img-logo {
    margin-left: 24px;
    margin-right: 5px;
  }

  &__logo {
    font-size: 16px;
    font-weight: bold;
    margin-right: 20px;
    line-height: 120%;
  }

  &__catalog-btn {
    margin-right: 20px;
    padding: 15.5px 25px;
    background-color: rgba(0, 0, 0, 0); 
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    border: 1px solid #73AFF4;
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
    border: 1px solid #73AFF4;
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

  &__link {
    margin-left: 20px;
    white-space: nowrap;

    &:hover {
      text-decoration: underline;
      color: #007bff; 
    }
  }
}

@media (max-width: 1300px) {
  .header {
    &__mobil-wrapper {
      display: flex;
      width: 70vw;
      margin: 0 auto;
      justify-content: space-between;
      padding: 10px;
    }

    &__wrapper {
      display: none;
    }

  }
}
</style>
