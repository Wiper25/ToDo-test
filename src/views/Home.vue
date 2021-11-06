<template>
  <div class="home">
    <h1 class="home__name-title">Создать задачу</h1>
      <div class="home__title">
    <b-form-input v-model="item.title" placeholder="Название"></b-form-input>
  </div>
    <div class="home__description">
    <b-form-input v-model="item.description" placeholder="Описание"></b-form-input>
  </div>
    <div class="home__status">
    <b-form-select class="home__select" v-model="item.colorCard" :options="options"></b-form-select>
      <b-form-group v-slot="{ ariaDescribedby }">
        <b-form-radio v-model="item.importance" :aria-describedby="ariaDescribedby" name="some-radios" value="high">&nbsp;Высокий приоритет</b-form-radio>
        <b-form-radio v-model="item.importance" :aria-describedby="ariaDescribedby" name="some-radios" value="average">&nbsp;Средний приоритет</b-form-radio>
        <b-form-radio v-model="item.importance" :aria-describedby="ariaDescribedby" name="some-radios" value="short">&nbsp;Низкий приоритет</b-form-radio>
    </b-form-group>
  </div>
  <div class="home__btn">
    <div class="text-center my-3">
  <b-button v-b-popover.hover="'Пожалуйста проверьте введенную информацию'" @click="setObj" title="ВНИМАНИЕ!!!">Создать</b-button>
</div>
</div>
  <p style="color:red;text-align:center;">{{error}}</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      options: [
        { value: '#ff0000', text: 'Красный маркер' },
        { value: '#0000ff	', text: 'Синий маркер' },
        { value: '#ffa500', text: 'Оранжевый маркер' },
        { value: '#00ff00', text: 'Зеленый маркер' },
        { value: '#ffff00', text: 'Желтый маркер' },
        { value: '#4b0082', text: 'Фиолетовый маркер' },
        { value: '#000000', text: 'Черный маркер' },
        { value: '#ff1493', text: 'Розовый маркер' },
        { value: '#4682B4', text: 'Голубой маркер' },
        { value: '#8B4513', text: 'Коричневый маркер' },
        { value: '#f0e68c', text: 'Бежевый маркер' },
        { value: '#808080', text: 'Серый маркер' },
      ],
      error:'',
      item: {},
      send:[]
    }
  },
    methods: {
    setObj(){
      if(this.item.title !== undefined && this.item.description !== undefined && this.item.importance !== undefined && this.item.colorCard !== undefined){
      this.item.status = false
      this.send.push(this.item);
      this.item = {}
      localStorage.setItem(`card`, JSON.stringify(this.send));
      }
      else {
        this.error = 'Пожалуйста заполните все поля для ввода';
      }
    }
  }
}
</script>

<style scoped>
.home {
  width: 35%;
  border: 1px solid;
  padding: 10px;
  margin: 0 auto;
  margin-top: 100px;
}
.home__name-title {
  text-align: center;
}
.home__select {
  width: 50%;
}
.home__title {
}
.home__description {
  margin: 10px 0px;
}
.home__status {
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
}
.home__color {
  width:100%;
}
.home__btn {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>