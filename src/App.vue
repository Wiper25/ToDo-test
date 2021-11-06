<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Главная</router-link>
      <router-link to="/list">Список задач</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
  #nav {
    display: flex;
    justify-content: space-evenly;
    width: 100%;
  }
  #app {
    font-family: 'Oswald', sans-serif;
    margin: 20px;
  }
</style>
