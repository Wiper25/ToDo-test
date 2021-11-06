<template>
  <div class="list">
    <div class="list__empty-block">
      <div class="list__to-do-list">
        <h5>Список дел</h5>
      </div>
      <b-form-select class="list__gruop" v-model="selected" :options="options"></b-form-select>
      <h4 class="list__empty" v-if="!cards" >Пусто</h4>
      <div v-if="selected == 'id'" class="list__block">
        <div class=" list__card" :class="{'done':card.status}" :key="i" v-for="(card,i) in cards">
          <div class="list__marker" :style="`background-color:${card.colorCard}`"></div>
          <b-card class="list__card-title text-center" bg-variant="dark" text-variant="white" :header="card.title">
            <b-card-text class="list__card-text">{{card.description}}</b-card-text>
            <div class="text-center my-3">
              <b-button @click="card.status = !card.status">{{card.status ? "Открыть" : "Закрыть"}}</b-button>
            </div>
            <h5 v-if="card.importance == 'high'">Высокий приоритет</h5>
            <h5 v-if="card.importance == 'average'">Средний приоритет</h5>
            <h5 v-if="card.importance == 'short'">Низкий приоритет</h5>
          </b-card>
        </div>
    </div>
    </div>
    
    <div class="text-center my-3">
      <b-button v-b-popover.hover="'Все записи будут стерты.'" href="/list"  @click="clear()" title="ВНИМАНИЕ!!!">Очистить</b-button>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      selected: 'id',
      options: [
        { value: 'id', text: 'Группировка не указана' },
        { value: 'name', text: 'По имени' },
        { value: 'color	', text: 'По цвету' },
        { value: 'priority	', text: 'По приоритету' },
      ],
      cards: JSON.parse(localStorage.getItem('card'))
    }
  },
  methods: {
    clear(){
      localStorage.clear()
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
.list__marker {
  width:95%;
  height:10px;
  margin: 0 auto;
  border-top-right-radius: 20px;
  border-top-left-radius: 20px;
}
.list__gruop {
  display: block;
  margin: 0 auto;
}
.done {
  text-decoration: line-through;
  color: black;
}
.list__empty-block {
    background-color: #cfcece;
    border-radius: 20px;
    padding-bottom: 10px;
    margin-top: 20px;
    text-align: center;
}

.list__to-do-list {
    background-color: #9e9e9e;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
}
.list__empty {
  margin: 10px;
  color: rgb(90, 86, 86);
}
</style>