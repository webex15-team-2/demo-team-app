<template>
  <header class="header">
    <div class="header__titles">
      <img src="@/assets/logo.png" alt="vue logo" width="50" height="50" />
      <h1>Vue 小作品集</h1>
    </div>
    <nav class="navigation">
      <router-link
        to="/"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Home</router-link
      >
      |
      <router-link
        to="/quiz"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Vue クイズ</router-link
      >|
      <router-link
        to="/palette"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Vue パレット</router-link
      >|
      <router-link
        to="/memo"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Vue メモ</router-link
      >
    </nav>
  </header>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 2rem;
}

.header__titles {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.navigation {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  gap: 0.8rem;
  font-size: 1.5rem;
}

.navigation__link {
  font-weight: bold;
  color: #2c3e50;
}

.navigation__link--exact-active {
  color: #42b983;
}
</style>
