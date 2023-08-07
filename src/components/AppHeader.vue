<script></script>

<template>
  <div class="header">
    <div class="header__container">
      <div class="header__logo">
        <img src="/src/assets/image/logo.png" alt="" />
      </div>
      <nav class="header__link">
        <a href="">Home</a>
        <a href="">About</a>
        <a href="">Product</a>
        <a href="">Contact</a>
      </nav>
    </div>
  </div>
</template>

<style lang="scss">
.header {
  &__container {
    max-width: 80%;
    margin: auto;
    display: flex;
    align-items: center;
    gap: 30px;
    padding: 10px 0px;
  }
  &__logo img {
    width: 70px;
  }
  &__link {
    display: flex;
    align-items: center;
    gap: 60px;
    font-weight: 500;
    font-size: 22px;
    a {
      text-decoration: none;
      color: rgb(46, 45, 45);
    }
  }
}
</style>
