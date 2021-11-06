<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Главная</router-link>
       <div>
        <b-button v-b-toggle.sidebar-right>Создать группу</b-button>
        <b-sidebar id="sidebar-right" left shadow>
      <div class="px-3 py-2">
        <b-button @click="setObj">Создать</b-button>
      </div>
    </b-sidebar>
  </div>
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
    margin: 20px;
  }
</style>
