<template>
  <div class="list">
    <div class="list__block">
    <div class=" list__card" :class="{'done':card.status}" :key="i" v-for="(card,i) in cards">
      <b-card class="list__card-title text-center" bg-variant="dark" text-variant="white" :header="card.title">
        <b-card-text class="list__card-text">{{card.description}}</b-card-text>
            <div class="text-center my-3">
              <b-button @click="card.status = !card.status">{{card.status ? "Открыть" : "Закрыть"}}</b-button>
            </div>
      </b-card>
    </div>
    </div>
    <div class="text-center my-3">
      <b-button v-b-popover.hover="'ВНИМАНИЕ!!! Все записи будут стерты.'" href="/list" @click="clear()" title="Очистка всего листа.">Очистить</b-button>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      cards: JSON.parse(localStorage.getItem('card'))
    }
  },
  methods: {
    clear(){
      console.log(cards)
      // localStorage.clear()
    },
  },
  beforeDestroy() {

  }
}
</script>
<style scoped>
.list__block {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
.list__card {
  width: 20%;
  margin: 20px;
}
.done {
  text-decoration: line-through;
  color: white;
}
</style>