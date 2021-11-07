<template>
  <div class="home">
    <h1 class="home__name-title">Создать задачу</h1>
    <div class="home__title">
      <b-form-input v-model="item.title" placeholder="Название"></b-form-input>
    </div>
    <div class="home__description">
      <b-form-input
        v-model="item.description"
        placeholder="Описание"
      ></b-form-input>
    </div>
    <div class="home__status">
      <b-form-select
        class="home__select"
        v-model="item.colorCard"
        :options="options"
      ></b-form-select>
      <b-form-group v-slot="{ ariaDescribedby }">
        <b-form-radio
          v-model="item.importance"
          :aria-describedby="ariaDescribedby"
          name="some-radios"
          value="A"
          >&nbsp;Высокий</b-form-radio
        >
        <b-form-radio
          v-model="item.importance"
          :aria-describedby="ariaDescribedby"
          name="some-radios"
          value="B"
          >&nbsp;Средний</b-form-radio
        >
        <b-form-radio
          v-model="item.importance"
          :aria-describedby="ariaDescribedby"
          name="some-radios"
          value="C"
          >&nbsp;Низкий</b-form-radio
        >
      </b-form-group>
    </div>
    <div class="home__btn">
      <div class="text-center my-3">
        <b-button
          v-b-popover.hover="'Пожалуйста проверьте введенную информацию'"
          @click="setObj"
          title="ВНИМАНИЕ!!!"
          >Создать</b-button
        >
      </div>
    </div>
    <p style="color: red; text-align: center">{{ error }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        { value: "red", text: "Красный маркер" },
        { value: "blue	", text: "Синий маркер" },
        { value: "orange", text: "Оранжевый маркер" },
        { value: "green", text: "Зеленый маркер" },
        { value: "yellow", text: "Желтый маркер" },
        { value: "darkmagenta", text: "Фиолетовый маркер" },
        { value: "black", text: "Черный маркер" },
        { value: "deeppink", text: "Розовый маркер" },
        { value: "dodgerblue", text: "Голубой маркер" },
        { value: "saddlebrown", text: "Коричневый маркер" },
        { value: "sandybrown", text: "Бежевый маркер" },
        { value: "grey", text: "Серый маркер" },
      ],
      error: "",
      item: {},
      send: [],
    };
  },
  methods: {
    setObj() {
      if (
        this.item.title !== undefined &&
        this.item.description !== undefined &&
        this.item.importance !== undefined &&
        this.item.colorCard !== undefined
      ) {
        this.item.status = false;
        this.send.push(this.item);
        this.item = {};
        localStorage.setItem(`card`, JSON.stringify(this.send));
      } else {
        this.error = "Пожалуйста заполните все поля для ввода";
      }
    },
  },
};
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
  width: 100%;
}
.home__btn {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>
