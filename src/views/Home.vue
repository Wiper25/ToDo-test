<template>
  <div class="home">
    <h1>Создать задачу</h1>
      <div class="home__title">
    <b-form-input v-model="item.title" placeholder="Название"></b-form-input>
  </div>
    <div class="home__description">
    <b-form-input v-model="item.description" placeholder="Описание"></b-form-input>
  </div>
    <div class="home__status">
    <b-form-select v-model="item.color" :options="options"></b-form-select>
      <b-form-group v-slot="{ ariaDescribedby }">
        <b-form-radio v-model="item.selected" :aria-describedby="ariaDescribedby" name="some-radios" value="high">&nbsp;Высокий приоритет</b-form-radio>
        <b-form-radio v-model="item.selected" :aria-describedby="ariaDescribedby" name="some-radios" value="average">&nbsp;Средний приоритет</b-form-radio>
        <b-form-radio v-model="item.selected" :aria-describedby="ariaDescribedby" name="some-radios" value="short">&nbsp;Низкий приоритет</b-form-radio>
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
      selected: 'red',
      options: [
        { value: 'red', text: 'Красный маркер' },
        { value: 'blue', text: 'Синий маркер' },
        { value: 'orange', text: 'Оранжевый маркер' },
      ],
      error:'',
      count: 0,
      item: {},
      send:[]
    }
  },
    methods: {
    setObj(){
      this.count++
      if(this.item.title !== undefined && 
      this.item.description !== undefined && 
      this.item.selected !== undefined && 
      this.item.color !== undefined ){
      this.item.id = this.count
      this.item.status = false
      this.send.push(this.item);
      this.item = {}
      localStorage.setItem(`card`, JSON.stringify(this.send));
      }else {
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
.home__title {
}
.home__description {
  margin: 10px 0px;
}
.home__status {
    display: flex;
    justify-content: space-around;
    align-items: center;
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